# 我的网站是如何建立的？


目前本站已经成型，进入日常维护阶段，现在来回顾一下它是如何建立的。网上已经有各种教程，而本文主要是我自己的经历，不会涉及那些重复的细节。
<!--more-->

## 开始
上上周看到有人用Github作免费网盘，我以前还见过有人专门建了repository来记笔记、写博客，我忽然也想有个写点东西记录自己的地方。我就查了一下如何用Github写博客，我才知道了[Github Pages](https://pages.github.com)。简单来说它可以免费自动托管静态网页，用它做一个自己的博客是绰绰有余的。

## 准备
### 域名
[Github Pages](https://pages.github.com)是免费的，不过它的网址都长`username.github.io`这样，感觉不够个性化。好在它是支持自定义域名的，我决定买一个。网站还没有建起来，但我还是先买了。我听说国内买域名需要实名审核，并且审核需要好几天。我一边等待审核通过，一边建网站，这样更省时间。最后我买了`kayak4665664.com`。

{{< admonition tip >}}
有的域名首年注册时看起来便宜，但以后续费比`.com`域名还要贵。
{{< /admonition >}}

### username.github.io
新建了一个repository，进行`Pages`设置。[Github Pages](https://pages.github.com)使用`Jekyll`将纯文本转化为静态网站，所以在设置过程中它会让你选择你的`Jekyll`主题。我还认真地比较了一下那几个主题，选了我觉得最好看的一个。其实后面很快我就发现，这些主题过于简单，不满足我的需求。之后用`git`克隆repository到了本地。

### 设计
我看了一些其他人的网站，初步确定我的网站要有评论、访问统计、站内搜索这几个功能。另外还要加入百度和谷歌分析，并且让它们收录我的网站。

### 工具
除了`Jekyll`，还有很多将纯文本转化为静态网站和博客的工具，比如我现在用的`Hugo`。由于[Github Pages](https://pages.github.com)默认使用`Jekyll`，我就选择了`Jekyll`。

`Jekyll`基于`Ruby`，可以用`gem`来安装。我使用的macOS自带一个`Ruby`，我就直接执行`gem install jekyll bundler`开始安装`Jekyll`、`Bundler`以及它们的依赖。安装一半，出现`fatal error: 'ruby/config.h' file not found`。谷歌了一下有人说是自带的`Ruby`版本太低，还有人说是`Xcode CommandLineTools`的问题。我直接用`Homebrew`安装了一个新的`Ruby`。安装之后设置了终端的环境变量，重新执行`gem install jekyll bundler`，这次安装好了。

{{< admonition warning >}}
我还查了一下怎么清理之前`gem install jekyll bundler`时的缓存和已安装的包，结果没有找到。我只好手动卸载了那些已安装的包、删除了缓存所在的目录，感觉根本没清理干净。
{{< /admonition >}}

## Jekyll
### 上手
在工作目录执行`bundle exec jekyll serve`，出现`cannot load such file -- webrick (LoadError)`。谷歌了一下，用`bundle add webrick`解决。

在本地预览了一下感觉没有问题，准备`push`到Github上用手机测试。但是出现了问题，`push`不上去。谷歌了一下没找到，百度了一下发现可能是`proxy`的问题，取消`git`设置的代理后解决。

用手机看了一下，网页是自动适配移动端的。这时候发现这个主题太简陋了，甚至没有分页的功能。刚开始我还准备自己实现出来，但又想想那么多功能都得一个个实现，工作量巨大，我还是找一个功能比较完整的主题吧。

### 主题
网上有不少`Jekyll`主题，我最后下载了[YAT](https://github.com/jeffreytse/jekyll-theme-yat)。它支持不少功能，可以用[Disqus](Disqus.com)和[Gitment](https://github.com/imsun/gitment)来评论。

下载之后，想要执行`bundle exec jekyll serve`预览一下，报错`Could not find gem 'jekyll-spaceship (~> 0.2)'`。我通过在`gem`安装`jekyll-spaceship`时设置版本为`0.2`来解决。在这里我还发现安装过程卡住了，但没有报错。用`Activity Monitor`看到`Ruby`的`Rcvd Bytes`是一直缓慢增加的，应该是国内网络的问题。谷歌了一下，在[Ruby China](https://gems.ruby-china.com)找到了换源的方法，换源之后成功安装。

再次执行`bundle exec jekyll serve`，这次可以预览新主题了。

### 个性化
根据自己的需求来对主题进行个性化修改，如标题、图片等。我本来想用[Gitment](https://github.com/imsun/gitment)，但我发现它不能登录Github账号，看了一下它的[Issues](https://github.com/imsun/gitment/issues)应该是停止服务了。所以只能用[Disqus](Disqus.com)，我注册了[Disqus](Disqus.com)账号，开启了评论功能。此外我还用了[不蒜子](http://busuanzi.ibruce.info)进行网站访问量统计，只需两行代码。

之后我开始增加一些内容。在预览内容的过程中渐渐发现了一些问题，这个主题它的字体偏小，不论在浅色还是深色模式下文字与背景的对比较低，总之我感觉读起来费眼睛。然而无法在配置文件中对字体进行设置，我只能直接去挨个修改`.scss`文件，比较麻烦。而它的翻译功能，调用了谷歌的网页翻译接口，在国内网络下几乎无法使用，导致网页变得卡顿，我直接将源代码中翻译相关的部分删除了。除此之外，[Disqus](Disqus.com)在国内网络下无法登录账号，测试了一下只能使用访客匿名评论，这也是一个缺点。

### 放弃
个性化之后，我感觉没有问题了。这时忽然想到[YAT](https://github.com/jeffreytse/jekyll-theme-yat)主题还支持PlantUML、Mermaid、Mathjax、Vedio、Audio等，我应该再测试一下。我直接用作者的`markdown`文件进行测试，结果发现这些东西都没有正常显示出来。

我还以为是我把源代码改坏了，我直接克隆了一份作者的repository。经测试发现同样不行，看来不是我修改代码的问题。但是问题在哪我也一直没有找到，考虑到这个主题还存在其他的缺点，我选择放弃它。

我又开始找主题，这一次更加仔细。最后找到了[LoveIt](https://github.com/dillonzq/LoveIt)主题，也就是我现在用的。

这是一个基于`Hugo`的主题，所以`Ruby`就没用了，我把它卸载了。

## Hugo
### 上手
先用`Homebrew`安装`Hugo`，[LoveIt](https://github.com/dillonzq/LoveIt)文档中推荐安装`extended`版本的`Hugo`，而`Homebrew`安装的`Hugo`就是`extended`版本的。

`Hugo`的目录结构和`Jekyll`的还是不太一样，用了一些时间才熟悉了。[LoveIt](https://github.com/dillonzq/LoveIt)的配置项非常多，也是需要先看一看文档的。

大概配置了一下，执行`hugo serve -e production --disableFastRender`进行预览。

### 个性化
之后就是个性化地设置，还有：
1. 注册[LeanCloud](https://www.leancloud.cn)以及[Valine](https://valine.js.org)用于评论和访问统计
2. 利用[https://realfavicongenerator.net](https://realfavicongenerator.net)生成网站图标
3. 注册[Gravartar](http://Gravatar.com)头像
4. 注册[Algolia](https://www.algolia.com)用于站内搜索
5. 使用`node.js`执行`npm install atomic-algolia`安装[atomic-algolia](https://github.com/chrisdmacrae/atomic-algolia)，用于自动化上传索引文件至[Algolia](https://www.algolia.com)
6. 注册[Mapbox](https://www.mapbox.com)

在这中间我还发现一个问题，本地预览的时候不能显示自定义的`404`模版，谷歌了一下发现：
{{< admonition info >}}
`hugo server` will not automatically load your custom `404.html` file, but you can test the appearance of your custom “not found” page by navigating your browser to `/404.html`.
{{< /admonition >}}

### 扩展
网站差不多建起来了。执行`hugo`，就会出现`/public`目录，把`/public`和自己的repository同步，就可以把网页托管到[Github Pages](https://pages.github.com)。之后再用[atomic-algolia](https://github.com/chrisdmacrae/atomic-algolia)上传生成的索引文件至[Algolia](https://www.algolia.com)。经过这两个步骤就完成了一次网站的部署。

另外，我又建了一个私有的repository，用于同步`/public`之外的源代码，所以每次部署都需要多同步一次。为了自动化这三个过程，我写了一个`Shell`脚本，一步到位。

这时候，我的域名终于通过了实名审核。我开始进行一些扩展：
1. 在Github上设置`CNAME`
2. 将repository导入[Vercel](https://vercel.com/)，这样每次更新repository，都会自动部署到[Vercel](https://vercel.com/)。据说百度不会收录[Github Pages](https://pages.github.com)托管的网站，而部署到[Vercel](https://vercel.com/)之后可以被收录
3. 在[Vercel](https://vercel.com/)中设置自定义域名
4. 加入[百度统计](https://tongji.baidu.com/)和[谷歌Analytics](https://analytics.google.com/)
5. 向[百度搜索资源平台](https://ziyuan.baidu.com/)和[谷歌Search Console](https://search.google.com)提交`sitemap`，在[必应Webmaster Tools](https://www.bing.com/webmasters/)中直接导入[谷歌Search Console](https://search.google.com)中已经提交的`sitemap`

## 最后
未来我还打算加入一点谷歌广告，这也是大部分网站都有的功能。

总的来说，这次的收获还是很多的！
