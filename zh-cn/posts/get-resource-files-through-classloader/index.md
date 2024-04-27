# 通过类加载器获取资源文件

我在完成[Springboot-Demo](https://www.kayak4665664.com/zh-cn/springboot-demo/)的过程中，遇到了一个获取资源文件的问题。
&lt;!--more--&gt;

刚开始，我使用Maven将项目打包成了jar包，然后运行，程序报错找不到json文件了。经过排查，我发现问题出在了我获取json文件的方式上，我使用了相对路径，但是在运行jar包时，相对路径是相对于jar包所在的目录，而不是相对于源代码目录，这样就找不到json文件了。

解决的方法是使用`ClassLoader`类的`getResourceAsStream`方法，它可以根据给定的路径名返回一个`InputStream`对象，然后就可以使用这个对象来读取资源文件的内容。比如：

```java
//假如存在一个Main类，获取类加载器对象
ClassLoader classLoader = Main.class.getClassLoader();
//根据资源文件名获取输入流对象
InputStream inputStream = classLoader.getResourceAsStream(&#34;test.log&#34;);
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/get-resource-files-through-classloader/  

