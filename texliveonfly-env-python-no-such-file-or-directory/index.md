# Texliveonfly, Env: Python: No Such File or Directory

Yesterday I used the texliveonfly package and got `env: python: No Such File or Directory` directly.
&lt;!--more--&gt;

I tried to execute `python`, and a prompt from Xcode Command Line Tools popped up, saying that I needed to download something, and it downloaded Python3.9, while I already had Python3.8🙃.

I tried to create a symbolic link with `ln`, but it didn&#39;t work.

{{&lt; admonition success &gt;}}
I thought since texliveonfly was written in Python, I could edit it directly. So I found `/Library/TeX/texbin/texliveonfly` and changed the first line of this file from `#!/usr/bin/env python` to `#!/usr/bin/env python3`, which solved the problem.
{{&lt; /admonition &gt;}}

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/texliveonfly-env-python-no-such-file-or-directory/  

