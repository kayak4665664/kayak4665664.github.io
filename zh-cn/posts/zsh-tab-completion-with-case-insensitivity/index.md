# zsh: Tab补全大小写不敏感

在macOS中，如果在`~`执行`cd documents`是可以切换到`Documents`目录的，但是无法用`Tab`补全。
&lt;!--more--&gt;
解决的方法是在`~/.zshrc`中添加如下代码：
```shell
autoload -Uz compinit &amp;&amp; compinit
zstyle &#39;:completion:*&#39; matcher-list &#39;m:{a-z}={A-Z}&#39;
```

重新打开终端就可以见到效果了。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/zsh-tab-completion-with-case-insensitivity/  

