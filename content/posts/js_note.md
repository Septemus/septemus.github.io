---
title: "Javascript 学习笔记"
date: 2023-07-31T22:24:11+08:00
draft: false
categories: ["college"]
featuredImagePreview: "/images/javascript.png"
featuredImage: "/images/javascript.png"
---

> # 语法和数据类型

> ## 数字

- 在 JavaScript 里面，数字均为双精度浮点类型（double-precision 64-bit binary format IEEE 754），即一个介于 ±2^−1023 和 ±2^+1024 之间的数字，或约为 ±10^−308 到 ±10^+308，数字精度为 53 位。整数数值仅在 ±(2^53 - 1) 的范围内可以表示准确。
  
- JavaScript 最近添加了 BigInt 的支持，能够用于表示极大的数字。使用 BigInt 的时候有一些注意事项，例如，你不能让 BigInt 和 Number 直接进行运算，你也不能用 Math 对象去操作 BigInt 数字。
- 请注意，十进制可以以 0 开头，后面接其他十进制数字，但是假如下一个接的十进制数字小于 8，那么该数字将会被当做八进制处理。

```javascript
0888 // 888 以十进制解析
0777 // 以八进制解析，为十进制的 511

```


> ## 变量的作用域

ECMAScript 6 之前的 JavaScript 没有语句块作用域；相反，语句块中声明的变量将成为语句块所在函数（或全局作用域）的局部变量。例如，如下的代码将在控制台输出 5，因为 x 的作用域是声明了 x 的那个函数（或全局范围），而不是 if 语句块。

```javascript
if (true) {
var x = 5;
}
console.log(x); // 5
```

如果使用 ECMAScript 6 中的 let 声明，上述行为将发生变化。

```javascript

if (true) {
let y = 5;
}
console.log(y); // ReferenceError: y 没有被声明

```


> ## 变量提升

JavaScript 变量的另一个不同寻常的地方是，你可以先使用变量稍后再声明变量而不会引发异常。这一概念称为变量提升；JavaScript 变量感觉上是被“提升”或移到了函数或语句的最前面。但是，提升后的变量将返回 undefined 值。因此在使用或引用某个变量之后进行声明和初始化操作，这个被提升的变量仍将返回 undefined 值。

```javascript
/**
 * 例子 1
 */
console.log(x === undefined); // true
var x = 3;

/**
 * 例子 2
 */
// will return a value of undefined
var myvar = "my value";

(function () {
console.log(myvar); // undefined
var myvar = "local value";
})();

```
上面的例子，也可写作：

```javascript
/**
 * 例子 1
 */
var x;
console.log(x === undefined); // true
x = 3;

/**
 * 例子 2
 */
var myvar = "my value";

(function () {
var myvar;
console.log(myvar); // undefined
myvar = "local value";
})();

```
由于存在变量提升，一个函数中所有的var语句应尽可能地放在接近函数顶部的地方。这个习惯将大大提升代码的清晰度。

在 ECMAScript 6 中，let 和 const 同样会被提升变量到代码块的顶部但是不会被赋予初始值。在变量声明之前引用这个变量，将抛出引用错误（ReferenceError）。这个变量将从代码块一开始的时候就处在一个“暂时性死区”，直到这个变量被声明为止。

```javascript

console.log(x); // ReferenceError
let x = 3;

```

> ## 函数提升

函数提升
对于函数来说，只有函数声明会被提升到顶部，而函数表达式不会被提升。

```javascript

/* 函数声明 */

foo(); // "bar"

function foo() {
  console.log("bar");
}

/* 函数表达式 */

baz(); // 类型错误：baz 不是一个函数

var baz = function () {
  console.log("bar2");
};

```

> ## 类没有提升

Class declaration hoisting
Unlike function declarations, class declarations are not hoisted (or, in some interpretations, hoisted but with the temporal dead zone restriction), which means you cannot use a class before it is declared.

```javascript
new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization

class MyClass {}
```


> ## 常量

常量的作用域规则与 let 块级作用域变量相同。若省略 const 关键字，则该标识符将被视为变量。

在同一作用域中，不能使用与变量名或函数名相同的名字来命名常量。例如：


```javascript
// 这会造成错误
function f() {}
const f = 5;

// 这也会造成错误
function f() {
  const g = 5;
  var g;

  //语句
}
```


然而，对象属性被赋值为常量是不受保护的，所以下面的语句执行时不会产生错误。

