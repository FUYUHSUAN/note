hostnamectl set-hostname centos7-1
systemctl disable firewalld
systemctl stop firewalld
getenforce
cd /etc/selinux
vi config

# NAT
centos7-2 (NAT、hostonly):
echo "1" > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -o ens33 -s {host-only's 網域} -j MASQUERADE (例如: iptables -t nat -A POSTROUTING -o ens33 -s 192.168.159.0/24 -j MASQUERADE)


centos7-3(NAT、hostonly):
ifconfig ens33 down
route add default gw {centos7-2's host-only ip} (例如:route add default gw 192.168.159.129)
vim /etc/resolv.conf  加上以下
    ```
    nameserver 8.8.8.8
    ```
---

# ssh(no password login)
centos7-2(NAT、hostonly):
cd /root/.ssh
ssh-keygen

centos7-3(NAT、hostonly):
ifconfig ens33 up
ssh-keygen
ssh-copy-id user@192.168.48.138(第一次需要密碼)
ssh user@192.168.48.149

Last login: Tue Dec 28 05:29:30 2021(此為結果，之後都不需要密碼)

---

# ssh(scp)
centos7-3(NAT、hostonly):
touch test3
scp test3 user@192.168.48.138:~   (將想傳的檔案test3 透過 ssh 輸入對方的ip即可，最後的~為家目錄)

centos7-2(NAT、hostonly):
cd ~(即可看到剛剛所傳的)

---

# dhcp
## Server(NAT, LAN segment)

1. yum install dhcp -y

2. ip addr add 192.168.10.1/24 brd + dev ens38 (LAN segment:a)

3. vim /etc/dhcp/dhcpd.conf
    ```
    subnet 192.168.10.0 netmask 255.255.255.0 {
        range 192.168.10.100 192.168.10.200;
        option routers 192.168.10.1;
        option domain-name-servers 8.8.8.8;
        default-lease-time 600;
        max-lease-time 7200;
    }
    ```

4. systemctl restart dhcpd

5. echo 1 > /proc/sys/net/ipv4/ip_forward

6. iptables -t nat -A POSTROUTING -o ens33 -s 192.168.10.0/24 -j MASQUERADE

## Client(LAN segment:a)

1. dhclient ens38 (LAN segment:a)

2. ip route show   (已經順利自動分配ip位置)
成功畫面
    ```
    [root@centos7-3 user]# ip route show
    default via 192.168.10.1 dev ens34 
    192.168.10.0/24 dev ens34 proto kernel scope link src 192.168.10.100 
    192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1 
    ```

---

# telnet
yum install telnet -y
yum install telnet-server 
yum install xinetd
systemctl stop firewalld
getenforce
cd /etc/xinetd.d/
gedit telnet 
```
service telnet

{
  flags = REUSE
  socket_type = stream
  wait = no
  user = root
  server = /usr/sbin/in.telnetd
  log_on_failure += USERID
  disable = no
}

```
systemctl start xinetd
netstat -tunlp | grep 23
ps -ef | grep telnet

* 開啟putty 連連看，連telnet前和後是不一樣

---

# www
- yum install php-mysql
- yum install mariadb-server mariadb
- yum install php  (會沒辦法顯示php)
systemctl start mariadb
systemctl status mariadb
mysql_secure_installation (ynnny)
mysql -uroot -p
    show databases;
    create database testdb;
    show databases;
    //create table addrbook;
    use testdb;       
    create table addrbook(name varchar(50) not null, phone varchar(10));
    insert into addrbook(name, phone) values ("tom", "1234567890");
    insert into addrbook(name, phone) values ("mary", "9876543210");
    select * from addrbook;
    exit
systemctl restart httpd
cd /var/www/html
touch test.php
gedit test.php
```
<?php
phpinfo();
?>
```

touch hi.php
gedit hi.php
```
<?php
$servername="localhost";
$username="root";
$password="user";
$dbname="testdb";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("conneciton failed: ". $conn->connect_error);
}
//echo "connection ok"

$sql="select name,phone from addrbook";
$result=$conn->query($sql);

if($result->num_rows>0){
   while($row=$result->fetch_assoc()){
      echo "name:". $row["name"]." phone:". $row["phone"]."<br>";
   }
}
?>
```
在windows上輸入ip位址+/hi.php

---

# nfs
- server
1. yum install -y nfs-utils
2. systemctl start rpcbind
3. systemctl start nfs-server
4. gedit /etc/exports
```
/mynfs 192.168.48.0/24(rw,sync,no_root_squash)    //(192.168.48.0/24是網域)
```
5. cd /
6. mkdir mynfs
7. exportfs -arv   
8. cd /mynfs
9. touch {1..4}

- client
1. yum install -y nfs-utils
2. systemctl start rpcbind
3. showmount -e 192.168.48.137 (server ip)
4. cd /
5. mkdir mydata
6. mount -t nfs 192.168.48.137:/mynfs  /mydata
7. cd /mydata
8. touch ping

---

# haproxy
- centos7-3(ip:192.168.48.139)
yum install -y epel-release
yum install haproxy -y
cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.bak
cd /etc/haproxy/
gedit haproxy.cfg
    ```
    // 加上這兩行另兩台的ip
    server server_name1 192.168.48.139:80 check
    server server_name2 192.168.48.137:80 check
    ```
systemctl stop firewalld
systemctl restart haproxy
windows網址要輸入:192.168.48.139+port(frontend  main //在/etc/haproxy/haproxy.cfg)
不須開httpd

- centos7-2(ip:192.168.48.138)
yum install httpd -y
cd /var/www/html
vi index.html (centos7-2)
systemctl status firewalld
systemctl start httpd

- centos7-4(ip:192.168.48.137)
yum install httpd -y
cd /var/www/html
vi index.html (centos7-4)
systemctl status firewalld
systemctl start httpd

---

# vsftpd
- centos7-3
yum install vsftpd -y
systemctl start vsftpd
systemctl status vsftpd
netstat -tunlp | grep 21
systemctl stop firewalld
cd /var/ftp/pub
touch test.ftp
cd ..
chmod 777 pub
cd /etc/vsftpd
gedit vsftpd.conf
    ```
    allow_ftpd_full_access,anon_mkdir_write_enable=YES和 anon_mkdir_write_enable=YES的註解都拿掉
    ```
systemctl restart vsftpd

- cmd
ftp 192.168.48.139
anonymous
a.b.c@gmail.com
cd pub
bin
get test.ftp
put test_win.txt

- 在centos7-3防守
1. `cd /etc/vsftpd`
2. `vi user_list`
3. 將使用者名稱加上去
4. 就成功了


---@

# samba
- centos7-3
yum install samba-client samba-common -y
yum install samba -y
systemctl start smb


gedit /etc/samba/smb.conf
 ```
    # See smb.conf.example for a more detailed config file or
    # read the smb.conf manpage.
    # Run 'testparm' to verify the config is correct after
    # you modified it.

    [global]
        workgroup = SAMBA
        security = user

        passdb backend = tdbsam

        printing = cups
        printcap name = cups
        load printers = yes
        cups options = raw

    [homes]
        comment = Home Directories
        valid users = %S, %D%w%S
        browseable = No
        read only = No
        inherit acls = Yes

    [printers]
        comment = All Printers
        path = /var/tmp
        printable = Yes
        create mask = 0600
        browseable = No

    [print$]
        comment = Printer Drivers
        path = /var/lib/samba/drivers
        write list = @printadmin root
        force group = @printadmin
        create mask = 0664
        directory mask = 0775
    [formary]
        comment = Shared Directory
        path = /formary
    
        create mode = 0660
        directory mode = 2770
        
        write list = mary
        public = yes

    [sharefolder]
        comment = Shared Directory
        path = /sharefolder
        browseable = yes
        writable = yes
    
        create mode = 0660
        directory mode = 2770

        public = yes
```
mkdir /sharefolder
chmod 777 /sharefolder
mkdir /formary
chmod 777 /formary 

* `useradd mary` :新增user mary
* `smbpasswd -a mary` :加入smb的密碼
* `smbpasswd -a user`
- for wundow
//192.168.48.139
- cmd
net use * /delete


---

# NetworkManage & Network
systemctl stop NetworkManager
systemctl status NetworkManager
cd /etc/sysconfig/network-scripts
vim ifcfg-ens33
 * 原本的
    ```
    TYPE="Ethernet"
    PROXY_METHOD="none"
    BROWSER_ONLY="no"
    BOOTPROTO="dhcp"
    DEFROUTE="yes"
    IPV4_FAILURE_FATAL="no"
    IPV6INIT="yes"
    IPV6_AUTOCONF="yes"
    IPV6_DEFROUTE="yes"
    IPV6_FAILURE_FATAL="no"
    IPV6_ADDR_GEN_MODE="stable-privacy"
    NAME="ens33"
    UUID="dbff48f0-2297-476d-9db3-deca5638bfa8"
    DEVICE="ens33"
    ONBOOT="yes"
    ```

    * 改變成的
    ```
    TYPE="Ethernet"
    BOOTPROTO=static
    NAME="ens33"
    DEVICE="ens33"
    ONBOOT="yes"
    IPADDR=192.168.48.100   //10.10.10.1
    NETMASK=255.255.255.0
    GATEWAY=192.168.48.2   //10.10.10.48
* `vim /etc/resolv.conf` :改變DNS
    * 原本的
    ```
    ; generated by /usr/sbin/dhclient-script
    search localdomain
    nameserver 192.168.48.2
    ```
    * 更改後
    ```
    ; generated by /usr/sbin/dhclient-script
    search localdomain
    nameserver 8.8.8.8

    ```
* `ip route show` :看看是否設定好
* `ping 8.8.8.8`
* `ping tw.yahoo.com`


* 如果後來網路斷掉用systemctl restart network
---

# bind
yum install bind bind-chroot bind-utils
systemctl start named
試試看dig`dig @127.0.0.1 www.pchome.com.tw` 和 `dig @12y7.0.0.1 www.nqu.edu.tw`
host -t A www.nqu.edu.tw 127.0.0.1
編輯`gedit /etc/named.conf` 將127.0.0.1 -> any 和 localhost -> any
在 cmd 中打上 `nslookup www.nqu.edu.tw 192.168.48.138`

systemctl restart named

gedit /var/named/a.com.zone

    ```

    $TTL 600 ;10 minutes

    @ IN SOA	@ ramy1231863.gmail.com (
            2021031803 ;serial
            10800      ;refresh
            900        ;retry
            604800     ;expire
            86400      ;minimum
            )
    @		NS    dns1.a.com.
    dns.com.	A     192.168.56.108
    dns1		A     192.168.56.108
    www		A     192.168.56.150
    eshop		CNAME www
    ftp		A     192.168.56.150
    abc		A     192.168.56.120
    ```
編輯 `gedit /etc/named.rfc1912.zones` 在最後增加以下

    ```
    zone "a.com" IN {
        type master;
        file "a.com.zone";
        allow-update { none; };
    };
    zone "56.168.192.in-addr.arpa" IN {
        type master;
        file "56.168.192.in-addr.arpa.zone";
        allow-update { none; };
    };
    ```
編輯`gedit /var/named/56.168.192.in-addr.arpa.zone`

    ```
    @ IN SOA	@ ramy1231863.gmail.com (
            2021031803 ;serial
            10800      ;refresh
            900        ;retry
            604800     ;expire
            86400      ;minimum
            )

    56.168.192.in-addr.arpa.    IN  NS dns1.a.com.
    56.168.192.in-addr.arpa.    IN  NS dns2.a.com.

    200.56.168.192.in-addr.arpa.  IN PTR www.a.com.
    150.56.168.192.in-addr.arpa.  IN PTR ftp.a.com.

    ```

最後將named重新啟動並打`nslookup 192.168.56.150 127.0.0.1`出現結果如下即完成
[root@centos7-2 user]# systemctl restart named
[root@centos7-2 user]# nslookup 192.168.56.150 127.0.0.1
150.56.168.192.in-addr.arpa	name = ftp.a.com.

 test for cmd`cmd:nslookup abc.a.com 192.168.48.138`
