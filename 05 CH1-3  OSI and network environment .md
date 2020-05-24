# 常見的網路格式
* (a)client/server(C/S模型) ==>基本的http架構
* (b)peer to peer(p2p) ==>同時具有客戶端及伺服器端的角色
  * e.g: 網路芳玲
*補充:Brower/Server模型 ==>B/S一定是C/S,C/S不一定是B/S.


# OSI 七層參考模型
* 由ISO訂定

層級 | 對應架構
-----|--------
應用層(Application Layer7) | 人和機器重要介面(非應用程式)/ e.g:http
呈現層(Presition Layer6)  |  encoding,decoding/encryption,decryption/cowpression,decompression
會議層(Session Layer5) | 決定誰可以傳送資料
傳輸層(Transport Layer4) | Provide all e2e(end to end)quality of service/TCP:reliable; UDP :fast(e.g:DNS)
網路層(Network Layeer3) | 定址(給每通訊地址)/路由(fide a path)
資料連結層(Data Link Layer2) | provide one hop 的傳輸品質/分兩層LLC和MAC
實體層(Physical Layer1) | 定義傳輸媒介，接角，訊號 e.g.網路線中有八條線，哪一條的功用是甚麼，皆由實體層定義

* WiFi:CSMA/CA==>當傳訊息時，會看上面是否有其他訊息
* Ethernet==>CSMA/CD

