## 1.对浏览器内核的理解           

```
浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。
渲染引擎 它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。

JS 引擎 则是解析 Javascript 语言，执行 javascript语言来实现网页的动态效果。

最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。有一个网页标准计划小组制作了一个 ACID 来测试引擎的兼容性和性能。内核的种类很多，常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit。
```

## 2.什么是<!DOCTYPE>?严格模式和混杂模式如何区分？它们有什么意义？

- DOCTYPE是html5标准网页声明，且必须声明在HTML文档的第一行。来告知浏览器的解析器用什么文档标准解析这个文档。

- 严格模式：又称标准模式，是指浏览器按照 W3C 标准解析代码。

- 混杂模式：又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码。

- 区分：浏览器解析时到底使用严格模式还是混杂模式，与网页中的 DTD(文档类型定义) 直接相关。

- 意义：严格模式与混杂模式存在的意义与其来源密切相关，如果说只存在严格模式，那么许多旧网站必然受到影响，如果只存在混杂模式，那么会回到当时浏览器大战时的混乱，每个浏览器都有自己的解析模式。所有的浏览器都需要提供两种模式：混杂模式服务于旧式规则，而严格模式服务于标准规则。

参考链接:<https://www.cnblogs.com/wuqiutong/p/5986191.html>

## 3.mate标签
提供给页面的一些元信息（名称/值对），有助于SEO。
属性值：
- name：名称/值对中的名称。author、description、keywords、generator、revised、others。 把 content 属性关联到一个名称。
- http-equiv：没有name时，会采用这个属性的值。content-type、expires、refresh、set-cookie。把content属性关联到http头部。
- content ： 名称/值对中的值， 可以是任何有效的字符串。 始终要和 name 属性或 http-equiv 属性一起使用。