```javascript

const MY_OBJECT = { key: "value" };
MY_OBJECT.key = "otherValue";

```
同样的，数组的被定义为常量也是不受保护的，所以下面的语句执行时也不会产生错误。



```javascript

const MY_ARRAY = ["HTML", "CSS"];
MY_ARRAY.push("JAVASCRIPT");
console.log(MY_ARRAY); //logs ['HTML','CSS','JAVASCRIPT'];


```

> ## 字符串转换为数字

- parseInt() 不会四舍五入
  
> ## 数组字面值中的多余逗号
你不必列举数组字面值中的所有元素。若你在同一行中连写两个逗号（,），数组中就会产生一个没有被指定的元素，其初始值是 undefined。以下示例创建了一个名为 fish 的数组：


```javascript
var fish = ["Lion", , "Angel"];

```
在这个数组中，有两个已被赋值的元素，和一个空元素（fish[0] 是 "Lion"，fish[1] 是 undefined，而 fish[2] 是 "Angel"）。

如果你在元素列表的尾部添加了一个逗号，它将会被忽略。在下面的例子中，数组的长度是 3，并不存在 myList[3] 这个元素。元素列表中其他所有的逗号都表示一个新元素（的开始）。

备注： 尾部的逗号在早期版本的浏览器中会产生错误，因而编程时的最佳实践方式就是移除它们。

```javascript
var myList = ["home", , "school"];
```

在下面的例子中，数组的长度是 4，元素 myList[0] 和 myList[2] 缺失。

```javascript

var myList = [, "home", , "school"];

```

再看一个例子。在这里，该数组的长度是 4，元素 myList[1] 和 myList[3] 被漏掉了。（但是）只有最后的那个逗号被忽略。

```javascript
var myList = ["home", , "school", ,];


```

> ## bool 对象

不要混淆作为布尔对象的真和假与布尔类型的原始值 true 和 false。布尔对象是原始布尔数据类型的一个包装器。
例如：
```javascript
var b = new Boolean(false);
if (b) //结果视为真
if (b == true) // 结果视为假
```

> ## 字面量

