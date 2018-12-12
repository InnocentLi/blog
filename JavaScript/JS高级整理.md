javascript 高级程序设计 笔记(超强整理)




# 基本类型
### typeof操作符
鉴于 ECMAScript 是松散类型的，因此需要有一种手段来检测给定变量的数据类型——typeof 就 是负责提供这方面信息的操作符。对一个值使用 typeof 操作符可能返回下列某个字符串:

 "undefined"——如果这个值未定义; 

 "boolean"——如果这个值是布尔值;

 "string"——如果这个值是字符串;

 "number"——如果这个值是数值;

 "object"——如果这个值是对象或 null; 

 "function"——如果这个值是函数。

 typeof null 会返回"object"，因为特殊值 **null 被认为是一个空的对象**引用。

## Undefined
使用 var 声明变量但未对其加以初始化时

```javascript
var message;
alert(message == undefined); //true

var message = undefined;
alert(message == undefined); //true

var message; // 这个变量声明之后默认取得了 undefined 值 
// 下面这个变量并没有声明
// var age
alert(message);// "undefined" 
alert(age);// 产生错误
```

## null 
```javascript
var car = null;
alert(typeof car);
// "object
```
**undefined 值是派生自 null 值的**，因此 ECMA-262 规定对它们的相等性测试要返回 true:
 alert(null == undefined);    //true

 alert(null === undefined);    //false

## Boolean

| Boolean   | true                       | false        |
| --------- | -------------------------- | ------------ |
| String    | 任何非空字符串             | ""(空字符串) |
| Number    | 任何非零数字值(包括无穷大) | 0和NaN       |
| Object    | 任何对象                   | null         |
| Undefined | 不存在                     | undefined    |


## Number

1. 浮点数值

isNaN()函数。这个函数接受一个参数，该参数可以 是任何类型，而函数会帮我们确定这个参数是否“不是数值”。浮点数精度17 位小数，所以0.1 加 0.2 的结果不是 0.3，而是 0.30000000000000004。(并不是所有的精度计算都是这样)因为这是基于 IEEE754 数值的浮点计算的通病 所以我们用精度保持的方法去进行计算

参考博客

https://github.com/camsong/blog/issues/9




2. 数值范围

Number.MIN_VALUE
Number.MAX_VALUE
超出会被转换成 Infinity 或 - Infinity 

3. NaN

```javascript
var a = NaN
var b = NaN
a == b // false

alert(isNaN(NaN));//true
alert(isNaN(10));//false(10 是一个数值) 
alert(isNaN("10"));//false(可以被转换成数值 10) 
alert(isNaN("blue"));//true(不能转换成数值) 
alert(isNaN(true));//false(可以被转换成数值 1)
```


4. 数值转换
  Number() 可以用于任何数据类型，

  parseInt()parseFloat()。用于把字符串转换成数值。

  Number()函数的转换规则如下。
  如果是 Boolean 值，true 和 false 将分别被转换为 1 和 0。  如果是数字值，只是简单的传入和返回。

  如果是 null 值，返回 0。

  如果是 undefined，返回 NaN。

  如果是字符串，遵循下列规则👇

  如果字符串中只包含数字(包括前面带正号或负号的情况)，则将其转换为十进制数值，即"1" 会变1，"123"会变成 123，而"011"会变成 11(注意:前导的零被忽略了);

  如果字符串中包含有效的浮点格式，如"1.1"，则将其转换为对应的浮点数值(同样，也会忽 略前导零);

  如果字符串中包含有效的十六进制格式，例如"0xf"，则将其转换为相同大小的十进制整 数值;

  如果字符串是空的(不包含任何字符)，则将其转换为 0;

  如果字符串中包含除上述格式之外的字符，则将其转换为 NaN。

  如果是对象，则调用对象的 valueOf()方法，然后依照前面的规则转换返回的值。如果转换的结果是 NaN，则调用对象的 toString()方法，然后再次依照前面的规则转换返回的字符串值。

```javascript
var num1 = Number("Hello world!"); //NaN
var num2 = Number(""); //0
var num3 = Number("000011"); //11 
var num4 = Number(true); //1

var num1 = parseInt("1234blue");// 1234
var num2 = parseInt("");// NaN
var num3 = parseInt("0xA");// 10(十六进制数) 
var num4 = parseInt(22.5);// 22
var num5 = parseInt("070");// 56(八进制数) 
var num6 = parseInt("70");// 70(十进制数) 
var num7 = parseInt("0xf");// 15(十六进制数)

var num1 = parseInt("10", 2);//2 (按二进制解析)
var num2 = parseInt("10", 8); //8 (按八进制解析)
var num3 = parseInt("10", 10); //10(按十进制解析)
var num4 = parseInt("10", 16); //16(按十六进制解析)
```

## String

```javascript
var age = 11;
var ageAsString = age.toString(); // 字符串"11" 
var found = true;
var foundAsString = found.toString(); // 字符串"true"
var num = 10;
alert(num.toString());// "10"
alert(num.toString(2));// "1010"
alert(num.toString(8));// "12"
alert(num.toString(10));// "10"
alert(num.toString(16));// "a"

var value1 = 10;
var value2 = true;
var value3 = null;
var value4;
alert(String(value1));// "10"
alert(String(value2));// "true"
alert(String(value3));// "null"
alert(String(value4));// "undefined"

var result1 = ("55" == 55); //true，因为转换后相等
var result2 = ("55" === 55); //false，因为不同的数据类型不相等

可以看下 	!== 和 !===
```

# 变量、作用域和内存问题

## 基本类型和引用类型的值
基本类型值指的是简单的数据段，而引用类型值指那些可能由多个值构成的对象。

基本类型的值有

Undefined、Null、Boolean、Number 和 String。**基本数据类型是按值访问的**

引用类型的值是保存在内存中的对象。在操作对象时，实际上是在操作对象的引用而不是实际的对象。
**引用类型的值是按引用访问的**。

- 基本类型值在内存中占据固定大小的空间，因此被保存在栈内存中; 
- 引用类型的值是对象，保存在堆内存中; 

#### 为什么会存在栈内存和堆内存之分

