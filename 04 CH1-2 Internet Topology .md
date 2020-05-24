# Internet topology

## hub(physical layer1 equipment)==>use signal to transmit
* Advantage:
  * broadcast easy
* Disadvantage:
  * security not good (When A transmit to B ,C and D can get the information ,but maybr they would discard it)
  * performance not good (When A transmit to B .At the same time C want to transmit to D. CandD need to wait for A->B finished that they can transmit )


## switch(Layer2 equipment(MAC Layer))==>Frame(訊框)->MAC address
* Advantage:
  * A <-> B , C <-> D can transmit at the same time
  * With learning function =>Know A,B,C,D each one's destination
  * security good (When A<->B,C can't see the information between A and B)
* Disadvantage:
  * They are more expensive compare to network bridges
  * Broadcast traffic may be troublesome on a switch


## additional
* Physical address :Network card number(網路卡卡號)==>Never change(like identity card)
* logical address:(ip address)go to different plases use different ip address.
* Port number:application=>like Shipper and Receiver.e.g:多應用程式，要了解哪個應用程式到哪個應用程式，用port來區分
* vitual host

## A.Star topology(星型拓撲)==>節點必須先傳到中央節點，再由中央節儉傳至其他節點。
* Advantage:
  * Simple
  * the link between node and control node,it won't effect other node's comm
* Disadvandage:
  * the control node fails all system crashes.
  
  
## B.Bus topology(直線型網路)
* ==>擴充時只要拔T行街頭，就能擴充。隨著結點閱多，傳輸效能越差，競爭越多
* transfer method:
 * 假設A ->B ,B收到，但C和D也收到，可是會將其拋棄，而直線型網路傳輸方式是會一直向兩旁傳，直到碰到終端機才停止
* Advantage:
 * Broadcast easy
* Disadvantage:
 * security not good
 * All broken when the middle's one broken
 * contention based(競爭式)
   * 可多人傳，但越多人傳，傳輸效能越差
   
   
 ## Ring topology(環型網路)
 * transfer method:
  * 誰擁有Token誰就可以傳，每傳一次，Token丟給下一個人
 * Advantage:
  * contention free (不用競爭傳輸效果好)
 * Disadvantage:
  * 貴(expensive)
  

## Tree topology(樹狀網路)
* ==>node to node only one transmition path.
* ==>In the tree topology we can't see the loop.
* e.g : our computer classroom(假設有50台電腦，但集線器上植有五十個孔，所以我們要運用兩台及限期將其串接完，形成樹狀)
* Disadvantage: 其中一條毀了，其傳輸路徑壞。
* 補:
 * loop topology :1.Advantage:robust good(任一條斷，還有其他可傳) 2.Disadvantage:Broadcast storm

### Hybrid topology (混和式網路)
* two different type

 