你不能在一条语句的开头就使用对象字面值，这将导致错误或产生超出预料的行为，因为此时左花括号（{）会被认为是一个语句块的起始符号

> ### 对象字面量

可以使用数字或字符串字面值作为属性的名字

对象属性名字可以是任意字符串，包括空串。如果对象属性名字不是合法的 javascript 标识符，它必须用""包裹。属性的名字不合法，那么便不能用。访问属性值，而是通过类数组标记 ("[]") 访问和赋值。

```javascript

var unusualPropertyNames = {
  "": "An empty string",
  "!": "Bang!"
}
console.log(unusualPropertyNames."");   // 语法错误：Unexpected string
console.log(unusualPropertyNames[""]);  // An empty string
console.log(unusualPropertyNames.!);    // 语法错误：Unexpected token !
console.log(unusualPropertyNames["!"]); // Bang!

```

> # 流程控制和错误处理


> ## finally块
finally块包含了在 try 和 catch 块完成后、下面接着 try...catch 的语句之前执行的语句。finally块无论是否抛出异常都会执行。如果抛出了一个异常，就算没有异常处理，finally块里的语句也会执行。

你可以用finally块来令你的脚本在异常发生时优雅地退出；举个例子，你可能需要在绑定的脚本中释放资源。接下来的例子用文件处理语句打开了一个文件（服务端的 JavaScript 允许你进入文件）。如果在文件打开时一个异常抛出，finally块会在脚本错误之前关闭文件。

```javascript
openMyFile();
try {
  writeMyFile(theData); //This may throw a error
} catch (e) {
  handleError(e); // If we got a error we handle it
} finally {
  closeMyFile(); // always close the resource
}
```
如果finally块返回一个值，该值会是整个try-catch-finally流程的返回值，不管在try和catch块中语句返回了什么：


```javascript
function f() {
  try {
    console.log(0);
    throw "bogus";
  } catch (e) {
    console.log(1);
    return true; // this return statement is suspended
    // until finally block has completed
    console.log(2); // not reachable
  } finally {
    console.log(3);
    return false; // overwrites the previous "return"
    console.log(4); // not reachable
  }
  // "return false" is executed now
  console.log(5); // not reachable
}
f(); // console 0, 1, 3; returns false

```

用finally块覆盖返回值也适用于在catch块内抛出或重新抛出的异常：

```javascript
function f() {
  try {
    throw "bogus";
  } catch (e) {
    console.log('caught inner "bogus"');
    throw e; // this throw statement is suspended until
    // finally block has completed
  } finally {
    return false; // overwrites the previous "throw"
  }
  // "return false" is executed now
}

try {
  f();
} catch (e) {
  // this is never reached because the throw inside
  // the catch is overwritten
  // by the return in finally
  console.log('caught outer "bogus"');
}

// OUTPUT
// caught inner "bogus"

```


> # 循环和迭代

> ## for in 和 for of 的区别

{{< link "https://juejin.cn/post/6916058482231754765" >}}



> # 函数

> ## 函数表达式


这样的函数表达式的标识符只在函数体内可见
```javascript
var myfunc=function disp(){console.log("hello")};
console.log(disp) //ReferenceError: disp is not defined
```

> ## 形参

原始参数（比如一个具体的数字）被作为值传递给函数；值被传递给函数，如果被调用函数改变了这个参数的值，这样的改变不会影响到全局或调用函数。

如果你传递一个对象（即一个非原始值，例如Array或用户自定义的对象）作为参数，而函数改变了这个对象的属性，这样的改变对函数外部是可见的，如下面的例子所示：

```javascript
function myFunc(theObject) {
  theObject.make = "Toyota";
}

var mycar = { make: "Honda", model: "Accord", year: 1998 };
var x, y;

x = mycar.make; // x 获取的值为 "Honda"

myFunc(mycar);
y = mycar.make; // y 获取的值为 "Toyota"
// (make 属性被函数改变了)


```

> ## 嵌套函数和闭包
你可以在一个函数里面嵌套另外一个函数。嵌套（内部）函数对其容器（外部）函数是私有的。它自身也形成了一个闭包。一个闭包是一个可以自己拥有独立的环境与变量的表达式（通常是函数）。

既然嵌套函数是一个闭包，就意味着一个嵌套函数可以”继承“容器函数的参数和变量。换句话说，内部函数包含外部函数的作用域。

可以总结如下：

内部函数只可以在外部函数中访问。
内部函数形成了一个闭包：它可以访问外部函数的参数和变量，但是外部函数却不能使用它的参数和变量。
下面的例子展示了嵌套函数：

```javascript
function addSquares(a, b) {
  function square(x) {
    return x * x;
  }
  return square(a) + square(b);
}
a = addSquares(2, 3); // returns 13
b = addSquares(3, 4); // returns 25
c = addSquares(4, 5); // returns 41
```

由于内部函数形成了闭包，因此你可以调用外部函数并为外部函数和内部函数指定参数：

```javascript
function outside(x) {
  function inside(y) {
    return x + y;
  }
  return inside;
}
fn_inside = outside(3); // 可以这样想：给一个函数，使它的值加 3
result = fn_inside(5); // returns 8

result1 = outside(3)(5); // returns 8
```

> ### 闭包对词法环境引用的捆绑

JavaScript 中的函数会形成了闭包。 闭包是由函数以及声明该函数的词法环境组合而成的。该环境包含了这个闭包创建时作用域内的任何局部变量。

```javascript
function makeAdder(x) {
  return function (y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2)); // 7
console.log(add10(2)); // 12
```

在这个示例中，我们定义了 makeAdder(x) 函数，它接受一个参数 x ，并返回一个新的函数。返回的函数接受一个参数 y，并返回x+y的值。

从本质上讲，makeAdder 是一个函数工厂 — 他创建了将指定的值和它的参数相加求和的函数。在上面的示例中，我们使用函数工厂创建了两个新函数 — 一个将其参数和 5 求和，另一个和 10 求和。

add5 和 add10 都是闭包。它们共享相同的函数定义，但是保存了不同的词法环境。在 add5 的环境中，x 为 5。而在 add10 中，x 则为 10。

> ## 使用arguments对象

函数的实际参数会被保存在一个类似数组的 arguments 对象中。在函数内，你可以按如下方式找出传入的参数：

```javascript
arguments[i];

```

其中i是参数的序数编号（译注：数组索引），以 0 开始。所以第一个传来的参数会是arguments[0]。参数的数量由arguments.length表示。

使用 arguments 对象，你可以处理比声明的更多的参数来调用函数。这在你事先不知道会需要将多少参数传递给函数时十分有用。你可以用arguments.length来获得实际传递给函数的参数的数量，然后用arguments对象来取得每个参数。

例如，设想有一个用来连接字符串的函数。唯一事先确定的参数是在连接后的字符串中用来分隔各个连接部分的字符（译注：比如例子里的分号“；”）。该函数定义如下：

```javascript
function myConcat(separator) {
  var result = ""; // 把值初始化成一个字符串，这样就可以用来保存字符串了！！
  var i;
  // iterate through arguments
  for (i = 1; i < arguments.length; i++) {
    result += arguments[i] + separator;
  }
  return result;
}

```

你可以给这个函数传递任意数量的参数，它会将各个参数连接成一个字符串“列表”：

```javascript
// returns "red, orange, blue, "
myConcat(", ", "red", "orange", "blue");

// returns "elephant; giraffe; lion; cheetah; "
myConcat("; ", "elephant", "giraffe", "lion", "cheetah");

// returns "sage. basil. oregano. pepper. parsley. "
myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley");

```

备注： arguments 变量只是“类数组对象”，并不是一个数组。称其为类数组对象是说它有一个索引编号和length属性。尽管如此，它并不拥有全部的 Array 对象的操作方法。

> ## 剩余参数


剩余参数语法允许将不确定数量的参数表示为数组。在下面的例子中，使用剩余参数收集从第二个到最后参数。然后，我们将这个数组的每一个数与第一个参数相乘。这个例子是使用了一个箭头函数，这将在下一节介绍。

```javascript
function multiply(multiplier, ...theArgs) {
  return theArgs.map((x) => multiplier * x);
}

var arr = multiply(2, 1, 2, 3);
console.log(arr); // [2, 4, 6]
```

> # 表达式和运算符

> ## 相等性

- 在比较两个操作数时，双等号（==）将执行类型转换，并且会按照 IEEE 754 标准对 NaN、-0 和 +0 进行特殊处理（故 NaN != NaN，且 -0 == +0）；
- 三等号（===）做的比较与双等号相同（包括对 NaN、-0 和 +0 的特殊处理）但不进行类型转换；如果类型不同，则返回 false；

在相等运算中，应注意以下几个问题：
- 如果操作数是布尔值，则先转换为数值，其中 false 转为 0，true 转换为 1。
- 如果一个操作数是字符串，另一个操作数是数字，则先尝试把字符串转换为数字。
- 如果一个操作数是字符串，另一个操作数是对象，则先尝试把对象转换为字符串。
- 如果一个操作数是数字，另一个操作数是对象，则先尝试把对象转换为数字。
- 如果两个操作数都是对象，则比较引用地址。如果引用地址相同，则相等；否则不等。

下面是特殊操作数的相等比较。
```javascript
console.log("1" == 1);  //返回true。字符串被转换为数字
console.log(true == 1);  //返回true。true被转换为1
console.log(false == 0);  //返回true。false被转换为0
console.log(null == 0);  //返回false
console.log(undefined == 0);  //返回false
console.log(undefined == null);  //返回true
console.log(NaN == "NaN");  //返回false
console.log(NaN ==1);  //返回false
console.log(NaN == NaN);  //返回false
console.log(NaN != NaN);  //返回true
```
{{< admonition type=warning title="NaN" open=false >}}
NaN与任何值都不相等，包括它自己。null 和 undefined 值相等，但是它们是不同类型的数据。在相等比较中，null 和 undefined 不允许被转换为其他类型的值。
{{< /admonition >}}

下面是特殊操作数的全等比较。
```javascript
console.log(null === undefined);  //返回false
console.log(0 === "0");  //返回false
console.log(0 === false);  //返回false

```
对于对象，主要比较引用的地址，不比较对象的值。
```javascript
var a = new String("abcd);  //定义字符串"abcd"对象
var b = new String("abcd);  //定义字符串"abcd"对象
console.log(a === b);  //返回false
console.log(a == b);  //返回false
```
在上面示例中，两个对象的值相等，但是引用地址不同，所以它们既不想等，也不全等。因此，对于复合型对象来说，相等==和全等===运算的结果是相同的。

> ## delete

delete操作符，删除一个对象的属性（不能是继承的或者私有的）或者一个数组中某一个键值。语法如下：

```javascript
delete objectName.property;
delete objectName[index];

```

objectName是一个对象名，property 是一个已经存在的属性，index是数组中的一个已经存在的键值的索引值。


你能使用 delete 删除各种各样的隐式声明，但是被var声明的除外。

如果 delete 操作成功，属性或者元素会变成 undefined。如果 delete可行会返回true，如果不成功返回false。

```javascript
x = 42;
var y = 43;
myobj = new Number();
myobj.h = 4; // create property h
delete x; // returns true (can delete if declared implicitly)
delete y; // returns false (cannot delete if declared with var)
delete Math.PI; // returns false (cannot delete predefined properties)
delete myobj.h; // returns true (can delete user-defined properties)
delete myobj; // returns true (can delete if declared implicitly)

```
删除数组元素
删除数组中的元素时，数组的长度是不变的，例如删除 a[3], a[4]，a[4] 和 a[3] 仍然存在变成了 undefined。

delete 删除数组中的一个元素，这个元素就不在数组中了。例如，trees[3]被删除，trees[3] 仍然可寻址并返回 undefined。

```javascript
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
delete trees[3];
if (3 in trees) {
  // 不会被执行
}

```
如果想让数组中存在一个元素但是是undefined值，使用undefined关键字而不是delete操作。如下： trees[3] 分配一个 undefined,但是这个数组元素仍然存在：

```javascript
var trees = new Array("redwood", "bay", "cedar", "oak", "maple");
trees[3] = undefined;
if (3 in trees) {
  // this gets executed（会被执行）
}

```

> ## instanceof

instanceof
如果所判别的对象确实是所指定的类型，则返回true。其语法如下：

```javascript
objectName instanceof objectType;

```
objectName 是需要做判别的对象的名称，而objectType是假定的对象的类型，例如Date或 Array.

当你需要确认一个对象在运行时的类型时，可使用instanceof. 例如，需要 catch 异常时，你可以针对抛出异常的类型，来做不同的异常处理。

例如，下面的代码使用 instanceof 去判断 theDay 是否是一个 Date 对象。因为 theDay 是一个 Date 对象，所以 if 中的代码会执行。

```javascript
var theDay = new Date(1995, 12, 17);
if (theDay instanceof Date) {
  // statements to execute
}

```

> # 字符串

> ## String 对象

除非必要，应该尽量使用 String 字面值，因为 String 对象的某些行为可能并不与直觉一致。举例：

```javascript
const firstString = "2 + 2"; //创建一个字符串字面量
const secondString = new String("2 + 2"); // 创建一个字符串对象
eval(firstString); // 返回数字 4
eval(secondString); // 返回包含 "2 + 2" 的字符串对象
```

> # 正则表达式

> ## exec和match的区别

使用.exec()方法时，与'g'标志关联的行为是不同的。（“class”和“argument”的作用相反：在.match()的情况下，字符串类（或数据类型）拥有该方法，而正则表达式只是一个参数，而在.exec()的情况下，它是拥有该方法的正则表达式，其中字符串是参数。对比*str.match(re)与re.exec(str)* ), 'g'标志与.exec()方法一起使用获得迭代进展。而match遇到g标志会直接输出全局范围内匹配的串,而且不会输出括号里面的缓存。

