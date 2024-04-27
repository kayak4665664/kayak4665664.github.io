# Randomize MAC Address for macOS

On iOS and iPadOS, you can enable private WiFi address to randomize MAC address in settings. There is no such option on macOS, but we can do it through the command line.
&lt;!--more--&gt;

I found SpoofMAC on Github, which is a Python script that works not only on macOS but also on Windows and Linux. It can randomize MAC address and set MAC address to any value.

{{&lt; link href=&#34;https://github.com/feross/spoofmac&#34; content=&#34;SpoofMAC&#34; title=&#34;SpoofMAC&#34; card=true &gt;}}

Installing SpoofMAC is simple, just `pip install SpoofMAC`.

## Usage 
Here is an example of using SpoofMAC to modify MAC address on macOS.

{{&lt; admonition tip &gt;}}
To run `spoof-mac` directly in the terminal, you need to add `bin` to `PATH`. If you are using `zsh`, you can add it in `~/.zshrc`, for example, `export PATH=$PATH:~/Library/Python/3.9/bin`.
{{&lt; /admonition &gt;}}

1. First, list all available devices
``` shell
spoof-mac list
```
You will get an output like this
{{&lt; admonition example &gt;}}
{?-} &#34;Ethernet&#34; on device &#34;en0&#34; with MAC address 70:56:51:BE:B3:00  
{?-} &#34;Wi-Fi&#34; on device &#34;en1&#34; with MAC address 70:56:51:BE:B3:01  
{?-} &#34;Bluetooth PAN&#34; on device &#34;en1&#34;  
{{&lt; /admonition &gt;}}

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
> URL: http://localhost:1313/posts/randomize-mac-address-for-macos/  

