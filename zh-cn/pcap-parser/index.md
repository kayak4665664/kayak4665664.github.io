# Pcap Parser

[上一篇文章](https://www.kayak4665664.com/zh-cn/capture-packets-for-mobile-apps/)介绍了如何抓包，这篇文章介绍编写程序解析抓包文件。
<!--more-->

{{< admonition info >}}
本文涉及的源代码在GitHub仓库：
{{< /admonition >}}

{{< link href="https://github.com/kayak4665664/Pcap-Parser" content="Pcap Parser" title="Pcap Parser - kayak4665664" card=true >}}

Pcap文件中包含了网络数据包的信息，包括源IP地址、目的IP地址、源端口、目的端口、传输层协议、应用层协议等。因此，程序的思路就是从数据链路层开始解析，直到应用层，解析出每一层的协议类型和协议数据。在实现上可以参考Wireshark的解析结果。

对于`C/C++`，可以使用`<pcap.h>`处理Pcap文件。之后，使用`<net/ethernet.h>`、`<netinet/ip.h>`、`<netinet/tcp.h>`定义的以太网头部、IP头部、TCP头部结构体解析数据链路层、网络层、传输层。另外，IP头部和TCP头部都有`options`，这个字段结构体中没有。

应用层的协议种类比较多，需要针对每一种协议编写程序。[我的程序](https://github.com/kayak4665664/Pcap-Parser)支持解析`HTTP`和`TLS`协议。

`HTTP`是明文协议，数据字段之间是用`\r\n`分隔的，另外需要考虑一个`HTTP`消息分成了好多个packet，对相关packet重组之后才能解析出正确的结果。而`TLS`是加密协议，比较复杂，要按照协议的结构进行解析，也要考虑重组的情况。

以上只是一些简单的思路，实际上还有许多复杂的情况没有覆盖。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/pcap-parser/  

