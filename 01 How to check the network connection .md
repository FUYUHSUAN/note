# 不能看網頁怎麼辦?如何解決
* Step1:open a terminal in cmd
* Step2:ping 127.0.0.1      (測試本機TCP/IP protocal 是否正常)
* Step3:ipconfig/all        (找出 ip address)
* Step4:ping 192.168.X.X    (pinge 剛剛找到的ip address)
  * 此處測試硬體
* Step5:ping 8.8.8.8 or 4.4.4.4 or 1.1.1.1 or 9.9.9.9  (ping Internet host's IP for DNS Domain)
  * 如果Step5可以Step6不行，代表DNS server 有問題。
  * 解決方法:change DNS server
* Step6:ping www.google.com (ping Internet host's DN(Domain Name))

## 補充1
* 用 ipconfig or  netstat-rn 都可以找到ip address
* 指令:
 * 持續 ping: ping 192.168.....-t 
 * 中斷 ping: ctrl +c
* window 有大小寫之分
* linux 沒有大小寫之分

### 補充2:(正值新冠狀病毒期間)
* Please stay @ 127.0.0.1.Don't go 255.255.255.255
 * 127.0.0.1 :local interface (本機)
 * 255.255.255.255 :broadcast only for destination can't set this IP to your computer.
 * 主旨:希望大家多留在家少出們
 
### 補充3:
* 在實體網路卡卡號中(Physical address)=>由6 byte 所組成
 * 前3byte:製造商id
 * 後3byte:流水號

