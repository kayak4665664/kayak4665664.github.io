# Get Resource Files Through ClassLoader

I encountered a problem when I was completing [Springboot-Demo](https://www.kayak4665664.com/springboot-demo/), which is to get resource files.
&lt;!--more--&gt;

At first, I packaged the project into a jar file using Maven, and then ran it. The program reported an error that it could not find the json file. After troubleshooting, I found that the problem was in the way I got the json file. I used a relative path, but when running the jar file, the relative path is relative to the directory where the jar file is located, not relative to the source code directory, so the json file cannot be found.

The solution is to use the `getResourceAsStream` method of the `ClassLoader` class, which can return an `InputStream` object according to the given path name, and then use this object to read the contents of the resource file. For example:

```java
//Assuming there is a Main class, get the class loader object
ClassLoader classLoader = Main.class.getClassLoader();
//Get the input stream object according to the resource file name
InputStream inputStream = classLoader.getResourceAsStream(&#34;test.log&#34;);
```

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/get-resource-files-through-classloader/  

