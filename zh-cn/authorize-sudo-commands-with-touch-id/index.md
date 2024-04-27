# 用Touch ID授权sudo命令

使用Touch ID来验证sudo命令，这样就不用每次都输入密码了。
&lt;!--more--&gt;

在Terminal中输入以下命令，之后重启Terminal即可。
``` shell
sudo sed -i &#34;.bak&#34; &#39;2s/^/auth       sufficient     pam_tid.so\&#39;$&#39;\n/g&#39; /etc/pam.d/sudo
```

这个命令首先备份`/etc/pam.d/sudo`为`/etc/pam.d/sudo.bak`，然后在第二行插入`auth       sufficient     pam_tid.so`。

如果恢复默认设置，可以使用以下命令：
``` shell
sudo mv /etc/pam.d/sudo.bak /etc/pam.d/sudo
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/authorize-sudo-commands-with-touch-id/  

