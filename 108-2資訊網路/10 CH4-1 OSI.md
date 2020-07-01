* IAB:
  * IETF -->RFC(request for comment)<-- TCP/IP
    * e.g:ipv4,ipv6
  * IRTF
* IEEE
  * 802.3(ethernet)
  * 802.11(wifi)
* RS232-c
  * 串列傳輸(serial communicational)
  * 9-pin
  * 由EIA所規劃制定
* OSI:由ISO所制定
* TCP/IP:由IAB負責協定

### 大資料在傳輸層進行拆組裝的動作
* Transpoet----------TH資料--->segment片段
* Nwtwork---------NH|TH資料--->packet
* DataLink-----DH|NH|TH資料|DT->frame(訊框)

### ethernet frame
* size:64-1518(bytes)
* include(14bytes(ethernet header)+4bytes(ethernet trails)
* MMS(Maximum segment slice):1460
* MTU(Maximum Transport unit；最大傳輸單元):1500(bytes)
  * 大小可改:window(難改),Linux(好改)
  * MTU:Ethernet(1500),WiFi(2304)
* 封包沒大於1500，正常不會被切割(因為每切割一次，都會造成浪費)
* 看看傳輸是否被干擾-->ISM頻率2.4~2.5，我使用，你也使用，就會干擾。
  * 如果有干擾:用小封包
  * 如果沒干擾:用大封包
  * 封包大小可調，調越大，越快，但每，但每種網路系統都有限制。
  
