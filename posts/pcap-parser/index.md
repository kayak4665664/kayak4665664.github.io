# Pcap-Parser

[Previous article](https://www.kayak4665664.com/capture-packets-for-mobile-apps/) introduces how to capture packets, and this article introduces how to write a program to parse the captured packet files.
&lt;!--more--&gt;

{{&lt; admonition info &gt;}}
The source code involved in this article is in the GitHub repository:

{{&lt; /admonition &gt;}}

{{&lt; link href=&#34;https://github.com/kayak4665664/Pcap-Parser&#34; content=&#34;Pcap-Parser&#34; title=&#34;Pcap Parser - kayak4665664&#34; card=true &gt;}}

The Pcap file contains the information of the network data packet, including source IP address, destination IP address, source port, destination port, transport layer protocol, application layer protocol, etc. Therefore, the idea of the program is to parse from the data link layer to the application layer and parse out the protocol type and protocol data of each layer. In terms of implementation, you can refer to the analysis results of Wireshark.

For `C/C&#43;&#43;`, `&lt;pcap.h&gt;` can be used to process Pcap files. Afterward, use `&lt;net/ethernet.h&gt;`, `&lt;netinet/ip.h&gt;`, `&lt;netinet/tcp.h&gt;` defined the Ethernet header, IP header, and TCP header structure to parse the data Link layer, network layer, and transport layer. In addition, both the IP header and the TCP header have `options`, which is not in the structure.

There are many types of protocols in the application layer, and programs need to be written for each protocol. [My program](https://github.com/kayak4665664/Pcap-Parser) supports parsing `HTTP` and `TLS` protocols.

`HTTP` is a plain text protocol, and the data fields are separated by `\r\n`. In addition, it is necessary to consider that an `HTTP` message is divided into several packets, and the correct result can only be parsed after reassembling the relevant packets. And `TLS` is an encryption protocol, which is more complicated. It needs to be parsed according to the structure of the protocol, and reassembling should also be considered.

The above are just some simple ideas. There are many complicated situations that have not been covered.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/pcap-parser/  

