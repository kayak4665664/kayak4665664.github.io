# Mac中的Kerberos是什么？

我在通知设置里忽然发现了这个Kerberos，这是什么？
&lt;!--more--&gt;

我问了Bing，它说：

{{&lt; admonition quote &gt;}}
您好，这是Bing。Kerberos是一种身份验证系统，可以让您在网络上安全地访问各种服务。Mac中的Kerberos是基于MIT Kerberos实现的，支持Kerberos v5和v4协议、GSSAPI、图形化认证界面和票据缓存。您可以使用命令行或者票据查看器应用来管理您的Kerberos票据。

1. [https://uit.stanford.edu/service/ess/mac/docs/kerberos_macOS](https://uit.stanford.edu/service/ess/mac/docs/kerberos_macOS)
2. [https://web.mit.edu/macdev/www/kerberos.html](https://web.mit.edu/macdev/www/kerberos.html)
3. [https://support.apple.com/zh-cn/guide/deployment/depe6a1cda64/web](https://support.apple.com/zh-cn/guide/deployment/depe6a1cda64/web)
4. [https://support.apple.com/en-gb/guide/deployment/depe6a1cda64/web](https://support.apple.com/en-gb/guide/deployment/depe6a1cda64/web)
{{&lt; /admonition &gt;}}

看来这个Kerberos是包含在macOS中的，它就位于`/System/Library/CoreServices/Applications/Ticket Viewer.app`，并不是恶意程序。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/what-is-kerberos-in-mac/  

