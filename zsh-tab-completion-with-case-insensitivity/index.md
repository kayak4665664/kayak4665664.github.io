# Zsh: Tab Completion With Case Insensitivity

If you are using macOS, you can switch to the `Documents` directory by executing `cd documents` in `~`, but you cannot use `Tab` to complete it.
&lt;!--more--&gt;

The solution is to add the following code to `~/.zshrc`:
```shell
autoload -Uz compinit &amp;&amp; compinit
zstyle &#39;:completion:*&#39; matcher-list &#39;m:{a-z}={A-Z}&#39;
```

Open a new terminal and you will see the effect.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zsh-tab-completion-with-case-insensitivity/  

