# 使用ImageMagick在命令行中压缩图像

我找到了ImageMagick，它是一个强大的图像处理工具，可以在命令行中使用。不仅可以用于压缩图像，而且可以用于其他很多事情。
&lt;!--more--&gt;

{{&lt; link href=&#34;https://imagemagick.org/&#34; content=&#34;ImageMagick&#34; title=&#34;ImageMagick&#34; card=true &gt;}}

可以通过Homebrew安装ImageMagick：`brew install imagemagick`。

使用ImageMagick可以在命令行中压缩图像。例如，我有一个图像`image.png`，我想要压缩它，我可以使用以下命令：

```
convert image.png -quality 80% image.png
```

而且，可以在压缩的同时转换图像的格式。如果我想要压缩图像并转换为JPEG格式，我可以使用以下命令：

```
convert image.png -quality 80% image.jpg
```

ImageMagick还有很多其他的功能，可以参照官方文档慢慢探索。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/use-imagemagick-to-compress-the-image-in-the-command-line/  