当一个方法执行时，每个方法都会建立自己的内存栈，在这个方法内定义的变量将会逐个放入这块栈内存里，随着方法的执行结束，这个方法的内存栈也将自然销毁了。因此，所有在方法中定义的变量都是放在栈内存中的；

当我们在程序中创建一个对象时，这个对象将被保存到运行时数据区中，以便反复利用（因为对象的创建成本通常较大），这个运行时数据区就是堆内存。堆内存中的对象不会随方法的结束而销毁，即使方法结束后，这个对象还可能被另一个引用变量所引用（方法的参数传递时很常见），则这个对象依然不会被销毁，只有当一个对象没有任何引用变量引用它时，系统的垃圾回收机制才会在核实的时候回收它。

#### 栈堆区别

栈使用的是一级缓存， 他们通常都是被调用时处于存储空间中，调用完毕立即释放堆（操作系统）： 一般由程序员分配释放， 若程序员不释放，程序结束时可能由OS回收，分配方式倒是类似于链表。

堆则是存放在二级缓存中，生命周期由虚拟机的垃圾回收算法来决定（并不是一旦成为孤儿对象就能被回收）。所以调用这些对象的速度要相对来得低一些
堆（数据结构）：堆可以被看成是一棵树，如：堆排序
栈（数据结构）：一种后进先出的的数据结构



栈内存是Os分配的

堆内存是自己手动申请的

例如IOS开发的的时候利用release释放内存

> 在MRC的内存管理模式下，与对变量的管理相关的方法有：retain, release 和 autorelease。retain 和 release 方法操作的是引用记数，当引用记数为零时，便自动释放内存。并且可以用 NSAutoreleasePool 对象，对加入自动释放池（autorelease 调用）的变量进行管理，当 drain 时回收内存。



## 复制变量值

```javascript
var num1 = 5;
var num2 = num1;
```

num1 和 num 2是完全独立的，也就是说这两个变量可以参与任何操作而不会相互影响

当从一个变量向另一个变量复制引用类型的值时，同样也会将存储在变量对象中的值复制一份放到
为新变量分配的空间中。这个值的副本实际上是一个指针，而这个指针指向存储在堆中的一个对象。

```javascript
 var obj1 = new Object();
 var obj2 = obj1;
 obj1.name = "Nicholas";
 alert(obj2.name);  //"Nicholas"
```

## 传递参数

Javascript中所有函数的参数都是按值传递的。也就是说，把函数外部的值复制给函数内部的参数，就和把值从一个变量复制到另一个变量一样。

**访问变量有按值和按引用两种方式，而参数只能按值传递。**

此处很好理解，就是如果

```javascript
var a = 1;
var b = a;
console.log(a);
//此时代码是在读取
//而这个代码
function c(a){
    a = 777;
}
//此时代码在传参数
//如果不理解可以参考js的get和set函数
```

如果是基本类型

```javascript
function addTen(num) {
    num += 10;
	return num; 
}
var count = 20;
var result = addTen(count);
alert(count); //20，没有变化 
alert(result); //30
```

如果是传递对象

```javascript
function setName(obj) { 
    obj.name = "Nicholas"; 
    obj = new Object(); 
    obj.name = "Greg";
}
var person = new Object();
setName(person);
alert(person.name);    //"Nicholas"
```

如果 person 是按引用传递的，那么 person 就会自动被修改为指向其 name 属性值为"Greg"的新对象。但是，当接下来再访问 person.name 时，显示的值仍然是"Nicholas"。这说明**即使在函数内部修改了参数的值，但原始的引用仍然保持未变。**

## 检测类型

instanceof  检测引用类型的值的时候很好用

```javascript
alert(person instanceof Object); // 变量 person 是 Object 吗? 
alert(colors instanceof Array); // 变量 colors 是 Array 吗? 
alert(pattern instanceof RegExp); //变量pattern 是RegExp吗?
```

但是缺点可能存在，最好的方法就是在高级技巧里的方法



## 执行环境及作用域

**作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。**

以下话不好翻译，直接看代码就行

> 每个执行环境都有一个与之关联的变量对象(variable object)，环境中定义的所有变量和函数都保存在这个对象中。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。
>
> 此处可以查看编译原理(龙书)
>
> 每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被推入一个环境栈中。而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。ECMAScript 程序中的执行流正是由这个方便的机制控制着。
>
> 当代码在一个环境中执行时，会创建变量对象的一个作用域链(scope chain)。作用域链的前端，始终都是当前执行的代码所 在环境的变量对象。如果这个环境是函数，则将其活动对象(activation object)作为变量对象。活动对 6 象在最开始时只包含一个变量，即 arguments 对象(这个对象在全局环境中是不存在的)。作用域链中 的下一个变量对象来自包含(外部)环境，而再下一个变量对象则来自下一个包含环境。这样，一直延 续到全局执行环境;全局执行环境的变量对象始终都是作用域链中的最后一个对象。 标识符解析是沿着作用域链一级一级地搜索标识符的过程。搜索过程始终从作用域链的前端开始， 然后逐级地向后回溯，直至找到标识符为止(如果找不到标识符，通常会导致错误发生)。 



```javascript
var 爷爷颜色 = "blue";
    function 爸爸(){
        var 爸爸颜色 = "red";
        function 儿子(){
            var 儿子颜色 = "green"
			// 这里可以访问爷爷颜色、爸爸颜色和儿子颜色 
        }
		// 这里可以访问爷爷颜色和爸爸颜色，但不能访问儿子颜色
        儿子();
    }
// 这里只能访问爷爷颜色 
爸爸();
```

以上代码共涉及 3 个执行环境:

全局环境(爷爷环境)、爸爸()的局部环境和 儿子()的局部环境。全局环境中有一个变量爷爷颜色 和一个函数 爸爸()。爸爸()的局部环境中有一个名为 爸爸颜色 的变量和一个名为 儿子()的函数，但它也可以访问全局环境中的变
量 爷爷颜色。儿子()的局部环境中有一个变量 儿子颜色，该变量只能在这个环境中访问到。无论全局环境(爷爷环境)还是爸爸()的局部环境都无权访问 儿子颜色。然而，在 儿子()内部则可以访问其他两个环境中的所有变量，因为那两个环境是它的父执行环境。

