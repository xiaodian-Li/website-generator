---
title: HTTP基础指南（图解http总结）
date: 2017-11-11 15:22:53
tags: [http网络]
categories: http基础
---
(以下是http相关知识，在前端开发中知道这些基础的知识也是必要的，本文是根据图解http的小总结，希望可以帮助大家更好的理解http)
## 了解Web及网络基础
1.相关概念：
* DNS:位于应用层，提供域名到IP地址之间的解析服务。<br><!--more-->
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/11.png)
* TCP协议: 位于传输层，提供可靠的字节流服务。（就是将大块数据分割成以报文段为单位的数据包进行管理）
* IP协议: 位于网络层，tcp/ip协议族中指网际协议，是一种协议名称，作用把各种数据包传递给对方。（确保成功发送，满足ip地址和mac地址）
* IP地址:指明节点被分配到的地址；MAC地址：指网卡所属的固定地址
* ARP协议:解析地址协议，根据IP反查MAC<br>
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/12.png)
* RFC:用来制定http协议技术标准文档
* TCP/IP协议族层次分为以下4层
* 应用层：决定了向用户提供应用服务时通信的活动。（eg:文件传输协议FTP，域名系统DNS，http协议）
* 传输层：为上层应用层，提供处于网络连接的两台计算机之间的数据传输。（性质不同的协议，传输控制协议TCP， 用户数据报协议UDP）
* 网络层：处理网络流动的数据包。（数据包是网络传输的）
* 链路层: 连接网络的硬件部分。
* 三次握手：发送端发送带SYN标志数据包给对方---->接收端接受回传带SYN/ACK标志数据包确认信息--→发送端回传一个带ACK标志的数据包。
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/13.png)
2.相关传输过程：
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/14.png)                  ![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/15.png)

3.URI与URL
* URI（Uniform Resource Identifier）：统一资源标识符。
* URL(Uniform Resource Locator)：统一资源定位符。
URI用字符串标识某一互联网资源，而URL表示资源的地点（互联网上所处的位置）。URL是URI的子集。

<br>

## 简单的HTTP协议
1.HTTP是客户端和服务端之间的通信。（是不保存状态的协议）
客户端：请求访问文本或者图像资源的一方
服务端：提供资源响应的一方.
2.请求报文构成：包括请求方法，URI,协议版本，可选请求首部字段，内容，实体构成的。
常用请求方法：
（1）GET：获取资源，请求访问已被URI识别的资源。
（2）POST:传输实体的主体，常用于表单。
（3）PUT：传输文件，要求请求报文主体包含文件内容（有安全性问题，通常不用）
（4）HEAD:获得报文首部，（不返回主体部分，用于确认URI有效性以及资源更新的日期时间等）
（5）DELETE:删除文件
（6）OPTIONS: 客户端带着询问支持的方法。
（7）CONNECT:在于代理服务器通信时建立隧道，实现用隧道协议通信
3.因为http是不保存协议，所以用到Cookie状态管理。
第一次客户端没带cookie到服务端，服务端响应返回添加cookie，第二次以后请求服务端就带有cookie，最后得到响应。
请求报文------响应报文--------请求报文
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/2.png)

<br>

## 返回结果的HTTP状态码
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/4.png)
* 2XX:成功
200：客户端发送的请求在服务器端正常处理了
204:请求成功，但没有资源返回
206： 客户端进行范围请求，服务器端执行了Get请求
*  3XX： 重定向
301： 永久重定向，请求资源被重新分配了新的URI，以后使用的是最新的URI
302，307：临时性重定向，请求资源被分配新的URI，只本次使用新的
303：请求的资源存在着另一个URI，使用get定向获取资源
301,302,303响应状态码返回时，几乎所有的浏览器都会把post-->get，并删除报文的主体，之后自动发送求
304： 客户端发送附带条件的请求，服务端允许请求访问资源，但未满足条件的情况
* 4XX：客户端错误
400： 请求报文中存在语法错误
401： 发送请求需要http认证的认证信息，（若之前进行过一次请求，就表示用户认证失败）
403： 对请求资源访问被服务器拒绝
404：服务器上无法找到请求资源
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/5.png)
*  5XX： 服务器错误
500：服务器在执行请求时发生故障（也可能web应用存在Bug）
503: 服务器暂时处于超负载活停机维护，无法处理请求

> 最后注意： 状态码和状况不一致，5开头不一定就是服务器错了，客户端的bug也可能造成5，web的内部出错，状态码依旧可以返回200

<br>


## HTTP报文内的HTTP信息
* http通信过程包括 从客户端→服务端 以及 服务端-→客户端。
请求行和响应报文的结构
![Alt text](https://minisite.daojia.com/assets/minisite/2017/sy/img/3.png)

* 请求行： 包括请求方法，请求URI和HTTP版本   (get /HTTP/1.1）
* 状态行：包括表明相应结果的状态码，原因短语和HTTP版本 （HTTP/1.1 200OK）
* 首部字段： 表示请求的各种条件和属性的各类首部
分为： 通用首部，请求首部，响应首部，实体首部。
* 其他: HTTP的RFC里未定义的首部（cookie等）

<br>