```javascript
var xArray;
while ((xArray = re.exec(str))) console.log(xArray);
// produces:
// ["fee ", index: 0, input: "fee fi fo fum"]
// ["fi ", index: 4, input: "fee fi fo fum"]
// ["fo ", index: 7, input: "fee fi fo fum"]

```

m 标志用于指定多行输入字符串应该被视为多个行。如果使用 m 标志，^和$匹配的开始或结束输入字符串中的每一行，而不是整个字符串的开始或结束。

> # 数组

> ## 属性

- 数组长度可以中途改变,变大变小都可以，但是变小后在变大超出容量的部位都会变成undefined
- 如果你在代码中给数组下标运算符的是一个非整型,负数数值，那么它将作为一个表示数组的对象的属性创建，而不是数组的元素。（不会被算到length里面）
- 数组可以在超过当前长度的区域赋值
- 数组可以被赋值成一个全新的数组

> ## forEach

传递给 forEach 的函数对数组中的每个元素执行一次，数组元素作为参数传递给该函数。未赋值的值不会在 forEach 循环迭代。

注意，在数组定义时省略的元素不会在 forEach 遍历时被列出，但是手动赋值为 undefined 的元素是会被列出的：
```javascript
const sparseArray = ["first", "second", , "fourth"];

sparseArray.forEach((element) => {
  console.log(element);
});
// first
// second
// fourth

if (sparseArray[2] === undefined) {
  console.log("sparseArray[2] 是 undefined"); // true
}

const nonsparseArray = ["first", "second", undefined, "fourth"];

nonsparseArray.forEach((element) => {
  console.log(element);
});
// first
// second
// undefined
// fourth

```

