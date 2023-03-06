# Use ImageMagick to Compress the Image in the Command Line

I found ImageMagick, which is a powerful image processing tool that can be used in the command line. Not only can it be used to compress images, but it can also be used for many other things.
<!--more-->

{{< link href="https://imagemagick.org/" content="ImageMagick" title="ImageMagick" card=true >}}

ImageMagick can be installed through Homebrew: `brew install imagemagick`.

It can be used to compress images in the command line. For example, I have an image `image.png`, and I want to compress it. I can use the following command:

```
convert image.png -quality 80% image.png
```

And, you can compress the image while converting the image format at the same time. If I want to compress the image and convert it to JPEG format, I can use the following command:

```
convert image.png -quality 80% image.jpg
```

ImageMagick also has many other features, which can be explored according to the official documentation.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/use-imagemagick-to-compress-the-image-in-the-command-line/  

