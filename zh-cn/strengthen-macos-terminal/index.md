# 强化macOS终端

macOS自带的终端很好用，但是感觉少了一些东西，所以我就把它强化一下。网上有好多人都推荐使用[Oh My Zsh](https://ohmyz.sh/)，但是不知道为什么，我在使用[Oh My Zsh](https://ohmyz.sh/)的时候经常会出现一些问题，所以这一次我没有使用它。
<!--more-->

## 美化
我用了starship来美化终端，它是一个轻量、迅速、跨平台的命令行主题。

{{< link href="https://starship.rs/zh-CN/" content="starship" title="starship" card=true >}}

在安装starship之前，需要安装[Nerd Font](https://www.nerdfonts.com/)字体，比如`Fira Code Nerd Font`。

可以使用Homebrew安装，然后在终端设置中启用`Fira Code Nerd Font`字体。

```bash
brew tap homebrew/cask-fonts
brew install --cask font-fira-code-nerd-font
```

之后，使用Homebrew来安装starship：`brew install starship`。在`~/.zshrc`的最后添加`eval "$(starship init zsh)"`，然后执行`source ~/.zshrc`。重新打开终端，就可以看到效果了。

更多的自定义配置可以参考[指南](https://starship.rs/zh-CN/guide/)。

## 扩展

### 1. zsh-fast-syntax-highlighting

这个插件可以高亮命令行输入的内容，让你的终端更加美观。

{{< link href="https://github.com/zdharma-continuum/fast-syntax-highlighting" content="zsh-fast-syntax-highlighting" title="zsh-fast-syntax-highlighting" card=true >}}

``` bash
brew install zsh-fast-syntax-highlighting
```

{{< admonition info >}}
To activate the syntax highlighting, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/opt/zsh-fast-syntax-highlighting/share/zsh-fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh`
{{< /admonition >}}

### 2. zsh-autosuggestions

这个插件可以根据你输入的内容，给出自动补全的建议。

{{< link href="https://github.com/zsh-users/zsh-autosuggestions" content="zsh-autosuggestions" title="zsh-autosuggestions" card=true >}}

``` bash
brew install zsh-autosuggestions
```

{{< admonition info >}}
To activate the autosuggestions, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autosuggestions/zsh-autosuggestions.zsh`  
You will also need to restart your terminal for this change to take effect.
{{< /admonition >}}

### 3. zsh-autocomplete

这个插件同样用于自动补全。

{{< link href="https://github.com/marlonrichert/zsh-autocomplete" content="zsh-autocomplete" title="zsh-autocomplete" card=true >}}

``` bash
brew install zsh-autocomplete
```

{{< admonition info >}}
1. Add at or near the top of your `.zshrc` file (before any calls to compdef): `source $HOMEBREW_PREFIX/share/zsh-autocomplete/zsh-autocomplete.plugin.zsh`
2. Remove any calls to compinit from your `.zshrc` file.
3. If you're using Ubuntu, add to your `.zshenv` file: `skip_global_compinit=1`  
Then restart your shell.
{{< /admonition >}}

### 4. zsh-autopair

这个插件可以自动配对括号、引号等。

{{< link href="https://github.com/hlissner/zsh-autopair" content="zsh-autopair" title="zsh-autopair" card=true >}}

``` bash
brew install zsh-autopair
```

{{< admonition info >}}
To activate autopair, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autopair/autopair.zsh`  
You will also need to restart your terminal for this change to take effect.
{{< /admonition >}}

### 5. z

这个插件可以快速跳转到你最常访问的目录。

{{< link href="https://github.com/rupa/z" content="z" title="z" card=true >}}

``` bash
brew install z
```

{{< admonition info >}}
For Bash or Zsh, put something like this in your `$HOME/.bashrc` or `$HOME/.zshrc`: `. $HOMEBREW_PREFIX/etc/profile.d/z.sh`
{{< /admonition >}}

另外，还可以在`.zshrc`中加入`setopt autocd`, 这样就可以直接输入目录名来切换到该目录了。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/strengthen-macos-terminal/  

