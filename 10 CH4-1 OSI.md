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

* OSI參考模型(資料封包的組成)

  層級 | 對應架構
-----|--------
應用層(Application Layer7) | 人和機器重要介面(非應用程式)/ e.g:http
呈現層(Presition Layer6)  |  encoding,decoding/encryption,decryption/cowpression,decompression
會議層(Session Layer5) | 決定誰可以傳送資料
傳輸層(Transport Layer4) | Provide all e2e(end to end)quality of service/TCP:reliable; UDP :fast(e.g:DNS)
網路層(Network Layeer3) | 定址(給每通訊地址)/路由(fide a path)
資料連結層(Data Link Layer2) | provide one hop 的傳輸品質/分兩層LLC和MAC
實體層(Physical Layer1) | 定義傳輸媒介，接角，訊號 e.g.網路線中有八條線，哪一條的功用是甚麼，皆由實體層定義
  
