# 当使用Touch ID解锁时聚焦（Spotlight）无法正常使用


前几天忽然发现聚焦搜索不出东西来了，同时在设置应用里搜索设置项也搜索不出来。似乎这个现象以前也有，这次终于被我注意到了。
&lt;!--more--&gt;

刚开始我以为是聚焦的索引出了问题，按网上的方法重置了几次索引，比如执行`sudo mdutil -a -E`。刚重置完是正常的，但过了一会又不行了，不知道问题出在哪了。

连续试了几天，我终于可以稳定复现这个问题：只有在我使用Touch ID解锁电脑的时候，聚焦搜索才会失效。如果我使用密码解锁，聚焦搜索就能正常使用，或者在Touch ID解锁后找个机会输入一次密码，比如执行`sudo`命令，聚焦搜索立刻就正常了。因为用密码或者Touch ID都是很常见的操作，很难想到问题出在这里。

我试了试新建了一个用户是正常的，但是用迁移助理把之前的时间机器备份导入之后，这个问题又出现了。

我在网上搜了一下，在Alfred论坛上也有人遇到了和我一样的问题，[Spotlight indexing issues in Ventura 13.6.1](https://www.alfredforum.com/topic/21140-spotlight-indexing-issues-in-ventura-1361/)，但是没有解决的办法。我在macOS的网站上反馈了一下就石沉大海了。

我想只要在Touch ID解锁后自动输入一次密码就可以缓解这个问题。我用`brew`分别安装了`sleepwatcher`和`expect`，分别用于监听电脑休眠和自动输入密码。我写了几个脚本：

### spotlight.exp
```shell
#! /usr/bin/expect -f
set script_dir [file dir [info script]]
set password [exec $script_dir/get_password.sh]
spawn sudo mdutil -vsa
expect &#34;Password:&#34;
send &#34;$password\r&#34;
interact
```
### get_password.sh
```shell
#!/bin/sh
password=$(security find-generic-password -a &#39;$YOUR_USER_NAME&#39; -s &#39;SleepwatcherPassword&#39; -w)
echo $password
```

这里需要提前执行`security add-generic-password -a &#39;$YOUR_USER_NAME&#39; -s &#39;SleepwatcherPassword&#39; -w &#39;$YOUR_PASSWORD&#39;`来保存密码.

### .wakeup
```shell
#!/bin/sh
expect /path/to/spotlight.exp
```

这样每次电脑休眠唤醒后，`sleepwatcher`会自动执行`.wakeup`脚本，自动输入密码，这样聚焦搜索就能正常使用了。但是如果锁定之后没有来得及休眠就又用Touch ID解锁了，还是会出现问题，不过这种情况比较少见。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/spotlight-not-working-properly-with-touch-id-unlock-on-macos/  

