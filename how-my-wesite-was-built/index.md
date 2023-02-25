# How My Wesite Was Built?


At present, my website has stabilized and entered the routine maintenance stage. Now let's review how it was built. There are various guidelines on the Internet, and this article is mainly about my own experience, so I won't involve those repeated details.
<!--more-->

## Beginning
Two weeks ago, I saw someone using Github as a free cloud drive. I have seen someone take notes and blog in a repository. Suddenly, I wanted to have a place to write something to record myself. I searched for how to blog on Github, and then I found [Github Pages](https://pages.github.com). In short, it can automatically host static webpages for free, and it is more than enough to build a blog of my own.

### Domain
[Github Pages](https://pages.github.com) is free, but its URLs all look like `username.github.io`, which feels not personalized enough. Fortunately, it supports custom domains, so I decided to buy one. The website hadn't been built yet, but I bought it first. I heard that buying a domain in China requires real-name verification, and the verification takes several days. If I wait for the verification while building my website, it will save time. Finally, I bought `kayak4665664.com`.

{{< admonition tip >}}
Some domains look cheap when they are registered in the first year, but later renewals are more expensive than `.com` domain.
{{< /admonition >}}

### username.github.io
Created a new repository and set `Pages` settings. [Github Pages](https://pages.github.com) uses `Jekyll` to transform plain text into static websites, so it will let you choose your `Jekyll` theme during the setup process. I even carefully compared those themes and chose the one that I thought was the best-looking. I soon discovered that these themes were too simple to meet my needs. Then I used `git` to clone the repository to the local.

### Design
I visited some others' websites and initially determined that my website should have the functions of comments, visit count, and in-site search. In addition, I also wanted to add Baidu and Google Analytics and let them index my website.

### Tool
In addition to `Jekyll`, there are many tools for transforming plain text into static websites and blogs, such as the `Hugo` I use now. Since [Github Pages](https://pages.github.com) uses `Jekyll` by default, I chose `Jekyll`.

`Jekyll` is based on `Ruby` and can be installed with `gem`. I use macOS and `Ruby` is a built-in software. I directly executed `gem install jekyll bundler` to start installing `Jekyll`, `Bundler`, and their dependencies. During the installation, `fatal error:'ruby/config.h' file not found` appeared. I googled it and found that some people said the version of the built-in `Ruby` was too low, but others said that it was a problem with `Xcode CommandLineTools`. I installed a new `Ruby` with `Homebrew` directly. After installation, set the environment variables in the terminal, re-executed `gem install jekyll bundler`, and the installation was complete this time.

{{< admonition warning >}}
I also searched for how to clean up the cache and installed packages of the last `gem install jekyll bundler`, but I didn't find it. I had to manually uninstall the installed packages and delete the directory where the cache was located. I felt that it was not cleaned up at all.
{{< /admonition >}}

## Jekyll
### Getting start
Executed `bundle exec jekyll serve` in the workplace, and `cannot load such file - webrick (LoadError)` appeared. I googled it and then solved it with `bundle add webrick`.

I previewed it locally and felt there were no problems. I prepared to `push` it to Github and test it with my mobile phone. But there was a problem, `push` did not work. Google didn't find it, but Baidu found that it may be a problem with `proxy`. It was resolved after unseting the proxy settings of `git`.

Browsing with my phone, the webpage was automatically adapted to the mobile interface. At this time, I found that this theme was too simple, and it didn't even have a pagination. In the beginning, I was planning to implement it myself, but I thought that so many functions would have to be implemented one by one, and the workload was huge. I'd better find a theme with more complete functions.

### Theme
There are many `Jekyll` themes on the Internet and finally downloaded [YAT](https://github.com/jeffreytse/jekyll-theme-yat). It has many functions. We can use [Disqus](Disqus.com) and [Gitment](https://github.com/imsun/gitment) to comment.

After downloading, I wanted to execute `bundle exec jekyll serve` to preview it, but the error `Could not find gem 'jekyll-spaceship (~> 0.2)'` appeared. I solved it by setting the version to `0.2` when installing `jekyll-spaceship` by `gem`. Here I also found that the installation was stuck, but there was no error. Using the `Activity Monitor`, I saw that the `Rcvd Bytes` of `Ruby` have been increasing slowly, which should be a network problem in China. Googled it, then found a way on [Ruby China](https://gems.ruby-china.com) to change the sources. The installation was successful after changing them.

Executed `bundle exec jekyll serve` again and this time I previewed the new theme.

### Personalizing
According to our own needs, we can make personalized changes to the theme, such as titles, pictures, etc. I originally wanted to use [Gitment](https://github.com/imsun/gitment), but I found that it can't log in to the Github account. I took a look at its [Issues](https://github.com/imsun/gitment/issues) and then found that the service should be stopped. So I can only use [Disqus](Disqus.com), I registered a [Disqus](Disqus.com) account and turned on the comment function. In addition, I also used [Bu Suanzi](http://busuanzi.ibruce.info) for website traffic statistics, which only requires two lines of code.

Then I started to add some content. In the process of previewing the content, I gradually discovered some problems. The font of this theme was too small, and the contrast between the text and the background was low whether in light or dark mode. In short, I felt that reading it tortures my eyes. However, the font cannot be set in the configuration file. I can only modify the `.scss` files one by one, which is more troublesome. And its translation function called Google's webpage translation interface, was almost unusable under the Chinese network, causing the webpage to become stuck. I directly deleted the translation-related part of the source code. In addition, [Disqus](Disqus.com) cannot log in to the account under the Chinese network. After a test, only anonymous guest comments can be used. This is also a disadvantage.

### Giving up
After personalization, I felt that there was no problem. It suddenly occurred to me that the [YAT](https://github.com/jeffreytse/jekyll-theme-yat) theme also supports PlantUML, Mermaid, Mathjax, Vedio, Audio, etc. I should test it again. I directly used the author's `markdown` files to test and found that these things were not displayed normally.

I thought it was because I changed the source code. I directly cloned the author's repository. After testing, I found that the same does not work. It seems that it is not a problem with my code modification. But I haven't found the problem. Considering that there were other shortcomings in this theme, I chose to abandon it.

I started looking for the subject again, this time more carefully. Finally, I found the [LoveIt](https://github.com/dillonzq/LoveIt) theme, which is what I use now.

This is a theme based on `Hugo`, so `Ruby` was useless, I uninstalled it.

## Hugo
### Getting start
First used `Homebrew` to install `Hugo`, [LoveIt](https://github.com/dillonzq/LoveIt) recommends installing the `extended` version of `Hugo`, and the `Hugo` installed by `Homebrew` is the `extended` version.

The directory structure of `Hugo` is still different from that of `Jekyll`, it took some time to get familiar with. [LoveIt](https://github.com/dillonzq/LoveIt) has a lot of configuration items, and we need to take a look at the document first.

Approximately configured, executed `hugo serve -e production --disableFastRender` to preview.

### Personalizing
After that were personalized settings, as well as:
1. Registered [LeanCloud](https://www.leancloud.cn) and [Valine](https://valine.js.org) for comments and visit statistics
2. Used [https://realfavicongenerator.net](https://realfavicongenerator.net) to generate website icons
3. Registered [Gravartar](http://Gravatar.com)
4. Registered [Algolia](https://www.algolia.com) for site search
5. Used `node.js` to execute `npm install atomic-algolia` to install [atomic-algolia](https://github.com/chrisdmacrae/atomic-algolia) to automatically upload index files to [Algolia](https://www.algolia.com)
6. Registered [Mapbox](https://www.mapbox.com)

During this period, I also found a problem. The custom `404` template could not be displayed in the local preview. Google found it:
{{< admonition info >}}
`hugo server` will not automatically load your custom `404.html` file, but you can test the appearance of your custom “not found” page by navigating your browser to `/404.html`.
{{< /admonition >}}

### Extension
The website was almost built. Executed `hugo`, and the `/public` directory would appear. Synchronized `/public` with our repository, and we can host the webpage to [Github Pages](https://pages.github.com). Then used [atomic-algolia](https://github.com/chrisdmacrae/atomic-algolia) to upload the generated index file to [Algolia](https://www.algolia.com). After these two steps, a website deployment was completed.

In addition, I built a private repository for synchronizing source code other than `/public`, so every deployment needs to be synchronized once more. To automate these three processes, I wrote a `Shell` script. Only one step.

At this time, my domain finally passed the real-name verification. I started to make some extensions:
1. Set up `CNAME` on Github
2. Imported the repository into [Vercel](https://vercel.com/), so that every time the repository is updated, it will be automatically deployed to [Vercel](https://vercel.com/). It is said that Baidu will not index sites hosted by [Github Pages](https://pages.github.com), and it can be indexed after being deployed to [Vercel](https://vercel.com/)
3. Set a custom domain in [Vercel](https://vercel.com/)
4. Added [Baidu Tongji](https://tongji.baidu.com/) and [Google Analytics](https://analytics.google.com/)
5. Submitted the `sitemap` to [Baidu Ziyuan](https://ziyuan.baidu.com/) and [Google Search Console](https://search.google.com), in [Bing Webmaster Tools](https://www.bing.com/webmasters/) directly imported the submitted `sitemap` into [Google Search](https://search.google.com) Console](https://search.google.com)

## End
In the future, I also plan to add a little Google advertisement, which is also a feature of most websites.

In general, there are a lot of gains this time!
