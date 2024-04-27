# Strengthen macOS Terminal

The terminal of macOS is very good, but it feels like it&#39;s missing something, so I strengthened it. There are many people who recommend using [Oh My Zsh](https://ohmyz.sh/), but I don&#39;t know why, I often have some problems when I use [Oh My Zsh](https://ohmyz.sh/), so this time I didn&#39;t use it.
&lt;!--more--&gt;

## Beautify

I used starship to beautify the terminal, which is a lightweight, fast, cross-platform command line theme.

{{&lt; link href=&#34;https://starship.rs/&#34; content=&#34;starship&#34; title=&#34;starship&#34; card=true &gt;}}

Before installing starship, you need to install the [Nerd Font](https://www.nerdfonts.com/) font, such as `Fira Code Nerd Font`.

You can use Homebrew to install it, and then enable the `Fira Code Nerd Font` font in the terminal settings.

```bash
brew tap homebrew/cask-fonts
brew install --cask font-fira-code-nerd-font
```

Then, use Homebrew to install starship: `brew install starship`. Add `eval &#34;$(starship init zsh)&#34;` at the end of `~/.zshrc`, and then execute `source ~/.zshrc`. Reopen the terminal, and you can see the effect.

More custom configuration can be found in the [guide](https://starship.rs/guide/).

## Extension

### 1. zsh-fast-syntax-highlighting

This plugin can highlight the content entered on the command line, making your terminal more beautiful.

{{&lt; link href=&#34;https://github.com/zdharma-continuum/fast-syntax-highlighting&#34; content=&#34;zsh-fast-syntax-highlighting&#34; title=&#34;zsh-fast-syntax-highlighting&#34; card=true &gt;}}

``` bash
brew install zsh-fast-syntax-highlighting
```

{{&lt; admonition info &gt;}}
To activate the syntax highlighting, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/opt/zsh-fast-syntax-highlighting/share/zsh-fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh`
{{&lt; /admonition &gt;}}

### 2. zsh-autosuggestions

This plugin can automatically complete the command line based on the history.

{{&lt; link href=&#34;https://github.com/zsh-users/zsh-autosuggestions&#34; content=&#34;zsh-autosuggestions&#34; title=&#34;zsh-autosuggestions&#34; card=true &gt;}}

``` bash
brew install zsh-autosuggestions
```

{{&lt; admonition info &gt;}}
To activate the autosuggestions, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autosuggestions/zsh-autosuggestions.zsh`  
You will also need to restart your terminal for this change to take effect.
{{&lt; /admonition &gt;}}

### 3. zsh-completions

This plugin can also complete the command line.

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

This plugin can automatically complete the brackets, and quotes.

{{&lt; link href=&#34;https://github.com/hlissner/zsh-autopair&#34; content=&#34;zsh-autopair&#34; title=&#34;zsh-autopair&#34; card=true &gt;}}

``` bash
brew install zsh-autopair
```

{{&lt; admonition info &gt;}}
To activate autopair, add the following at the end of your `.zshrc`: `source $HOMEBREW_PREFIX/share/zsh-autopair/autopair.zsh`  
You will also need to restart your terminal for this change to take effect.
{{&lt; /admonition &gt;}}

### 5. z

This plugin can quickly jump to the directory you want to go to.

{{&lt; link href=&#34;https://github.com/rupa/z&#34; content=&#34;z&#34; title=&#34;z&#34; card=true &gt;}}

``` bash
brew install z
```

{{&lt; admonition info &gt;}}
For Bash or Zsh, put something like this in your `$HOME/.bashrc` or `$HOME/.zshrc`: `. $HOMEBREW_PREFIX/etc/profile.d/z.sh`
{{&lt; /admonition &gt;}}

In addition, you can also add `setopt autocd` to your `.zshrc` file, which will automatically change the current directory to the directory you entered.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/strengthen-macos-terminal/  

