# Sips: MacOS Built-in Image Processing Tool

I accidentally discovered the built-in `sips` command line tool in macOS, which is used to process and manipulate images. It supports multiple image formats and provides some common image processing functions such as compression, resizing, rotation, etc.
&lt;!--more--&gt;

## Some examples

1. Compress image
``` bash
sips -s format jpeg ~/image.jpeg --out ~/image.jpeg --setProperty formatOptions 50%
```

2. Change image size
``` bash
sips --resampleWidth 500 --resampleHeight 300 input.jpg --out output.jpg
```

3. Resize image proportionally
``` bash
sips --resampleHeightWidth 500 300 input.jpg --out output.jpg
```

4. Rotate image
``` bash
sips --rotate 90 input.jpg --out output.jpg
```

5. Convert image format
``` bash
sips -s format jpeg input.png --out output.jpg
```

6. View image information
``` bash
sips -g all input.jpg
```


---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/sips-tool-in-macos/  

