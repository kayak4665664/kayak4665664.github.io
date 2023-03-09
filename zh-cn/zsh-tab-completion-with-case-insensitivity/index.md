# zsh: Tab补全大小写不敏感

在macOS中，如果在`~`执行`cd documents`是可以切换到`Documents`目录的，但是无法用`Tab`补全。
<!--more-->
解决的方法是在`~/.zshrc`中添加如下代码：
```shell
autoload -Uz compinit && compinit
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'
```

重新打开终端就可以见到效果了。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/zsh-tab-completion-with-case-insensitivity/  