其中，内部环境可以通过作用域链访问所有的外部环境，但外部环境不能访问内部环境中的任何变量和函数。这些环境之间的联系是线性、有次序的。每个环境都可以向上搜索作用域链，以查询变量和函数名;但任何环境都不能通过向下搜索作用域链而进入另一个执行环境。

爷爷只知道自己的颜色，爸爸知道爷爷自己的和爸爸自己的颜色，儿子什么都知道包括自己的颜色。

其实可以这么理解

儿子=>父亲=>爷爷 这是一个单项链表，当我在某个位置读取函数或者是变量时都会先读区 head-> val，当不存在时。head= head -> next

> 函数参数也被当作变量来对待，因此其访问规则与执行环境中的其他变量相同

### 延长作用域链

try- catch语句

with语句

### ES6之前没有块级作用域

```javascript
if (true) {
   var color = "blue";
}
alert(color);    //"blue"

//这里是在一个if语句中定义了变量color。如果是在 C、C++或 Java 中，color 会在 if 语句执行完毕后被
//销毁。但在 JavaScript 中，if 语句中的变量声明会将变量添加到当前的执行环境(在这里是全局环境)中。
```

#### 声明变量

使用 var 声明的变量会自动被添加到最接近的环境中。如果初始化变量时没有使用 var 声明，该变量会自
动被添加到全局环境。

```javascript
function add(num1, num2) {
    var sum = num1 + num2;
	return sum; 
}
var result = add(10, 20); //30
alert(sum); //由于 sum 不是有效的变量，因此会导致错误\


function add(num1, num2) {
    sum = num1 + num2;
	return sum; 
}
var result = add(10, 20); //30
alert(sum); //30
```

#### 查询标识符

>当在某个环境中为了读取或写入而引用一个标识符时，必须通过搜索来确定该标识符实际代表什
>么。搜索过程从作用域链的前端开始，向上逐级查询与给定名字匹配的标识符。如果在局部环境中找到
>了该标识符，搜索过程停止，变量就绪。如果在局部环境中没有找到该变量名，则继续沿作用域链向上
>搜索。搜索过程将一直追溯到全局环境的变量对象。如果在全局环境中也没有找到这个标识符，则意味
>着该变量尚未声明。

也就是说，我会首先搜索最近的区域，如果没有则会向上搜索直到找到标识符为止。

```javascript
var color = "blue";
function getColor(){
    return color;
}
alert(getColor());  //"blue"
```

如果局部环境中存在着同名标识符，就不会使用位于父环境中的标识符

```javascript
var color = "blue";
function getColor(){
    var color = "red";     
    return color;
}
alert(getColor());  //"red"
```

## 垃圾收集 

此处垃圾回收写的不好，我只做摘抄，新版本的GC参考Node.js

>标记清除
> JavaScript 中最常用的垃圾收集方式是标记清除(mark-and-sweep)。当变量进入环境(例如，在函 数中声明一个变量)时，就将这个变量标记为“进入环境”。从逻辑上讲，永远不能释放进入环境的变 量所占用的内存，因为只要执行流进入相应的环境，就可能会用到它们。而当变量离开环境时，则将其 标记为“离开环境”。 
>
>可以使用任何方式来标记变量。比如，可以通过翻转某个特殊的位来记录一个变量何时进入环境， 或者使用一个“进入环境的”变量列表及一个“离开环境的”变量列表来跟踪哪个变量发生了变化。说 到底，如何标记变量其实并不重要，关键在于采取什么策略。 
>
>垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记(当然，可以使用任何标记方 式)。然后，它会去掉环境中的变量以及被环境中的变量引用的变量的标记。而在此之后再被加上标记 的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后，垃圾收集器 完成内存清除工作，销毁那些带标记的值并回收它们所占用的内存空间。 
>
>到 2008 年为止，IE、Firefox、Opera、Chrome 和 Safari 的 JavaScript 实现使用的都是标记清除式的 垃圾收集策略(或类似的策略)，只不过垃圾收集的时间间隔互有不同。 







等下整理










# 引用类型

## Object

创建 Object 实例的方式有两种。

```javascript
// new操作符后跟Object构造函数
var person = new Object();
person.name = "Nicholas";
person.age = 29;

//子面量表示法
var person = {
    name : "Nicholas",
    age : 29
};
```

一般来说，访问对象属性时使用的都是点表示法，这也是很多面向对象语言中通用的语法。不过， 在 JavaScript 也可以使用方括号表示法来访问对象的属性。在使用方括号语法时，应该将要访问的属性 以字符串的形式放在方括号中，如下面的例子所示。 

```javascript
alert(person["name"]); //"Nicholas" 
alert(person.name); //"Nicholas" 
```

从功能上看，这两种访问对象属性的方法没有任何区别。但方括号语法的主要优点是可以通过变量 来访问属性，例如: 

```javascript
var propertyName = "name"; alert(person[propertyName]); //"Nicholas" 
```

创建方式
var o = new Object();

### Object属性和方法

Object 的每个实例都具有下列属性和方法。

##### constructor:

保存着用于创建当前对象的函数。对于前面的例子而言，构造函数(constructor) 就是 Object()。

##### hasOwnProperty(propertyName):

用于检查给定的属性在当前对象实例中(而不是在实例 的原型中)是否存在。其中，作为参数的属性名(propertyName)必须以字符串形式指定(例 如:o.hasOwnProperty("name"))。

##### isPrototypeOf(object):

用于检查传入的对象是否是传入对象的原型。

##### propertyIsEnumerable(propertyName):

用于检查给定的属性是否能够使用 for-in 语句来枚举。与 hasOwnProperty()方法一样，作为参数的属性名必须以字符串形式指定。

##### toLocaleString():

返回对象的字符串表示，该字符串与执行环境的地区对应。

##### toString():

返回对象的字符串表示。 valueOf():返回对象的字符串、数值或布尔值表示。通常与 toString()方法的返回值
相同。

##### valueOf()方法

JavaScript调用valueOf方法将对象转换为原始值

```javascript
var str2 = new String("http://www.xyz.com");// new一个字符串对象

console.log( str2.valueOf() === str2 );   // false
// 两者的值相等，但不全等，因为类型不同，前者为string类型，后者为object类型
```

