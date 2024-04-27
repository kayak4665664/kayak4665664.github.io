# Multiple Versions of Edge Browser Appear on Mac

Suddenly, I found that there are two Edge Dev on my Mac, 111.0.1660.13 and 111.0.1660.12, and both of them can launch normally. I want to keep the latest version and uninstall the old one.
&lt;!--more--&gt;

## method
### 1
Take the Dev version as an example. Switch the directory to the following location
```
cd /Applications/Microsoft\ Edge\ Dev.app/Contents/Frameworks/Microsoft\ Edge\ Framework.framework/Versions
```
You can also press `control &#43; shift &#43; G` in the Finder to go to the location

### 2
Execute `ls -l`, and you will see similar output
{{&lt; admonition example &gt;}}
drwxrwxr-x 14 user admin 448 Feb 11 11:32 111.0.1660.12  
drwxrwxr-x 14 user admin 448 Feb 17 08:54 111.0.1660.13  
lrwxrwxr-x 1 user admin 13 Feb 17 08:54 Current -&gt; 111.0.1660.13  
{{&lt; /admonition &gt;}}
Or click `Current` in the Finder to confirm the version linked to

### 3
Use `rm -rf` to remove other older versions, or you can also delete them in Finder

### 4
The last step, this step can also be done in the Finder
```
cd ~/Library/Application\ Support/Microsoft
rm -rf EdgeUpdater
```

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/multiple-versions-of-edge-browser-appear-on-mac/  

