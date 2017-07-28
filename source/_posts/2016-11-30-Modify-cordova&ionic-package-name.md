title: 修改ionic中android程序的包名
date: 2016/11/30 15:42
updated: 2016/11/30 15:42
tags:
	- Ionic
	- Android
---


默认ionic新建工程的时候指定的Android版本包名是：com.ionicframework.starter；这样固定死包名的话会导致一个问题，多个ionic工程无法正常安装到手机当中，后面安装的程序始终会把之前的程序覆盖掉，这样的话就太悲剧了。
现在给大家演示一下如何修改ionic工程的包名：

#1.修改android工程下源码文件的路径和Java文件的包名：
   修改java文件包名：找到platforms\android\src\com\ionicframework\starter\*.java，用记事本打开后，修改package为你自己定义好的，我这里为了简单就改成com.ionicframework.starter2；
   

   <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-1.png">
        <img src="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-1.png" alt="Modify-cordova&ionic-package-name-1" />
   </a>
   

 修改源码文件的路径：platforms\android\src\com\ionicframework\starter改成platforms\android\src\com\ionicframework\starter2；
   
#2.修改AndroidManifest.xml，找到platforms\android下面的AndroidManifest.xml，用记事本打开后，修改里面的package内容：
   
   
  <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-2.png">
       <img src="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-2.png" alt="Modify-cordova&ionic-package-name-2" />
  </a>

#3.修改android.json：找到platforms\android下面的android.json，用记事本打开，修改其中的installed_plugins中各个插件对应的主包名：
   
 <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-3.png">
      <img src="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-3.png" alt="Modify-cordova&ionic-package-name-3" />
 </a>

#4.修改ionic工程下的config.xml文件，修改里面的widget节点的id属性值：
   
 <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-4.png" >
      <img src="http://resource.zwjay.cn/jekyll/img/Modify-cordova&ionic-package-name-4.png" alt="Modify-cordova&ionic-package-name-4" />
 </a>

	
这样，整个工程的android版本的包名就彻底改好了，虽然很麻烦，但是有时候还是可以派上用场的，希望对大家有所帮助！




