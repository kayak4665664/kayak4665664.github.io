# Randomize MAC Address for macOS

On iOS and iPadOS, you can enable private WiFi address to randomize MAC address in settings. There is no such option on macOS, but we can do it through the command line.
<!--more-->

I found SpoofMAC on Github, which is a Python script that works not only on macOS but also on Windows and Linux. It can randomize MAC address and set MAC address to any value.

{{< link href="https://github.com/feross/spoofmac" content="SpoofMAC" title="SpoofMAC" card=true >}}

Installing SpoofMAC is simple, just `pip install SpoofMAC`.

## Usage 
Here is an example of using SpoofMAC to modify MAC address on macOS.

{{< admonition tip >}}
To run `spoof-mac` directly in the terminal, you need to add `bin` to `PATH`. If you are using `zsh`, you can add it in `~/.zshrc`, for example, `export PATH=$PATH:~/Library/Python/3.9/bin`.
{{< /admonition >}}

1. First, list all available devices
``` shell
spoof-mac list
```
You will get an output like this
{{< admonition example >}}
{?-} "Ethernet" on device "en0" with MAC address 70:56:51:BE:B3:00  
{?-} "Wi-Fi" on device "en1" with MAC address 70:56:51:BE:B3:01  
{?-} "Bluetooth PAN" on device "en1"  
{{< /admonition >}}

2. Then, randomize MAC address
``` shell
sudo spoof-mac randomize en1
# or
sudo spoof-mac randomize wifi
```

To restore MAC address, just run
``` shell
sudo spoof-mac reset en1
# or
sudo spoof-mac reset wifi
```


---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/randomize-mac-address-for-macos/  

