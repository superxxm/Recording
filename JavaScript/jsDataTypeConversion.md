# 数据类型转换
## 目录
	1. 强制转换
		1.1 Number()
		1.2 String()
		1.3 Boolean()
	2. 自动转换
		2.1 自动转换为布尔值
		2.2 自动转换为字符串
		2.3 自动转换为数值
	3. 参考链接

JavaScript是一种动态类型语言，变量没有类型限制，可以随时赋予任意值。

	var x = y ? 1 : 'a';

上面代码中，变量`x`到底是数值还是字符串，取决于另一个变量`y`的值，只有代码运行时，才可能知道`x`的类型。

虽然变量没有类型，但是数据本身和各种运算符是由类型的，如果运算符发现，数据类型与预期不符，就会自动转换类型。

## 1. 强制转换
强制转换主要是指使用`Number`，`String`和`Boolean`三个构造函数，手动将各种类型的值，转换成数字，字符串或者布尔值。
### 1.1 Number()
使用`Number`函数，可以将任意类型的值转化成数值。

（1）原始类型值的转换规则

原始类型的值主要是字符串，布尔值，`undefined`和`null`，它们都能被`Number`转成数值或`NaN`。

	//数值： 转换后还是原来的值
	Number(324) //324
	//字符串： 如果可以解析为数值，则转换为想应数值
	Number('324') //324
	//字符串： 如果不可以被解析为数值，返回NaN
	Number('323adfa') //NaN
	//空字符串转为0
	Number('') //0
	//布尔值： true转成1，false转成0
	Number(true) //1
	Number(false) //0
	//undefined： 转成NaN
	Number(undefined) //NaN
	//null：转成0
	Number(null) //0

`Number()`函数将字符串转为数值，要比`parseInt()`严格很多。基本上，只要有一个字符无法转成数值，整个字符串就会转成`NaN`。

	parseInt('23 cats') //23
	Number('23 cats') //NaN

`parseInt()`逐个解析字符，而`Number()`整体转换字符串的类型。

另外，`Number()`函数会自动过滤一个字符串前导和后缀的空格。

	Number('\t\v\r12.34\n') //12.34

（2）对象的转换规则

简单的规则是，`Number`方法的参数是对象时，将返回`NaN`。

	Number({a: 1}) //NaN
	Number([1, 2, 3]) //NaN

实际上，`Number`背后的真正规则复杂的多，内部处理步骤如下。
>1. 调用对象自身的`valueOf()`方法。如果返回原始类型的值，则直接对该值使用`Number()`函数，不再进行后续步骤。
>2. 如果`valueOf()`方法返回的还是对象，则改为调用对象自身的`toString()`方法。如果返回原始类型的值，则对该值使用`Number()`函数，不再进行后续步骤。
>3. 如果`toString()`方法返回的是对象，就报错。

如下：

	Number(obj)
	//等同于
	if(typeof obj.valueOf() === 'object') {
		Number(obj.toString());
	} else {
		Number(obj.valueOf());
	}

上面代码中，`Number()`函数将`obj`对象转为数值。首先，调用`obj.valueOf`方法，结果返回对象本身。于是，继续调用`obj.toString()`，这时字符串`[object Object]`，对这个字符串使用`Number`函数，得到`NaN`。

默认情况下，对象的`valueOf()`方法返回对象本身，所以一般总会调用`toString()`方法，而`toString()`方法返回对象的类型字符串，所以会有下面结果。

	Number({}) //NaN

如果`toString()`方法返回的不是原始类型的值，结果就会报错。

	var obj = {
		valueOf: function() {
			return {};		
		},
		toString: function() {
			return {};
		}
	};
	Number(obj)
	//TypeError: Cannot convert object to primitive value

上面代码的`valueOf()`和`toString()`方法，返回的都是对象，所以转成数值时会报错。

从上面的例子可以看出，`valueOf()`和`toString()`都是可以自定义的。

	Number({
		valueOf: function() {
			return 2;
		}
	})
	//2
	Number({
		toString: function() {
			return 3;
		}
	})
	//3
	Number({
		valueOf: function() {
			return 2;
		},
		toString: function() {
			return 3;
		}
	})
	//2
上面对三个对象使用`Number`函数，第一个对象返回`valueOf()`方法的值，第二个对象返回`toString()`方法的值，第三个对象表示`valueOf()`方法先于`toString()`方法执行。
### 1.2 String()