> ## 多维数组

多维数组
数组是可以嵌套的，这就意味着一个数组可以作为一个元素被包含在另外一个数组里面。利用 JavaScript 数组的这个特性，可以创建多维数组。

以下代码创建了一个二维数组。

```javascript
const a = new Array(4);
for (i = 0; i < 4; i++) {
  a[i] = new Array(4);
  for (j = 0; j < 4; j++) {
    a[i][j] = "[" + i + "," + j + "]";
  }
}

```

这个例子创建的数组拥有以下行数据：

Row 0: [0,0] [0,1] [0,2] [0,3]
Row 1: [1,0] [1,1] [1,2] [1,3]
Row 2: [2,0] [2,1] [2,2] [2,3]
Row 3: [3,0] [3,1] [3,2] [3,3]

> ## 类数组对象（伪数组）

使用类数组对象
一些 JavaScript 对象，如 document.getElementsByTagName() 返回的 NodeList 或 arguments 等 JavaScript 对象，有与数组相似的行为，但它们并不共享数组的所有方法。arguments 对象提供了 length 属性，但没有实现如 forEach() 等数组方法。

不能直接在类数组对象上调用数组方法。

```javascript
function printArguments() {
  arguments.forEach((item) => {
    console.log(item);
  }); // TypeError: arguments.forEach is not a function
}
```

