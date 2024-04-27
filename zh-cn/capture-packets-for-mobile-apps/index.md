# 手机App抓包

使用`Charles`、`Wireshark`和`tcpdump`对手机App抓包。
&lt;!--more--&gt;

{{&lt; admonition info &gt;}}
我在macOS上对iPhone进行抓包，但是对于其他系统和设备，方法和原理也是类似的。
{{&lt; /admonition &gt;}}

## Wireshark

Wireshark是一个开源的网络分析工具，可以用来抓取网络数据包。它可以在macOS、Windows和Linux上运行。

在macOS上，可以使用`brew`安装Wireshark：

```shell
brew install --cask wireshark
```
使用Wireshark抓包也很简单，比如选择`Wi-Fi`接口就可以抓无线网卡的数据包。

&lt;div align=&#34;center&#34;&gt;
{{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/Screenshot%202023-03-17%20at%2010.40.36.png&#34; alt=&#34;Wireshark&#34;&gt;}}
&lt;/div&gt;


## tcpdump

tcpdump是一个命令行工具，可以用来抓取网络数据包。假如在没有图形界面的服务器上，可以使用它来抓取数据包。

在macOS上，可以使用`brew`安装tcpdump：

```shell
brew install tcpdump
```

使用tcpdump抓包，比如抓取`12345`端口的数据包并保存为`pcap`文件：

```shell
tcpdump port 12345 -w capture.pcap
```

## Charles

Charles是一个HTTP代理服务器，可以用来抓取HTTP和HTTPS的数据包，和Fiddler类似。

在macOS上，也使用`brew`安装Charles：

```shell
brew install --cask charles
```

## 手机App抓包

对于MacBook，如果已经连接了Wi-Fi，就不能开启无线热点了。所以需要用Charles来建立一个代理服务器，然后手机连接到这个代理服务器上。主要步骤如下：

1. macOS设备和iPhone都连接到第三个设备开启的移动热点，确保处于同一个局域网内。
2. 在macOS设备中启动Charles，设置代理服务，默认端口为`8888`。  
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/Screenshot%202023-03-16%20at%2022.09.40.png&#34; alt=&#34;Charles&#34;&gt;}}
  &lt;/div&gt;

3. 在iPhone的无线网络设置中，将代理服务器设置为macOS设备的IP地址，端口为`8888`。  
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2160.PNG&#34; alt=&#34;代理服务器&#34;&gt;}}
  &lt;/div&gt;

4. iPhone在浏览器中访问[chls.pro/ssl](chls.pro/ssl)，下载并安装证书。  
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2161.PNG&#34; alt=&#34;安装证书&#34;&gt;}}
  &lt;/div&gt;

5. iPhone在`General -&gt; About -&gt; Certificate Trust Settings`中，将Charles的证书设置为信任。  
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2162.PNG&#34; alt=&#34;信任证书&#34;&gt;}}
  &lt;/div&gt;

6. iPhone在`General -&gt; VPN &amp; Device Management`中安装Charles的描述文件。  
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2163.PNG&#34; alt=&#34;安装描述文件&#34;&gt;}}
  &lt;/div&gt;

7. 由于Charles只能抓取HTTP和HTTPS的数据包，所以这里在macOS设备中启动Wireshark，选择`Wi-Fi`接口抓取所有协议的数据包。

8. 在iPhone中打开需要抓包的App，进行相关操作。

9. Wireshark停止抓包，之前设置的代理服务器端口是`8888`，所以可以通过`tcp.port == 8888`过滤无关的数据包，将过滤后的包保存为pcap文件。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/capture-packets-for-mobile-apps/  

