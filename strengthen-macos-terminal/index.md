# Strengthen macOS Terminal

The terminal of macOS is very good, but it feels like it's missing something, so I strengthened it. There are many people who recommend using [Oh My Zsh](https://ohmyz.sh/), but I don't know why, I often have some problems when I use [Oh My Zsh](https://ohmyz.sh/), so this time I didn't use it.
<!--more-->

## Beautify

I used starship to beautify the terminal, which is a lightweight, fast, cross-platform command line theme.

{{< link href="https://starship.rs/" content="starship" title="starship" card=true >}}

Before installing starship, you need to install the [Nerd Font](https://www.nerdfonts.com/) font, such as `Fira Code Nerd Font`.

You can use Homebrew to install it, and then enable the `Fira Code Nerd Font` font in the terminal settings.

```bash
brew tap homebrew/cask-fonts
brew install --cask font-fira-code-nerd-font
```

Then, use Homebrew to install starship: `brew install starship`. Add `eval "$(starship init zsh)"` at the end of `~/.zshrc`, and then execute `source ~/.zshrc`. Reopen the terminal, and you can see the effect.

More custom configuration can be found in the [guide](https://starship.rs/guide/).

## Extension

### 1. zsh-fast-syntax-highlighting

This plugin can highlight the content entered on the command line, making your terminal more beautiful.

{{< link href="https://github.com/zdharma-continuum/fast-syntax-highlighting" content="zsh-fast-syntax-highlighting" title="zsh-fast-syntax-highlighting" card=true >}}

``` bash
brew install zsh-fast-syntax-highlighting
```

{{< admonition info >}}
To activate the syntax highlighting, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/opt/zsh-fast-syntax-highlighting/share/zsh-fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh`
{{< /admonition >}}

### 2. zsh-autosuggestions

This plugin can automatically complete the command line based on the history.

{{< link href="https://github.com/zsh-users/zsh-autosuggestions" content="zsh-autosuggestions" title="zsh-autosuggestions" card=true >}}

``` bash
brew install zsh-autosuggestions
```

{{< admonition info >}}
To activate the autosuggestions, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autosuggestions/zsh-autosuggestions.zsh`  
You will also need to restart your terminal for this change to take effect.
{{< /admonition >}}

### 3. zsh-completions

This plugin can also complete the command line.

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

This plugin can automatically complete the brackets, and quotes.

{{< link href="https://github.com/hlissner/zsh-autopair" content="zsh-autopair" title="zsh-autopair" card=true >}}

``` bash
brew install zsh-autopair
```

{{< admonition info >}}
To activate autopair, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autopair/autopair.zsh`  
You will also need to restart your terminal for this change to take effect.
{{< /admonition >}}

### 5. z

This plugin can quickly jump to the directory you want to go to.

{{< link href="https://github.com/rupa/z" content="z" title="z" card=true >}}

``` bash
brew install z
```

{{< admonition info >}}
For Bash or Zsh, put something like this in your `$HOME/.bashrc` or `$HOME/.zshrc`: `. $HOMEBREW_PREFIX/etc/profile.d/z.sh`
{{< /admonition >}}

In addition, you can also add `setopt autocd` to your `.zshrc` file, which will automatically change the current directory to the directory you entered.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/strengthen-macos-terminal/  