```javascript
var array = ["ABC", true, 12, -5];
console.log(array.valueOf() === array);   // true
// Array：返回数组对象本身
```



## 

## Array

### 创建数组

```javascript
创建数组的基本方式有两种。第一种是使用 Array 构造函数
var colors = new Array();
第二种是后面写数字，表示创建长度为20的数组
var colors = new Array(20);
也可以向 Array 构造函数传递数组中应该包含的项
var colors = new Array("red", "blue", "green");
可以直接赋值为数组即可
var arr = []；
```

其实我们不必纠结创建数组的方式，目前看很多源码都是利用 var arr = []；方式进行创建的，就可以了。

### 检测数组

前几章提到过

```javascript
if(value instanceof Array){
	//对数组执行某些操作
}

if(Array.isArray(value)){ 
    //对数组执行某些操作
}
//最强方法
if(Object.prototype.toSting.call(value) == "[object Array]"){
	//对数组执行某些操作
}
```

### 转换方法

```javascript
var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组 
alert(colors.toString());// red,blue,green
alert(colors.valueOf());// red,blue,green
alert(colors);// red,blue,green
```

#### join方法

```javascript
  var colors = ["red", "green", "blue"];
  alert(colors.join(","));       //red,green,blue
  alert(colors.join("||"));      //red||green||blue
```

### 栈方法

```javascript
var colors = new Array();// 创建一个数组 
var count = colors.push("red", "green"); // 推入两项 
alert(count); //2 
count = colors.push("black");// 推入另一项
alert(count);     //3
var item = colors.pop(); // 取得最后一项 
alert(item);      //"black"
alert(colors.length);   //2
```

### 队列方法



### 迭代方法

every():对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true。
filter():对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。
forEach():对数组中的每一项运行给定函数。这个方法没有返回值。
map():对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。
some():对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true。

### 归并方法





## Date类型



深拷贝





## 单体内置对象

Global对象
Global 对象的 encodeURI()和 encodeURIComponent()方法，在汽车之家的项目中用到了这个方法

Math对象
random()方法

```javascript
function rand (){
  	i = (i * 3) % 101;
	return i;
} 
```

## RegExp类型(正则)

如果作为复习可略过摘自老姚的博客并加上笔记

https://zhuanlan.zhihu.com/p/29707385

PS:红宝书介绍的十分有限

### 为什么单独开辟正则？

因为还是很重要的，在很多源码中正则出现频率非常高，不是每个我要匹配的或者查询的字符要去手写，而是直接一行正则就可以解决，比如在你输入密码的时候，要求你必须大小写字母或数字，比如你输入邮箱的时候，比如手机号的匹配，再比如匹配更复杂的(匹配开头是a结尾是b的字符)，正则表达式都要优于"暴力"匹配，

介绍在开头







### 字符匹配

#### 模糊匹配

精确匹配如下

```javascript
var regex = /hello/;
console.log( regex.test("hello") );
// => true
```

但是正则强大之处在于可以模糊匹配

##### 横向模糊匹配

横向模糊指的是，一个正则可匹配的字符串的长度不是固定的，可以是多种情况的。 

其实现的方式是使用量词。譬如 {m,n}，表示连续出现最少 m 次，最多 n 次。比如正则 /ab{2,5}c/ 表示匹配这样一个字符串:第一个字符是 "a"，接下来是 2 到 5 个字符 "b"，最后 是字符 "c"。 

```javascript
  var regex = /ab{2,5}c/g;
  var string = "abc abbc abbbc abbbbc abbbbbc abbbbbbc abbbbbbbbbbbbbbbbc";
  console.log( string.match(regex) );
  // => ["abbc", "abbbc", "abbbbc", "abbbbbc"]

很明显 abc中的b只出现一次
```

match的意思是找到一个或多个正则表达式的匹配。

g的意思是全局匹配，即在目标字符串中按顺序找到满足匹配模式的所有子串，强调的是“所有”，而不只是“第一个” 。g 是单词 global 的首字母。 

##### 纵向模糊匹配

纵向模糊指的是，一个正则匹配的字符串，具体到某一位字符时，它可以不是某个确定的字符，可以有多种可能。 

其实现的方式是使用字符组。譬如 [abc]，表示该字符是可以字符 "a"、"b"、"c" 中的任何一个。 比如 /a[123]b/ 可以匹配如下三种字符串: "a1b"、"a2b"、"a3b"。

```javascript
var regex = /a[123]b/g;
var string = "a0b a1b a2b a3b a4b acb a12b";
console.log( string.match(regex) );
// => ["a1b", "a2b", "a3b"]


var regex = /a[123][123]b/g;
var string = "a0b a1b a2b a3b a4b acb a12b";
console.log( string.match(regex) );
// => ["a1b", "a2b", "a3b"]
```

#### 字符组

需要强调的是，虽叫字符组(字符类)，但只是其中一个字符。 例如 [abc]，表示匹配一个字符，它可以是 "a"、"b"、"c" 之一。 

##### 范围表示法

比如 [123456abcdefGHIJKLM]，可以写成 [1-6a-fG-M]。用连字符 - 来省略和简写。

因为连字符有特殊用途，那么要匹配 "a"、"-"、"z" 这三者中任意一个字符，该怎么做呢?不能写成 [a-z]，因为其表示小写字符中的任何一个字符。可以写成如下的方式:[-az] 或 [az-] 或 [a\\-z]。即要么放在开头，要么放在结尾，要么转义。总之不会让引擎认为是范围表示法就行了。

##### 排除字符组

纵向模糊匹配，还有一种情形就是，某位字符可以是任何东西，但就不能是 "a"、"b"、"c"。 此时就是排除字符组(反义字符组)的概念。例如 \[^abc]，表示是一个除 "a"、"b"、"c"之外的任意一个字 符。字符组的第一位放 ^(脱字符)，表示求反的概念。 当然，也有相应的范围表示法。 

#### 常见的简写形式



