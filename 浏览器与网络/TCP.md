 # 1、相关概念
 **相关概念**这部分，描述了tcp协议中涉及的几处概念，相当于名词解释。    
 建议阅读时先扫一遍这部分。后续阅读中，如果涉及相关概念，在回来差字典。便于理解。（可以开两个网页来看。）
 ## 1.1、报文结构

![报文结构](/images/tcp2.png)       

**tcp**：***传输控制协议*** ,以上是tcp的报文结构。其各部分表示的含义如下：  

* 16位的源端口与目标端口分别表示了，数据从哪个进程来，到哪个进程去。
* 32位序号（Sequence Number简写seq），用以解决网络包乱序问题。
* 32位确认序号（Acknowledgement Number简写ack），用以解决丢包问题。
* 4位首部长度：表示tcp报头有多少个4字节。
* 6位标识位置（TCP Flag ），包的类型，主要用于操控tcp的状态机。（详细内容请看下节）
* 16位窗口大小（Window）, 或者叫Sliding Window滑动窗口大小，对应 ***滑动窗口机制***。
* 16位校验和（checksum）
* 16位紧急指针 (Urgent Pointer)    
---
这里需要注意的是：    
1. tcp协议包里，是没有IP的。IP在下一层的IP协议里。tcp关注的是端口号，是两个进程间的事。
2. 一个tcp链接，需要四元祖标识（src_ip, src_port, dst_ip, dst_port）。只有四个属性完全相等时，才能表示为同一链接。

 ## 1.2、标识位(Tcp Flag)
* URG: 标识紧急指针是否有效   
* ACK: 标识确认序号是否有效   
* PSH: 用来提示接收端应用程序立刻将数据从tcp缓冲区读走   
* RST: 要求重新建立连接. 我们把含有RST标识的报文称为**复位报文段**   
* SYN: 请求建立连接. 我们把含有SYN标识的报文称为**同步报文段**   
* FIN: 通知对端, 本端即将关闭. 我们把含有FIN标识的报文称为**结束报文段**   

## 1.3、TCP状态机
**网络上的传输是没有连接的**，包括TCP也是一样的。而TCP所谓的“连接”，其实只不过是在通讯的双方维护一个“**连接状态**”，让它看上去好像有连接一样。所以，TCP的状态变换是非常重要的。    
TCP的状态机是一个具有11种状态的有限状态机。
<center>

  ![状态机](/images/tcp_status.png)
</center>      

上图中涉及的11种状态，对应的描述，如下表所示。      

|    状态         |             描述                              | 
|----------------|:---------------------------------------------:|
|  CLOSED        |  关闭状态，没有连接活动或正在进行                  |  
|  LISTEN        |  监听状态，服务器正在等待连接进入                  | 
|  SYN RCVD      |  收到一个连接请求，尚未确认                       | 
|  SYN SENT      |  已经发出连接请求，等待确认                       |
|  ESTABLISHED   |  连接建立，正常数据传输状态                       |
|  FIN WAIT 1    | （主动关闭）已经发送关闭请求，等待确认              |
|  FIN WAIT 2    | （主动关闭）收到对方关闭确认，等待对方关闭请求        |
|  TIMED WAIT    |  完成双向关闭，等待所有分组死掉                    |
|  CLOSING       |  双方同时尝试关闭，等待对方确认                    |
|  CLOSE WAIT    | （被动关闭）收到对方关闭请求，已经确认              |
|  LAST ACK      | （被动关闭）等待最后一个关闭确认，并等待所有分组死掉  |   
        
> 介绍完了tcp相关的基本概念，我们继续介绍tcp的运行机制。我将分成两部分来描述，即**保障可靠性**的相关机制和**提高性能**的相关机制。

 # 保障可靠性
 ## 确认应答机制
 tcp协议会将**数据的每个字节**都标记上编号（**序列号**）。每次数据传送，都会在报头的**seq位**，标注上当前传送到了哪一部分（序号表示）。而与之对应的ACK报文都会在**ack位**上返回上次的seq位上的序号，以表示这部分数据，我收到了。       


 <center> 

 ![ack机制](/images/tcp_ack.jpg)         
 </center>

 ## 链接管理机制
 

 
 ## 超时重传机制
 
 ## 流量管理机制
 
 ## 拥塞控制机制   
 
 ## 校验和机制
 
 # 提高性能
 ## 滑动窗口机制
 
 ## 快重传机制
 
 ## 延迟应答

 ## 捎带应答


# 参考文献
* [TCP/IP Reference | Nmap Network Scanning](https://nmap.org/book/tcpip-ref.html)
* [TCP 状态机](https://www.cnblogs.com/huntaiji/p/4043967.html)
* [TCP 详解](https://blog.csdn.net/sinat_36629696/article/details/80740678)
* [TCP 的那些事儿（上）](https://kb.cnblogs.com/page/209100/)
* [TCP 的那些事儿（下）](https://kb.cnblogs.com/page/209101/)
* [TCP协议分析](https://www.jianshu.com/p/d6dcb880b56b?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)
