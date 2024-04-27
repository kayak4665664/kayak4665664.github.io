# Build a Image Hosting Service With jsDelivr and Github Repository

I used to put the pictures of my website on the storage space of Qiniu Cloud. Although Qiniu Cloud is not bad, the traffic under the `https` protocol needs to be charged. So, I used jsDelivr and Githubc repository to build a free image hosting service.
&lt;!--more--&gt;

## The method is very simple
1. Create a public Github repository
2. Upload the picture to the repository
3. Get the link of the picture, such as `https://cdn.jsdelivr.net/gh/user/repository/image.jpeg`, `user` is your Github username, `repository` is your repository name, `image.jpeg` is the name of the picture you uploaded

In addition, this can also be combined with the previous introduction of [ImageMagick](https://www.kayak4665664.com/Use-ImageMagick-to-compress-the-image-in-the-command-line), you can write a simple script, automatically compress the picture and upload it to the Github repository, and then get the link of the picture.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/build-a-image-hosting-service-with-jsdelivr-and-github-repository/  

