# iOS17模拟定位

最近需要在iPhone上模拟定位，研究了一下，终于发现了一个简单有效的方法。
&lt;!--more--&gt;

我在网上找到了好几种办法，在不越狱iPhone的情况下。第一种是使用[AnyGo](https://itoolab.com/gps-location-changer/)，这个软件是有效的，但是需要付费。第二种是用一个具有root权限的安卓手机，在上面安装这个[OTGLocation](https://github.com/cczhr/OTGLocation)，之后把iPhone连接到这个安卓手机上。其他方法还有借助Xcode、爱思助手，或者是外接设备，甚至还可以模拟卫星信号欺骗手机。

我觉得这些办法都太麻烦了，在[https://shawnhuangyh.com/post/ios-17-location-simulation/](https://shawnhuangyh.com/post/ios-17-location-simulation/)这里找到一个简单有效的办法，主要使用了[pymobiledevice3](https://github.com/doronz88/pymobiledevice3)。

### 1. 在macOS上安装pymobiledevice3：
```bash
python3 -m pip install -U pymobiledevice3
```
### 2. 在iPhone中开启开发者模式，位于`Settings -&gt; Privacy &amp; Security -&gt; Developer Mode`。

### 3. 将iPhone连接到macOS上，在macOS上执行：
```bash
sudo python3 -m pymobiledevice3 remote start-tunnel
```
将会打印类似以下内容：
```
Interface: utun6
RSD Address: fd7b:e5b:6f53::1
RSD Port: 64337
Use the follow connection option:
--rsd fd7b:e5b:6f53::1 64337
```
`RSD Address`和`RSD Port`在第5步要用到。

### 4. 确保iPhone此时还没有锁屏，在macOS上执行：
```bash
sudo pymobiledevice3 mounter auto-mount
```

### 5. 继续在macOS中执行：
```bash
pymobiledevice3 developer dvt simulate-location set --rsd &lt;RSD Address&gt; &lt;RSD Port&gt; -- &lt;latitude&gt; &lt;longtitude&gt;
```
将`&lt;&gt;`中的内容替换为自己的内容，分别为第3步中的`RSD Address`和`RSD Port`，以及要模拟的纬度和经度。此时在iPhone上查看，定位应该已经变成了模拟的位置。在停止模拟后，iPhone的定位会自动恢复正常。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/simulate-locations-for-ios17/  

