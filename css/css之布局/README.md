## 1.Flex布局(弹性盒模型)
[Flex 布局教程：语法篇(阮一峰)](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)  
[Flex 布局教程：实例篇(阮一峰)](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

## 2.Grid网格布局
[Grid网格布局教程(阮一峰)](http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)

## 3.圣杯布局和双飞翼布局
- 圣杯布局

html代码中  main部分首先要放在cotent的最前部分。然后是left,right

1. 将三者都 float:left , 再加上一个position:relative (因为相对定位后面会用到）

2. main部分 width:100%占满

3. 此时main占满了，所以要把left拉到最左边，使用margin-left:-100%

4. 这时left拉回来了，但会覆盖middle内容的左端，要把main内容拉出来，所以在外围content加上 padding:0 220px 0 200px

5. main内容拉回来了，但left也跟着过来了，所以要还原，就对left使用相对定位 left:-200px  同理，right也要相对定位还原 right:-220px

6. 到这里大概就自适应好了。如果想content高度保持一致可以给left main right都加上min-height:130px

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191028103344708.png)

代码如下：
```css
        * {
            margin: 0;
            padding: 0;
        }
        body {
            min-width: 700px;
        }
        header,
        footer {
            border: 1px solid #333;
            background: #aaa;
            text-align: center;
        }
        .content {
            padding: 0 220px 0 200px;
        }
        main,.left,.right {
            position: relative;
            float: left;
            min-height: 130px;
        }
        main {
            width: 100%;
            background-color: aqua;
            word-wrap: break-all;
        }
        .left {
            margin-left: -100%;
            left: -200px;
            width: 200px;
            background-color: brown;
        }
        .right {
            margin-left: -220px;
            right: -220px;
            width: 220px;
            background-color: burlywood;
        }
        footer {
            clear: both;
        }
```
```html
 <header>头部</header>
    <div class="content">
        <main>
            <p>kdddddddddddddddd
                dddddddddddddddflsdfl
                fdsfddddddsdd
            </p>
        </main>
        <aside class="left">
            <p> i am left</p>
        </aside>
        <aside class="right">
            <p>i am right</p>
        </aside>
    </div>
    <footer>尾部</footer>
```
- 双飞翼布局
原理：主体元素上设置左右边距，预留两翼位置。左右两栏使用浮动和负边距归位。

1. html代码中，main要放最前边，left right

2. 将main left right 都float:left

3. 将main占满 width:100%

4. 此时main占满了，所以要把left拉到最左边，使用margin-left:-100% 同理 right使用margin-left:-220px。
（这时可以直接继续上边圣杯布局的步骤，也可以有所改动）

5. main内容被覆盖，除了使用外围的padding，还可以考虑使用margin。
给main增加一个内层div-- main-inner, 然后margin:0 220px 0 200px

![在这里插入图片描述](https://img-blog.csdnimg.cn/201910281050522.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)
代码：
```css
      .left,
      .right,
      .main {
        min-height: 200px;
      }
      .left {
        width: 200px;
        background-color: thistle;
      }
      .main {
        background: #999;
      }
      .right {
        width: 300px;
        background-color: violet;
      }
      /* 双飞翼布局重点 */
      .left,
      .main,
      .right {
        float: left;
      }
      .main {
        width: 100%;
      }
      .main-inner {
        margin-left: 200px;
        margin-right: 300px;
      }
      .left {
        margin-left: -100%;
      }
      .right {
        margin-left: -300px;
      }
```
```html
    <div class="main"><div class="main-inner">中心区</div></div>
    <div class="left">left</div>
    <div class="right">right</div>
```
## 4.左右两栏布局
左侧定宽，右侧自适应

- float+magin

```css
.left {
    float: left;
    width: 200px;
    min-height:100px;
    background-color: red;
}
.right {
    margin-left: 200px;
    background-color: blue;
}

```

- float+BFC

BFC不会受到浮动元素的影响
```css
.container{
  width:100%;
}
.float{
  height:200px;
  width:200px;
  background:red;
  opacity:0.3;
  float:left;
}
.main{
  background:green;
  height:200px;
  overflow:hidden;/*触发BFC*/
}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191028135203543.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)



-  Flex实现

```css
    .container{
    display: flex;
    }
    .left{
    width: 200px;
    height:200px;
    background:red;
    opacity:0.3;
    }
    .main{
    flex: 1;
    background:green;
    height:200px;
    }
```
```html
    <div class="container">
        <div class="left">
            <h1>左边固定</h1>
        </div>
        <div class="main"><h1>右边自适应</h1></div>
    </div>
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191028135717910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2xpdGNhbmdvc2g=,size_16,color_FFFFFF,t_70)

- Grid实现

```css
 .container {
        width: 100%;
        display: grid;
        grid-template-columns: 200px 1fr;
    }
    .left{
    height:200px;
    background:red;
    opacity:0.3;
    }
    .main{
    background:green;
    height:200px;
    }
```

参考链接：[两栏自适应布局方案](https://segmentfault.com/a/1190000004424442)、 [七种实现左侧固定，右侧自适应两栏布局的方法](https://zhuqingguang.github.io/2017/08/16/adapting-two-layout/)

## 5.三栏布局
两侧固定，中间自适应

- Flex
```css
 * {
        margin: 0;
        padding: 0;
      }
      .left,
      .right,
      .center {
        min-height: 100px;
      }
      .wrapper {
        display: flex;
      }
      .left{
        background-color: red;
        width: 300px;
      }
      .center {
        background-color: orange;
        flex: 1;
      }
      .right {
        background-color: blue;
        width: 300px;
      }
```
```html
    <div class="wrapper">
      <aside class="left"></aside>
      <main class="center">
        <h1>flex布局</h1>
        <p>中间内容</p>
      </main>
      <aside class="right"></aside>
    </div>
```
效果图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191028144554894.png)

- 绝对定位


```css
      * {
        margin: 0;
        padding: 0;
      }
      aside {
        position: absolute;
        width: 300px;
        min-height: 100px;
      }
      aside.left {
        left: 0;
        background-color: red;
      }
      aside.right {
        right: 0;
        background-color: blue;
      }
      main.center {
        position: absolute;
        left: 300px;
        right: 300px;
        min-height: 100px;
        background-color: orange;
      }
```
```html
    <aside class="left"></aside>
    <aside class="right"></aside>
    <main class="center">
    </main>
```

- Grid

```css
    * {
        margin: 0;
        padding: 0;
      }
      /* 网格布局 */
      .wrapper {
        display: grid;
        height: 200px;
        width: 100%;
        grid-template-columns: 300px 1fr 300px;
      }
      
      .left {
        background-color: red;
      }
      .center {
        background-color: orange;
      }
      .right {
        background-color: blue;
      }
```
```html
    <div class="wrapper">
      <aside class="left"></aside>
      <main class="center">
      </main>
      <aside class="right"></aside>
    </div>
```

参考：[详解 CSS 七种三栏布局技巧](https://zhuanlan.zhihu.com/p/25070186)