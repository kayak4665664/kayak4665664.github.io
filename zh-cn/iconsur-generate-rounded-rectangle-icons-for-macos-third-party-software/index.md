# iconsur：为macOS第三方软件生成圆角矩形图标

总有一些软件的图标和macOS的不适应，iconsur可以为它们生成圆角矩形的图标，美化我们的macOS。
<!--more-->

iconsur的Github主页：

{{< link href="https://github.com/rikumi/iconsur" content="iconsur" title="iconsur" card=true >}}

可以在[Releases](https://github.com/rikumi/iconsur/releases)中下载。也可以用Homebrew：`brew install iconsur`，或者是npm：`npm install -g iconsur`。

iconsur在App Store中为软件寻找最相似的iOS app，把这个软件的图标替换成iOS app的图标。例如：

```
sudo iconsur set /Applications/Microsoft\ Word.app/
```

另外，iconsur也可以为软件在本地生成图标。例如：

```
sudo iconsur set /Applications/Visual\ Studio\ Code.app/ -l
```

其他用法可以参照[Github](https://github.com/rikumi/iconsur)或是执行`iconsur help`。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/iconsur-generate-rounded-rectangle-icons-for-macos-third-party-software/  