| 字符组 | 具体含义                                                     |
| ------ | ------------------------------------------------------------ |
| \d     | 表示 [0-9]。表示是一位数字。 记忆方式:其英文是 digit(数字)。 |
| \D     | 表示 \[^0-9]。表示除数字外的任意字符。                       |
| \w     | 表示 [0-9a-zA-Z_]。表示数字、大小写字母和下划线。记忆方式:w 是 word 的简写，也称单词字符。 |
| \W     | 表示 \[^0-9a-zA-Z_]。非单词字符。                            |
| \s     | 表示 [ \t\v\n\r\f]。表示空白符，包括空格、水平制表符、垂直制表符、换行符、回车符、换页 符。  记忆方式:s 是 space 的首字母，空白符的单词是 white space。 |
| \S     | 表示 \[^ \t\v\n\r\f]。 非空白符。                            |
| .      | 表示 \[^\n\r\u2028\u2029]。通配符，表示几乎任意字符。换行符、回车符、行分隔符和段分隔符 除外。记忆方式:想想省略号 ... 中的每个点，都可以理解成占位符，表示任何类似的东西。 |

如果匹配任意字符，可以使用以下几种[\d\D]、[\w\W]、[\s\S] 和 [^] 中任何的一个。

#### 量词

##### 简写形式

| 量词 | 具体含义                                                     |
| ---- | ------------------------------------------------------------ |
| {m,} | 表示至少出现 m 次。                                          |
| {m}  | 等价于 {m,m}，表示出现 m 次。                                |
| ?    | 等价于 {0,1}，表示出现或者不出现。 记忆方式:问号的意思表示，有吗? |
| +    | 等价于 {1,}，表示出现至少一次。 记忆方式:加号是追加的意思，得先有一个，然后才考虑追加。 |
| *    | 等价于{0,}表示出现任意次，有可能不出现。 记忆方式:看看天上的星星，可能一颗没有，可能零散有几颗，可能数也数不过来。 |

#### 贪婪匹配与惰性匹配

```javascript
var regex = /\d{2,5}/g;
var string = "123 1234 12345 123456 23456" ;
console.log( string.match(regex) );
// => ["123", "1234", "12345", "12345","23456"]
```

其中正则 /\d{2,5}/，表示数字连续出现 2 到 5 次。会匹配 2 位、3 位、4 位、5 位连续数字。 但是其是贪婪的，它会尽可能多的匹配。你能给我 6 个，我就要 5 个。你能给我 3 个，我就要 3 个。 

反正只要在能力范围内，越多越好。 我们知道有时贪婪不是一件好事(请看文章最后一个例子)。而惰性匹配，就是尽可能少的匹配: 

```javascript
  var regex = /\d{2,5}?/g;
  var string = "123 1234 12345 123456";
  console.log( string.match(regex) );
  // => ["12", "12", "34", "12", "34", "12", "34", "56"]
```

其中 /\d{2,5}?/ 表示，虽然 2 到 5 次都行，当 2 个就够的时候，就不再往下尝试了。 

| 惰性量词 | 贪婪量词 |
| -------- | -------- |
| {m,n}?   | {m,n}    |
| {m,}?    | {m,}     |
| ??       | ?        |
| +?       | +        |
| *?       | *        |

#### 多选分支

一个模式可以实现横向和纵向模糊匹配。而多选分支可以支持多个子模式任选其一。 

具体形式如下:(p1|p2|p3)，其中 p1、p2 和 p3 是子模式，用 |(管道符)分隔，表示其中任何之一。 例如要匹配字符串 "good" 和 "nice" 可以使用 /good|nice/。

```javascript
 var regex = /good|nice/g;
 var string = "good idea, nice try.";
 console.log( string.match(regex) );
 // => ["good", "nice"]


 var regex = /a|b/g;
 var string = "good idea, nice try , agian, bus.";
 console.log( string.match(regex) );
 // => ["a", "b","a","b"]
```





/good|goodbye/，去匹配 "goodbye" 字符串时，结果是 "good":

```javascript
var regex = /good|goodbye/g;
var string = "goodbye";
console.log( string.match(regex) );
// => ["good"]

var regex = /goodbye|good/g;
var string = "goodbye";
console.log( string.match(regex) );
// => ["goodbye"]
```

也就是说，分支结构也是**惰性的**，即当前面的匹配上了，后面的就不再尝试了。

#### 案例分析

> ```
> #ffbbad
> #Fc01DF
> #FFF
> #ffE
> 
> ```

自己尝试写的

```javascript
var regex = /#[0-9a-fA-F]{6}|#[0-9a-fA-F]{3}/g
var string = "#ffbbad #Fc01DF #FFF #ffE #dasda ###";
console.log( string.match(regex) );


和标准答案相同😄
```

匹配时间

```javascript
自己尝试写的
var regex = /[2][0-4]:[0-6][0-9]|[01][0-9]:[0-6][0-9]/g
var string = "23:59 02:07 21:38 15:43 27:21 20:71";
console.log( string.match(regex));


标准答案👇
var regex = /^([01][0-9]|[2][0-3]):[0-5][0-9]$/;
console.log( regex.test("23:59") );
console.log( regex.test("02:07") );


```

匹配日期

yyyy-mm-dd

这是个坑，没考虑到闰年和平年，先这么写了

假设我只能活到2999年

```javascript
var regex = /^[0-9]{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$/;
console.log( regex.test("2017-06-10") );
```

window 操作系统文件路径

wtf

> F:\study\javascript\regex\regular expression.pdf
> F:\study\javascript\regex\
> F:\study\javascript
> F:\

```javascript
  var regex = /^[a-zA-Z]:\\([^\\:*<>|"?\r\n/]+\\)*([^\\:*<>|"?\r\n/]+)?$/;
  console.log( regex.test("F:\\study\\javascript\\regex\\regular expression.pdf") );
  console.log( regex.test("F:\\study\\javascript\\regex\\") );
  console.log( regex.test("F:\\study\\javascript") );
  console.log( regex.test("F:\\") );
  // => true
  // => true
  // => true
  // => true
```

匹配div标签的id

要求从 

```html
  <div id="container" class="main"></div>
```

提取出 id="container"。 可能最开始想到的正则是: 

```javascript
  var regex = /id=".*"/
  var string = '<div id="container" class="main"></div>';
  console.log(string.match(regex)[0]);
  // => id="container" class="main"
```

