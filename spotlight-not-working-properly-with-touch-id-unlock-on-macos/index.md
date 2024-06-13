# Spotlight Not Working Properly With Touch ID Unlock on MacOS


A few days ago, I suddenly found that Spotlight could not search anything, and the settings application could not search for settings items either. It seems that this phenomenon has occurred before, and this time I finally noticed it.
&lt;!--more--&gt;

At first, I thought it was a problem with the index of Spotlight, and I reset the index several times according to the methods on the Internet, such as executing `sudo mdutil -a -E`. It was normal immediately after the reset, but it didn&#39;t work after a while, and I don&#39;t know what went wrong.

After trying for several days, I finally can reproduce this problem stably: only when I unlock the computer using Touch ID, the Spotlight search will fail. If I unlock with a password, the Spotlight search can work normally, or after unlocking with Touch ID, find an opportunity to enter the password once, such as executing the `sudo` command, the Spotlight search will immediately work normally. Because using a password or Touch ID is a very common operation, it is difficult to think that the problem lies here.

I tried to create a new user, and it was normal, but after importing the previous Time Machine backup using the migration assistant, this problem reappeared.

I searched online and found that someone on the Alfred forum encountered the same problem as me, [Spotlight indexing issues in Ventura 13.6.1](https://www.alfredforum.com/topic/21140-spotlight-indexing-issues-in-ventura-1361/), but there is no solution. I reported it on the macOS website and no more response.

I think as long as I automatically enter the password once after unlocking with Touch ID, this problem can be alleviated. I used `brew` to install `sleepwatcher` and `expect` respectively, used to monitor computer sleep and automatically enter the password. I wrote a few scripts:

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

Here you need to execute `security add-generic-password -a &#39;$YOUR_USER_NAME&#39; -s &#39;SleepwatcherPassword&#39; -w &#39;$YOUR_PASSWORD&#39;` in advance to save the password.

### .wakeup
```shell
#!/bin/sh
expect /path/to/spotlight.exp
```

In this way, every time the computer wakes up from sleep, `sleepwatcher` will automatically execute the `.wakeup` script, automatically enter the password, so that the Spotlight search can work normally. But if you unlock with Touch ID after locking without sleeping, the problem will still occur, but this situation is relatively rare.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/spotlight-not-working-properly-with-touch-id-unlock-on-macos/  

