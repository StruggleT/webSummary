# CSS
 Cascading Style Sheet 层叠样式表

---
## TODO:

> 1. CSS各种选择器
> 2. CSS三种显示模式
> 3. CSS背景属性
> 4. CSS三大特性
> 5. CSS盒子模型
> 6. CSS浮动
> 7. CSS定位
> 9. CSS3的新特性

---
## css选择器
- 基础选择器

| 序号		| 选择器		| 名称	| 说明	|css版本 |
|-----------|----------|  -------|-------------|-----------|
|1|	*|	通用选择器|	选择所有元素，包括html和body|	2|
|2|	div,span|	标签选择器|	根据标签选择元素	|1|
|3|	#	|id选择器|	选择指定id元素	|1|
|4	|`.`	|类选择器	|选择指定class|	1|
|5	|[attr]|	属性选择器|	根据元素属性去选择|	2-3|

属性选择器的几种用法
```css
[href] {color: red;}

[type="password"] {color: red;}

[href^="http"] {color: red;}

[href$=".cn"] {color: red;}

[href*="baidu"] {color: red;}

[class~="def"] {color: red;}/*属性值具有多值时，使用如<p class="abc def"></p>*/

[lang|="en"] {color: red;}/*属性中有'-'时使用，如<p lang="en-us"></p>*/
```
- 复合选择器

|序号	|选择器	|名称	|说明	|css版本|
|------------|------------|---------|-----------|------------|
|1|	s1,s2,s3	|分组选择器	|选择多个选择器的元素	|1|
|2	|s1 s2	|后代选择器|	指定选择器的后代元素	|1|
|3	|s1 > s2|	子选择器|	指定选择器的子元素|	1|
|4	|s1+s2	|相邻兄弟选择器	|选择相邻且之后的元素	|1|
|5	|s1~s2	|兄弟选择器|	选择之后的元素|	2-3|

