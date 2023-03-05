# Mac上出现了多个版本的Edge浏览器

忽然发现我的Mac上竟然有2个Edge Dev，分别是111.0.1660.13和111.0.1660.12，而且这2个都能正常启动。我希望保留最新版本的，把旧版的卸载掉。
<!--more-->

## 方法
### 1
以Dev版本为例，切换目录到以下位置
```
cd /Applications/Microsoft\ Edge\ Dev.app/Contents/Frameworks/Microsoft\ Edge\ Framework.framework/Versions
```
也可以在访达中按下`control + shift + G`，输入要前往的位置

### 2
执行`ls -l`，可以看到类似的输出
{{< admonition example >}}
drwxrwxr-x 14 user admin 448 Feb 11 11:32 111.0.1660.12
drwxrwxr-x 14 user admin 448 Feb 17 08:54 111.0.1660.13
lrwxrwxr-x 1 user admin 13 Feb 17 08:54 Current -> 111.0.1660.13
{{< /admonition >}}
或者在访达中点击`Current`，确认指向的版本

### 3
使用`rm -rf`删除其他旧版本的，或者也可以在访达中删除

### 4
最后一步，这一步同样也可以在访达中进行
```
cd ~/Library/Application\ Support/Microsoft
rm -rf EdgeUpdater
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/multiple-versions-of-edge-browser-appear-on-mac/  

