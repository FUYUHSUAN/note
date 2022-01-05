## Server(NAT, LAN segment)

1. yum install dhcp -y

2. ip addr add 192.168.10.1/24 brd + dev ens37 (LAN segment:a)

3. vim /etc/dhcp/dhcpd.conf
    ```
    subnet 192.168.10.0 netmask 255.255.255.0 {
        range 192.168.10.100 192.168.10.200;
        option routers 192.168.10.1;
        option domain-name-servers 8.8.8.8;
        dafault-lease-time 600;
        max-lease-time 7200;
    }
    ```

4. systemctl restart dhcpd

5. echo 1 > /proc/sys/net/ipv4/ip_forward

6. iptables -t nat -A POSTROUTING -o ens33 -s 192.168.10.0/24 -j MASQUERADE

## Client(LAN segment:a)

1. dhclient ens34 (LAN segment:a)

2. ip route show
成功畫面
    ```
    [root@centos7-3 user]# ip route show
    default via 192.168.10.1 dev ens34 
    192.168.10.0/24 dev ens34 proto kernel scope link src 192.168.10.100 
    192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1 
    ```




tail -n 30 /var/log/messages
netstat -tlunp | grep dhcp