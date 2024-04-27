# Simulate Locations for iOS17

I need to simulate location on iPhone recently. After some research, I finally found a simple and effective method.
&lt;!--more--&gt;

I found several methods online, without jailbreaking iPhone. The first one is to use [AnyGo](https://itoolab.com/gps-location-changer/), which is effective but requires payment. The second one is to use an Android phone with root permission, install [OTGLocation](https://github.com/cczhr/OTGLocation), and then connect the iPhone to this Android phone. Other methods include using Xcode, i4Tools, or external devices, or even simulating satellite signals to deceive the iPhone.

I think these methods are too complicated. I found a simple and effective method at [https://shawnhuangyh.com/post/ios-17-location-simulation/](https://shawnhuangyh.com/post/ios-17-location-simulation/), which mainly uses [pymobiledevice3](https://github.com/doronz88/pymobiledevice3).

### 1. Install pymobiledevice3 on macOS:
```bash
python3 -m pip install -U pymobiledevice3
```

### 2. Enable developer mode on iPhone, located at `Settings -&gt; Privacy &amp; Security -&gt; Developer Mode`.

### 3. Connect the iPhone to macOS, and execute:
```bash
sudo python3 -m pymobiledevice3 remote start-tunnel
```
It will print something like the following:
```
Interface: utun6
RSD Address: fd7b:e5b:6f53::1
RSD Port: 64337
Use the follow connection option:
--rsd fd7b:e5b:6f53::1 64337
```
`RSD Address` and `RSD Port` will be used in step 5.

### 4. Make sure the iPhone is not locked at this time, and execute on macOS:
```bash
sudo pymobiledevice3 mounter auto-mount
```

### 5. Continue to execute on macOS:
```bash
pymobiledevice3 developer dvt simulate-location set --rsd &lt;RSD Address&gt; &lt;RSD Port&gt; -- &lt;latitude&gt; &lt;longtitude&gt;
```

Replace `&lt;RSD Address&gt;` and `&lt;RSD Port&gt;` with the values printed in step 3, and replace `&lt;latitude&gt;` and `&lt;longtitude&gt;` with the latitude and longitude you want to simulate. Look at the iPhone, the location has been simulated successfully. After terminating the simulation, the iPhone will return to the real location.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/simulate-locations-for-ios17/  

