# zsh: Tab Completion With Case Insensitivity

If you are using macOS, you can switch to the `Documents` directory by executing `cd documents` in `~`, but you cannot use `Tab` to complete it.
<!--more-->

The solution is to add the following code to `~/.zshrc`:
```shell
autoload -Uz compinit && compinit
zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'
```

Open a new terminal and you will see the effect.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zsh-tab-completion-with-case-insensitivity/  

