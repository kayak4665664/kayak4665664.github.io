# 用jsDelivr和Github仓库搭建图床

之前我一直把网站的图片放在七牛云的存储空间里，虽然七牛云还不错，但是`https`协议下的流量需要收费。所以，我就用jsDelivr和Githubc仓库搭建了一个免费的图床。
&lt;!--more--&gt;

## 方法很简单
1. 创建一个公开的Github仓库
2. 上传图片到仓库
3. 得到图片的链接，比如`https://cdn.jsdelivr.net/gh/user/repository/image.jpeg`, `user`是你的Github用户名，`repository`是你的仓库名，`image.jpeg`是你上传的图片名

而且，这样还可以配合上一篇介绍的[ImageMagick](https://www.kayak4665664.com/zh-cn/Use-ImageMagick-to-compress-the-image-in-the-command-line)，可以写一个简单的脚本，自动压缩图片并上传到Github仓库，然后得到图片的链接。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/build-a-image-hosting-service-with-jsdelivr-and-github-repository/  

