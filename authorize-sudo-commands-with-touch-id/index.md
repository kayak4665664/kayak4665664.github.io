# Authorize sudo Commands With Touch ID

Authorize sudo commands with Touch Id, so you don&#39;t have to enter your password every time.
&lt;!--more--&gt;

In Terminal, enter the following command, then restart Terminal.
``` shell
sudo sed -i &#34;.bak&#34; &#39;2s/^/auth       sufficient     pam_tid.so\&#39;$&#39;\n/g&#39; /etc/pam.d/sudo
```

This command first backs up `/etc/pam.d/sudo` to `/etc/pam.d/sudo.bak`, then inserts `auth       sufficient     pam_tid.so` on the second line.

If you want to restore the default settings, you can use the following command:
``` shell
sudo mv /etc/pam.d/sudo.bak /etc/pam.d/sudo
```

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/authorize-sudo-commands-with-touch-id/  

