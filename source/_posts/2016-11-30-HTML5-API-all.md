title: HTML5-API汇总学习
date: 2016/11/30 15:43
updated: 2016/12/12 10:17
tags:
	- HTML5
---


看`MDN` 的文档才知道HTML5很多API还没有学习过，这里记录学习HTML5 新 api。

`<!DOCTYPE html> <meta charset="UTF-8">`

HTML5是最新进化的标准,它定义了HTML。这个词代表了两个不同的概
- 这是一个新版本的HTML语言,与新元素、属性和行为
- 和一组更大的技术,允许更加多样化和功能强大的Web站点和应用程序。这组有时被称为HTML5&朋友和通常缩短HTML5。

HTML5 大概包含以下几点

1.  语义:允许您更精确地描述你的内容是什么。
2.  连通性:允许您以新的和创新的方式与服务器通信。
3.  离线存储:允许网页在客户端本地存储数据和离线操作更有效率。
4.  多媒体:制作视频和音频开放网络中的一等公民。
5.  2d / 3d图形和效果:允许一个更加多样化的选择范围。
6.  性能和集成:提供更大的速度优化和更好的使用计算机硬件。
7.  设备访问:允许使用各种输入和输出设备。
8.  样式:让作者编写更复杂的主题。

   <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/html5-all.png">
        <img src="http://resource.zwjay.cn/jekyll/img/html5-all.png" alt="html5-all" />
   </a>


<!--more-->

# 语义化

## 语义化标签，在 `HTML4` 中 `<div>` 标签不精确，不够明显的描述文档轮廓。在 `HTML5` 更新语义化标签。

```html
<section>

  <h1>Forest elephants</h1> 

  <section>
    <h1>Introduction</h1>
    <p>In this section, we discuss the lesser known forest elephants.</p>
  </section>

  <section>
    <h1>Habitat</h1>
    <p>Forest elephants do not live in trees but among them.</p>
  </section>

  <aside>
    <p>advertising block</p>
  </aside>

</section>

<footer>
  <p>(c) 2010 The Example company</p>
</footer>
```

这样可以直观的看出html的结构，而且更利于SEO。

HTML5中引入的新语义元素带来的能力描述web文档的结构和轮廓在一个标准的方式。他们给人们带来一个很大的优势在HTML5浏览器和需要帮助他们理解页面结构,例如人需要一些辅助技术的帮助。这些新的语义元素是使用简单,用很少的负担,也可以工作在non-HTML5浏览器。因此他们应该使用没有限制。

## 标签使用选择顺序（参考）

   <a class="fancybox_img"  rel="group" href="http://resource.zwjay.cn/jekyll/img/in-post/html-tag.png">
        <img src="http://resource.zwjay.cn/jekyll/img/in-post/html-tag.png" alt="html5-all" />
   </a>

## `video` `audio`

```html
<video src="http://v2v.cc/~j/theora_testsuite/320x240.ogg" controls>
  Your browser does not support the <code>video</code> element.
</video>
```

- controls : Displays the standard HTML5 controls for the audio on the web page.
- autoplay : Makes the audio play automatically.
- loop : Make the audio repeat (loop) automatically.


```html
<audio src="/test/audio.ogg">
<p>Your browser does not support the <code>audio</code> element.</p>
</audio>
```

- "none" does not buffer the file
- "auto" buffers the media file
- "metadata" buffers only the metadata for the file

### 用JS控制多媒体标签

```javascript
<audio id="demo" src="audio.mp3"></audio>
<div>
  <button onclick="document.getElementById('demo').play()">Play the Audio</button>
  <button onclick="document.getElementById('demo').pause()">Pause the Audio</button>
  <button onclick="document.getElementById('demo').volume+=0.1">Increase Volume</button>
  <button onclick="document.getElementById('demo').volume-=0.1">Decrease Volume</button>
</div>
```

更多API点击 [https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement)

## 在HTML5中的表单

[https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-pattern](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-pattern)

### `input`标签 `type` 属性

- search 
- tel
- url
- email
- number
- text
- checkbox
- radio
- date
- color
- datetime
- file
- image
- hidden
- month
- password
- range
- reset
- submit
- week

其他属性
- list  用法 
 
```html
<input list="browsers" name="myBrowser" /></label>
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Internet Explorer">
  <option value="Opera">
  <option value="Safari">
  <option value="Microsoft Edge">
</datalist>
```

- pattern
 一个正则表达式检查与控制的价值。模式必须匹配整个价值,而不仅仅是一个子集。使用title属性来描述模式来帮助用户。这个属性适用于当type属性的值是文本,搜索,电话,地址,电子邮件,或密码,否则它将被忽略。正则表达式语言JavaScript RegExp算法是一样的,与“u”参数,使其治疗模式的序列unicode代码点。模式不是包围正斜杠。

## MathML (数学表达式标签)

