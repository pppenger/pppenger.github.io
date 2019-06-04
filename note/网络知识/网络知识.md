### TCP

#### tcp flags

URG：紧急指针标志
**ACK：确认序号标志**
PSH：push标志
RST：重置连接标志
**SYN：同步序号，用于建立连接过程**
**FIN：finsish标志，用于释放连接**

#### TCP三次握手

流程：
第一次握手，建立连接时，客户端发送SYN包（syn=j）到服务器，并进入SYN_SEND状态，等待服务器确认；

第二次握手：服务器收到SYN包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；

第三次握手：客户端收到服务器的SYN+ACK包向服务器发送确认包ACK（ack=k+1），此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手

##### 首次握手隐患---SYN超时

问题起因：

server收到client的SYN，回复SYN-ACK的时候未收到ACK确认；
server不断重试直至超时，Linux默认等待63秒才短开连接

针对SYN Flood的防护措施

SYN队列满后，通过tcp_syncookies参数回发SYN Cookie

若为正常连接则Client会回发SYN Cookie，直接建立连接

##### 建立连接后，Client出现故障怎么办

保活机制

向对方发送保活探测报文，如果未收到响应则继续发送
尝试次数达到保活探测数仍未收到响应则中断连接

#### TCP四次挥手

第一次挥手：Client发送一个FIN，用来关闭Client到Server的数据传送，Client进入FIN_WAIT_1状态；

第二次挥手：Server收到FIN后，发送一个ACK给Client，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），Server进入CLOSE_WAIT状态；

第三次挥手：Server发送一个FIN，用来关闭Server到Client的数据传送，Server进入LAST_ACK状态；

第四次挥手：Client收到FIN后，Client进入TIME_WAIT状态，接着发送一个ACK给Server，确认序号为收到序号+1，Server进入CLOSERD状态，完成四次挥手；

##### 为什么会有TIME_WAIT状态？

确保有足够的时间让对方收到ACK包
避免新旧连接混淆

##### 服务器出现大量CLOSE_WAIT状态的原因？

对方关闭socket连接，我方忙于读或写，没有及时关闭连接

检查代码，特别是释放资源的代码
检查配置，特别是处理请求的线程配置

### UDP

#### UDP的特点

面向非连接；
不维护连接状态，支持同时向多个客户端传输相同的消息；
数据包报头只有8个字节，额外开销较小；
吞吐量只受限于数据生成速率，传输速率以及机器性能；
尽量大努力交付，不保证可靠交付，不需要维持复杂的链接状态表；
面向报文，不对应用程序提交的报文信息进行拆分或者合并；