但你可以通过 Function.prototype.call() 间接调用它们。

```javascript
function printArguments() {
  Array.prototype.forEach.call(arguments, (item) => {
    console.log(item);
  });
}

```
数组原型方法也可以用于字符串，因为它们以类似于数组的方式提供对其中字符的顺序访问：

```javascript
Array.prototype.forEach.call("a string", (chr) => {
  console.log(chr);
});
```

> # Map和Set

> ## Object 和 Map 比较

Object和Map的比较
一般地，objects会被用于将字符串类型映射到数值。Object允许设置键值对、根据键获取值、删除键、检测某个键是否存在。而Map具有更多的优势。

- Object 的键均为 String 类型，在 Map 里键可以是任意类型。
- 必须手动计算Object的尺寸，但是可以很容易地获取使用Map的尺寸。
- Map的遍历遵循元素的插入顺序。
- Object有原型，所以映射中有一些缺省的键。（可以用 map = Object.create(null) 回避）。
这三条提示可以帮你决定用Map还是Object：

- 如果键在运行时才能知道，或者所有的键类型相同，所有的值类型相同，那就使用Map。
- 如果需要将原始值存储为键，则使用Map，因为Object将每个键视为字符串，不管它是一个数字值、布尔值还是任何其他原始值。
- 如果需要对个别元素进行操作，使用Object。

> ## Array和Set比较

Array和Set的对比
一般情况下，在 JavaScript 中使用数组来存储一组元素，而新的集合对象有这些优势：

- 数组中用于判断元素是否存在的indexOf 函数效率低下。
- Set对象允许根据值删除元素，而数组中必须使用基于下标的 splice 方法。
- 数组的indexOf方法无法找到NaN值。
- Set对象存储不重复的值，所以不需要手动处理包含重复值的情况。
  

> # 对象

> ## 属性

- 对象中未赋值的属性的值为undefined（而不是null）。
- 枚举一个对象的所有属性
  从 ECMAScript 5 开始，有三种原生的方法用于列出或枚举对象的属性：

  - for...in 循环 该方法依次访问一个对象及其原型链中所有可枚举的属性。
  - Object.keys(o) 该方法返回对象 o 自身包含（不包括原型中）的所有可枚举属性的名称的数组。
  - Object.getOwnPropertyNames(o) 该方法返回对象 o 自身包含（不包括原型中）的所有属性 (无论是否可枚举) 的名称的数组。
  
> ## 构造函数

- 构造函数中this指向新创建的对象

> ## 对象属性索引

在 JavaScript 1.0 中，你可以通过名称或序号访问一个属性。但是在 JavaScript 1.1 及之后版本中，如果你最初使用名称定义了一个属性，则你必须通过名称来访问它；而如果你最初使用序号来定义一个属性，则你必须通过索引来访问它。

这个限制发生在你通过构造函数创建一个对象和它的属性（就象我们之前通过 Car 对象类型所做的那样）并且显式地定义了单独的属性（如 myCar.color = "red"）之时。如果你最初使用索引定义了一个对象属性，例如 myCar[5] = "25"，则你只可能通过 myCar[5] 引用它。 