因为 . 是通配符，本身就匹配双引号的，而量词 * 又是贪婪的，当遇到 container 后面双引号时，是不会 停下来，会继续匹配，直到遇到最后一个双引号为止。 

解决之道，可以使用惰性匹配: 

```javascript
var regex = /id=".*?"/
var string = '<div id="container" class="main"></div>';
console.log(string.match(regex)[0]);
// => id="container"
```

当然，这样也会有个问题。效率比较低，因为其匹配原理会涉及到“回溯”这个概念。可以优化如下:

```javascript
 var regex = /id="[^"]*"/
 var string = '<div id="container" class="main"></div>';
 console.log(string.match(regex)[0]);
 // => id="container"
```

### 位置匹配

在 ES5 中，共有 6 个锚:

^、$、\b、\B、(?=p)、(?!p)

^(脱字符)匹配开头，在多行匹配中匹配行开头。 

$(美元符号)匹配结尾，在多行匹配中匹配行结尾。 

比如

```javascript
var regex = /m&/g
var string = 'abcdefghijklmn';
 console.log(string.replace(regex,"#"));
```



### 括号的作用 

### 回溯法原理 

### 拆分 

### 构建 

### 编程 





## Function

### 理解参数

ECMAScript函数不介意传递进来多少个参数，也不在乎传进来参数是什么数据类型。函数体内可以通过 arguments 对象来访问这个参数数组，从而获取传递给函数的每一个参数。

所以以下两个函数是相等的

```javascript
function sayHi(name, message) {
    alert("Hello " + name + "," + message);
}

function sayHi() {
    alert("Hello " + arguments[0] + "," + arguments[1]);
}
```

通过访问 arguments 对象的 length 属性可以获知有多少个参数传递给了函数。下面这个函数会
在每次被调用时，输出传入其中的参数个数:

```javascript
 function howManyArgs() {
    alert(arguments.length);
}
howManyArgs("string", 45);  //2
howManyArgs();              //0
howManyArgs(12);            //1
```

 **arguments的值永远与对应命名参数的值保持同步。** 

```javascript
function doAdd(num1, num2) {
    arguments[1] = 10;
    alert(arguments[0] + num2);
} 
```

每次执行这个 doAdd()函数都会重写第二个参数，将第二个参数的值修改为 10。**因为 arguments对象中的值会自动反映到对应的命名参数**，所以修改 arguments[1]，也就修改了 num2，结果它们的值都会变成 10。

**它们的内存空间是独立的，但它们的值会同步**

> 这并不是说读取这两个值会访问相同的内存空间。另外还要记住，如果只传入了一个参数，那么为 arguments[1]设置的值不会反应到命名参数中。这是因为 arguments 对象的长度是由传入的参数个数决定的，不是由定义函数时的命名参数的个数决定的。
>
> 没有传递值的命名参数将自动被赋予 undefined 值。这就跟定义了变量但又没有初始化一样。例如，如果只给 doAdd()函数传递了一个参数，则 num2 中就会保存undefined 值。

**arguments遍历求和**

```javascript
function add() {
    var sum =0,
        len = arguments.length;
    for(var i=0; i<len; i++){
        sum += arguments[i];
    }
    return sum;
}
add()                           // 0
add(1)                          // 1
add(1,2,3,4);                   // 10
```

当非严格模式中的函数**有**包含剩余参数默认参数和解构赋值，那么`arguments`对象中的值**不会**跟踪参数的值（反之亦然）。相反, `arguments`反映了调用时提供的参数：

```javascript
function func(a = 55) { 
  arguments[0] = 99; // updating arguments[0] does not also update a
  console.log(a);
}
func(10); // 10

function func(a = 55) { 
  a = 99; // updating a does not also update arguments[0]
  console.log(arguments[0]);
}
func(10); // 10

function func(a = 55) { 
  console.log(arguments[0]);
}
func(); // undefined
```

### 创建function

```javascript

//函数声明
function sum (num1, num2) {
        return num1 + num2;
}
//这与下面使用函数表达式定义函数的方式几乎相差无几。
// 函数表达式
    var sum = function(num1, num2){
        return num1 + num2;
};

//但是在解析的时候就会发生区别，
//举个🌰
//此方法没有问题
sum(1, 2)//3
function sum (num1, num2) {
        return num1 + num2;
}
//但是此方法会有问题
sum(1, 2)//报错
var sum = function(num1, num2){
        return num1 + num2;
};
```

**Function 构造函数**可以接收任意数量的参数， 但最后一个参数始终都被看成是函数体，而前面的参数则枚举出了新函数的参数。来看下面的例子: 

var sum = new Function("num1", "num2", "return num1 + num2"); // 不推荐 

### 作为值的函数

因为 ECMAScript 中的函数名本身就是变量，所以函数也可以作为值来使用。也就是说，不仅可以 像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。来看 一看下面的函数。

```javascript
function callFun(fun, fargu){
        return fun(fargu);
}
```

这个函数接受两个参数。第一个参数应该是一个函数，第二个参数应该是要传递给该函数的一个值。
然后，就可以像下面的例子一样传递函数了。

```javascript
function add10(num){
    return num + 10;
}

var result1 = callFun(add10, 10);
alert(result1);   //20

function getGreeting(name){
    return "Hello, " + name;
}

var result2 = callFun(getGreeting, 10);
alert(result2);   //"Hello,10"
```

假设有一个对象数组，我们想要根据某个对象属性对数组进行排序。而传递给数组 sort()方法的比较函数要接收两个参数，即要比较的值。可是，我们需要一种方式来指明按照哪个属性来排序。要解决这个问题，可以**定义一个函数，它接收一个属性名，然后根据这个属性名来创建一个比较函数**，下面就是这个函数的定义。

```javascript
function createComparisonFunction(propertyName) {
        return function(object1, object2){
            var value1 = object1[propertyName];
            var value2 = object2[propertyName];
            if (value1 < value2){
                return -1;
            } else if (value1 > value2){
                return 1;
			}
        };
}


data.sort(createComparisonFunction("name")); 8
var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
alert(data[0].name);  //Nicholas
data.sort(createComparisonFunction("age"));
alert(data[0].name);  //Zachary
```

### 函数内部属性

arguments 和 this

斐波那契

