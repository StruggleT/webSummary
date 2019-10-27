## 1.CSS 的解析顺序
```
css 选择器匹配元素是逆向解析
```
- 因为所有样式规则可能数量很大，而且绝大多数不会匹配到当前的 DOM 元素（因为数量很大所以一般会建立规则索引树），所以有一个快速的方法来判断「这个 selector 不匹配当前元素」就是极其重要的。
- 如果正向解析，例如「div div p em」，我们首先就要检查当前元素到 html 的整条路径，找到最上层的 div，再往下找，如果遇到不匹配就必须回到最上层那个 div，往下再去匹配选择器中的第一个 div，回溯若干次才能确定匹配与否，效率很低。
- 逆向匹配则不同，如果当前的 DOM 元素是 div，而不是 selector 最后的 em，那只要一步就能排除。只有在匹配时，才会不断向上找父节点进行验证。

`所以为了减少查找时间，尽量不要直接使用标签选择器。`
## 2.红色区域的大小是多少？
```css
.box {
    width: 200px;
    height: 200px;
    padding: 20px;
    margin: 20px;
    background: red;
    border: 20px solid yellow;
    box-sizing: border-box;
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027210958327.png)

答案是120px+(20*2)px=160px
## 3.水平垂直居中
- [16种水平居中垂直居中的方法](https://juejin.im/post/58f818bbb123db006233ab2a)

## 4.如何实现一个最大的正方形
-  用` padding-bottom `撑开边距就可以了。

```css
 section {
    width:100%;
    padding-bottom: 100%;
    background: #333;
}
```

## 5.css 如何开启 gpu 加速
- 请参考网易云社区的文章:[CSS动画的性能分析和浏览器GPU加速](https://juejin.im/post/5bd947326fb9a0226924ad77#heading-2)

## 6.position的值， relative和absolute分别是相对于谁进行定位的？
- absolute :生成绝对定位的元素， 相对于最近一级的 定位不是 static 的父元素来进行定位。

-  fixed （老IE不支持）生成绝对定位的元素，通常相对于浏览器窗口或 frame 进行定位。

- relative 生成相对定位的元素，相对于其在普通流中的位置进行定位。

- static 默认值。没有定位，元素出现在正常的流中

- sticky 生成粘性定位的元素，容器的位置根据正常文档流计算得出

## 7.CSS中link 和@import的区别是？
- link属于HTML标签，而@import是CSS提供的;

-  页面被加载的时，link会同时被加载，而@import被引用的CSS会等到引用它的CSS文件被加载完再加载;

-  import只在IE5以上才能识别，而link是HTML标签，无兼容问题;

- link方式的样式的权重 高于@import的权重.

## 8.行高的构成
- 行高是由 line-box 组成的
- line-box 是由一行里的 inline-box 组成的
- inline-box中最高的那个，或字体最大的拿个决定行高

## 9.inline-block的间隙形成原因及如何解决
两个并列的inline-block中间会有一条裂缝，这个的原因是两个标签之间有空格，浏览器把这些空格当成文字中空格，所以这两个块中间多少有间隙。

解决办法：

- 删除两个标签间的空格，但是这样html排版不好
- 容器元素font-size: 0 然后再在里面再重新设置字体大小

## 10.边框图片的实现？
```css
        .box{
            width: 400px;
            height: 150px;
            border: 20px solid #ccc;
            margin-bottom: 30px;
        }

        .box:first-child{
            /*border-image: url("images/border01.jpg") 167/20px round;*/
            /*1.在内容变化的容器可以使用，边框自动填充*/
            /*2.用法：*/
            /*2.1 图片资源*/
            border-image-source: url("images/border01.jpg");
            /*2.2 切割的尺寸 默认的单位px 而且不能使用小数*/
            /*2.2.1 切割的位置距离对应的边的距离  切了四刀   4个切割的尺寸*/
            border-image-slice: 167;/*167 167 167 167*/
            /*2.3 边框的宽度*/
            border-image-width: 20px;
            /*2.4 平铺的方式  三种平铺方式 round stretch repeat*/
            /*round 环绕 完整的自适应（等比缩放）平铺在边框内*/
            /*stretch 拉伸 拉伸显示在边框内容 变形的*/
            /*repeat 平铺 从边框的中间向两侧平铺 自适应平铺但是不是完整的*/
            border-image-repeat: round;

        }
        .box:nth-child(2){
            border-image: url("images/border01.jpg") 167/20px stretch;
        }
        .box:last-child{
            border-image: url("images/border01.jpg") 167/20px repeat;
        }
