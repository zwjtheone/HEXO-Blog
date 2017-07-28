title: 关于script标签位置
date: 2016-2-10 20:08:08
updated: 2016-11-30 21:10:08
tags:
	- JavaScript
---


按照HTML5标准中的HTML语法规则，如果在`</body>`后再出现`<script>`或任何元素的开始标签，都是parse error，浏览器会忽略之前的`</body>`，即视作仍旧在body内。所以实际效果和写在</body>之前是没有区别的。所以html5标准建议大家将script标签写入到`</body>`标签之前原因：如果你写在`</body>`标签之后，不会有任何错误，上诉已经说明，但是在加载过程中，会将script标签修正到`</body>`内部，这个修正过程相比直接写入在性能损耗上会一点损耗，，这样你通过document.body获取的最后一个元素就是script元素，所以大家以后按照HMTL5 标准将script标签写入`</body>`(包含引入JS文件以及直接内嵌JS程序)
```
<!DOCTYPE html>  
<html>  
<head>  
<title>标题</title>  
</head>  
<body>  
<!-- 页面内容 -->  
<script type=”text/javascript” src=”文件1.js”></script>  
<script type=”text/javascript” src=”文件2.js”></script>  
<script type=”text/javascript” src=”文件n.js”></script>  
</body>  
</html>  

```