#### arguments.callee

```javascript
function factorial(num){
        if (num <=1) {
            return 1;
        } else {
            return num * factorial(num-1)
        }
}
//相等

function factorial(num){
    if (num <=1) {
        return 1;
    } else {
        return num * arguments.callee(num-1)
} }

//在这个重写后的 factorial()函数的函数体内，没有再引用函数名 factorial。
//这样，无论引用 函数时使用的是什么名字，都可以保证正常完成递归调用。例如:

var trueFactorial = factorial;
factorial = function(){
       return 0;
};
    alert(trueFactorial(5));     //120
//变量 trueFactorial 获得了 factorial 的值，实际上是在另一个位置上保存了一个函数 的指针。
//然后，我们又将一个简单地返回 0 的函数赋值给 factorial 变量。
//如果像原来的 factorial() 那样不使用 arguments.callee，调用 trueFactorial()就会返回 0。
//可是，在解除了函数体内的代 码与函数名的耦合状态之后，trueFactorial()仍然能够正常地计算阶乘;
//至于 factorial()，它现 在只是一个返回 0 的函数。
	alert(factorial(5));         //0
```

####  this

js红宝书在这里解释的有点少，参考博客

https://juejin.im/post/596a28f6f265da6c360a2716

这句话被反复强调，就是**this 是在函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用。**

在 JavaScript 中，影响 this 指向的绑定规则有四种：

- 默认绑定

- 隐式绑定

- 显式绑定

- new 绑定

##### 默认绑定

这是最直接的一种方式，就是不加任何的修饰符直接调用函数，如：

```javascript
function foo() {
  console.log(this.a)   // 输出 a
}
var a = 2;  //  变量声明到全局对象中
foo();

function aaa() {
    this.a = 4; // 输出4
    foo();
}


```

复制代码使用 var 声明的变量 a，被绑定到全局对象中，如果是浏览器，则是在 window 对象。foo() 调用时，引用了默认绑定，this 指向了全局对象。

这其实造成了一个不安全的问题(在高级技巧里提到过)



##### 隐式绑定

这种情况会发生在调用位置存在「**上下文对象**」的情况，如：

```javascript
function foo() {
  console.log(this.a);
}

let obj1 = {
  a: 1,
  foo,
};

let obj2 = {
  a: 2,
  foo,
}

obj1.foo();   // 输出 1
obj2.foo();   // 输出 2
```

当**函数调用的时候，拥有上下文对象的时候，`this` 会被绑定到该上下文对象。**
正如上面的代码，
`obj1.foo()` 被调用时，`this` 绑定到了 `obj1`,
而 `obj2.foo()` 被调用时，`this` 绑定到了 `obj2`。

##### 显式绑定

这种就是使用 `Function.prototype` 中的三个方法 `call()`, `apply()`, `bind()` 了。
这三个函数，都可以改变函数的 `this` 指向到指定的对象，
不同之处在于，`call()` 和 `apply()` 是立即执行函数，并且接受的参数的形式不同：

- call(this, arg1, arg2, ...)
- apply(this, [arg1, arg2, ...])

而 `bind()` 则是创建一个新的包装函数，并且返回，而不是立刻执行。

- bind(this, arg1, arg2, ...)

`apply()` 接收参数的形式，有助于函数嵌套函数的时候，把 `arguments` 变量传递到下一层函数中。

思考下面代码：

```javascript
function foo() {
  console.log(this.a);  // 输出 1
  bar.apply({a: 2}, arguments);
}

function bar(b) {
  console.log(this.a + b);  // 输出 5
}

var a = 1;
foo(3);
```

上面代码中， `foo()` 内部的 `this` 遵循默认绑定规则，绑定到全局变量中。

而 `bar()` 在调用的时候，调用了 `apply()` 函数，把 `this` 绑定到了一个新的对象中 `{a: 2}`，而且原封不动的接收 `foo()` 接收的函数。

##### new 绑定

最后一种，则是使用 `new` 操作符会产生 `this` 的绑定。

在理解 `new` 操作符对 `this` 的影响，首先要理解 `new` 的原理。

在 JavaScript 中，`new` 操作符并不像其他面向对象的语言一样，而是一种模拟出来的机制。

在 JavaScript 中，所有的函数都可以被 `new` 调用，这时候这个函数一般会被称为「构造函数」，实际上并不存在所谓「构造函数」，更确切的理解应该是对于函数的「构造调用」。

使用 `new` 来调用函数，会自动执行下面操作：

1. 创建一个全新的对象。
2. 这个新对象会被执行 [[Prototype]] 连接。
3. 这个新对象会绑定到函数调用的 this。
4. 如果函数没有返回其他对象，那么 new 表达式中的函数调用会自动返回这个新对象。

所以如果 `new` 是一个函数的话，会是这样子的：

```javascript
function New(Constructor, ...args){
    let obj = {};   // 创建一个新对象
    Object.setPrototypeOf(obj, Constructor.prototype);  // 连接新对象与函数的原型
    return Constructor.apply(obj, args) || obj;   // 执行函数，改变 this 指向新的对象
}

function Foo(a){
    this.a = a;
}

New(Foo, 1);  // Foo { a: 1 }
```

所以，在使用 `new` 来调用函数时候，我们会构造一个新对象并把它绑定到函数调用中的 `this` 上。

##### 优先级

如果一个位置发生了多条改变 this 的规则，那么优先级是如何的呢？

看几段代码：

```javascript
// 显式绑定 > 隐式绑定
function foo() {
    console.log(this.a);
}

let obj1 = {
    a: 2,
    foo,
}

obj1.foo();     // 输出 2
obj1.foo.call({a: 1});      // 输出 1复制代码
```

这说明「显式绑定」的优先级大于「隐式绑定」

```javascript
// new 绑定 > 显式绑定
function foo(a) {
    this.a = a;
}

let obj1 = {};

let bar = foo.bind(obj1);
bar(2);
console.log(obj1); // 输出 {a:2}

let obj2 = new bar(3);
console.log(obj1); // 输出 {a:2}
console.log(obj2); // 输出 foo { a: 3 }复制代码
```



### 函数属性和方法

