hexo# [赵伟杰的技术博客](http://zwjay.cn)


### 发布三部曲

>  * hexo g    // 生成文章
>  * hexo s  -- debug  // 开启本地服务器预览(选)
>  * hexo d    // 发布到github,然后在进入到.gitignore文件夹中去手动提交到自己名字的github
>  **后面添加 -- debug 可看报错信息**

如果`hexo d` 没有发布上去的时候，最好把public 文件夹删除再运行一下,然后再运行`hexo d`


<!-- 
## 提交百度seo
在source目录下输入：
curl -H 'Content-Type:text/plain' --data-binary @urls.txt "http://data.zz.baidu.com/urls?site=meiminjun.github.io&token=qdkA29iGaFLKdAFv" 
-->
