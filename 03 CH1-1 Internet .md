# Internet
* 比較:
  * Internet(網際網路 or 互聯網)=>由TCP/IP協定所構成，由全球多個網路所形成的全球超大網路架構
  * internet(網路和網路之間的關係)
  * intranet(內網)
  
* 分類:
  * 集中式架構:
    * 優 : 可管控進來資料
    * 缺 : 1.中間壞，大家無法相通 2.機器通訊前一定要與中間相通，任何一同斷了，即連不上
    * e.g: Teamviewer (連接至中間，將兩點串通)
  * 分散式架構:
    * 優 : 任何一台壞了都沒關係
    * 缺 : 得到的資訊非全面性
    * e.g: 現在Tnternet 多用此方法
    
 
## Internet 最初的主要功能
* 電子郵遞
* 遠端使用(Remote Login ; Talnet)
  * 1.不加密 2.用 port:23
  * 如今使用SSH 
    * 加密
    * port : 22 => in band(包括control & data 皆走同一通道)
* 檔案傳輸(FTP)
  * port : 21 (control)
  * port : 20 (data)   ===>走不同通道稱 out-of-band

* 補:
 * Data Comm(資訊網路):e.g Intel,桌機,傳統LAN...
 * Tele Comm(電信網路):e.g 3G,4G,5G,WAN ...


## 網路類型
* 1.PNG(Personal Area Network)=>個人網路
  * 範圍:10m 左右
  * e.g 藍芽
* 2.LAN(Local Area Network)=>區域網路
  * 範圍:100-200m 左右
  * e.g :
    * Ethernet(IEEE 802.3) ==>(IEEE念法I triple E)
    * WiFi(IEEE 802.11)
* 3.MAN(Metropolitan Area Network)=>廣域網路
  * 範圍:2km-10km
  * e.g: wimax(IEEE 802.16)=>now dead
* 4.WAN(Wide Area Network)=>廣域網路
  * 範圍:10km以上
  * used:
    * wired
    * ADSL Fiber cable
* 補:WWAN
  * 3G(IMT-2000),4G,5G(IMT-2020)
* 補:Body Network
  * range:inside 1m
  * e.g:智慧手錶，AR眼鏡
  
* 補
  * 3G =>3.5G =>3.75G =>4G =>5G
    * 4G (LTE-A) 有700MHz,900MHz,1800MHz,2100MHz,2600MHz ==>皆為單一通道，彼此間不連續
    * 3.9G
      * wimax(失敗)
      * LTE 
    * 4.5G-CA(carrier aggregation)==>仔波聚合ㄛ

  

 
   


