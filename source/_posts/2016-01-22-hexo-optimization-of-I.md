title: HEXO之我的优化
date: 2016-1-22 20:08:08
updated: 2016-11-30 20:08:08
tags:
	- HEXO
---

hexo 本身生成的是一套静态页面,但是用的其主题的ejs模板相互嵌套,发现最后生成的html文件结构混乱,`style`,`scipt`,标签穿插在其中.对于我这个稍微有一点代码洁癖的人来说,感觉异常不爽,另外,也不满足`script`放在dom节点后的规则.而且,`script`标签在html中,会形成阻塞,最终导致页面加载时的耗时增加.另外,`CSS`,和`script`的静态资源放到服务器上,因我的廉价vps,响应时间长,出网低,也会导致最终这些资源加载缓慢.用控制台`network`查看,耗时从请求到完全完成,大概在**6.8s**左右.对于一套静态页面来说,我觉得这是不能允许的.
![大图](http://7xrbxz.dl1.z0.glb.clouddn.com/hexo%E4%B9%8B%E6%88%91%E7%9A%84%E4%BC%98%E5%8C%96.png)

<!--more-->

---

# 问题
所以有以下几点需要解决:
1.整合`<sctipt>` 
2.静态资源加载缓慢
3.html结构混乱
4.css,js 可以再压缩减小文件大小.


# 整合`<sctipt>` 

我的方法是把所有ejs中的`script`标签,放到after-footer.ejs 中的**一个**`script`中.并加defer,其他script标签则放在之后.
``` javascript
<script defer>
    var yiliaConfig = {
        fancybox: <%= theme.fancybox %>,
        animate: <%= theme.animate %>,
        isHome: <%= is_home() %>,
        isPost: <%= is_post() %>,
        isArchive: <%= is_archive() %>,
        isTag: <%= is_tag() %>,
        isCategory: <%= is_category() %>,
        open_in_new: <%= theme.open_in_new %>
    }
    
    <!-- ........................ -->
</script>
```

# 静态资源加载缓慢

国内CDN加速,需要把网站备案,不过幸好还有各种的免费云空间，例如七牛。可以将主体的js静态资源存放回国内。主要还是修改主题更改文件指向。把CSS,JS文件,上传七牛云.然后主题_config.yml加入你要配置的路径.在ejs相应位置用`theme.fancybox` 来代替路径.并且指定`async` 属性,让多个`script`异步加载.

``` yml
# 加载资源地址配置
#css
jqueryfancyboxcss: http://7xrbjk.dl1.z0.glb.clouddn.com/jquery.fancybox.css
```

``` css
{% if theme.fancybox %}
<%- css(theme.jqueryfancyboxcss) %>
{% endif %}
```

``` yml
#js
main: http://7xrbjk.dl1.z0.glb.clouddn.com/main.js
```

``` javascript
{% if theme.main %}
<script async src="<%- url_for(theme.main) %>"></script>
{% endif %}
```

上面是直接用的七牛外链地址,当然也可以用七牛的镜像存储
![镜像存储](http://7xrbxz.dl1.z0.glb.clouddn.com/hexo%E4%B9%8B%E6%88%91%E7%9A%84%E4%BC%98%E5%8C%96-2.png)

>- 那么自动拉取的文件前面会有`/js...`的前缀,就可以这样配置

``` yml
# 加载资源地址配置
others: others
css: http://7xrbjk.dl1.z0.glb.clouddn.com/css/
js: http://7xrbjk.dl1.z0.glb.clouddn.com/js/
images: http://7xrbjk.dl1.z0.glb.clouddn.com/images/
```

``` javascript
{% if theme.fancybox %}
  <link href="{{ url_for(theme.css) }}/fancybox/source/jquery.fancybox.css?v=2.1.5" rel="stylesheet" type="text/css"/>
{% endif %}
``` 
``` css
{% if theme.maincss %}
  <link href="{{ url_for(theme.css) }}/css/style.css" rel="stylesheet" type="text/css"/>
{% endif %}
```

# html结构混乱 和 CSS JS 压缩
可以采用hexo插件 [hexo插件(官网)](https://hexo.io/plugins/) 来自动完成压缩
- hexo-clean-css --- Minify CSS files with clean-css. 
- hexo-uglify --- Minify JavaScript files with UglifyJS.
- hexo-beautify --- Beautify Hexo generated HTML, CSS and JS files, using js-beautify. (这个可以格式化html)

开始安装后 `hexo g` 不起作用,css js 都没有压缩,我尝试`npm install xxx`不加`--save` 解决,不知道为什么..

# 最后
![最后](http://7xrbxz.dl1.z0.glb.clouddn.com/hexo%E4%B9%8B%E6%88%91%E7%9A%84%E4%BC%98%E5%8C%96-03.png)

效果显著.从请求到全部加载完成,`1.16s`,好像百度云CDN加速有免费版,不需要备案,不过需要要修改dns到百度指定的dns,效果也是很不错的.
