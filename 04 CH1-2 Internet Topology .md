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
  *the control node fails all system crashes.
  
## B.Bus topology(直線型網路)
* ==>擴充時只要拔T行街頭，就能擴充。隨著結點閱多，傳輸效能越差，競爭越多
* 
 