```

```html
    <div class="box"></div>
    <div class="box"></div>
    <div class="box"></div>
```
实现效果图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027213715881.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)

## 11.CSS Hack
在一部分不合法，但是在某些浏览器上生效的写法就叫CSS Hack，一般用来兼容老的浏览器， 缺点是难理解、难维护、易失效

替代方案：

- 特征检测
- 针对性的加class
	- 比如第一步检测是IE6，那么只需要添加一个专门的 class 名来兼容IE6就好

写Hack时需要注意
- 标准属性写在前面， hack代码写在后面

## 12.单行文本溢出显示省略号
```css
overflow: hidden;
text-overflow: ellipsis;
white-space: no-wrap;
```
## 13.display: none; 与 visibility: hidden; 的区别?
==结构：==

- display:none

	- 会让元素完全从渲染树中消失，渲染的时候不占据任何空间, 不能点击，
- visibility: hidden
	- 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，不能点击
- opacity: 0
	- 不会让元素从渲染树消失，渲染元素继续占据空间，只是内容不可见，可以点击
	
==继承:==

- display: none和opacity: 

	- 非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示。
	
- visibility: hidden
	- 继承属性，子孙节点消失由于继承了hidden，通过设置visibility: visible;可以让子孙节点显式。

==性能:==

- display:none
	- 修改元素会造成文档回流。读屏器不会读取display: none元素内容，性能消耗较大
- visibility:hidden
	- 修改元素只会造成本元素的重绘,性能消耗较少。读屏器读取visibility: - - hidden元素内容
- opacity: 0
	- 修改元素会造成重绘，性能消耗较少

## 14.CSS单位
- px 绝对单位。传统上一个像素对应于计算机屏幕上的一个点，而对于高清屏则对应更多。

- % 父元素宽度的比例。

	- 如果对 html 元素设置 font-size 为百分比值，则是以浏览器默认的字体大小16px为参照计算的（所有浏览器的默认字体大小都为 16px），如62.5%即等于10px（62.5% * 16px = 10px）。
	
- em 相对单位。 不同的属性有不同的参照值。

	- 对于字体大小属性（font-size）来说，em 的计算方式是相对于父元素的字体大小
	- border, width, height, padding, margin, line-height）在这些属性中，使用em单位的计算方式是参照该元素的 font-size，1em 等于该元素设置的字体大小。同理如果该元素没有设置，则一直向父级元素查找，直到找到，如果都没有设置大小，则使用浏览器默认的字体大小。
	
- rem 是相对于根元素 html 的 font-size 来计算的，所以其参照物是固定的。

	- 好处：rem 只需要修改 html 的 font-size 值即可达到全部的修改，即所谓的牵一发而动全身。
	
- vw, vh, vmin, vmax 相对单位，是基于视窗大小（浏览器用来显示内容的区域大小）来计算的。

	- vw：基于视窗的宽度计算，1vw 等于视窗宽度的百分之一
	- vh：基于视窗的高度计算，1vh 等于视窗高度的百分之一
	- vmin：基于vw和vh中的最小值来计算，1vmin 等于最小值的百分之一
	- vmax：基于vw和vh中的最大值来计算，1vmax 等于最大值的百分之一

## 15.CSS 优化、提高性能的方法有哪些？
- 多个 css 合并，尽量减少 HTTP 请求
- css 雪碧图
- 抽象提取公共样式，减少代码量
- 选择器优化嵌套，尽量避免层级过深 （用‘>’替换‘ ’）
- 属性值为 0 时，不加单位
- 压缩CSS代码
- 避免使用[ CSS 表达式](http://www.divcss5.com/css3-style/c50224.shtml)
	- 它们要计算成千上万次并且可能会对你页面的性能产生影响。

## 16.CSS 有哪些继承属性?
- 关于文字排版的属性如：
	- font
	- word-break
	- letter-spacing
	- text-align
	- text-rendering
	- word-spacing
	- white-space
	- text-indent
	- text-transform
	- text-shadow
- line-height
- color
- visibility
- cursor

## 17.li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？(也称幽灵字符)
行框的排列会受到中间空白（回车\空格）等的影响，因为空格也属于字符, 这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为 0，就没有空格了

## 18.什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的 IE？
- 响应式设计就是网站能够兼容多个不同大小的终端，而不是为每个终端做一个特定的版本
- 基本原理是利用 CSS3 媒体查询，为不同尺寸的设备适配不同样式
- 对于低版本的 IE，可采用 JS 获取屏幕宽度，然后通过监听window.onresize 方法来实现兼容

## 19.请列举几种隐藏元素的方法
- visibility: hidden; 这个属性只是简单的隐藏某个元素，但是元素占用的空间任然存在
- opacity: 0; CSS3 属性，设置 0 可以使一个元素完全透明
- position: absolute; 设置一个很大的 left 负值定位，使元素定位在可见区域之外
- display: none; 元素会变得不可见，并且不会再占用文档的空间。
- transform: scale(0); 将一个元素设置为缩放无限小，元素将不可见，元素原来所在的位置将被保留
- <div hidden="hidden"> HTML5 属性,效果和 display:none;相同，但这个属性用于记录一个元素的状态
- height: 0; 将元素高度设为 0 ，并消除边框
- filter: blur(0); CSS3 属性，将一个元素的模糊度设置为 0

## 20.请解释 CSS sprites，以及你要如何在页面或网站中实现它
- CSS Sprites 其实就是把网页中一些背景图片整合到一张图片文件中，再利用 CSS 的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position 可以用数字能精确的定位出背景图片的位置。
- CSS Sprites 为一些大型的网站节约了带宽，让提高了用户的加载速度和用户体验，不需要加载更多的图片。

## 21.meta viewport 是做什么用的，怎么写？

```html
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```
控制页面在移动端不要缩小显示。

## 22.字体图标
图片是有诸多优点的，但是缺点很明显，比如图片不但增加了总文件的大小，还增加了很多额外的"http请求"，这都会大大降低网页的性能的。更重要的是图片不能很好的进行“缩放”，因为图片放大和缩小会失真。 学习移动端响应式，很多情况下希望我们的图标是可以缩放的。此时，一个非常重要的技术出现了，这就是字体图标（iconfont)。

`如何使用`

1. 上传生成字体包

   当UI设计人员给我们svg文件的时候，我们需要转换成我们页面能使用的字体文件， 而且需要生成的是兼容性的适合各个浏览器的。

​    推荐网站： <http://icomoon.io>

2. 下载兼容字体包
3. 字体引入到HTML
首先把以下4个文件放入到 fonts文件夹里面。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191027221323956.png)
	1. 第一步：在样式里面声明字体： 告诉别人我们自己定义的字体

```css
	  @font-face {
     font-family: 'icomoon';
     src:  url('fonts/icomoon.eot?7kkyc2');
     src:  url('fonts/icomoon.eot?7kkyc2#iefix') format('embedded-opentype'),
       url('fonts/icomoon.ttf?7kkyc2') format('truetype'),
       url('fonts/icomoon.woff?7kkyc2') format('woff'),
       url('fonts/icomoon.svg?7kkyc2#icomoon') format('svg');
     font-weight: normal;
     font-style: normal;
   }
```
	2. 第二步：给盒子使用字体
```css
	span {
   		font-family: "icomoon";
   	}
```
	3. 第三步：盒子里面添加结构
```css
	span::before {
   		 content: "\e900";
   	}
   或者  
   <span></span>  
```