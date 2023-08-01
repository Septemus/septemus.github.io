# Javascript 学习笔记


> # 语法和数据类型


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