<math style="display: block;"> <mtable columnalign="right center left"> <mtr> <mtd> <msup> <mrow> <mo> ( </mo> <mi> a </mi> <mo> + </mo> <mi> b </mi> <mo> ) </mo> </mrow> <mn> 2 </mn> </msup> </mtd> <mtd> <mo> = </mo> </mtd> <mtd> <msup><mi> c </mi><mn>2</mn></msup> <mo> + </mo> <mn> 4 </mn> <mo> ⋅ </mo> <mo>(</mo> <mfrac> <mn> 1 </mn> <mn> 2 </mn> </mfrac> <mi> a </mi><mi> b </mi> <mo>)</mo> </mtd> </mtr> <mtr> <mtd> <msup><mi> a </mi><mn>2</mn></msup> <mo> + </mo> <mn> 2 </mn><mi> a </mi><mi> b </mi> <mo> + </mo> <msup><mi> b </mi><mn>2</mn></msup> </mtd> <mtd> <mo> = </mo> </mtd> <mtd> <msup><mi> c </mi><mn>2</mn></msup> <mo> + </mo> <mn> 2 </mn><mi> a </mi><mi> b </mi> </mtd> </mtr> <mtr> <mtd> <msup><mi> a </mi><mn>2</mn></msup> <mo> + </mo> <msup><mi> b </mi><mn>2</mn></msup> </mtd> <mtd> <mo> = </mo> </mtd> <mtd> <msup><mi> c </mi><mn>2</mn></msup> </mtd> </mtr> </mtable> </math>