这条规则的例外是从与 HTML 对应的对象，例如 forms 数组。对于这些数组的元素，你总是既可以通过其序号（依据其在文档中出现的顺序），也可以按照其名称（如果有的话）访问它。举例而言，如果文档中的第二个 <form> 标签有一个 NAME 属性且值为 "myForm"，访问该 form 的方式可以是 document.forms[1]，document.forms["myForm"] 或 document.myForm。

> ## get和set



当使用 使用对象初始化器 的方式定义 getter 和 setter 时，只需要在 getter 方法前加 get，在 setter 方法前加 set，当然，getter 方法必须是无参数的，setter 方法只接受一个参数 (设置为新值），例如：

```javascript
var o = {
  a: 7,
  get b() {
    return this.a + 1;
  },
  set c(x) {
    this.a = x / 2;
  },
};

```
使用 Object.defineProperties 的方法，同样也可以对一个已创建的对象在任何时候为其添加 getter 或 setter 方法。这个方法的第一个参数是你想定义 getter 或 setter 方法的对象，第二个参数是一个对象，这个对象的属性名用作 getter 或 setter 的名字，属性名对应的属性值用作定义 getter 或 setter 方法的函数，下面是一个例子定义了和前面例子一样的 getter 和 setter 方法：

```javascript
var o = { a: 0 };

Object.defineProperties(o, {
  b: {
    get: function () {
      return this.a + 1;
    },
  },
  c: {
    set: function (x) {
      this.a = x / 2;
    },
  },
});

o.c = 10; // Runs the setter, which assigns 10 / 2 (5) to the 'a' property
console.log(o.b); // Runs the getter, which yields a + 1 or 6
```
这两种定义方式的选择取决于你的编程风格和手头的工作量。当你定义一个原型准备进行初始化时，可以选择第一种方式，这种方式更简洁和自然。但是，当你需要添加 getter 和 setter 方法 —— 因为并没有编写原型或者特定的对象 ——使用第二种方式更好。第二种方式可能更能表现 JavaScript 语法的动态特性——但也会使代码变得难以阅读和理解。

> # 类

> ## 初始化

Similar to functions, class declarations also have their expression counterparts.

```javascript
const MyClass = class {
  // Class body...
};
```

Class expressions can have names as well. The expression's name is only visible to the class's body.

```javascript
const MyClass = class MyClassLongerName {
  // Class body. Here MyClass and MyClassLongerName point to the same class.
};
new MyClassLongerName(); // ReferenceError: MyClassLongerName is not defined
```

> ### 类不能提升

```javascript
console.log(Color)//ReferenceError: Cannot access 'Color' before initialization
class Color {
    constructor(...values) {
      this.values = values;
    }
  }

```

> ## 方法

Without methods, you may be tempted to define the function within the constructor:

```javascript
class Color {
  constructor(r, g, b) {
    this.values = [r, g, b];
    this.getRed = function () {
      return this.values[0];
    };
  }
}

console.log(new Color().getRed === new Color().getRed); // false
```
```javascript
class Color {
    constructor(...values) {
      this.values = values;
    }
    disp(){
        console.log(this.values)
    }
  }
console.log(new Color().disp===new Color().disp)
```

This also works. However, a problem is that this creates a new function every time a Color instance is created, even when they all do the same thing!

In contrast, if you use a method, it will be shared between all instances. A function can be shared between all instances, but still have its behavior differ when different instances call it, because the value of this is different. 

> ## private

In order to refer to a private field anywhere in the class, you must declare it in the class body (you can't create a private property on the fly

{{< admonition type=info title="属性，方法，get，set都能是私有" open=false >}}
{{< /admonition >}}

{{< admonition type=info title="Chrome exception" open=false >}}
Code run in the Chrome console can access private properties outside the class. This is a DevTools-only relaxation of the JavaScript syntax restriction.
{{< /admonition >}}

> ### 同类可以互相读写

A class method can read the private fields of other instances, as long as they belong to the same class.

```javascript

class Color {
    #values;
    constructor(r, g, b) {
      this.#values = [r, g, b];
    }
    redDifference(anotherColor) {
      // #values doesn't necessarily need to be accessed from this:
      // you can access private fields of other instances belonging
      // to the same class.
      anotherColor.#values=[1,2,3];
      return this.#values[0] - anotherColor.#values[0];
    }
    showV()
    {
        console.log(this.#values);
    }
  }
  
  const red = new Color(255, 0, 0);
  const crimson = new Color(220, 20, 60);
  red.redDifference(crimson); // 35
//   console.log()
crimson.showV()

```

> ### 私有属性不存在去访问会直接报错


和公有属性不同


> ### 派生类对象不可访问基类对象

Derived classes don't have access to the parent class's private fields — this is another key aspect to JavaScript private fields being "hard private". Private fields are scoped to the class body itself and do not grant access to any outside code.

```javascript
class ColorWithAlpha extends Color {
  log() {
    console.log(this.#values); // SyntaxError: Private field '#values' must be declared in an enclosing class
  }
}
```


> ## static

they are not accessible from instances.
```javascript
console.log(new Color(0, 0, 0).isValid); // undefined

```

> ### static initialization block

There is also a special construct called a static initialization block, which is a block of code that runs when the class is first loaded.

```javascript
class MyClass {
  static {
    MyClass.myStaticProperty = "foo";
  }
}

console.log(MyClass.myStaticProperty); // 'foo'
```

> ### super

You can have code before super(), but you cannot access this before super() — the language prevents you from accessing the uninitialized this.

```javascript
class ColorWithAlpha extends Color {
  #alpha;
  constructor(r, g, b, a) {
      this.#alpha = a; //ReferenceError: Color is not defined
    super(r, g, b);
  }
  get alpha() {
    return this.#alpha;
  }
  set alpha(value) {
    if (value < 0 || value > 1) {
      throw new RangeError("Alpha value must be between 0 and 1");
    }
    this.#alpha = value;
  }
}

```

> ## Promise

> ### Always return when next function has a argument

Always return results when next function has a argument, otherwise callbacks won't catch the result of a previous promise (with arrow functions, () => x is short for () => { return x; }). If the previous handler started a promise but did not return it, there's no way to track its settlement anymore, and the promise is said to be "floating".

```javascript
doSomething()
  .then((url) => {
    // I forgot to return this
    fetch(url);
  })
  .then((result) => {
    // result is undefined, because nothing is returned from
    // the previous handler.
    // There's no way to know the return value of the fetch()
    // call anymore, or whether it succeeded at all.
  });
```

This may be worse if you have race conditions — if the promise from the last handler is not returned, the next then handler will be called early, and any value it reads may be incomplete.

```javascript
const listOfIngredients = [];

doSomething()
  .then((url) => {
    // I forgot to return this
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        listOfIngredients.push(data);
      });
  })
  .then(() => {
    console.log(listOfIngredients);
    // Always [], because the fetch request hasn't completed yet.
  });
```


> ## DOM

> ### 捕获和冒泡


都是冒泡，内部元素的事件会先被触发，然后再触发外部元素，即： <p> 元素的点击事件先触发，然后会触发 <div> 元素的点击事件。

都是捕获，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： <div> 元素的点击事件先触发 ，然后再触发 <p> 元素的点击事件。

既有捕获又有冒泡，就会先触发捕获再触发冒泡。

> ### insertBefore

如果给定的子节点是对文档中现有节点的引用，insertBefore() 会将其从当前位置移动到新位置

> ### HTMLCollection和NodeList

> #### 都不是数组

他们看起来可能是一个数组，但其实不是。

你可以像数组一样，使用索引来获取元素。

但无法使用数组的方法： valueOf(), pop(), push(), 或 join() 。

变成数组的方法：

```javascript
const fakeArr = document.getElementsByTagName('div');

const realArr = Array.prototype.slice.call(fakeArr);
```

或
```javascript
const fakeArr = document.getElementsByTagName('div');

const realArr = Array.apply(null,fakeArr);

```



或

```javascript
const fakeArr = document.getElementsByTagName('div');

const realArr = [...fakeArr]
```

或

```javascript
const fakeArr = document.getElementsByTagName('div');

const realArr = Array.from(fakearr)
```

> #### 区别

HTMLCollection是一个动态集合，NodeList是一个静态集合。

其中动态集合和静态集合的最大区别在于：动态集合指的就是元素集合会随着DOM树元素的增加而增加，减少而减少；静态集合则不会受DOM树元素变化的影响。

HTMLCollection是一个对象的索引，而NodeList是一个对象的克隆；所以当这个对象数据量非常大的时候，显然克隆这个对象所需要花费的时间是很长的。

