# 随机化macOS的MAC地址

在iOS和iPadOS上，可以在设置中开启私有WiFi地址来随机化MAC地址。在macOS上没有这个选项，但是我们可以通过命令行来实现这一点。
<!--more-->

我在Github上找到了SpoofMAC，它是一个Python脚本，不仅适用于macOS，也可以在Windows和Linux上使用。它可以随机化MAC地址，也可以将MAC地址设置为任何值。

{{< link href="https://github.com/feross/spoofmac" content="SpoofMAC" title="SpoofMAC" card=true >}}

安装SpoofMAC很简单，只需要`pip install SpoofMAC`。

## 使用方法

下面是在macOS上使用SpoofMAC修改MAC地址的示例。

{{< admonition tip >}}
要直接在终端中运行`spoof-mac`，需要将`bin`添加到`PATH`中。如果你使用的是`zsh`，你可以在`~/.zshrc`中添加,例如`export PATH=$PATH:~/Library/Python/3.9/bin`。
{{< /admonition >}}

1. 首先，列出所有可用的设备
``` shell
spoof-mac list
```
将会得到类似下面的输出
{{< admonition example >}}
{?-} "Ethernet" on device "en0" with MAC address 70:56:51:BE:B3:00  
{?-} "Wi-Fi" on device "en1" with MAC address 70:56:51:BE:B3:01  
{?-} "Bluetooth PAN" on device "en1"  
{{< /admonition >}}

2. 然后，随机化MAC地址
``` shell
sudo spoof-mac randomize en1
# 或者
sudo spoof-mac randomize wifi
```
要复原MAC地址，只需运行
``` shell
sudo spoof-mac reset en1
# 或者
sudo spoof-mac reset wifi
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/randomize-mac-address-for-macos/  