[https://developer.mozilla.org/en-US/docs/Web/MathML](https://developer.mozilla.org/en-US/docs/Web/MathML)

# 链接

## Web Sockets

允许创建一个永久的页面和服务器之间的连接和交换,是HTML5一种新的协议。它实现了浏览器与服务器全双工通信(full-duplex)。一开始的握手需要借助HTTP请求完成。

[https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)


## Server-Sent 服务端推送事件

[http://www.ibm.com/developerworks/cn/web/1307_chengfu_serversentevent/](http://www.ibm.com/developerworks/cn/web/1307_chengfu_serversentevent/)
[https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)

`EventSource` 对象提供的标准事件


名称 | 说明 | 事件处理方法
---|--- |--- 
open | 当成功与服务器建立连接时产生 | 
message | 当收到服务器发送的事件时产生 | onmessage
error |	当出现错误时产生 | onerror

```javascript
var es = new EventSource('events');
es.onmessage = function(e) {
    console.log(e.data);
};

es.addEventListener('myevent', function(e) {
    console.log(e.data);
});

 var es = new EventSource('sse/movement'); 
 es.addEventListener('message', function(e) { 
     var pos = e.data.split(','), x = pos[0], y = pos[1]; 
     $('#box').css({ 
         left : x + 'px', 
         top : y + 'px' 
         }); 
     });
```

> 第一种办法是在其他浏览器上使用原生 EventSource 对象，而在 IE 上则使用简易轮询或 COMET 技术来实现；另外一种做法是使用 polyfill 技术，即使用第三方提供的 JavaScript 库来屏蔽浏览器的不同。本文使用的是 polyfill 技术，只需要在页面中加载第三方 JavaScript 库即可。应用本身的浏览器端代码并不需要进行改动。一般推荐使用第二种做法，因为这样的话，在服务器端只需要使用一种实现技术即可。

## WebRTC

RTC代表实时通信的技术,允许连接到其他人和控制视频会议直接在浏览器中,而不需要一个插件或外部应用程序。WebRTC（Web实时通信）是一种技术，使Web应用程序和网站来捕捉和可选的音频和/或视频流媒体，以及交换任意数据之间的浏览器不需要中介。该系列标准包括WebRTC能够共享数据和执行会议的对等，而不需要用户安装插件或任何其他第三方软件。
WebRTC由几个相互关联的应用程序接口和协议，共同实现这。文件，你会发现这里将帮助你理解WebRTC的基础，如何设置和使用数据和媒体的连接，和更多。


# 离线&存储

## The application cache manifest="example.appcache"

```html
<html manifest="example.appcache">
  ...
</html>
``` 
这种方式已经过时，不推荐使用。

## 在线&离线事件

### navigator.onLine

navigator.onLine return true/false

e.g
```javascript
window.addEventListener('load', function() {
  var status = document.getElementById("status");
  var log = document.getElementById("log");

  function updateOnlineStatus(event) {
    var condition = navigator.onLine ? "online" : "offline";

    status.className = condition;
    status.innerHTML = condition.toUpperCase();

    log.insertAdjacentHTML("beforeend", "Event: " + event.type + "; Status: " + condition);
  }

  window.addEventListener('online',  updateOnlineStatus);
  window.addEventListener('offline', updateOnlineStatus);
});
```

## Web Storage API

- sessionStorage 
- localStorage 

[https://github.com/mdn/web-storage-demo](https://github.com/mdn/web-storage-demo)

- Storage.length 

- Storage.key()
 当传入一个数字，这个方法会返回这个名字在storage中根据索引。
- Storage.getItem() 
 当传入一个`key`的名字，返回值
- Storage.setItem()
 当传入一个`key`的名字，会在storage增加这个键值对，或者当存在时更新这个值。
- Storage.removeItem()
 当传入一个`key`的名字，会删除这个键值对。
Storage.clear()
 当调用这个方法，会清空storage。

e.g
```javascript
if(!localStorage.getItem('bgcolor')) {
  populateStorage();
}
setStyles();

function populateStorage() {
  localStorage.setItem('bgcolor', document.getElementById('bgcolor').value);
  localStorage.setItem('font', document.getElementById('font').value);
  localStorage.setItem('image', document.getElementById('image').value);
}

function setStyles() {
  var currentColor = localStorage.getItem('bgcolor');
  var currentFont = localStorage.getItem('font');
  var currentImage = localStorage.getItem('image');

  document.getElementById('bgcolor').value = currentColor;
  document.getElementById('font').value = currentFont;
  document.getElementById('image').value = currentImage;

  htmlElem.style.backgroundColor = '#' + currentColor;
  pElem.style.fontFamily = currentFont;
  imgElem.setAttribute('src', currentImage);
}
```

## IndexedDB API

### 基本使用

1. Open a database.
2. Create an object store in the database. 
3. Start a transaction and make a request to do some database operation, like adding or retrieving data.
4. Wait for the operation to complete by listening to the right kind of DOM event.
5. Do something with the results (which can be found on the request object).


*兼容*
```javascript
// In the following line, you should include the prefixes of implementations you want to test.
window.indexedDB = window.indexedDB || window.mozIndexedDB || window.webkitIndexedDB || window.msIndexedDB;
// DON'T use "var indexedDB = ..." if you're not in a function.
// Moreover, you may need references to some window.IDB* objects:
window.IDBTransaction = window.IDBTransaction || window.webkitIDBTransaction || window.msIDBTransaction || {READ_WRITE: "readwrite"}; // This line should only be needed if it is needed to support the object's constants for older browsers
window.IDBKeyRange = window.IDBKeyRange || window.webkitIDBKeyRange || window.msIDBKeyRange;
// (Mozilla has never prefixed these objects, so we don't need window.mozIDB*)
```

### 基本例子

```
const dbName = "the_name";

var request = indexedDB.open(dbName, 2);

request.onerror = function(event) {
  // Handle errors.
};
request.onupgradeneeded = function(event) {
  var db = event.target.result;

  // Create an objectStore to hold information about our customers. We're
  // going to use "ssn" as our key path because it's guaranteed to be
  // unique - or at least that's what I was told during the kickoff meeting.
  var objectStore = db.createObjectStore("customers", { keyPath: "ssn" });

  // Create an index to search customers by name. We may have duplicates
  // so we can't use a unique index.
  objectStore.createIndex("name", "name", { unique: false });

  // Create an index to search customers by email. We want to ensure that
  // no two customers have the same email, so use a unique index.
  objectStore.createIndex("email", "email", { unique: true });

  // Use transaction oncomplete to make sure the objectStore creation is 
  // finished before adding data into it.
  objectStore.transaction.oncomplete = function(event) {
    // Store values in the newly created objectStore.
    var customerObjectStore = db.transaction("customers", "readwrite").objectStore("customers");
    for (var i in customerData) {
      customerObjectStore.add(customerData[i]);
    }
  };
};
```

## 从web应用程序使用文件

### 基本使用方法

现在可以从HTML5的`File API`读取本地文件，通过`<input>`的`type='file'`，其实是通过 [FileReader](https://developer.mozilla.org/en-US/docs/DOM/FileReader)

```html
<input type='file' id='input'>
```

如果选择了文件会返回文件对象通过dom访问得到。

```javascript
var selectedFile = document.getElementById('input').files[0];
```

jquery:

```javascript
var selectedFile = $('#input').get(0).files[0];

var selectedFile = $('#input')[0].files[0];
```

选择文件后触发方法：

```html
<input type="file" id="input" onchange="handleFiles(this.files)">
```

如果你想选择多个文件 给 `input` 加上 `multiple` 属性

```html
<input type="file" id="input" multiple onchange="handleFiles(this.files)">
```

给选择文件夹上监听事件。

```javascript
var inputElement = document.getElementById("input");
inputElement.addEventListener("change", handleFiles, false);
function handleFiles() {
  var fileList = this.files; /* now you can work with the file list */
}
```

### e.g 显示文件大小

```javascript
function updateSize() {
  var nBytes = 0,
      oFiles = document.getElementById("uploadInput").files,
      nFiles = oFiles.length;
  for (var nFileId = 0; nFileId < nFiles; nFileId++) {
    nBytes += oFiles[nFileId].size;
  }
  var sOutput = nBytes + " bytes";
  // optional code for multiples approximation
  for (var aMultiples = ["KiB", "MiB", "GiB", "TiB", "PiB", "EiB", "ZiB", "YiB"], nMultiple = 0, nApprox = nBytes / 1024; nApprox > 1; nApprox /= 1024, nMultiple++) {
    sOutput = nApprox.toFixed(3) + " " + aMultiples[nMultiple] + " (" + nBytes + " bytes)";
  }
  // end of optional code
  document.getElementById("fileNum").innerHTML = nFiles;
  document.getElementById("fileSize").innerHTML = sOutput;
}
```

```html
<body onload="updateSize();">
<form name="uploadForm">
<p><input id="uploadInput" type="file" name="myFiles" onchange="updateSize();" multiple> selected files: <span id="fileNum">0</span>; total size: <span id="fileSize">0</span></p>
<p><input type="submit" value="Send file"></p>
</form>
</body>
```

### 使用`hidden`的`file input` 通过 `click()` 来触发选择文件


```html
<input type="file" id="fileElem" multiple accept="image/*" style="display:none" onchange="handleFiles(this.files)">
<a href="#" id="fileSelect">Select some files</a>
```

```javascript
var fileSelect = document.getElementById("fileSelect"),
  fileElem = document.getElementById("fileElem");

fileSelect.addEventListener("click", function (e) {
  if (fileElem) {
    fileElem.click();
  }
  e.preventDefault(); // prevent navigation to "#"
}, false);
```

### 通过`label`元素来触发隐藏的`file input`

```html
<input type="file" id="fileElem" multiple accept="image/*" style="display:none" onchange="handleFiles(this.files)">
<label for="fileElem">Select some files</label>
```

### 选择文件通过拖拽拖放

[文档](https://developer.mozilla.org/en-US/docs/Web/Events/dragenter)

```javascript
var dropbox;

dropbox = document.getElementById("dropbox");
dropbox.addEventListener("dragenter", dragenter, false);
dropbox.addEventListener("dragover", dragover, false);
dropbox.addEventListener("drop", drop, false);

function drop(e) {
  e.stopPropagation();
  e.preventDefault();

  var dt = e.dataTransfer;
  var files = dt.files;

  handleFiles(files);
}


function handleFiles(files) {
  for (var i = 0; i < files.length; i++) {
    var file = files[i];
    var imageType = /^image\//;
    
    if (!imageType.test(file.type)) {
      continue;
    }
    
    var img = document.createElement("img");
    img.classList.add("obj");
    img.file = file;
    preview.appendChild(img); // Assuming that "preview" is the div output where the content will be displayed.
    
    var reader = new FileReader();
    reader.onload = (function(aImg) { return function(e) { aImg.src = e.target.result; }; })(img);
    reader.readAsDataURL(file);
  }
}
```

### 使用 object URLs

```javascript
var objectURL = window.URL.createObjectURL(fileObj);

window.URL.revokeObjectURL(objectURL);
```

####　e.g: 使用 object URLs 显示图像

```html
<input type="file" id="fileElem" multiple accept="image/*" style="display:none" onchange="handleFiles(this.files)">
<a href="#" id="fileSelect">Select some files</a>
<div id="fileList">
  <p>No files selected!</p>
</div>
```

```javascript
  window.URL = window.URL || window.webkitURL;
  var fileSelect = document.getElementById("fileSelect"),
      fileElem   = document.getElementById("fileElem"),
      fileList   = document.getElementById("fileList");
  fileSelect.addEventListener("click", function (e) {
    if (fileElem) {
      fileElem.click();
    }
    e.preventDefault(); // prevent navigation to "#"
  }, false);
  function handleFiles(files) {
    if (!files.length) {
      fileList.innerHTML = "<p>No files selected!</p>";
    } else {
      fileList.innerHTML = "";
      var list = document.createElement("ul");
      fileList.appendChild(list);
      for (var i = 0; i < files.length; i++) {
        var li = document.createElement("li");
        list.appendChild(li);
        var img = document.createElement("img");
        img.src = window.URL.createObjectURL(files[i]);
        img.height = 60;
        img.onload = function () {
          window.URL.revokeObjectURL(this.src);
        }
        li.appendChild(img);
        var info = document.createElement("span");
        info.innerHTML = files[i].name + ": " + files[i].size + " bytes";
        li.appendChild(info);
      }
    }
  }
```

1. A new unordered list (<ul>) element is created.
2. The new list element is inserted into the <div> block by calling its element.appendChild() method.
3. For each File in the FileList represented by files:
4. Create a new list item (<li>) element and insert it into the list.
5. Create a new image (<img>) element.
6. Set the image's source to a new object URL representing the file, using window.URL.createObjectURL() to create the blob URL.
7. Set the image's height to 60 pixels.
8. Set up the image's load event handler to release the object URL since it's no longer needed once the image has been loaded. This is done by calling the window.URL.revokeObjectURL() method and passing in the object URL string as specified by img.src.
9. Append the new list item to the list.

### 上传选择的文件

```javascript
function FileUpload(img, file) {
  var reader = new FileReader();  
  this.ctrl = createThrobber(img);
  var xhr = new XMLHttpRequest();
  this.xhr = xhr;
  
  var self = this;
  this.xhr.upload.addEventListener("progress", function(e) {
        if (e.lengthComputable) {
          var percentage = Math.round((e.loaded * 100) / e.total);
          self.ctrl.update(percentage);
        }
      }, false);
  
  xhr.upload.addEventListener("load", function(e){
          self.ctrl.update(100);
          var canvas = self.ctrl.ctx.canvas;
          canvas.parentNode.removeChild(canvas);
      }, false);
  xhr.open("POST", "http://demos.hacks.mozilla.org/paul/demos/resources/webservices/devnull.php");
  xhr.overrideMimeType('text/plain; charset=x-user-defined-binary');
  reader.onload = function(evt) {
    xhr.send(evt.target.result);
  };
  reader.readAsBinaryString(file);
}
```

1. The XMLHttpRequest's upload progress listener is set to update the throbber with new percentage information so that as the upload progresses the throbber will be updated based on the latest information.
2. The XMLHttpRequest's upload load event handler is set to update the throbber progress information to 100% to ensure the progress indicator actually reaches 100% (in case of granularity quirks during the process). It then removes the throbber since it's no longer needed. This causes the throbber to disappear once the upload is complete.
3. The request to upload the image file is opened by calling XMLHttpRequest's open() method to start generating a POST request.
4. The MIME type for the upload is set by calling the XMLHttpRequest function overrideMimeType(). In this case, we're using a generic MIME type; you may or may not need to set the MIME type at all depending on your use case.
5. The FileReader object is used to convert the file to a binary string.
6. Finally, when the content is loaded the XMLHttpRequest function send() is called to upload the file's content.

### 使用 `object URLs` 显示 `PDF`

```html
<iframe id="viewer">
```

```javascript
var obj_url = window.URL.createObjectURL(blob);
var iframe = document.getElementById('viewer');
iframe.setAttribute('src', obj_url);
window.URL.revokeObjectURL(obj_url);
```

### 扩展

[blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)

一个`blob`对象就是这个文件的原始数据。
　　　
# 媒体

## 使用 `HTML5` 的 `audio` & `video 
　　　
```html
<video src="http://v2v.cc/~j/theora_testsuite/320x240.ogg" controls>
  Your browser does not support the <code>video</code> element.
</video>
<audio src="/test/audio.ogg">
<p>Your browser does not support the <code>audio</code> element.</p>
</audio>
```
## WebRTC API (Web Real-Time Communication)

这个API很强大，webRTC （Web Real-Time Communication）是一个支持网页浏览器进行实时语音对话或视频对话的技术，缺点是只在 PC 的 Chrome 上支持较好，移动端支持不太理想。

### 使用webRTC录制视频基本流程

[MDN WEBRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API)

1. 调用 window.navigator.webkitGetUserMedia() 获取用户的PC摄像头视频数据。
2. 将获取到视频流数据转换成 window.webkitRTCPeerConnection (一种视频流数据格式)。
3. 利用 WebScoket 将视频流数据传输到服务端。

## 使用 Camera API 
这个API目前只适用于Firefox 浏览器 ,下面的例子在手机端浏览器打开，会显示拍照选项，拍照后，或选择照片后会显示在网页上。

[https://developer.mozilla.org/en-US/docs/Mozilla/B2G_OS/API/Camera_API](https://developer.mozilla.org/en-US/docs/Mozilla/B2G_OS/API/Camera_API)

语法
```javascript
var cameraManager = window.navigator.mozCameras;
```

```html
<input type="file" id="take-picture" accept="image/*">
<img src="about:blank" alt="" id="show-picture">
```

```javascript
(function () {
    var takePicture = document.querySelector("#take-picture"),
        showPicture = document.querySelector("#show-picture");

    if (takePicture && showPicture) {
        // Set events
        takePicture.onchange = function (event) {
            // Get a reference to the taken picture or chosen file
            var files = event.target.files,
                file;
            if (files && files.length > 0) {
                file = files[0];
                try {
                    // Get window.URL object
                    var URL = window.URL || window.webkitURL;

                    // Create ObjectURL
                    var imgURL = URL.createObjectURL(file);

                    // Set img src to ObjectURL
                    showPicture.src = imgURL;

                    // Revoke ObjectURL after imagehas loaded
                    showPicture.onload = function() {
                        URL.revokeObjectURL(imgURL);  
                    };
                }
                catch (e) {
                    try {
                        // Fallback if createObjectURL is not supported
                        var fileReader = new FileReader();
                        fileReader.onload = function (event) {
                            showPicture.src = event.target.result;
                        };
                        fileReader.readAsDataURL(file);
                    }
                    catch (e) {
                        // Display error message
                        var error = document.querySelector("#error");
                        if (error) {
                            error.innerHTML = "Neither createObjectURL or FileReader are supported";
                        }
                    }
                }
            }
        };
    }
})();
```

## `track` 标签

> track用来指定 audio 元素和 video 元素的字幕、标题、章节等轨信息。HTML5追加内容，现在还没什么浏览器支持，将来有可能会有改动。

HTML代码

```html

<video src="brave.webm">
 <track kind="subtitles" src="brave.ja.vtt" srclang="zh" label="Chinese">
 <track kind="subtitles" src="brave.en.vtt" srclang="en" label="English">
 <track kind="subtitles" src="brave.de.vtt" srclang="de" label="Deutsch">
</video>
```

# 3D图形和效果

## `Canvas` 画布

```html
<canvas id="tutorial" width="150" height="150"></canvas>
```

得到`canvas` 上下文

```javascript
var canvas = document.getElementById('tutorial');
if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```


e.g:
```javascript
ctx.fillStyle = "rgb(200,0,0)";
        ctx.fillRect (10, 10, 50, 50);

        ctx.fillStyle = "rgba(0, 0, 200, 0.5)";
        ctx.fillRect (30, 30, 50, 50);
```

具体用法 
[http://www.runoob.com/tags/ref-canvas.html](http://www.runoob.com/tags/ref-canvas.html)

## WebGl

如果说`Canvas`实在2D上做图，那么`WebGL`就提供了浏览器3D绘图的能力，这是百度百科的解释：

> WebGL（全写Web Graphics Library）是一种3D绘图标准，这种绘图技术标准允许把JavaScript和OpenGL ES 2.0结合在一起，通过增加OpenGL ES 2.0的一个JavaScript绑定，WebGL可以为HTML5 Canvas提供硬件3D加速渲染，这样Web开发人员就可以借助系统显卡来在浏览器里更流畅地展示3D场景和模型了，还能创建复杂的导航和数据视觉化。显然，WebGL技术标准免去了开发网页专用渲染插件的麻烦，可被用于创建具有复杂3D结构的网站页面，甚至可以用来设计3D网页游戏等等。

[https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API)

主要代表有[three.js](https://github.com/mrdoob/three.js)

先不做研究。

## SVG
                                                                                                 
> 矢量图像的基于xml的格式,可以直接嵌入到HTML中。

[http://www.w3school.com.cn/svg/](http://www.w3school.com.cn/svg/)

# 性能和集成

## Web Workers

> 网络工作者提供一个简单的方法Web内容在后台线程运行脚本。工作线程可以执行任务而不干扰用户界面。此外,他们可以执行I / O使用XMLHttpRequest(虽然responseXML和通道属性总是零)。一旦创建,一个工人可以将消息发送到创建它的JavaScript代码发布信息到指定的事件处理程序的代码(反之亦然)。本文提供了一个详细的介绍使用web工人。

[https://developer.mozilla.org/en-US/docs/DOM/Using_web_workers](https://developer.mozilla.org/en-US/docs/DOM/Using_web_workers)

## XMLHttpRequest level2 (AJax 2.0)

[https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest]()

## History API

> 允许浏览器的操作历史。这是特别有用的页面加载交互新信息。

[https://developer.mozilla.org/en-US/docs/Web/API/History_API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)

## `contenteditable="true"
 
 这个属性可以让html页面上的内容被编辑。
 
```html
<div contenteditable="true">
  This text can be edited by the user.
</div>
```

## History APi

[https://developer.mozilla.org/en-US/docs/Web/API/History_API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)

允许浏览器的操作历史。这是对页面加载交互新信息特别有用。（操作url的`hash`值）

```javascript
window.history.back();//类似浏览器后退按钮，相对应
window.history.forward();
```

// 通过`go()`方法来返回前进到特定页面

```javascript
window.history.go(-1);//后退一个页面
window.history.go(-2);//后退两个页面
window.history.go(1);//前进一个页面
```

您可以通过查看长度属性的值来确定历史堆栈中的页数：

```javascript
var numberOfEntries = window.history.length;
```

## HTML Drag and Drop API

> HTML拖放接口使应用程序能够使用拖和Firefox等浏览器滴特征。例如，有了这些功能，用户可以选择用鼠标拖动元素，拖动元素到一个可删除的元素，这些元素和下降释放鼠标按键。

[https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)

事件 | 事件方法 | 介绍
---|--- |---
drag |	ondrag |	Fired when an element or text selection is being dragged.
dragend |	ondragend |	Fired when a drag operation is being ended (for example, by releasing a mouse button or hitting the escape key). (See Finishing a Drag.)
dragenter |	ondragenter |	Fired when a dragged element or text selection enters a valid drop target. (See Specifying Drop Targets.)
dragexit |	ondragexit |	Fired when an element is no longer the drag operation's immediate selection target.
dragleave |	ondragleave |	Fired when a dragged element or text selection leaves a valid drop target.
dragover |	ondragover |	Fired when an element or text selection is being dragged over a valid drop target (every few hundred milliseconds).
dragstart |	ondragstart |	Fired when the user starts dragging an element or text selection. (See Starting a Drag Operation.)
drop |	ondrop	Fired when | an element or text selection is dropped on a valid drop target. (See Performing a Drop.)

## Document.hasFocus()

> 文件。hasfocus()方法返回一个布尔值，指示是否文件或任何元素在文档具有焦点。此方法可用于确定文档中的活动元素是否具有焦点.。

*语法*

```javascript
focused = document.hasFocus();
```

```javascript
setInterval( checkPageFocus, 200 );

function checkPageFocus() {
  var info = document.getElementById("message");

  if ( document.hasFocus() ) {
    info.innerHTML = "The document has the focus.";
  } else {
    info.innerHTML = "The document doesn't have the focus.";
  }
}

function openWindow() {
  window.open (
    "http://developer.mozilla.org/",
    "mozdev",
    "width=640,
    height=300,
    left=150,
    top=260"
  );
}
```

## Document.focus()

> 让元素获得焦点

```javascript
document.getElementById("message").focus();
```

## 基于Web的协议处理程序

[https://www.w3.org/TR/2011/WD-html5-20110525/timers.html#custom-handlers](https://www.w3.org/TR/2011/WD-html5-20110525/timers.html#custom-handlers)

> 实现调起本地邮箱软件发送邮件
```html
<a href="mailto:webmaster@example.com">Web Master</a>
```

> 在 `APP中的网页` `Hybird APP` 用 `URL Scheme` 来调用其他APP

1. [你所知道好玩有趣的 iOS URL Scheme 有哪些?](https://www.zhihu.com/question/19907735)
2. [利用 URL schemes 实现 Siri 启动应用程序](http://www.idownloadblog.com/2011/11/07/quickly-launch-apps-with-siri/?utm_source=dlvr.it&utm_medium=twitter)
3. [一个收录大部分 URL schemes 的维基页面](http://wiki.akosma.com/IPhone_URL_Schemes)
4. [ 一个 iOS URL schemes 目录](http://handleopenurl.com/scheme)

### 注册事件

> 将web应用程序设置为协议处理程序不是一个困难的过程.。基本上，Web应用程序使用registerprotocolhandler()以浏览器为一个给定的协议处理程序登记本身的潜力。

[registerProtocolHandler()](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/registerProtocolHandler)

```javascript
navigator.registerProtocolHandler("burger",
                                  "http://www.google.co.uk/?uri=%s",
                                  "Burger handler");
```

触发

```html
<p>Hey have you seen <a href="burger:cheeseburger">this</a> before?</p>
```

实际上是访问的 `http://www.google.co.uk/?uri=burger:cheeseburger`

## window.requestAnimationFrame()

> 在浏览器动画程序中，我们通常使用一个定时器来循环每隔几毫秒移动目标物体一次，来让它动起来。如今有一个好消息，浏览器开发商们决定：“嗨，为什么我们不在浏览器里提供这样一个API呢，这样一来我们可以为用户优化他们的动画。”所以，这个requestAnimationFrame()函数就是针对动画效果的API，你可以把它用在DOM上的风格变化或画布动画或WebGL中。

好处

> 浏览器可以优化并行的动画动作，更合理的重新排列动作序列，并把能够合并的动作放在一个渲染周期内完成，从而呈现出更流畅的动画效果。比如，通过requestAnimationFrame()，JS动画能够和CSS动画/变换或SVG SMIL动画同步发生。另外，如果在一个浏览器标签页里运行一个动画，当这个标签页不可见时，浏览器会暂停它，这会减少CPU，内存的压力，节省电池电量。

> 兼容

```javascript
window.requestAnimationFrame = window.requestAnimationFrame 
                                || window.mozRequestAnimationFrame 
                                || window.webkitRequestAnimationFrame 
                                || window.msRequestAnimationFrame;
```

例子

```javascript
var start = null;
var element = document.getElementById("SomeElementYouWantToAnimate");
element.style.position = 'absolute';

function step(timestamp) {
  if (!start) start = timestamp;
  var progress = timestamp - start;
  element.style.left = Math.min(progress/10, 200) + "px";
  if (progress < 2000) {
    window.requestAnimationFrame(step);
  }
}

window.requestAnimationFrame(step);
```

## FullScreen API

> 全屏API提供Web内容是利用用户的整个屏幕上出现了一个简单的方法。该API可以让你轻松地直接浏览器使元素和它的孩子，如果有，占据全屏，消除所有浏览器的用户界面和其他应用程序的屏幕时间。

```javascript
document.addEventListener("keydown", function(e) {
  if (e.keyCode == 13) {
    toggleFullScreen();
  }
}, false);


function toggleFullScreen() {
  if (!document.fullscreenElement) {
      document.documentElement.requestFullscreen();
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen(); 
    }
  }
}
```


事件
- Document.fullscreen
- Document.fullscreenElement
- Document.onfullscreenchange
- Document.onfullscreenerror

## Pointer Lock API

[http://www.tfan.org/pointer-lock-api/](http://www.tfan.org/pointer-lock-api/)

> 指针锁定(以前叫做 鼠标锁定) 提供了一种输入方法，这种方法是基于鼠标随着时间推移的运动的（也就是说，deltas），而不仅是鼠标光标的绝对位置。通过它可以访问原始的鼠标运动，把鼠标事件的目标锁定到一个单独的元素，这就消除了鼠标在一个单独的方向上到底可以移动多远这方面的限制，并从视图中删去光标。
  
  这个 API 对于需要大量的鼠标输入来控制运动，旋转物体，以及更改项目的应用程序来说非常有用。对高度视觉化的应用程序尤其重要，例如那些使用第一人称视角的应用程序，以及 3D 视图和建模。
  
  举例来说，你可以创建让你的用户简单地通过移动鼠标而不需要点击任何按钮就可以控制视角的应用。那么这些按钮就可以被用作其他动作。这类鼠标输入对于查看地图，卫星图像，或者第一人称场景（例如在一个游戏中或者一个全景视频中）是非常方便使用的。
  
  即使在光标移到浏览器或者屏幕区域之外，指针锁定也能够让你访问鼠标事件。例如，你的用户可以通过不断地移动鼠标来持续旋转或操纵一个 3D 模型。如果没有指针锁定的话，这些旋转或操纵会在指针到达浏览器或者屏幕边缘的那一刻停止。尤其是游戏玩家将会因为此功能而兴奋不已，因为他们可以疯狂地点击按钮，来回地滑动鼠标光标，而不必担心离开了游戏区域，进而不小心误点到另外一个应用程序上，结果将鼠标焦点移离了游戏。杯具了！

# 访问设备

##　Touch events

> 移动端的触摸事件

```javascript
function startup() {
  var el = document.getElementsByTagName("canvas")[0];
  el.addEventListener("touchstart", handleStart, false);
  el.addEventListener("touchend", handleEnd, false);
  el.addEventListener("touchcancel", handleCancel, false);
  el.addEventListener("touchmove", handleMove, false);
  log("initialized.");
}
```
### 接口

- Touch 
```javascript
touch = new Touch(touchInit);
```
1. Touch.clientX
2. Touch.clientY
3. Touch.force
4. Touch.identifier
...
- TouchEvent 
- TouchList

### 事件
- touchstart
- touchend
- touchmove
- touchcancel

## HTML5定位

```javascript
function geoFindMe() {
  var output = document.getElementById("out");

  if (!navigator.geolocation){
    output.innerHTML = "<p>Geolocation is not supported by your browser</p>";
    return;
  }

  function success(position) {
    var latitude  = position.coords.latitude;
    var longitude = position.coords.longitude;

    output.innerHTML = '<p>Latitude is ' + latitude + '° <br>Longitude is ' + longitude + '°</p>';

    var img = new Image();
    img.src = "https://maps.googleapis.com/maps/api/staticmap?center=" + latitude + "," + longitude + "&zoom=13&size=300x300&sensor=false";

    output.appendChild(img);
  }

  function error() {
    output.innerHTML = "Unable to retrieve your location";
  }

  output.innerHTML = "<p>Locating…</p>";

  navigator.geolocation.getCurrentPosition(success, error);
}
```

## 设备的陀螺仪

> 通过这个API可以访问设备的陀螺仪信息


```javascript
window.addEventListener("devicemotion", handleMotion, true);
```


1. DeviceMotionEvent.acceleration
2. DeviceMotionEvent.accelerationIncludingGravity
3. DeviceMotionEvent.rotationRate
4. DeviceMotionEvent.interval

简单的例子

```javascript
var ball   = document.querySelector('.ball');
var garden = document.querySelector('.garden');
var output = document.querySelector('.output');

var maxX = garden.clientWidth  - ball.clientWidth;
var maxY = garden.clientHeight - ball.clientHeight;

function handleOrientation(event) {
  var x = event.beta;  // In degree in the range [-180,180]
  var y = event.gamma; // In degree in the range [-90,90]

  output.innerHTML  = "beta : " + x + "\n";
  output.innerHTML += "gamma: " + y + "\n";

  // Because we don't want to have the device upside down
  // We constrain the x value to the range [-90,90]
  if (x >  90) { x =  90};
  if (x < -90) { x = -90};

  // To make computation easier we shift the range of 
  // x and y to [0,180]
  x += 90;
  y += 90;

  // 10 is half the size of the ball
  // It center the positioning point to the center of the ball
  ball.style.top  = (maxX*x/180 - 10) + "px";
  ball.style.left = (maxY*y/180 - 10) + "px";
}

window.addEventListener('deviceorientation', handleOrientation);
```

实例 [摇一摇](http://www.cnblogs.com/waitingbar/p/4682215.html)

# HTML5 Notification API

> PC端的浏览器桌面通知功能。

## 例子

```javascript
	var Notification = window.Notification || window.mozNotification || window.webkitNotification;

	Notification.requestPermission(function (permission) {
		// console.log(permission);
	});

	function show() {
		window.setTimeout(function () {
			var instance = new Notification(
				"标题", {
					body: "消息",
					icon: "http://resource.zwjay.cn/jekyll/img/avatar-zwj.jpg"

				}
			);

			instance.onclick = function () {
				// Something to do
			};
			instance.onerror = function () {
				// Something to do
			};
			instance.onshow = function () {
				// Something to do
			};
			instance.onclose = function () {
				// Something to do
			};
		}, 3000);
	}
```

```html
<button type="button" onclick="show()">Notify me!</button>
```

# 最后：新增的CSS3

1. [FlexBox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes) 
2. 动画
3. 多列 （column-count）
4. 过渡
5. 2D 3D 转换
6. ....