参考链接:[你知道哪些复合选择器？](https://segmentfault.com/a/1190000017534489)

- 伪类选择器

|序号	|选择器	|名称	|说明	|css版本|
|------------|------------|---------|-----------|------------|
|1	|::first-line	|伪元素选择器	|块级首行	|1|
|2	|::first-letter	|伪元素选择器	|块级首字母	|1|
|3	|::before	|伪元素选择器	|选择元素之前插入内容	|2|
|4	|::after	|伪元素选择器	|选择元素之后插入内容	|2|
|5	|::selection	|伪元素选择器	|光标滑动选择内容	|2|

- 伪类选择器之结构性伪类选择器

|序号	|选择器	|名称|	说明|	css版本|
|------------|------------|---------|-----------|------------|
|1	|:root	|根元素选择器	|文档根元素，一般为html|	3|
|2	|:first-child	|子元素选择器	|第一个子元素	|2|
|3	|:last-child	|子元素选择器	|最后一个子元素	2|2|
|5	|:only-of-type	|子元素选择器	|子元素只有一种类型的|	1|
|6	|:nth-child(n)	|子元素选择器	|第n个子元素	|2|

```css
ul > li:first-child{ /*li且是第一个子元素的li元素*/
    color:red;
}
ul > li:last-child{/*li且是最后一个元素的li元素*/
    color: blue;
}
span:only-child{/*span且在它父元素下是唯一的span元素；建议把父元素写出来*/
    color: green;
}
span:only-of-type{/*span且在它父元素下是唯一类型的span元素；建议把父元素写出来*/
    color:green;
};
```
-  伪类选择器之UI选择器(input标签用)

|序号	|选择器	|名称|	说明|	css版本|
|------------|------------|---------|-----------|------------|
|1|:enabled	|表单元素选择器	|input非disabled时|2|
|2|:disable	|表单元素选择器	|input标签disabled时|1|
|3|:checked	|表单元素选择器	|input标签checked时|2|
|4|:default	|表单元素选择器	|选择元素之后插入内容|2|
|5|:valid	|表单元素选择器	|选择元素之后插入内容|2|
|6|:invalid	|表单元素选择器	|块级首字母|1|
|7|:required	|表单元素选择器	|选择元素之前插入内容|2|
|8|:optional	|表单元素选择器	|选择元素之后插入内容|2|
- 伪类选择器之动态伪类

|序号	|选择器	|名称|	说明|	css版本|
|-------|------------|---------|-----------|------------|
|1|:link|动态伪类选择器|未被访问时|2|
|2|:visited|动态伪类选择器|已被访问时|1|
|3|:hover|动态伪类选择器|鼠标以上时|2|
|4|:active|动态伪类选择器|访问中跳转页面时|2|
|5|:focus|动态伪类选择器|获得焦点时|2|

link/visited/hover/active是有顺序的，其他顺序可能无效，这是个坑。
focus用在input获取焦点时使用。

## CSS三种显示模式
-  块级元素(block-level)

每个块元素通常都会独自占据一整行或多整行，可以对其设置宽度、高度、对齐等属性，常用于网页布局和网页结构的搭建。

```
	常见的块元素有<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>等，其中<div>标签是最典型的块元素。 
```
	- 块级元素的特点：
	
（1）总是从新行开始

（2）高度，行高、外边距以及内边距都可以控制。

（3）宽度默认是容器的100%

（4）可以容纳内联元素和其他块元素。

- 行内元素(inline-level)

行内元素（内联元素）不占有独立的区域，仅仅靠自身的字体大小和图像尺寸来支撑结构，一般不可以设置宽度、高度、对齐等属性，常用于控制页面中文本的样式。

```
	常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中<span>标签最典型的行内元素。
```
	- 行内元素的特点：

（1）和相邻行内元素在一行上。

（2）高、宽无效，但水平方向的padding和margin可以设置，垂直方向的无效。

（3）默认宽度就是它本身内容的宽度。

（4）行内元素只能容纳文本或则其他行内元素。（a特殊 a里面可以放块级元素 ）

- 行内块元素（inline-block）

在行内元素中有几个特殊的标签——img、input 、td，可以对它们设置宽高和对齐属性。
	- 行内块元素的特点：

（1）和相邻行内元素（行内块）在一行上,但是之间会有空白缝隙。

（2）默认宽度就是它本身内容的宽度。

（3）高度，行高、外边距以及内边距都可以控制。

## CSS三大特性

- 层叠性

所谓层叠性是指多种CSS样式的叠加。
是浏览器处理冲突的一个能力,如果一个属性通过两个相同选择器设置到同一个元素上，那么这个时候一个属性就会将另一个属性层叠掉
比如先给某个标签指定了内部文字颜色为红色，接着又指定了颜色为蓝色，此时出现一个标签指定了相同样式不同值的情况，这就是样式冲突。  就近原则
一般情况下，如果出现样式冲突，则会按照CSS书写的顺序，以最后的样式为准。

* 继承性

所谓继承性是指书写CSS样式表时，子标签会继承父标签的某些样式，如文本颜色和字号。想要设置一个可继承的属性，只需将它应用于父元素即可。简单的说就是`子承父业`。

参考链接:[继承和层叠性](https://www.jianshu.com/p/36e65575225b)

* CSS优先级

定义CSS样式时，经常出现两个或更多规则应用在同一元素上，这时就会出现优先级的问题。
在考虑权重时，还需要注意一些特殊的情况，具体如下：

```
	继承样式的权重为0。即在嵌套结构中，不管父元素样式的权重多大，被子元素继	承时，他的权重都为0，也就是说子元素定义的样式会覆盖继承来的样式。

	行内样式优先。应用style属性的元素，其行内样式的权重非常高，可以理解为远大于100。总之，他拥有比上面提高的选择器都大的优先级。

	权重相同时，CSS遵循就近原则。也就是说靠近元素的样式具有最大的优先级，或者说排在最后的样式优先级最大。

	CSS定义了一个!important命令，该命令被赋予最大的优先级。也就是说不管权重如何以及样式位置的远近，!important都具有最大优先级。
```
	*	css特殊性（Specificity）
关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity，我们称为CSS 特性或称非凡性，它是一个衡量CSS值优先级的一个标准 具体规范入如下：

specificity用一个四位的数 字串(CSS2是三位)来表示，更像四个级别，值从左到右，左面的最大，一级大于一级，数位之间没有进制，级别之间不可超越。 

| 继承或者* 的贡献值           | 0,0,0,0 |
| -------------------- | ------- |
| 每个元素（标签）贡献值为         | 0,0,0,1 |
| 每个类，伪类贡献值为           | 0,0,1,0 |
| 每个ID贡献值为             | 0,1,0,0 |
| 每个行内样式贡献值            | 1,0,0,0 |
| 每个!important贡献值  重要的 | ∞ 无穷大   |


权重是可以叠加的
比如的例子：

```
		div ul  li   ------>      0,0,0,3

		.nav ul li   ------>      0,0,1,2

		a:hover      -----—>      0,0,1,1

		.nav a       ------>      0,0,1,1   

		#nav p       ----->       0,1,0,1
```

* 优先级总结
1. 使用了 !important声明的规则。
2. 内嵌在 HTML 元素的 style属性里面的声明。
3. 使用了 ID 选择器的规则。
4. 使用了类选择器、属性选择器、伪元素和伪类选择器的规则。
5. 使用了元素选择器的规则。
6. 只包含一个通用选择器的规则。
7. 同一类选择器则遵循就近原则。
## CSS背景属性
|属性	|描述	|CSS|
|----|----|-----|
|[background](https://www.w3school.com.cn/cssref/pr_background.asp)	|在一个声明中设置所有的背景属性。|	1|
|[background-attachment](https://www.w3school.com.cn/cssref/pr_background-attachment.asp)	|设置背景图像是否固定或者随着页面的其余部分滚动。	|1|
|[background-color](https://www.w3school.com.cn/cssref/pr_background-color.asp)	|设置元素的背景颜色。	|1|
|[background-image](https://www.w3school.com.cn/cssref/pr_background-image.asp)	|设置元素的背景图像。	|1|
|[background-position](https://www.w3school.com.cn/cssref/pr_background-position.asp)	|设置背景图像的开始位置。	|1|
|[background-repeat](https://www.w3school.com.cn/cssref/pr_background-repeat.asp)	|设置是否及如何重复背景图像。	|1
|[background-clip](https://www.w3school.com.cn/cssref/pr_background-clip.asp)	|规定背景的绘制区域。	|3
|[background-origin](https://www.w3school.com.cn/cssref/pr_background-origin.asp)	|规定背景图片的定位区域。	|3|
|[background-size](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)	|规定背景图片的尺寸。	|3|
## CSS盒模型
盒模型有两种， IE 怪异盒子模型（border box）、W3C标准盒子模型(content box)；

盒模型是由： 内容(content)、内边距(padding)、边框(border)、外边距(margin) 组成的。

标准模型的宽高是指的content区宽高； IE盒模型的宽高是指的content+padding+border的宽高。
```css
 .box{
       width: 200px;
       height: 200px;
       background-color: red;
       border: 20px solid yellow;
       box-sizing: content-box;
       margin: 0;
    }
```
- IE盒模型如图：

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025094632143.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025094044175.png)

 此时的width为200px,包括了内容+padding+border,content内容大小为width-border = 160px

 - 标准盒模型：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025094834944.png)![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025094410959.png)

width就是内容的宽度，注意在浏览器中的渲染的实际宽度将是 240px。

 `Note`: 对于新的web站点，你可能希望首先将box-sizing设置为border-box，如下所示：
 { box-sizing: border-box; }
这使得处理元素大小的工作变得容易得多，并且通常消除了在布局内容时可能遇到的许多陷阱。然而，在某些情况下，你应谨慎使用这个属性。例如： 你正在编写一个将由其他人使用的共享组件库，如果他们网站的其余部分没有设置此值，他们可能会发现很难使用你的组件库。

参考链接：[border-size](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing) 和 [盒模型](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

## 纯CSS实现三角形
- 原理：把div的width和height设置为0，就是把content(内容)区域设置为0，然后设置border的宽度，并让其颜色为transparent(透明)，想获取朝那边三角形,给相反的一边设置颜色，具体代码如下：

```css
.box{
        width: 0;
        height: 0;
        border: 20px transparent solid;
        border-left-color: aqua;
    }
```

实现效果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025104109787.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025125741920.png)

参考链接:<https://blog.csdn.net/qq_34645412/article/details/78062304>

## 图片之间有缝隙的问题

先直接看问题，如图：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025112955910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)

我们发现，不同div之间，上下有空白间隙，不同img之间，左右有间隙，而且，不同浏览器的左右间隙大小不同。

上图代码：

```html
  <div class="box1">
        <img src="1111111.jpg" alt="" width="200" height="200">
        <img src="22222222222.jpg" alt="" width="200" height="200">  
  </div> 
  <div class="box2">
        <img src="4444444.jpg" alt="" width="200" height="200">  
        <img src="781573228.jpg" alt="" width="200" height="200">
  </div>
```
水平方向的缝隙①和③形成原因：在一个div中，每个img标签之间有回车或则空格形成的。

垂直方向的缝隙②和④形成原因：inline-block元素在块级元素中留空隙就是因为图像的默认垂直对齐方式是基线对齐(
基线对齐在原理上相当于图像底边与匿名文本大写英文字母X的底边对齐)；而匿名文本是有行高的，继承父级元素设置的行高，默认为normal(即font-size的1.2倍)，所以X的底边距离行框有一段距离，这段距离就是图像留出的空隙。
于是，解决这个问题有以下几个解决办法

　　1、display:block

　　因为垂直对齐方式只能作用于替换元素和行内元素，更改为块级元素，会使垂直对齐方式失效

　　2、父级的line-height: 0

　　这样使匿名文本与行框的距离为0

　　3、vertical-align: top/middle/bottom

参考链接：[深入理解line-height与vertical-align](https://www.cnblogs.com/xiaohuochai/p/5271217.html)	、[深度剖析Baseline设计原理](https://juejin.im/post/59c9bc196fb9a00a402e0166)、[你可能不知道的vertical-align](https://zhuanlan.zhihu.com/p/52441893)

## CSS浮动
- [什么是浮动](https://www.cnblogs.com/starof/p/4608962.html/)

了解浮动先了解什么是标准流(普通流)？
普通流实际上就是一个网页内标签元素正常从上到下，从左到右排列顺序的意思，比如块级元素会独占一行，行内元素会按顺序依次前后排列；按照这种大前提的布局排列之下绝对不会出现例外的情况叫做普通流布局。

- 浮动的定位方式

浮动让元素脱离普通流，向父容器的左边或右边移动直到碰到包含容器的边【经测试碰到padding即停】或者碰到其他浮动元素。文本和行内元素将环绕浮动元素。

- 浮动的包裹性和破坏性
1. 包裹性
	包裹性指的是元素尺寸刚好容纳内容。
	具有包裹性的其他属性：
	- display:inline-block/table-cell/...
	- position:absolute/fixed/sticky
	- overflow:hidden/scroll
	
	浮动之所以会产生包裹性这样的效果是因为`float属性会改变元素display属性最终的计算值`。
2. 破坏性
这里破坏性是指元素浮动后可能导致父元素高度塌陷。
其他破坏性的属性：
	* display:none
	*  position:absolute/fixed/sticky
	
浮动破坏性原理：
因为浮动元素被从文档正常流中移除了，父元素当然还处在正常流中，所以父元素不能被浮动元素撑大。

- [如何清除浮动](https://www.cnblogs.com/starof/p/4608962.html)

浮动的元素布局时不会占据父元素的布局空间，即父元素布局时不会管浮动元素，[浮动元素有可能超出父元素](https://www.cnblogs.com/lrzw32/p/4948514.html)，从而对其他元素造成影响。

方法一：让父元素变为一个BFC。 父元素 overflow: auto/hidden。 让父元素去关注里面的高度。 必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度。

方法二： 使用伪元素清楚浮动
```css
.clearfix::before,
.clearfix::after{
    content: ".";
    display: block;
    height: 0;
    overflow: hidden;
}
.clearfix:after{
    clear: both;
}
.clearfix {
    zoom: 1; /* IE < 8 */
}
```
参考链接：[清除浮动的四种方式及原理](https://juejin.im/post/59e7190bf265da4307025d91)
## BFC
- [什么是BFC?](https://www.cnblogs.com/libin-1/p/7098468.html)

Formatting context(格式化上下文) 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于上述定位方案的普通流。

- 触发BFC
 只要元素满足下面任一条件即可触发 BFC 特性：
	- body 根元素
	- 浮动元素：float 除 none 以外的值
	- 绝对定位元素：position (absolute、fixed)
	- display 为 inline-block、table-cells、flex
	- overflow 除了 visible 以外的值 (hidden、auto、scroll)
- BFC 特性及应用
1. 同一个 BFC 下外边距会发生折叠
```
	div{
   	width: 100px;
   	height: 100px;
   	background: hotpink;
   	margin: 100px;
	}
<body>
	<div></div>
    <div></div>
</body>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025200346527.png)

从效果上看，因为两个 div 元素都处于同一个 BFC 容器下 (这里指 body 元素) 所以第一个 div 的下边距和第二个 div 的上边距发生了重叠，所以两个盒子之间距离只有 100px，而不是 200px。

首先这不是 CSS 的 bug，我们可以理解为一种规范，如果想要避免外边距的重叠，可以将其放在不同的 BFC 容器中。
```html
<div class="container">
    <p></p>
</div>
<div class="container">
    <p></p>
</div>
```
```css
.container {
    overflow: hidden;
}
p {
    width: 100px;
    height: 100px;
    background: hotpink;
    margin: 100px;
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025203858581.png)

2. BFC 可以包含浮动的元素（清除浮动）

```html
<div style="border: 1px solid red;">
    <div style="width: 100px;height: 100px;background: blue;float: left;"></div>
</div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025201204935.png)

由于容器内元素浮动，脱离了文档流，所以容器只剩下 2px 的边距高度。如果使触发容器的 BFC，那么容器将会包裹着浮动元素。

```html
<div style="border: 1px solid red;overflow: hidden">
    <div style="width: 100px;height: 100px;background: blue;float: left;"></div>
</div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025201301149.png)

3. BFC 可以阻止元素被浮动元素覆盖

先看下元素被覆盖的效果：

```css
.box1 {
		width: 200px;
		height: 100px;
		background-color: pink;
		float: left;
	}
	.box2 {
		width: 400px;
		height: 300px;
		background-color: skyblue;
	}
```
```html
<div class="box1">我是box1，设置了左浮动</div>
<div class="box2">没设置浮动，然后随便打点字，哈哈实话实说撒借酷酷的方式对方是否</div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025202101673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)

这时候其实第二个元素有部分被浮动元素所覆盖，(但是文本信息不会被浮动元素所覆盖) 如果想避免元素被覆盖，可触第二个元素的 BFC 特性，在第二个元素中加入 overflow: hidden，就会变成：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191025202147789.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)

参考链接：[史上最全面、最透彻的BFC原理剖析](https://juejin.im/entry/59c3713a518825396f4f6969)

## CSS定位
- `position:static;`(静态定位)
静态定位是所有元素的默认定位方式，当position属性的取值为static时，可以将元素定位于静态位置。 所谓静态位置就是各个元素在HTML文档流中默认的位置。
- `position:relative;`(相对定位)
相对定位是将元素相对于它在标准流中的位置进行定位，当position属性的取值为relative时，可以将元素定位于相对位置。
对元素设置相对定位后，可以通过边偏移属性改变元素的位置，`但是它在文档流中的位置仍然保留`。

	`tips:` 
	1. 相对定位最重要的一点是，它可以通过边偏移移动位置，但是原来的所占的位置，继续占有。
	2. 其次，每次移动的位置，是以自己的左上角为基点移动（相对于自己来移动位置）
- `position:absolute;`(绝对定位)
 绝对定位最重要的一点是，它可以通过边偏移移动位置，但是它完全脱标，完全不占位置。
 - `position:fixed;`(固定定位)
 当对元素设置固定定位后，它将脱离标准文档流的控制，始终依据浏览器窗口来定义自己的显示位置。不管浏览器滚动条如何滚动也不管浏览器窗口的大小如何变化，该元素都会始终显示在浏览器窗口的固定位置。
## [CSS3的新特性](https://juejin.im/entry/595f1e3c5188250d914dd53c)
- 新增选择器 p:nth-child(n){color: rgba(255, 0, 0, 0.75)}
- 弹性盒模型 display: flex;
- 多列布局 column-count: 5;
- 媒体查询 @media (max-width: 480px) {.box: {column-count: 1;}}
- 个性化字体 @font-face{font-family: BorderWeb; src:url(BORDERW0.eot);}
- 颜色透明度 color: rgba(255, 0, 0, 0.75);
- 圆角 border-radius: 5px;
- 渐变 background:linear-gradient(red, green, blue);
- 阴影 box-shadow:3px 3px 3px rgba(0, 64, 128, 0.3);
- 倒影 box-reflect: below 2px;
- 文字装饰 text-stroke-color: red;
- 文字溢出 text-overflow:ellipsis;
- 背景效果 background-size: 100px 100px;
- 边框效果 border-image:url(bt_blue.png) 0 10;
- 平滑过渡 transition: all .3s ease-in .1s;
- 动画 @keyframes anim-1 {50% {border-radius: 50%;}} animation: anim-1 1s;
- 变形 transform
	- 旋转 transform: rotate(20deg);
	- 倾斜 transform: skew(150deg, -10deg);
	- 位移 transform: translate(20px, 20px);
	- 缩放 transform: scale(.5);
