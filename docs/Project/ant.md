# Frontend



## 支付宝前端前锋营



### HTML - 阿相



#### 1. CS/BS架构

CS client server客户端开发：（网络游戏、聊天软件、视频软件）

1. 研发成本高，不同客户端，不同语言

2. 客户端安装、升级成本高



BS browser server：直接的网页内容（社交网站、搜索引擎、个人博客）

1. 资源加载慢，依赖网速
2. 端侧渲染性能相对较弱
3. 解决研发成本高的问题
4. 不需要更新的问题，因为网页版都是直接拿取的



狭义的前端：

HTML：页面内容

CSS：页面央视

Javascript：页面逻辑



#### 2. 跨平台开发

支付宝首页可以使用支付宝打开百度

支付宝实际上是内嵌了一个浏览器

听说手机上的APP重复装了十几个chrome内核

有些软件会直接调用safari的内核

app体积大的原因之一



小程序也属于web技术

支付宝的大部分功能都是通过浏览器加载的，就不用关心系统是IOS还是Android，节约了很大的成本



制约：

1. 能调用的系统api比较少，比如调用拍照、读取文件--JS Bridge
2. 加载网络速度较慢--离线包技术
3. 依赖浏览器的UI渲染，性能受限于浏览器--同层渲染

#### 3. Node.js

让前端不仅局限于客户端

服务器--网络--浏览器--网页内容



浏览器：（C/C++）

1. 连接网络
2. 执行HTML/CSS绘制页面
3. 执行JS处理逻辑
4. 本地文件的读取

前端（HTML/CSS/Javascript）

1. 处理UI交互逻辑
2. 调用服务端接口
3. 页面UI的绘制

服务器：（java/c++）

1. 处理业务逻辑
2. 数据的天删改查
3. 本地文件的读写
4. 提供网络接口





把浏览器跑在云端就是Node.js需要解决的问题

让javascript不仅局限于客户端的开发 







#### 总结

狭义的前端：应用软件中的展示和用户交互开发技术

广义的前端：跨平台的应用开发技术。有非正式的称呼“大前端”。



#### 工具环境: chrome Devtools

可视化的页面看设计出来的网页长什么样

排查故障

command+option+i

或者右键+检查

windows f12



主要用到元素、控制台和网络

元素：

HTML描述了网页的结构

下面的CSS描述了长什么样

CSS里面的盒模型：padding内边距、margin外边距、border边框

直接在devtools调试即可



控制台：

90%要用到控制台

console.log() 打印日志出来




直接在console里面打就行：

点clear console就能直接清空console

```javascript
function add(left, right) {return left + right;}


add(1, 2)

会返回3

Math.random() //编写小脚本可以快速写成,0-1的随机数
Math.random() * 10 //1-10的随机数
```



js是弱类型的语言，不要求声明变量类型





网络：帮我们知道这个网站到底请求了些什么东西

比如做爬虫也可以用这个功能

标头：请求的header

载荷：上传了哪些数据payload

响应：新的html代码



上面有过滤功能，里面的图片必然是最高清的图片















#### 工具环境：VScode

尽量不要输入中文和空格



新建html文件后，输入感叹号就能生成html的东西

code spell checker插件

live server右键html文件直接open with live server就行

查看-视图-终端



warp ---下一代终端

```shell
node -v
npm -v
node ./hello.js // 可以直接用node跑js代码
```





新建server

```javascript
const http = require('node:http');

// Create a local server to receive data from
const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({
    data: 'Hello World!'
  }));
});

server.listen(8000);
```





node直接跑了浏览器，让js变成编写服务端的语言

个人本地：127.0.0.1:



npm可以帮我们下载别人的代码

这个request功能必须要npm下载之后才能使用



```shell
npm install request
```

```javascript
const http = require('http');
const request = require('request')

// Create a local server to receive data from
const server = http.createServer((req, res) => {
  request.get('https://baidu.com', {}, (err, rs, body) => {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end(body);
  })
  
});

server.listen(8000);
```



#### HTML初探