## 4.html语义化
- 用正确的标签做正确的事情。
- html语义化让页面的内容结构化，结构更清晰，便于对浏览器，搜索引擎解析；
- 即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的；
- 搜索引擎的爬虫也依赖于HTML标记确定上下文和各个关键字的权重，利于SEO;
- 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。
## 5. HTML5有哪些新特性，移除了哪些元素？如何处理HTML5新标签的浏览器兼容问题？
- 新特性：
1. [新的语义化标签](https://www.w3school.com.cn/html/html5_new_elements.asp): header footer nav main article section
2. 	用于绘画的canvas元素；
3. 用于媒介回放的[video和audio元素](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)；
4.	对本地离线存储有更好的支持，localStorage长期存储数据，浏览器关闭后数据不丢失；sessionStorage的数据在浏览器关闭后自动删除；
5.	[表单增强](http://caibaojian.com/html5/form.html)：calendar,date,time,email,url,search；
6.	新的技术:webworker,websockt、Geolocation；
- 移除的元素
1. 纯表现的元素：basefont,big,center,font,s,strike,tt,u;
2. 对可用性产生负面影响的元素：frame,frameset,noframes;
- 如何处理html5新标签的浏览器兼容    [参考此链接](https://blog.csdn.net/zhouziyu2011/article/details/58588947)
1. 当在页面中使用HTML5新标签时，可能会得到三种不同的结果：
(1) 新标签被当作错误处理并被忽略，在DOM构建时会当作这个标签不存在。
(2) 新标签被当作错误处理，并在DOM构建时，这个新标签会被构造成行内元素。
(3)新标签被识别为HTML5标签，然后用DOM节点对其进行替换。
2. 解决方法
	(1)  通过动态创建html5新标签：
	```
	document.creatElement(tagName);
	```
 	(2)通过JS解决
 	
 	a.使用html5shim：
 	在<head\>中调用以下代码：
	```
	<!--[if lt IE 9]>
	<script> src="http://html5shim.googlecode.com/svn/trunk/html5.js</script>
	<![endif]-->
	```
	b.使用kill IE6

	在</body\>之前调用以下代码：
	```
	<!--if lte IE 6]>
	<script src="http://letskillie6.googlecode.com/svn/trunk/letskillie6.zh_CN.pack.js"></script> 
	<![endif]-->
	```
## 6.行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？
定义：CSS 规范规定，每个元素都有 display 属性，确定该元素的类型，每个元素都有默认的 display 值，如 div 的 display 默认值为“block”，则为“块级”元素；span 默认 display 属性值为“inline”，是“行内”元素。

- 行内元素有：a b span img input select strong（强调的语气）
- 块级元素有：div ul ol li dl dt dd h1 h2 h3 h4…p
- 空元素：
	* 常见: br hr img input link meta
	* 不常见: area base col command embed keygen param source track wbr
	
不同浏览器（版本）、HTML4（5）、CSS2 等实际略有差异 参考:<http://stackoverflow.com/questions/6867254/browsers-default-css-for-html-elements>

## 7.html5哪些标签可以做SEO优化

title、meta、header、footer、nav、article、[aside](https://www.w3school.com.cn/html5/html5_aside.asp)
## 8.src和href的区别
- src是指向外部资源的位置，指向的内容会嵌入到文档中当前标签所在的位置，在请求src资源时会将其指向的资源下载并应用到文档内，如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，知道将该资源加载、编译、执行完毕，所以一般js脚本会放在底部而不是头部。

- href是指网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。
## 9. 渐进增强和优雅降级
- 渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能，达到更好的用户体验。
- 优雅降级：一开始就构建完整的功能，然后再针对低版本的浏览器进行兼容。 	
 			
## 10.页面导入样式时，使用 link 和@import 有什么区别？
- link 属于 XHTML 标签，除了加载 CSS 外，还能用于定义 RSS, 定义 rel 连接属性等作用；而@import 是 CSS 提供的，只能用于加载 CSS;
- 页面被加载的时，link 会同时被加载，而@import 引用的 CSS 会等到页面被加载完再加载;
- import 是 CSS2.1 提出的，只在 IE5 以上才能被识别，而 link 是 XHTML 标签，无兼容问题;
- link 支持使用 js 控制 DOM 去改变样式，而@import 不支持;
## 11.em 与 i 的区别
- 都表示斜体
- em是语义化的标签
- i是样式标签
## 12.哪些元素可以自闭合？ 
表单元素input、img、hr、br、mate、link
## 13.渐进增强和优雅降级
- ==渐进增强==：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能，达到更好的用户体验。
- ==优雅降级==：一开始就构建完整的功能，然后再针对低版本的浏览器进行兼容。	
## 14.defer和async的区别
- *defer*要等到整个页面在内存中正常渲染结束（DOM结构完全生成，以及其他脚本执行完成），才会执行。多个defer脚本会按照它们在页面出现的顺序加载。==“渲染完再执行”==
- *async*一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。多个async脚本是不能保证加载顺序的。==“下载完就执行”==
- 可以参考:<https://juejin.im/entry/5a7ad55ef265da4e81238da9>
## 15.html 中 title 属性和 alt 属性的区别？
-  含义不同：
img标签alt属性是当图片不存在时或加载失败时的替代文字（进行显示）；img标签title属性是对图片的描述与进一步说明。
- 在浏览器的表现不同：
在FF、chrome和IE8+中，当鼠标经过图片时title属性的值会显示，而alt属性的值不会显示；只有在IE6、IE7中，如果img标签没有写title属性，而写了alt属性的时候，alt属性值会进行显示；如果img写了title属性和alt属性的时候，只会显示title属性值。 
- 对于网站SEO来说
搜索引擎对图片意思的判断，主要靠alt属性。所以在图片alt属性中以简要文字说明，同时包含关键词，也是页面优化的一部分。条件允许的话，可以在title属性里，进一步对图片说明。
## 16.为什么我们要弃用table标签？
table的缺点在于服务器把代码加载到本地服务器的过程中，本来是加载一行执行一行，但是table标签是里面的东西全都下载完之后才会显示出来，那么如果图片很多的话就会导致网页一直加载不出来，除非所有的图片和内容都加载完。以前的手机网速慢，厂家重视内容的展现而不是样式的展现，所以那个时候用table，而现在网速很快，大家都重视用户体验，当我们浏览淘宝店铺的时候，如果要等到所有的图片全都加载完之后才显示出来的话那也太蠢了，所以table标签现在我们基本放弃使用了。
原文：<https://blog.csdn.net/qq_37746973/article/details/80679242>
## 17.请描述一下 cookies，sessionStorage 和 localStorage 的区别？
- cookie 是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）
- cookie 数据始终在同源的 http 请求中携带（即使不需要），记会在浏览器和服务器间来回传递。
- sessionStorage 和 localStorage 不会自动把数据发给服务器，仅在本地保存。
- 存储大小：
	- cookie 数据大小不能超过 4k。
	- sessionStorage 和 localStorage 虽然也有存储大小的限制，但比 cookie 大得多，可以达到 5M 或更大。
- 有效期（生命周期）：
	- localStorage: 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
	- sessionStorage: 数据在当前浏览器窗口关闭后自动删除。
	- cookie: 设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭
- 共享
	- sessionStorage不能共享，localStorage在同源文档之间共享，
	- cookie在同源且符合path规则的文档之间共享
详细可以参考:<https://blog.csdn.net/you23hai45/article/details/49052251>
## 18.HTML5全局属性
- [请点击此处](https://www.w3school.com.cn/tags/html_ref_standardattributes.asp)
## 19.HTML5 的 form 如何关闭自动补全功能？
- 给不想要提示的 form 或某个 input 设置为 autocomplete=off。
- form标签的其他新属性：<https://www.w3school.com.cn/tags/tag_form.asp>
- form表单提交的注意事项：<https://blog.csdn.net/lucky541788/article/details/81835064>
## 20.title 与 h1 的区别、b 与 strong 的区别、i 与 em 的区别？
- title 属性没有明确意义只表示是个标题，H1 则表示层次明确的标题，对页面信息的抓取也有很大的影响；
- <font color=red>strong</font> 是标明重点内容，有语气加强的含义，使用阅读设备阅读网络时：strong 会重读，而 b 是展示强调内容。
- i 内容展示为斜体，em 表示强调的文本；
- Physical Style Elements -- 自然样式标签
b, i, u, s, [pre](https://www.cnblogs.com/wengxuesong/p/5541924.html)

- Semantic Style Elements -- 语义样式标签
strong, em, ins, del, code

应该准确使用语义样式标签, 但不能滥用, 如果不能确定时首选使用自然样式标签。
## 21.Label 的作用是什么？是怎么用的？
- 作用：label 标签来定义表单控制间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。
-  [lable标签的使用](https://blog.csdn.net/gnail_oug/article/details/72852150)
## 22.怎样自定义redio、checkbox、select的样式

主要应用了lable标签和伪元素

```html
 <label>
      <input type="checkbox"  id="cb">
      <i></i>
 </label>
```

```css
 /*css部分*/
 #cb {
   display: none;
}
 #cb + i {
    /* content: ' '; */
	font-style: normal;
	display: inline-block;
	width: 20px;
	height: 20px;
	background-color: grey;
	border-radius: 50%;
}
				
#cb:checked + i{
   background-color: hotpink;
 }
#cb:checked + i::after {
    content: ' ';
    display: inline-block;
	margin: 5px;
	width: 10px;
	height: 10px;
	background-color: #ffffff;
	border-radius: 50%;
}
```
## 23.关于iframe以及它有哪些缺点？
- iframe的使用方法：
```html
<iframe src="要引入的文件路径" frameborder="0"></iframe>
```
- 缺点
	- iframe 会阻塞主页面的 Onload 事件；
	- 搜索引擎的检索程序无法解读这种页面，不利于 SEO;
	- iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
	
使用 iframe 之前需要考虑这两个缺点。如果需要使用 iframe，最好是通过 javascript动态给 iframe 添加 src 属性值，这样可以绕开以上两个问题。
## 24.实现不使用 border 画出 1px 高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果。
```html
<div style="height:1px;overflow:hidden;background:red"></div>
```
## 25.相对路径，绝对路径，物理路径，根目录
- 物理路径：它就是指硬盘上文件的路径，比如下面的文件位置表示方法：
<font color=hotpink>    d:\wwwroot\html\a.html
       d:\wwwroot\html\photo\b.html
       d:\wwwroot\html\photo\c.html
       d:\wwwroot\html\photo\ours\d.html</font>
- 相对路径：以引用文件之网页所在位置为参考基础，而建立出的目录路径。因此，当保存于不同目录的网页引用同一个文件时，所使用的路径将不相同，故称之为相对路径。

	1. 图像文件和HTML文件位于同一文件夹：只需输入图像文件的名称即可，如&lt;img src="logo.gif" /&gt;。
	2. 图像文件位于HTML文件的下一级文件夹：输入文件夹名和文件名，之间用“/”隔开，如&lt;img src="img/img01/logo.gif" /&gt;。
	3. 图像文件位于HTML文件的上一级文件夹：在文件名之前加入“../” ，如果是上两级，则需要使用 “../ ../”，以此类推，如&lt;img src="../logo.gif" /&gt;。
- 绝对路径：它就是带有网址的路径。比如你有一个域名www.cc.com，其域名指向d:\wwwroot，如：
<font color=hotpink> https://www.cc.com/cc.html</font>
- 网站根目录：去掉绝对路径前面的域名就是根目录，所以它可以理解为是网站的最上层目录。它的表示方法如下：
<font color=hotpink> /cc.html</font>

<font color=red>tips:·使用根目录和绝对路径的好处是表示路径比较简单，都是从网站的最上策目录里查找，一级一级的向下查。缺点是程序不容易移植(比如把网站做为另一个网站的一个栏目，移动到一个新的文件夹中就不行了。</font>
## 26.Link 标签 rel="Stylesheet"?
Link标签有两个作用：1. 定义文档与外部资源的关系；2. 是链接样式表。

下面是链接外部样式表
```html
<head>
<link rel="stylesheet" type="text/css" href="theme.css" />
</head>
```
*href* 为 URL地址；

*type*为链接文件的格式；

*rel*  该属性规定当前文档与被链接文档之间的关系。但是，只有 rel 属性的 "stylesheet" 值得到了所有浏览器的支持。其他值只得到了部分地支持。
参考链接：<https://www.w3school.com.cn/tags/tag_link.asp>
## 27.HTML5-dom扩展
-  获取元素
~~~javascript
document.getElementsByClassName ('class'); 
//通过类名获取元素，以伪数组形式存在。

document.querySelector('selector');
//通过CSS选择器获取元素，符合匹配条件的第1个元素。

document.querySelectorAll('selector'); 
//通过CSS选择器获取元素，以伪数组形式存在。
~~~

- 类名操作

~~~javascript
Node.classList.add('class'); 
//添加class

Node.classList.remove('class'); 
//移除class

Node.classList.toggle('class'); 
//切换class，有则移除，无则添加

Node.classList.contains('class'); 
//检测是否存在class
~~~

- 自定义属性

> 在HTML5中我们可以自定义属性，其格式如下data-*=""

~~~html

<div id="demo" data-my-name="itcast" data-age="10">
<script>
/*
  Node.dataset是以对象形式存在的，当我们为同一个DOM节点指定了多个自定义属性时，
  Node.dataset则存储了所有的自定义属性的值。
  */
var demo = document.querySelector(反馈);
//获取
//注：当我们如下格式设置时，则需要以驼峰格式才能正确获取
var name = demo.dataset['myName'];
var age = demo.dataset['age'];
//设置
demo.dataset['name'] = 'web developer';
<script/>
~~~
## 28.HTML5新增的API
[详细点击此处](https://blog.csdn.net/litcangosh/article/details/102724426)
## 29.浏览器是怎么对 HTML5 的离线储存资源进行管理和加载的呢？
- 在线的情况下，浏览器发现 html 头部有 manifest 属性，它会请求 manifest 文件，如果是第一次访问 app，那么浏览器就会根据 manifest 文件的内容下载相应的资源并且进行离线存储。如果已经访问过 app 并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的 manifest 文件与旧的 manifest 文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
- 离线的情况下，浏览器就直接使用离线存储的资源。

在离线状态时，操作 window.applicationCache 进行需求实现。
参考链接：[HTML5 离线缓存-manifest简介](https://yanhaijing.com/html/2014/12/28/html5-manifest/)

## 30.谈谈你对WEB标准的理解
- web标准的构成
 Web标准不是某一个标准，而是由W3C和其他标准化组织制定的一系列标准的集合。
主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面。
~~~
结构标准：结构用于对网页元素进行整理和分类，咱们主要学的是HTML。 最重要
表现标准：表现用于设置网页元素的版式、颜色、大小等外观样式，主要指的是CSS。
行为标准：行为是指网页模型的定义及交互的编写，咱们主要学的是 Javascript
~~~
- web标准的好处
*1*、让Web的发展前景更广阔 
*2*、内容能被更广泛的设备访问
*3*、更容易被搜寻引擎搜索
*4*、降低网站流量费用
*5*、使网站更易于维护
*6*、提高页面浏览速度

## 31.替换元素和非替换元素
- 替换元素：
可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。
~~~
例如浏览器会根据<img>标签的src属性的值来读取图片信息并显示出来，而如果查看(x)html代码，则看不到图片的实际内容；又例如根据<input>标签的type属性来决定是显示输入框，还是单选按钮等。
~~~
`(x)html`中的`<img>`、`<input>`、`<textarea>`、`<select>`、`<object>`都是替换元素。这些元素往往没有实际的内容，即是一个`空元素`。

## 32.Html5的离线缓存怎么使用，工作原理是什么？

- 使用：

```html
<html lang="en" manifest="./study.appcache">
```

```
CACHE MANIFEST

CACHE:

#此部分写需要缓存的资源 （#是注释的意思）

./images/img1.jpg
./images/img2.jpg
./images/img3.jpg
./images/img4.jpg


NETWORK:

#此部分要写需要有网络才可访问的资源，无网络刚不访问

./js/main.js

*

FALLBACK:

#当访问不到某个资源的情况下，自动由另一个资源替换

./css/online.css ./css/offline.css

./online.html ./offline.html

```
参考:[Html5离线缓存使用](https://blog.csdn.net/litcangosh/article/details/102724426)

- 工作原理：

HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。

- 缺点

  - 更新的资源，需要二次刷新才会被页面采用
  - 不支持增量更新，只有manifest发生变化，所有资源全部重新下载一次
  - 缺乏足够容错机制，当清单中任意资源文件出现加载异常，都会导致整个manifest策略运行异常

## 33.如何实现浏览器内多个标签页之间的通信？
  参考链接：[实现浏览器内多个标签页之间的通信](https://blog.csdn.net/lxcao/article/details/52777066)

## 34.网页验证码是干嘛的，是为了解决什么问题？

区分用户是计算机还是人的公共全自动程序。可以防止恶意破解密码、刷票、
论坛灌水;有效防止黑客对某一个特定注册用户用特定程序暴力破解方式进行
不断的登陆尝试;