## call
call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法。

例子：
```javascript

	var foo = {
		
		value:2
	}

	function bar() {
		console.log(this.value)
	}
	bar.call(foo) // 2
```

从这个例子中可以看出两点：

- call 改变了 this 的指向，指向到 foo
- bar函数也执行了

### 模拟实现基本原理
上述例子试想当调用 call 的时候，把 foo 对象改造成如下：

```javascript
var foo = {
    value: 2,
    bar: function() {
        console.log(this.value)
    }
};

foo.bar(); // 2
```
这个时候的this就指向了foo函数了，但是foo对象又添加了一个多余的属性，因此我们需要bar用delete给删除就行了。

因此模拟的步骤分为三步：

1. 将函数设为对象的属性
2. 执行该函数
3. 删除该函数

以上述例子：

```javascript
// 第一步
foo.fn = bar
// 第二步
foo.fn()
// 第三步
delete foo.fn
```
fn 是对象的属性名，反正最后也要删除它，所以起成什么都无所谓。

- 最终的实现及应用

```javascript
	var value = 3

	var foo = {
		
		value:2
	}

	function bar(name,age) {

		console.log(this.value)

		console.log(name)

		console.log(age)
	}
	
	Function.prototype.call2 = function (context) {
		 //没传参数或者为null是默认是window
		var context = context || window
		 // 首先要获取调用call的函数，用this可以获取
		context.fn = this

		var args = []

		for(var i = 1;i<arguments.length;i++){

				args.push('arguments[' + i + ']')
		}

		eval('context.fn('+args+')')

		// 执行了args.push('arguments[' + i + ']')后
		// args = [ 'arguments[1]', 'arguments[2]' ]包含2个字符
		// 然后执行eval('context.fn(' + args + ')')
		// +令 args 执行 args.toString() 相当于eval('context.fn(' + ‘arguments[1], arguments[2]’+ ')')
		// 字符串合并，即eval('context.fn( arguments[1], arguments[2] )')
		// 执行context.fn( arguments[1], arguments[2] )

		delete context.fn

	}
	bar.call2(null)// 3  undefinde undefinde

	bar.call2(foo,'cc',18) // 2  cc 18
```

## apply
实现原理和call差不多

```javascript
Function.prototype.apply = function (context, arr) {
    var context = Object(context) || window;
    context.fn = this;

    var result;
    if (!arr) {
        result = context.fn();
    }
    else {
        var args = [];
        for (var i = 0, len = arr.length; i < len; i++) {
            args.push('arr[' + i + ']');
        }
        result = eval('context.fn(' + args + ')')
    }

    delete context.fn
    return result;
}
```