来自Tim Berners-Lee 英国计算机科学家，万维网之父

科研人员查阅和共享材料太低效

35岁发明了world wide web让人们可以自由分享知识和想法的技术解决方案



HTML 超文本标记语言-如何存储和展示

URI 统一资源定位符，网络中资源的唯一地址-如何找到

HTTP 超文本传输协议-如何传输



1990年，浏览器诞生，Tim在NeXT电脑

1994年，网景公司成立，第一款商业浏览器Nestcape Navigator-浏览器商业化



在2012年前并没有特别发展



Html 2012年有html5

node 2009年出现



html5有更多语义化的标签、更便捷更强的多媒体能力，以及绘图、地理位置、数据缓存的能力





›html是由元素组成

元素由标签加内容组成的

元素可以相互嵌套

元素：

```html
<br/>  换行元素
<h1></h1> 标题
<img src='xxxxx'/> 图片元素
<p></p> 表示段落
<a></a>超链接 
<a href="https://taobao.com">淘宝网</a>

<span></span> 一般用于对于部分段的内容进行组合
<div></div>表示区块，一般用于聚合元素
<meta name="author" content="乐驰">

有序列表
<ol>
  <li></li>
</ol>

无序列表
<ul>
  <li></li>
</ul>
说明列表
<dl>
  <dt></dt>
  <dd></dd>
</dl>
导航栏
<nav>
  <a href=""></a>
</nav>



```

H1-h6标题

元素属性只能用在开始标签或单个标签，不能用于结束标签

有一些是全局属性，可用于所有的html元素，比如id、class、style

meta元素标签不需要闭合标签，仅设置在head元素中

viewport移动开发有趣的地方

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="hello.js"></script>
</head>
<body>
    <h1>乐驰</h1>
    <h2>Charles Chi Le</h2>
    <p>专业：生物医学</p>>
    <a href="https://charleschile.com">点击前往乐驰的个人blog</a>
    <p></p>
    <img src="WechatIMG313.jpeg", width="300">

</body>
</html>
```



现在用表格元素越来越少了，因为性能不行



语义化标签：






表单元素：表单元素在网页中主要负责数据采集的功能

比较复杂的一个元素

input是最常见的表单元素

```html
<form>
 First name:<br>
<input type="text" name="firstname" place>
<br>
 Last name:<br>
<input type="text" name="lastname">
</form> 

```












### 开发图书管理系统

1. 首页显示
2. 上传图片



分而治之、模块拆分



2个html

首页三个大版块



产品经理文档标注好



公共部分就是代码可以复用的部分

画廊做好左右滚动

列表



今天将html的部分写出来





- 打开文档后执行npm install
- npm run 0-init





Target = blank是重新开一个页面，然后跳转



### CSS 

cascade tyle sheets

p：选择器

color：属性

red：

```css
p {
  color: red;
  width: 500px;
  border: 1px splid black;
}
```



CSS的历史

比html晚好几年

1994年提出最初的建议

2001年微软发布IE6成为前端工程师的噩梦

要兼容IE6

2003年推出CSS禅意花园



11年CSS3



background: green;

Opacity: 0.5; 透明度50%



CSS



对div不会生效



hover下划线去掉的属性

visited访问过的

padding: 10px 15px 15px 5px;

（上右下左）

px像素 css中最基本的单位

%基于父体大小百分比缩放

```css
img {
  width: 10%;
  height: 20vw
}
```



浏览器的尺寸大小：视口

原始尺寸：图片默认是有尺寸的



如何改变img元素大小视口宽高的一半，随视口变化而变化

```css
img {
  width: 50vw;
  height: 50vh;
}
```



```css
p {
  background: rgba(222, 222, 222, 0.5);
}
```



还有RGBA颜色，最后一位表示透明度

```css
p {
  font-family:
}
```



文本的布局：text-align

Vertical-align垂直对齐

css文本：line-height行间距



开发里面行高默认

line-height: 1.5;



#1677ff蚂蚁的品牌色



快捷输入类型：
Img.名字 + tab

或者p.title + tab



dotted\dashed\solid



圆角：

Border-radius



```css
.box {
  border-radius: 30px;
}
```



设置成50%就是一个圆形





Background-size: contain保持横纵比

Background-size: cover完全覆盖背景



```css
div {
  background-repeat:no-repeat; //取消重复渲染
  
}
```



注释的快捷键command+/

```
box-shadow
```



通配符*

```css
* {
  border-size:
}
```

Content-box

和border-box

260\200

```css
.content-box {
    width: 200px;
    height: 200px;
    margin: 20px;
    padding: 20px;
    border: 10px solid #1677ff;
    box-sizing: content-box;
    background: gold;
  }
  .border-box {
    width: 200px;
    height: 200px;
    margin: 20px;
    padding: 20px;
    border: 10px solid #1677ff;
    box-sizing: border-box;
    background: gold;
  }
