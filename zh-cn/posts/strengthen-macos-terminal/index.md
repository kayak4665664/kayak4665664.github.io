# 强化macOS终端

macOS自带的终端很好用，但是感觉少了一些东西，所以我就把它强化一下。网上有好多人都推荐使用[Oh My Zsh](https://ohmyz.sh/)，但是不知道为什么，我在使用[Oh My Zsh](https://ohmyz.sh/)的时候经常会出现一些问题，所以这一次我没有使用它。
&lt;!--more--&gt;

## 美化
我用了starship来美化终端，它是一个轻量、迅速、跨平台的命令行主题。

{{&lt; link href=&#34;https://starship.rs/zh-CN/&#34; content=&#34;starship&#34; title=&#34;starship&#34; card=true &gt;}}

在安装starship之前，需要安装[Nerd Font](https://www.nerdfonts.com/)字体，比如`Fira Code Nerd Font`。

可以使用Homebrew安装，然后在终端设置中启用`Fira Code Nerd Font`字体。

```bash
brew tap homebrew/cask-fonts
brew install --cask font-fira-code-nerd-font
```

之后，使用Homebrew来安装starship：`brew install starship`。在`~/.zshrc`的最后添加`eval &#34;$(starship init zsh)&#34;`，然后执行`source ~/.zshrc`。重新打开终端，就可以看到效果了。

更多的自定义配置可以参考[指南](https://starship.rs/zh-CN/guide/)。

## 扩展

### 1. zsh-fast-syntax-highlighting

这个插件可以高亮命令行输入的内容，让你的终端更加美观。

{{&lt; link href=&#34;https://github.com/zdharma-continuum/fast-syntax-highlighting&#34; content=&#34;zsh-fast-syntax-highlighting&#34; title=&#34;zsh-fast-syntax-highlighting&#34; card=true &gt;}}

``` bash
brew install zsh-fast-syntax-highlighting
```

{{&lt; admonition info &gt;}}
To activate the syntax highlighting, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/opt/zsh-fast-syntax-highlighting/share/zsh-fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh`
{{&lt; /admonition &gt;}}

### 2. zsh-autosuggestions

这个插件可以根据你输入的内容，给出自动补全的建议。

{{&lt; link href=&#34;https://github.com/zsh-users/zsh-autosuggestions&#34; content=&#34;zsh-autosuggestions&#34; title=&#34;zsh-autosuggestions&#34; card=true &gt;}}

``` bash
brew install zsh-autosuggestions
```

{{&lt; admonition info &gt;}}
To activate the autosuggestions, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autosuggestions/zsh-autosuggestions.zsh`  
You will also need to restart your terminal for this change to take effect.
{{&lt; /admonition &gt;}}

### 3. zsh-autocomplete

这个插件同样用于自动补全。

{{&lt; link href=&#34;https://github.com/marlonrichert/zsh-autocomplete&#34; content=&#34;zsh-autocomplete&#34; title=&#34;zsh-autocomplete&#34; card=true &gt;}}

``` bash
brew install zsh-autocomplete
```

{{&lt; admonition info &gt;}}
1. Add at or near the top of your `.zshrc` file (before any calls to compdef): `source $HOMEBREW_PREFIX/share/zsh-autocomplete/zsh-autocomplete.plugin.zsh`
2. Remove any calls to compinit from your `.zshrc` file.
3. If you&#39;re using Ubuntu, add to your `.zshenv` file: `skip_global_compinit=1`  
Then restart your shell.
{{&lt; /admonition &gt;}}

### 4. zsh-autopair

这个插件可以自动配对括号、引号等。

{{&lt; link href=&#34;https://github.com/hlissner/zsh-autopair&#34; content=&#34;zsh-autopair&#34; title=&#34;zsh-autopair&#34; card=true &gt;}}

``` bash
brew install zsh-autopair
```

{{&lt; admonition info &gt;}}
To activate autopair, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autopair/autopair.zsh`  
You will also need to restart your terminal for this change to take effect.
{{&lt; /admonition &gt;}}

### 5. z

这个插件可以快速跳转到你最常访问的目录。

{{&lt; link href=&#34;https://github.com/rupa/z&#34; content=&#34;z&#34; title=&#34;z&#34; card=true &gt;}}

``` bash
brew install z
```

{{&lt; admonition info &gt;}}
For Bash or Zsh, put something like this in your `$HOME/.bashrc` or `$HOME/.zshrc`: `. $HOMEBREW_PREFIX/etc/profile.d/z.sh`
{{&lt; /admonition &gt;}}

另外，还可以在`.zshrc`中加入`setopt autocd`, 这样就可以直接输入目录名来切换到该目录了。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/strengthen-macos-terminal/  

