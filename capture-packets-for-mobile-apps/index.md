# Capture Packets for Mobile Apps

Packet capture for mobile apps using `Charles`, `Wireshark` and `tcpdump`.
&lt;!--more--&gt;

{{&lt; admonition info &gt;}}
I capture packets for iPhone on macOS, but the methods and principles are similar for other systems and devices.
{{&lt; /admonition &gt;}}

## Wireshark

Wireshark is an open-source network analysis tool that can be used to capture network packets. It can run on macOS, Windows, and Linux.

On macOS, Wireshark can be installed using `brew`:

```shell
brew install --cask wireshark
```

Capturing packets with Wireshark is also very simple. For example, selecting the `Wi-Fi` interface can capture packets from the wireless network card.

&lt;div align=&#34;center&#34;&gt;
{{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/Screenshot%202023-03-17%20at%2010.40.36.png&#34; alt=&#34;Wireshark&#34;&gt;}}
&lt;/div&gt;

## tcpdump

`tcpdump` is a command line tool that can be used to capture network packets. For example, if you want to capture packets on a server without a graphical interface, you can use it.

On macOS, `tcpdump` can also be installed using `brew`:

```shell
brew install tcpdump
```

Capturing packets with `tcpdump`, for example, capture packets from the `12345` port and save them as a `pcap` file:

```shell
tcpdump port 12345 -w capture.pcap
```

## Charles

Charles is an HTTP proxy and monitor that can be used to capture HTTP and HTTPS packets. It&#39;s like Fiddler on Windows.

On macOS, we can install Charles using `brew`:

```shell
brew install --cask charles
```

## Capture Packets for Mobile Apps

For MacBook, if Wi-Fi is already connected, the wireless hotspot cannot be turned on. So you need to use Charles to set up a proxy server, and then the phone connects to the proxy server. The main steps are as follows:

1. Both the macOS device and the iPhone are connected to a mobile hotspot turned on by the third device, making sure they are on the same local area network.
2. On the macOS device, open Charles and set up a proxy server. The proxy server port is `8888` by default.
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/Screenshot%202023-03-16%20at%2022.09.40.png&#34; alt=&#34;Charles&#34;&gt;}}
  &lt;/div&gt;

3. On the iPhone, set the proxy server to the macOS device. The proxy server port is `8888`.
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2160.PNG&#34; alt=&#34;Proxy&#34;&gt;}}
  &lt;/div&gt;

4. Access [chls.pro/ssl](chls.pro/ssl) in the iPhone browser, download and install the certificate.
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2161.PNG&#34; alt=&#34;Certificate installation&#34;&gt;}}
  &lt;/div&gt;

5. Trust the certificate in the iPhone settings `General -&gt; About -&gt; Certificate Trust Settings`.
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2162.PNG&#34; alt=&#34;Certificate trust settings&#34;&gt;}}
  &lt;/div&gt;

6. Install the configuration file for the proxy server in the iPhone settings `General -&gt; VPN &amp; Device Management`.
  &lt;div align=&#34;center&#34;&gt;
  {{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/IMG_2163.PNG&#34; alt=&#34;Configuration file&#34;&gt;}}
  &lt;/div&gt;

7. Since Charles can only capture HTTP and HTTPS packets, start Wireshark on the macOS device and select the `Wi-Fi` interface to capture packets of all protocols.

8. Open the mobile app on the iPhone and use it.

9. Stop capturing packets in Wireshark. The previously set proxy server port is `8888`, so you can filter irrelevant data packets through `tcp.port == 8888`, and save the filtered packets as a pcap file.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/capture-packets-for-mobile-apps/  

