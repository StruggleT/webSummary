## 变量

- 变量命名规范

1. 变量名必须以英文字母、_、$开头
2. 变量名可以包括英文字母、_、$、数字
3. 不可以使用系统的关键字、保留字作为变量名

- var变量

var定义的变量没有块级作用域，只有函数级作用域。var 定义的变量会提升

- let变量

let变量是es6中引进的，用let定义的变量会生成一个作用域，外部不能访问。因此对于变量的私有化要求更加严格。let定义的变量有以下几个特点：

1. let定义的变量拥有块级作用域

3. let在块级作用域中不存在变量提升

5. 不能在同一作用域中（函数作用域和块级作用域）用let声明相同的变量

- [关于let与var在for循环中的小问题](https://blog.csdn.net/litcangosh/article/details/101356877) 
## 常量
const定义的是常量，不可以修改并且必须初始化。使用const定义数组时，数组名不能改变，但数组的内容可以通过push改变。

参考：[let和const命令(阮一峰)](http://es6.ruanyifeng.com/#docs/let)

## JS数据类型
JS中有 6 种原始值，分别是：

- boolean
- number
- string
- undefined
- symbol
- null

引用类型：

- 对象
- 数组
- 函数

## typeof详解
typeof操作符返回的是一个字符串，用来指示未经计算的操作数类型。typeof是唯一一个使用未声明对象不会报错（会返回undefined）的操作符。它的返回值分别是：

- boolean
- number
- string
- undefined
- [symbol](http://es6.ruanyifeng.com/#docs/symbol)
- object
- function
- bigint

其中的 null，虽然是基本变量,但是因为设计的时候null是全0，而对象是000开头，对象在底层都表示为二进制,所以有(typeof null)为object这个误判。

## 类型转换
参考：[深入理解JS的类型、值、类型转换](https://github.com/amandakelake/blog/issues/34)|[javascript数据转换](https://learnku.com/articles/7380/javascript-type-conversion)



---
# `关于变量和类型转换的一些面试题`

### 1.不使用临时变量，交换两个数值变量的值

- 算术运算 

```javascript
var a = 1,
    b = 2;

a = a + b; // a = 3, b = 2
b = a - b; // a = 3, b = 1
a = a - b; // a = 2, b = 1
```
通过算术运算过程中的技巧，可以巧妙地将两个值进行互换。但是，有个缺点就是变量数据溢出。因为JavaScript能存储数字的精度范围是 -253 到 253。所以，加法运算，会存在溢出的问题。

- 异或运算

```javascript
		var a = 1 // a = 0001
		var b = 2 // b = 0010
		a = a ^ b // a = 0011 , b = 0010
		b = a ^ b // b = 0001 , a = 0011
		a = a ^ b // a = 0010 , b = 0001
```
避免了使用算术运算带来的弊端，不会发生溢出问题。

- ES6的解构

```javascript
let a = 1,
	b = 2;
	
[a, b] = [b, a];
```

- 利用数组特性进行交换

```javascript
var a = 1,
	b = 2;
a = [a,b];
a = a[0];
b = a[1];

```

### 2.基本类型有哪几种？null 是对象吗？基本数据类型和复杂数据类型存储有什么区别？
- 基本类型有6种，分别是undefined,null,bool,string,number,symbol(ES6新增)。
- 虽然 typeof null 返回的值是 object,但是null不是对象，而是基本数据类型的一种。
- 基本数据类型存储在`栈内存`，存储的是`值`。
- 复杂数据类型的值存储在`堆内存`，地址（指向堆中的值）存储在栈内存。当我们把对象赋值给另外一个变量的时候，复制的是地址，指向同一块内存空间，当其中一个对象改变时，另一个对象也会变化。

### 3.instanceof 的实现原理是什么？
instanceof 是通过原型链判断的，A instanceof B, 在A的原型链中层层查找，是否有原型等于B.prototype，如果一直找到A的原型链的顶端(null;即`Object.proptotype.__proto__`),仍然不等于B.prototype，那么返回false，否则返回true.

- instanceof实现的代码

```javascript
// A instanceof B
function instanceOf(A, B) {//A 表示左表达式，B 表示右表达式
    var O = B.prototype;// 取 B 的显式原型
    A = A.__proto__;    // 取 A 的隐式原型
    while (true) { 
        if (A === null) //已经找到顶层
            return false;  
        if (O === A)   //当 O 严格等于 A 时，返回 true
            return true; 
        A = A.__proto__;  //继续向上一层原型链查找
    } 
}
```

### 4.如何判断一个变量是不是数组？
原文链接：[寒冬求职季之你必须要懂的原生JS](https://juejin.im/post/5cab0c45f265da2513734390)
- 使用 Array.isArray 判断，如果返回 true, 说明是数组
- 使用 instanceof Array 判断，如果返回true, 说明是数组
- 使用 Object.prototype.toString.call 判断，如果值是 [object Array], 说明是数组
- 通过 constructor 来判断，如果是数组，那么 arr.constructor === Array. (`不准确`，因为我们可以指定` obj.constructor = Array`)

```javascript
function fn() {
    console.log(Array.isArray(arguments));   //false; 因为arguments是类数组，但不是数组
    console.log(Array.isArray([1,2,3,4]));   //true
    console.log(arguments instanceof Array); //fasle
    console.log([1,2,3,4] instanceof Array); //true
    console.log(Object.prototype.toString.call(arguments)); //[object Arguments]
    console.log(Object.prototype.toString.call([1,2,3,4])); //[object Array]
    console.log(arguments.constructor === Array); //false
    arguments.constructor = Array;
    console.log(arguments.constructor === Array); //true
    console.log(Array.isArray(arguments));        //false
}
fn(1,2,3,4);
```
### 5.` == 与 ===`的区别？
`===` 不需要进行类型转换，只有`类型`相同并且`值`相等时，才返回 true.

`== `如果两者类型不同，首先需要进行`类型转换`。具体流程如下:

1. 首先判断两者类型是否相同，如果相等，判断值是否相等.
2. 如果类型不同，进行类型转换
3. 判断比较的是否是 null 或者是 undefined, 如果是, 返回 true .
4. 判断两者类型是否为 string 和 number, 如果是, 将字符串转换成 number
5. 判断其中一方是否为 boolean, 如果是, 将 boolean 转为 number 再进行判断
6. 判断其中一方是否为 object 且另一方为 string、number 或者 symbol , 如果是, 将 object 转为原始类型再进行判断

`note:注意复杂数据类型，比较的是引用地址`

-  关于`[ ] = = ![ ]`

	- 首先，我们需要知道` !` 优先级是高于 `==` (更多运算符优先级可查看: 运算符优先级)
	- `![ ] `引用类型转换成布尔值都是true,因此![]的是false
	- 根据上面的比较步骤中的第五条，其中一方是 boolean，将 boolean 转为 number 再进行判断，false转换成 number，对应的值是 0.
	- 根据上面比较步骤中的第六条，有一方是 number，那么将object也转换成Number,空数组转换成数字，对应的值是0.(空数组转换成数字，对应的值是0，如果数组中只有一个数字，那么转成number就是这个数字，其它情况，均为NaN)
	- 0 == 0; 为true

### 6.`obj.toString() `和`Object.prototype.toString.call(obj)`
同样是检测对象obj调用toString方法，obj.toString()的结果和Object.prototype.toString.call(obj)的结果不一样，这是为什么？

这是因为toString为Object的原型方法，而Array ，function等类型作为Object的实例，都重写了toString方法。不同的对象类型调用toString方法时，根据原型链的知识，调用的是对应的重写之后的toString方法（function类型返回内容为函数体的字符串，Array类型返回元素组成的字符串.....），而不会去调用Object上原型toString方法（返回对象的具体类型），所以采用obj.toString()不能得到其对象类型，只能将obj转换为字符串类型；因此，在想要得到对象的具体类型时，应该调用Object上原型toString方法。
