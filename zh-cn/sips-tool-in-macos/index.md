# Sips: MacOS自带图像处理工具


无意间发现了macOS内置的sips命令行工具，用于处理和操作图像。它支持多种图像格式，并提供了一些常见的图像处理功能，如压缩、改变尺寸、旋转等。
&lt;!--more--&gt;

## 一些示例

1. 压缩图像
``` bash
sips -s format jpeg ~/image.jpeg --out ~/image.jpeg --setProperty formatOptions 50%
```

2. 改变图像尺寸
``` bash
sips --resampleWidth 500 --resampleHeight 300 input.jpg --out output.jpg
```

3. 按比例调整图像大小
``` bash
sips --resampleHeightWidth 500 300 input.jpg --out output.jpg
```

4. 旋转图像
``` bash
sips --rotate 90 input.jpg --out output.jpg
```

5. 转换图像格式
``` bash
sips -s format jpeg input.png --out output.jpg
```

6. 查看图像信息
``` bash
sips -g all input.jpg
```


---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/sips-tool-in-macos/  