```



overflow控制溢出行为

overflow-x 和-y 用来控制沿着x轴划动

White-space: 换行





相对定位：relative

```css
.box {
  position: relative;
  top: 20px;
}
```



绝对定位：absolute

从正常布局流中移出，变成单独的一个图层

固定布局：fixed

像磁贴一样，在屏幕上的位置不会变动



Z-index：展示元素的顺序



越小图层越在下面

文字垂直+水平居中

Line-height



flex布局：justify-content

定义了主轴上的对齐方式



善于用搜索引擎：

flex的速查https://www.webhek.com/apps/flex-cheatsheet



transform





向左垂直向上移动就是取负号即可



Scale(10)放大10倍



过渡：一个元素在不同状态之间切换的时候定义不同的过渡效果



```css
ant:hover {
  
}
```

动画animation相较于脚本实现动画技术，比较简单、流畅、高性能



```html
<!-- <style>
    <!-- 覆盖浏览器默认样式 -->
    
    
    .card-list {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
    .box-submit-img {
        width: 200px;
        height: 200px;
        object-fit: contain;
    }
    .card {
        display: inline-block;
        width: 200px;
        height:300px;
        margin: 50px 8px;
        padding: 8px;
        border-radius: 8px;
        box-shadow: 0 30px 30px 0 rgba(140, 153, 191, 0.20);
    }
    .box-img {
        width: 200px;
        height: 100px;
        object-fit: cover;
    }
    .box-title {
        margin: 12px auto;
        font-size: 24px;
        font-weight: bold;
    }
    .box-author {
        margin: 6px auto;
        font-size: 16px;
    }
    .box-desc {
        margin: 6px auto;
        font-size: 16px;
    }
</style> -->
```





### JavaScript

#### 什么是javascript

最早的界面不需要javascript，就是后端直接拉html表单，拼在一起就行

现在javascript可以实现3D渲染



java和javascript的关系

雷锋和雷峰塔的关系

演化路径挺特别的



js可以通过html标签直接引入







#### javascript语言基础

图灵完备：可以计算所有可计算的问题

javascript是图灵完备的

sql、html就不是图灵完备的额

C++和java肯定是图灵完备的



js代码里面，变量的定义尽量不要使用var了：

```javascript
test = '1';
if (test) {
  var test = 2;
}
console.log(test); // 输出的是2
```





建议使用const和let

js是弱类型的，都可以直接用let定义

string 双引号或者单引号

number

boolean

null

undefined



等于 == 

全等于	===

```javascript
3 == 3; // true
3 == '3'; // true
3 === 3; // true
3 === '3'; // false
```

尽量使用全等于





```
<!-- <li class="gallary-item">
                    <img src="./data/pic/pic-1.png" />
                    <p class="name">落日</p>
                    <p class="photographer">by 蚂蚁</p>
                    <p class="desc">长河落日圆</p>
                </li>
                <li class="gallary-item">
                    <img src="./data/pic/pic-2.png" />
                    <p class="name">礁石</p>
                    <p class="photographer">by 蚂蚁</p>
                    <p class="desc">东临碣石，以观沧海</p>
                </li>
                <li class="gallary-item">
                    <img src="./data/pic/pic-3.png" />
                    <p class="name">波浪</p>
                    <p class="photographer">by 蚂蚁</p>
                    <p class="desc">木落雁嗷嗷，洞庭波浪高</p>
                </li> -->
```



拓展：typescript，兼容js语法



#### window和dom

DOM，即为 Document Object Model，是用于控制文档的标准对象。DOM 和该页面载入的 html 文档是对应的。DOM 是万维网联盟（W3C）的标准，当前由 WHATWG 和 W3C 共同维护。





#### JSON和网络请求



JavaScript Object Notation (JSON)

数据规范的格式

```json
{
  "name": "波浪",
  "photographer": "蚂蚁",
  "desc": "木落雁嗷嗷，洞庭波浪高",
  "picPath": "data/pic/pic-3.png"
}
```

```json
{ 	
  "numberType": 1,
  "stringType": "string",
  "booleanType": false,
  "arrayType": ["string",false,1],
  "objectType": {},
  "nullType": null
}
```



请求是需要时间的

浏览器是单线程的

浏览器的设计中有异步这个概念

线程不会阻塞



### Node.js

零启

#### node.js概述

js是运行在浏览器当中的

Node.js是javascript的一种运行环境

是将v8引擎加工成可以在任何操作系统中运动的javascript的平台



桌面应用：语雀、钉钉、vscode都是基于node开发的



javascript有爬虫模块



#### node.js基础

第一步：

```shell
npm -init -y
node hello.js
```



1、使⽤ require(‘os’) 引⽤⼀个 Node.js 内置模块 os
2、调⽤ os 模块的 platform() ⽅法获取操作系统平台类型

```js
const os = require('os'); // os是内置模块
console.log(os.platform()); // darwin mac平台
```



同步和异步

同步：按照代码顺序执行

异步：不按照代码顺序执行，异步的执行效率更高



js是单线程的，但是我们可以通过异步编程来同时执行多个任务



文件IO、网络请求、dom渲染、canvas绘制、进程间通信



实现方式：callback、promise、generator、async/await 





发布/订阅模型简介



事件监听-->事件对象<--事件发布

发送者将消息发送到指定地方

消息将被通知给指定的接受者



一个对象能监听的事件可以是多个的：单击、双击等等

发布发布订阅的用法

```js
const EventEmiter = require('events');
const eventEmiter = new EventEmiter; // 实例化

eventEmiter.on('notice', (msg)=>{
    console.log('I have received a message: ', msg);
})
//setTime是一个异步队列
setTimeout(() => {
    eventEmiter.emit('notice', 'hello') // 这一行后执行
}, 3000);  // 3秒钟，即使改成0，也会是后执行
//单线程，任务队列{task1, task2}	异步队列{task1, task2}
// 只有所有的同步任务队列执行完毕之后，才会执行异步队列

console.log('hello');  // 这一行先执行，异步
```





异步文件读写

```js
const fs = require('fs'); // file system

// 在node里面经常是err first的，就是第一个参数是err，然后有错误的话会第一时间就throw掉
fs.readFile('a.txt', 'utf-8', (err, data) => {
    if (err) throw err;
    console.log(data); // 然后再执行这行代码  
});

console.log('reading file ...'); // 先执行这行代码

```



同步文件读写

带sync就会执行同步文件读写，即只有执行完上一行代码才会继续执行下面一行代码

```js
const fs = require('fs');
// 同步写入
fs.writeFileSync('a.txt', 'Hello Node.js!', 'utf-8');
// 同步读取
const data = fs.readFileSync('a.txt','utf-8');

console.log(data); // 先执行读取文件的操作

console.log('reading file...'); // 最后执行打印日志
```



通常我们会使用异步来编程，防止后续堵塞

读取文件地址

```js
const fs = require('fs');
const path = require('path');

console.log(__dirname); ///Users/lechi/Desktop/Frontend/demo, 打印文件所在的路径

let filePath = path.join(__dirname, 'data', 'obj.json');
console.log(filePath); 
```



读取json并写入json文件中

```js
const fs = require('fs');
const path = require('path');

const obj = [
    {
      "name": "波浪",
      "photographer": "蚂蚁",
      "desc": "木落雁嗷嗷，洞庭波浪高",
      "picPath": "data/pic/pic-3.png"
    },
    {
      "name": "落日",
      "photographer": "蚂蚁",
      "desc": "长河落日圆",
      "picPath": "data/pic/pic-1.png"
    },
    {
      "name": "礁石",
      "photographer": "蚂蚁",
      "desc": "东临碣石，以观沧海",
      "picPath": "data/pic/pic-2.png"
    }
  ]
  

const filePath = path.join(__dirname, 'data', 'obj.json')

fs.writeFile(filePath, JSON.stringify(obj,null,2), (err, data) =>{
    if (err) {
        console.log('write fail');
    }
    else {
        console.log('write success');
    }
});

console.log(filePath);
```



自己写模块

在add的js文件里：

```js
exports.add = (x,y) => {
    return x + y;
};
```

然后调用自己的模块

```js
const compute = require('./add')
// 或者const{add} = require('/add')
const sum = compute.add(1, 2)
console.log(sum);
```







npm

是包管理系统

npm默认随着node一起安装

npm提供命令行工具用于管理模块



Json.stringfy

json.parse





#### node.js web服务

安装express，并且更新package.json中的依赖：

```shell
npm i express -S
```



http协议简介：（request、response）

http是文本协议，一次http请求分为请求和相应2个阶段



建立一个简单的express服务

```js
const express = require('express')
const app = express()

app.get('/', function (req, res) {
  res.send('Hello World')
})
// 80端口是默认端口
app.listen(80, ()=>{
    console.log('app is serving on port 80...');
})
```



如何在编辑后自动重启服务？



访问静态资源

static指定目录即可



既访问静态资源又新建接口

```js
const express = require('express')
const app = express()


app.use(express.static('web'))

app.get('/hello', function (req,res) {
    res.send('Hello Node')
})


app.listen(3000, ()=>{
    console.log('app is serving on port 3000...');
})
```





#### 图片管理系统

```js
    const res = await fetch('/pic/list');
    const pics = await res.json();
    pics.forEach(appendPic);
```















Index.js:

```js
function $(selector) {
    return document.querySelector(selector);
  }
  
  function appendPic(item) {
    // const { name, desc } = item || {};
  
    // 补充 html 的生成逻辑
    const html = `<li class="gallary-item">
    <img src="${item.picPath}" />
    <p class="name">${item.name}</p>
    <p class="photographer">by ${item.photographer}</p>
    <p class="desc">${item.desc}</p>
  </li>`;
  
    $('#pics').innerHTML += html;
  }
  
  async function fetchPics() {
    // 后续 pics 的内容通过请求后端获取
    // const pics = [
    //   {
    //     name: '波浪',
    //     photographer: '蚂蚁',
    //     desc: '木落雁嗷嗷，洞庭波浪高',
    //     picPath: 'data/pic/pic-3.png',
    //   },
    //   {
    //     name: '落日',
    //     photographer: '蚂蚁',
    //     desc: '长河落日圆',
    //     picPath: 'data/pic/pic-1.png',
    //   },
    //   {
    //     name: '礁石',
    //     photographer: '蚂蚁',
    //     desc: '东临碣石，以观沧海',
    //     picPath: 'data/pic/pic-2.png',
    //   },
    // ];

    // let pics = [];

    const res = await fetch('/web/data/data.json');
    const pics = await res.json();
    pics.forEach(appendPic);


    

    // fetch('/web/data/data.json').then(function(res) {
    //     return res.json();
    // }).then((pics) =>{
    //     pics.forEach(appendPic);
    // });
  
    // 修改为循环，可以使用 for，也可以使用 forEach
    // pics.forEach(appendPic);
    // appendPic(pics[0]);
    // appendPic(pics[1]);
    // appendPic(pics[2]);
  }
  
  fetchPics();
```



























