ECMAScript 中的函数是对象，因此函数也有属性和方法。每个函数都包含两个 属性:length 和 prototype。其中，length 属性表示函数希望接收的命名参数的个数，如下面的例子所示。

```javascript
function sayName(name){
    alert(name);
}
function sum(num1, num2){
    return num1 + num2;
}
function sayHi(){
    alert("hi");
}
alert(sayName.length);      //1
alert(sum.length);          //2
alert(sayHi.length);        //0
```

以上代码定义了 3 个函数，但每个函数接收的命名参数个数不同。首先，sayName()函数定义了一个参数，因此其 length 属性的值为 1。类似地，sum()函数定义了两个参数，结果其 length 属性中保存的值为 2。而 sayHi()没有命名参数，所以其 length 值为 0。

> 对于 ECMAScript 中的引用类型而言，prototype 是保存它们所有实例方法的真正所在。换句话说，toString()和 valueOf()等方法实际上都保存在 prototype 名下，只不过是通过各自对象的实例访问罢了。在创建自定义引用类型以及实现继承时，prototype 属性的作用是极为重要的(第 6 章将详 细介绍)。在 ECMAScript 5 中，prototype 属性是不可枚举的，因此使用 for-in 无法发现。 

每个函数都包含两个非继承而来的方法:apply()和 call()。这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内 this 对象的值。首先，apply()方法接收两个参数:一个 是在**其中运行函数的作用域**，另一个是**参数数组**。其中，第二个参数可以是 Array 的实例，也可以是 arguments 对象。例如: 

```javascript
function sum(num1, num2){
    return num1 + num2;
}
function callSum1(num1, num2){
    
    return sum.apply(this, arguments);
}
function callSum2(num1, num2){
    return sum.apply(this, [num1, num2]);
}
alert(callSum1(10,10));   //20
alert(callSum2(10,10));   //20
```

在上面这个例子中，callSum1()在执行 sum()函数时传入了 this 作为 this 值(因为是在全局作用域中调用的，所以传入的就是 window 对象)和 arguments 对象。而 callSum2 同样也调用了sum()函数，但它传入的则是 this 和一个参数数组。这两个函数都会正常执行并返回正确的结果。

在使用 call()方法的情况下，callSum()必须明确地传入每一个参数。结果与使用 apply()没有 什么不同。至于是使用 apply()还是 call()，完全取决于你采取哪种给函数传递参数的方式最方便。 如果你打算直接传入 arguments 对象，或者包含函数中先接收到的也是一个数组，那么使用 apply() 肯定更方便。否则，选择 call()可能更合适。(在不给函数传递参数的情况下，使用哪个方法都无所谓。

事实上，传递参数并非 apply()和 call()真正的用武之地;它们真正强大的地方是**能够扩充函数赖以运行的作用域**。下面来看一个例子。 

```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){
    alert(this.color);
} 
sayColor(); //red 
sayColor.call(this);//red
sayColor.call(window);//red
sayColor.call(o);//blue

```



这个例子是在前面说明 this 对象的示例基础上修改而成的。这一次，sayColor()也是作为全局函数定义的，而且当在全局作用域中调用它时，它确实会显示"red"——因为对 this.color 的求值会转换成对 window.color 的求值。而 sayColor.call(this)和 sayColor.call(window)，则是两 种显式地在全局作用域中调用函数的方式，结果当然都会显示"red"。但是，当运行 sayColor.call(o) 时，函数的执行环境就不一样了，因为此时函数体内的 this 对象指向了 o，于是结果显示的是"blue"。 

使用 call()(或 apply())来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系。 在前面例子的第一个版本中，我们是先将 sayColor()函数放到了对象 o 中，然后再通过 o 来调用它的; 而在这里重写的例子中，就不需要先前那个多余的步骤了。 

bind()。这个方法会创建一个函数的实例，其 this 值会被绑定到传给 bind()函数的值。	

```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){
    alert(this.color);
}
var objectSayColor = sayColor.bind(o);
objectSayColor();    //blue
```





### 手写call，bind，apply









### 没有重载(深入理解)

```javascript
function addSomeNumber(num){
    return num + 100;
}
function addSomeNumber(num) {
    return num + 200;
}
var result = addSomeNumber(100); //300
//相当于
var addSomeNumber = function (num){
    return num + 100;
};
addSomeNumber = function (num) { 
    return num + 200;
};
var result = addSomeNumber(100); //300
```









# 面向对象

## 理解对象



## 创建对象


1. 工厂模式


2. 构造函数模式


3. 原型模式

4. 组合使用构造函数模式和原型模式


5. 动态原型模式


6. 寄生构造函数模式


7. 稳妥构造函数模式



## 继承

1. 原型链

2. 借用构造函数

3. 组合继承

4. 原型式继承 

5. 寄生式继承

6. 寄生组合式继承



# 函数表达式

## 闭包
闭包是指有权访问另一个 函数作用域中的变量的函数。


## 关于this对象

## 模仿块级作用域

ES6块级作用

## 私有变量

ES6 私有变量


# BOM

## window对象

全局作用域

窗口关系及框架

## screen

## history




# 客户端检测



# DOM


# Canvas 

性能非常好的原因就是借助了显卡加速

CSS3性能如果加入translate z 0 也会提升性能



# HTML5 脚本编程



# 错误处理与调试

# json



# Ajax 和 Comet

## XMLHttpRequest对象

## XMLHttpRequest 2 

# 高级技巧

## 高级函数

### 安全的类型检测

```javascript
 var isArray = value instanceof Array;
```

可以利用Object 原生的 toString()方法进行调用

返回的是[object ,NativeConstructorName ]的字符串

```javascript
function isArray(value){
	Object.prototype.toSting.call(value) == "[object Array]"
}
```

### 作用域安全的构造函数

```javascript
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
}
var person = new Person("Nicholas", 29, "Software Engineer");
```



### 函数柯里化



### 函数绑定



## 防篡改对象

### 不可扩展对象

### 密封的对象

### 冻结的对象

### 

## 高级定时器

### 重复的定时器



### Yielding Processes

### 函数节流

## 自定义事件

# 离线应用和客户端缓存

## 离线检测



# 新型API

## requestAnimationFrame()

## Web Workers

# ES6

promise

map set

let const





