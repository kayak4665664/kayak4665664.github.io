# Texliveonfly, Env: Python: No Such File or Directory

昨天用了一下texliveonfly宏包，直接出现了`env: python: No Such File or Directory`。
&lt;!--more--&gt;

我试着执行了一下`python`，结果弹出了一个Xcode Command Line Tools的提示，说要下载一些东西，然后它下载了Python3.9，而我之前已经有了Python3.8🙃。

我试着用`ln`建立软连接，但是没有用。

{{&lt; admonition success &gt;}}
我想既然texliveonfly是用Python写的，我可以直接编辑它。于是我找到了`/Library/TeX/texbin/texliveonfly`，然后将这个文件第一行的`#!/usr/bin/env python`改成了`#!/usr/bin/env python3`，这样就解决了。
{{&lt; /admonition &gt;}}

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/texliveonfly-env-python-no-such-file-or-directory/  

