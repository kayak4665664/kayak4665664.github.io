# battery: 限制Apple Silicon Macbook的电池充电

今天发现了一个有可以限制Apple Silicon Macbook电池充电的命令行工具，名字叫做**battery**。
<!--more-->

{{< link href="https://github.com/actuallymentor/battery" content="battery" title="battery" card=true >}}

之前我一直在用[AlDente](https://www.kayak4665664.com/zh-cn/aldente-limit-macbook-maximum-charging-percentage/)，与它相比，**battery**的优点是可以直接在命令行中使用，而且完全免费，而AlDente如果不付费就只能使用最基础的功能，而且它的图标还一直在菜单栏占用了一个位置。

只需一行命令即可安装：

``` bash
curl -s https://raw.githubusercontent.com/actuallymentor/battery/main/setup.sh | bash
```

安装完成后，可以使用`battery help`查看帮助信息，就是这么简单。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/battery-battery-charge-limiter-for-apple-silicon-macbook-devices/  

