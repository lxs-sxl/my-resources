# 2.1 ES6 let 与 const

ES2015(ES6) 新增加了两个重要的 JavaScript 关键字: let 和 const。

let 声明的变量只在 let 命令所在的代码块内有效。

const 声明一个只读的常量，一旦声明，常量的值就不能改变。

___

## let 命令

基本用法:

```
{
  let a = 0;
  a   // 0
}
a   // 报错 ReferenceError: a is not defined
```

**代码块内有效**

let 是在代码块内有效，var 是在全局范围内有效:

```
{ 
	let a = 0; var b = 1; 
} 
a   // ReferenceError: a is not defined
b	1
```

**不能重复声明**

let 只能声明一次 var 可以声明多次:

```
let a = 1; let a = 2; var b = 3; var b = 4; a b
```

for 循环计数器很适合用 let

```
for (var i = 0; i < 10; i++) { setTimeout(function(){ console.log(i); }) } for (let j = 0; j < 10; j++) { setTimeout(function(){ console.log(j); }) }
```

变量 i 是用 var 声明的，在全局范围内有效，所以全局中只有一个变量 i, 每次循环时，setTimeout 定时器里面的 i 指的是全局变量 i ，而循环里的十个 setTimeout 是在循环结束后才执行，所以此时的 i 都是 10。

变量 j 是用 let 声明的，当前的 j 只在本轮循环中有效，每次循环的 j 其实都是一个新的变量，所以 setTimeout 定时器里面的 j 其实是不同的变量，即最后输出 12345。（若每次循环的变量 j 都是重新声明的，如何知道前一个循环的值？这是因为 JavaScript 引擎内部会记住前一个循环的值）。

### 不存在变量提升

let 不存在变量提升，var 会变量提升:

```
console.log(a); 
let a = "apple"; 
console.log(b); 
var b = "banana";
```

变量 b 用 var 声明存在变量提升，所以当脚本开始运行的时候，b 已经存在了，但是还没有赋值，所以会输出 undefined。

变量 a 用 let 声明不存在变量提升，在声明变量 a 之前，a 不存在，所以会报错。

___

## const 命令

const 声明一个只读变量，声明之后不允许改变。意味着，一旦声明必须初始化，否则会报错。

基本用法:

```
const PI \= "3.1415926";

PI  // 3.1415926

const MY\_AGE;  // SyntaxError: Missing initializer in const declaration
```

暂时性死区:

```
var PI \= "a";

if(true){

  console.log(PI);  // Cannot access 'PI' before initialization

  const PI \= "3.1415926";

}
```

ES6 明确规定，代码块内如果存在 let 或者 const，代码块会对这些命令声明的变量从块的开始就形成一个封闭作用域。代码块内，在声明变量 PI 之前使用它会报错。

### 注意要点

const 如何做到变量在声明初始化之后不允许改变的？其实 const 其实保证的不是变量的值不变，而是保证变量指向的内存地址所保存的数据不允许改动。此时，你可能已经想到，简单类型和复合类型保存值的方式是不同的。是的，对于简单类型（数值 number、字符串 string 、布尔值 boolean）,值就保存在变量指向的那个内存地址，因此 const 声明的简单类型变量等同于常量。而复杂类型（对象 object，数组 array，函数 function），变量指向的内存地址其实是保存了一个指向实际数据的指针，所以 const 只能保证指针是固定的，至于指针指向的数据结构变不变就无法控制了，所以使用 const 声明复杂类型对象时要慎重。

# 2.2 ES6 解构赋值

## 概述

解构赋值是对赋值运算符的扩展。

他是一种针对数组或者对象进行模式匹配，然后对其中的变量进行赋值。

在代码书写上简洁且易读，语义更加清晰明了；也方便了复杂对象中数据字段获取。

___

## 解构模型

在解构中，有下面两部分参与：

解构的源，解构赋值表达式的右边部分。

解构的目标，解构赋值表达式的左边部分。

___

## 数组模型的解构（Array）

**基本**

```
let [a, b, c] = [1, 2, 3];
// a = 1
// b = 2
// c = 3
```

**可嵌套**

```
let [a, [[b], c]] = [1, [[2], 3]];
// a = 1
// b = 2
// c = 3
```

**可忽略**

```
let [a, , b] = [1, 2, 3];
// a = 1
// b = 3
```

**不完全解构**

```
let [a = 1, b] = []; // a = 1, b = undefined
```

**剩余运算符**

```
let [a, ...b] = [1, 2, 3];
//a = 1
//b = [2, 3]
```

**字符串等**

在数组的解构中，解构的目标若为可遍历对象，皆可进行解构赋值。可遍历对象即实现 Iterator 接口的数据。

```
let [a, b, c, d, e] = 'hello';
// a = 'h'
// b = 'e'
// c = 'l'
// d = 'l'
// e = 'o'
```

**解构默认值**

```
let [a = 2] = [undefined]; // a = 2
```

当解构模式有匹配结果，且匹配结果是 undefined 时，会触发默认值作为返回结果。

```
let [a = 3, b = a] = [];     // a = 3, b = 3
let [a = 3, b = a] = [1];    // a = 1, b = 1
let [a = 3, b = a] = [1, 2]; // a = 1, b = 2
```

-   a 与 b 匹配结果为 undefined ，触发默认值：`a = 3; b = a =3`
-   a 正常解构赋值，匹配结果：`a = 1`，b 匹配结果 `undefined` ，触发默认值：`b = a =1`
-   a 与 b 正常解构赋值，匹配结果：`a = 1，b = 2`

___

## 对象模型的解构（Object）

**基本**

```
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
// foo = 'aaa'
// bar = 'bbb'
 
let { baz : foo } = { baz : 'ddd' };
// foo = 'ddd'
```

**可嵌套可忽略**

```
let obj = {p: ['hello', {y: 'world'}] };
let {p: [x, { y }] } = obj;
// x = 'hello'
// y = 'world'
let obj = {p: ['hello', {y: 'world'}] };
let {p: [x, {  }] } = obj;
// x = 'hello'
```

**不完全解构**

```
let obj = {p: [{y: 'world'}] };
let {p: [{ y }, x ] } = obj;
// x = undefined
// y = 'world'
```

**剩余运算符**

```
let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40};
// a = 10
// b = 20
// rest = {c: 30, d: 40}
```

**解构默认值**

```
let {a = 10, b = 5} = {a: 3};
// a = 3; b = 5;
let {a: aa = 10, b: bb = 5} = {a: 3};
// aa = 3; bb = 5;
```

# 2.3 ES6 Symbol

## 概述

ES6 引入了一种新的原始数据类型 Symbol ，表示独一无二的值，最大的用法是用来定义对象的唯一属性名。

ES6 数据类型除了 Number 、 String 、 Boolean 、 Object、 null 和 undefined ，还新增了 Symbol 。

___

## 基本用法

Symbol 函数栈不能用 new 命令，因为 Symbol 是原始数据类型，不是对象。可以接受一个字符串作为参数，为新创建的 Symbol 提供描述，用来显示在控制台或者作为字符串的时候使用，便于区分。

```
let sy = Symbol("KK");
console.log(sy);   // Symbol(KK)
typeof(sy);        // "symbol"
 
// 相同参数 Symbol() 返回的值不相等
let sy1 = Symbol("kk"); 
sy === sy1;       // false
```



___

## 使用场景

### 作为属性名

**用法**

由于每一个 Symbol 的值都是不相等的，所以 Symbol 作为对象的属性名，可以保证属性不重名。

```
let sy = Symbol("key1");
 
// 写法1
let syObject = {};
syObject[sy] = "kk";
console.log(syObject);    // {Symbol(key1): "kk"}
 
// 写法2
let syObject = {
  [sy]: "kk"
};
console.log(syObject);    // {Symbol(key1): "kk"}
 
// 写法3
let syObject = {};
Object.defineProperty(syObject, sy, {value: "kk"});
console.log(syObject);   // {Symbol(key1): "kk"}
```

Symbol 作为对象属性名时不能用.运算符，要用方括号。因为.运算符后面是字符串，所以取到的是字符串 sy 属性，而不是 Symbol 值 sy 属性。

```
let syObject = {};
syObject[sy] = "kk";
 
syObject[sy];  // "kk"
syObject.sy;   // undefined
```



### 注意点

Symbol 值作为属性名时，该属性是公有属性不是私有属性，可以在类的外部访问。但是不会出现在 for...in 、 for...of 的循环中，也不会被 Object.keys() 、 Object.getOwnPropertyNames() 返回。如果要读取到一个对象的 Symbol 属性，可以通过 Object.getOwnPropertySymbols() 和Reflect.ownKeys() 取到。

```
let syObject = {};
syObject[sy] = "kk";
console.log(syObject);
 
for (let i in syObject) {
  console.log(i);
}    // 无输出
 
Object.keys(syObject);                     // []
Object.getOwnPropertySymbols(syObject);    // [Symbol(key1)]
Reflect.ownKeys(syObject);                 // [Symbol(key1)]
```



### 定义常量

在 ES5 使用字符串表示常量。例如：

```
const COLOR_RED = "red";
const COLOR_YELLOW = "yellow";
const COLOR_BLUE = "blue";
```

但是用字符串不能保证常量是独特的，这样会引起一些问题：

```
const COLOR_RED = "red";
const COLOR_YELLOW = "yellow";
const COLOR_BLUE = "blue";
const MY_BLUE = "blue";
 
function ColorException(message) {
   this.message = message;
   this.name = "ColorException";
}
 
function getConstantName(color) {
    switch (color) {
        case COLOR_RED :
            return "COLOR_RED";
        case COLOR_YELLOW :
            return "COLOR_YELLOW ";
        case COLOR_BLUE:
            return "COLOR_BLUE";
        case MY_BLUE:
            return "MY_BLUE";         
        default:
            throw new ColorException("Can't find this color");
    }
}
 
try {
   
   var color = "green"; // green 引发异常
   var colorName = getConstantName(color);
} catch (e) {
   var colorName = "unknown";
   console.log(e.message, e.name); // 传递异常对象到错误处理
}
```

但是使用 Symbol 定义常量，这样就可以保证这一组常量的值都不相等。用 Symbol 来修改上面的例子。

```
const COLOR_RED = Symbol("red");
const COLOR_YELLOW = Symbol("yellow");
const COLOR_BLUE = Symbol("blue");
 
function ColorException(message) {
   this.message = message;
   this.name = "ColorException";
}
function getConstantName(color) {
    switch (color) {
        case COLOR_RED :
            return "COLOR_RED";
        case COLOR_YELLOW :
            return "COLOR_YELLOW ";
        case COLOR_BLUE:
            return "COLOR_BLUE";
        default:
            throw new ColorException("Can't find this color");
    }
}
 
try {
   
   var color = "green"; // green 引发异常
   var colorName = getConstantName(color);
} catch (e) {
   var colorName = "unknown";
   console.log(e.message, e.name); // 传递异常对象到错误处理
}
```

Symbol 的值是唯一的，所以不会出现相同值得常量，即可以保证 switch 按照代码预想的方式执行。

### Symbol.for()

Symbol.for() 类似单例模式，首先会在全局搜索被登记的 Symbol 中是否有该字符串参数作为名称的 Symbol 值，如果有即返回该 Symbol 值，若没有则新建并返回一个以该字符串参数为名称的 Symbol 值，并登记在全局环境中供搜索。

```
let yellow = Symbol("Yellow");
let yellow1 = Symbol.for("Yellow");
yellow === yellow1;      // false
 
let yellow2 = Symbol.for("Yellow");
yellow1 === yellow2;     // true
```



### Symbol.keyFor()

Symbol.keyFor() 返回一个已登记的 Symbol 类型值的 key ，用来检测该字符串参数作为名称的 Symbol 值是否已被登记。

```
let yellow1 = Symbol.for("Yellow");
Symbol.keyFor(yellow1);    // "Yellow"
```

# 3.1.1 ES6 Map 与 Set

## Map 对象

Map 对象保存键值对。任何值(对象或者原始值) 都可以作为一个键或一个值。

## Maps 和 Objects 的区别

-   一个 Object 的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值。
-   Map 中的键值是有序的（FIFO 原则），而添加到对象中的键则不是。
-   Map 的键值对个数可以从 size 属性获取，而 Object 的键值对个数只能手动计算。
-   Object 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。

![](https://www.runoob.com/wp-content/uploads/2018/12/1_HmXTMmVps1oJ7MU-odCpUA.jpeg)

### Map 中的 key

**key 是字符串**

```
var myMap = new Map();
var keyString = "a string"; 
 
myMap.set(keyString, "和键'a string'关联的值");
 
myMap.get(keyString);    // "和键'a string'关联的值"
myMap.get("a string");   // "和键'a string'关联的值"
                         // 因为 keyString === 'a string'
```

**key 是对象**

```
var myMap = new Map();
var keyObj = {}, 
 
myMap.set(keyObj, "和键 keyObj 关联的值");

myMap.get(keyObj); // "和键 keyObj 关联的值"
myMap.get({}); // undefined, 因为 keyObj !== {}
```

**key 是函数**

```
var myMap = new Map();
var keyFunc = function () {}, // 函数
 
myMap.set(keyFunc, "和键 keyFunc 关联的值");
 
myMap.get(keyFunc); // "和键 keyFunc 关联的值"
myMap.get(function() {}) // undefined, 因为 keyFunc !== function () {}
```

**key 是 NaN**

```
var myMap = new Map();
myMap.set(NaN, "not a number");
 
myMap.get(NaN); // "not a number"
 
var otherNaN = Number("foo");
myMap.get(otherNaN); // "not a number"
```

虽然 NaN 和任何值甚至和自己都不相等(NaN !== NaN 返回true)，NaN作为Map的键来说是没有区别的。

### Map 的迭代

对 Map 进行遍历，以下两个最高级。

### for...of

```
var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 将会显示两个 log。 一个是 "0 = zero" 另一个是 "1 = one"
for (var [key, value] of myMap) {
  console.log(key + " = " + value);
}
for (var [key, value] of myMap.entries()) {
  console.log(key + " = " + value);
}
/* 这个 entries 方法返回一个新的 Iterator 对象，它按插入顺序包含了 Map 对象中每个元素的 [key, value] 数组。 */
 
// 将会显示两个log。 一个是 "0" 另一个是 "1"
for (var key of myMap.keys()) {
  console.log(key);
}
/* 这个 keys 方法返回一个新的 Iterator 对象， 它按插入顺序包含了 Map 对象中每个元素的键。 */
 
// 将会显示两个log。 一个是 "zero" 另一个是 "one"
for (var value of myMap.values()) {
  console.log(value);
}
/* 这个 values 方法返回一个新的 Iterator 对象，它按插入顺序包含了 Map 对象中每个元素的值。 */
```



### forEach()

```
var myMap = new Map();
myMap.set(0, "zero");
myMap.set(1, "one");
 
// 将会显示两个 logs。 一个是 "0 = zero" 另一个是 "1 = one"
myMap.forEach(function(value, key) {
  console.log(key + " = " + value);
}, myMap)
```



### Map 对象的操作

**Map 与 Array的转换**

```
var kvArray = [["key1", "value1"], ["key2", "value2"]];
 
// Map 构造函数可以将一个 二维 键值对数组转换成一个 Map 对象
var myMap = new Map(kvArray);
 
// 使用 Array.from 函数可以将一个 Map 对象转换成一个二维键值对数组
var outArray = Array.from(myMap);
```

**Map 的克隆**

```
var myMap1 = new Map([["key1", "value1"], ["key2", "value2"]]);
var myMap2 = new Map(myMap1);
 
console.log(original === clone); 
// 打印 false。 Map 对象构造函数生成实例，迭代出新的对象。
```

**Map 的合并**

```
var first = new Map([[1, 'one'], [2, 'two'], [3, 'three'],]);
var second = new Map([[1, 'uno'], [2, 'dos']]);
 
// 合并两个 Map 对象时，如果有重复的键值，则后面的会覆盖前面的，对应值即 uno，dos， three
var merged = new Map([...first, ...second]);
```

___

## Set 对象

Set 对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用。

### Set 中的特殊值

Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

-   +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复；
-   undefined 与 undefined 是恒等的，所以不重复；
-   NaN 与 NaN 是不恒等的，但是在 Set 中只能存一个，不重复。

**代码**

```
let mySet = new Set();
 
mySet.add(1); // Set(1) {1}
mySet.add(5); // Set(2) {1, 5}
mySet.add(5); // Set(2) {1, 5} 这里体现了值的唯一性
mySet.add("some text"); 
// Set(3) {1, 5, "some text"} 这里体现了类型的多样性
var o = {a: 1, b: 2}; 
mySet.add(o);
mySet.add({a: 1, b: 2}); 
// Set(5) {1, 5, "some text", {…}, {…}} 
// 这里体现了对象之间引用不同不恒等，即使值相同，Set 也能存储
```



### 类型转换

**Array**

```
// Array 转 Set
var mySet = new Set(["value1", "value2", "value3"]);
// 用...操作符，将 Set 转 Array
var myArray = [...mySet];
String
// String 转 Set
var mySet = new Set('hello');  // Set(4) {"h", "e", "l", "o"}
// 注：Set 中 toString 方法是不能将 Set 转换成 String
```

### Set 对象作用

**数组去重**

```
var mySet = new Set([1, 2, 3, 4, 4]);
[...mySet]; // [1, 2, 3, 4]
```

**并集**

```
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var union = new Set([...a, ...b]); // {1, 2, 3, 4}
```

**交集**

```
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var intersect = new Set([...a].filter(x => b.has(x))); // {2, 3}
```

**差集**

```
var a = new Set([1, 2, 3]);
var b = new Set([4, 3, 2]);
var difference = new Set([...a].filter(x => !b.has(x))); // {1}
```

# 3.1.2 ES6 Reflect 与 Proxy

## 概述

Proxy 与 Reflect 是 ES6 为了操作对象引入的 API 。

Proxy 可以对目标对象的读取、函数调用等操作进行拦截，然后进行操作处理。它不直接操作对象，而是像代理模式，通过对象的代理对象进行操作，在进行这些操作时，可以添加一些需要的额外操作。

Reflect 可以用于获取目标对象的行为，它与 Object 类似，但是更易读，为操作对象提供了一种更优雅的方式。它的方法与 Proxy 是对应的。

___

## 基本用法

### Proxy

一个 Proxy 对象由两个部分组成： target 、 handler 。在通过 Proxy 构造函数生成实例对象时，需要提供这两个参数。 target 即目标对象， handler 是一个对象，声明了代理 target 的指定行为。

```
let target = {
    name: 'Tom',
    age: 24
}
let handler = {
    get: function(target, key) {
        console.log('getting '+key);
        return target[key]; // 不是target.key
    },
    set: function(target, key, value) {
        console.log('setting '+key);
        target[key] = value;
    }
}
let proxy = new Proxy(target, handler)
proxy.name     // 实际执行 handler.get
proxy.age = 25 // 实际执行 handler.set
// getting name
// setting age
// 25
 
// target 可以为空对象
let targetEpt = {}
let proxyEpt = new Proxy(targetEpt, handler)
// 调用 get 方法，此时目标对象为空，没有 name 属性
proxyEpt.name // getting name
// 调用 set 方法，向目标对象中添加了 name 属性
proxyEpt.name = 'Tom'
// setting name
// "Tom"
// 再次调用 get ，此时已经存在 name 属性
proxyEpt.name
// getting name
// "Tom"
 
// 通过构造函数新建实例时其实是对目标对象进行了浅拷贝，因此目标对象与代理对象会互相
// 影响
targetEpt
// {name: "Tom"}
 
// handler 对象也可以为空，相当于不设置拦截操作，直接访问目标对象
let targetEmpty = {}
let proxyEmpty = new Proxy(targetEmpty,{})
proxyEmpty.name = "Tom"
targetEmpty // {name: "Tom"}
```



### 实例方法

```
get(target, propKey, receiver)
```

用于 target 对象上 propKey 的读取操作。

```
let exam ={
    name: "Tom",
    age: 24
}
let proxy = new Proxy(exam, {
  get(target, propKey, receiver) {
    console.log('Getting ' + propKey);
    return target[propKey];
  }
})
proxy.name 
// Getting name
// "Tom"
```

get() 方法可以继承。

```
let proxy = new Proxy({}, {
  get(target, propKey, receiver) {
      // 实现私有属性读取保护
      if(propKey[0] === '_'){
          throw new Erro(`Invalid attempt to get private     "${propKey}"`);
      }
      console.log('Getting ' + propKey);
      return target[propKey];
  }
});
 
let obj = Object.create(proxy);
obj.name
// Getting name
```



```
set(target, propKey, value, receiver)
```

用于拦截 target 对象上的 propKey 的赋值操作。如果目标对象自身的某个属性，不可写且不可配置，那么set方法将不起作用。

```
let validator = {
    set: function(obj, prop, value) {
        if (prop === 'age') {
            if (!Number.isInteger(value)) {
                throw new TypeError('The age is not an integer');
            }
            if (value > 200) {
                throw new RangeError('The age seems invalid');
            }
        }
        // 对于满足条件的 age 属性以及其他属性，直接保存
        obj[prop] = value;
    }
};
let proxy= new Proxy({}, validator)
proxy.age = 100;
proxy.age           // 100
proxy.age = 'oppps' // 报错
proxy.age = 300     // 报错
```

第四个参数 receiver 表示原始操作行为所在对象，一般是 Proxy 实例本身。

```
const handler = {
    set: function(obj, prop, value, receiver) {
        obj[prop] = receiver;
    }
};
const proxy = new Proxy({}, handler);
proxy.name= 'Tom';
proxy.name=== proxy // true
 
const exam = {}
Object.setPrototypeOf(exam, proxy)
exam.name = "Tom"
exam.name === exam // true
```

注意，严格模式下，set代理如果没有返回true，就会报错。

### apply(target, ctx, args)

用于拦截函数的调用、call 和 reply 操作。target 表示目标对象，ctx 表示目标对象上下文，args 表示目标对象的参数数组。

```
function sub(a, b){
    return a - b;
}
let handler = {
    apply: function(target, ctx, args){
        console.log('handle apply');
        return Reflect.apply(...arguments);
    }
}
let proxy = new Proxy(sub, handler)
proxy(2, 1) 
// handle apply
// 1
```



```
has(target, propKey)
```

用于拦截 HasProperty 操作，即在判断 target 对象是否存在 propKey 属性时，会被这个方法拦截。此方法不判断一个属性是对象自身的属性，还是继承的属性。

```
let  handler = {
    has: function(target, propKey){
        console.log("handle has");
        return propKey in target;
    }
}
let exam = {name: "Tom"}
let proxy = new Proxy(exam, handler)
'name' in proxy
// handle has
// true
```

注意：此方法不拦截 for ... in 循环。

```
construct(target, args)
```

用于拦截 new 命令。返回值必须为对象。

```
let handler = {
    construct: function (target, args, newTarget) {
        console.log('handle construct')
        return Reflect.construct(target, args, newTarget)  
    }
}
class Exam { 
    constructor (name) {  
        this.name = name 
    }
}
let ExamProxy = new Proxy(Exam, handler)
let proxyObj = new ExamProxy('Tom')
console.log(proxyObj)
// handle construct
// exam {name: "Tom"}
```



```
deleteProperty(target, propKey)
```

用于拦截 delete 操作，如果这个方法抛出错误或者返回 false ，propKey 属性就无法被 delete 命令删除。

```
defineProperty(target, propKey, propDesc)
```

用于拦截 Object.definePro若目标对象不可扩展，增加目标对象上不存在的属性会报错；若属性不可写或不可配置，则不能改变这些属性。

```
let handler = {
    defineProperty: function(target, propKey, propDesc){
        console.log("handle defineProperty");
        return true;
    }
}
let target = {}
let proxy = new Proxy(target, handler)
proxy.name = "Tom"
// handle defineProperty
target
// {name: "Tom"}
 
// defineProperty 返回值为false，添加属性操作无效
let handler1 = {
    defineProperty: function(target, propKey, propDesc){
        console.log("handle defineProperty");
        return false;
    }
}
let target1 = {}
let proxy1 = new Proxy(target1, handler1)
proxy1.name = "Jerry"
target1
// {}
```

**erty 操作**

```
getOwnPropertyDescriptor(target, propKey)
```

用于拦截 Object.getOwnPropertyD() 返回值为属性描述对象或者 undefined 。

```
let handler = {
    getOwnPropertyDescriptor: function(target, propKey){
        return Object.getOwnPropertyDescriptor(target, propKey);
    }
}
let target = {name: "Tom"}
let proxy = new Proxy(target, handler)
Object.getOwnPropertyDescriptor(proxy, 'name')
// {value: "Tom", writable: true, enumerable: true, configurable: 
// true}
```

**ptor 属性**

```
getPrototypeOf(target)
```

主要用于拦截获取对象原型的操作。包括以下操作：

```
- Object.prototype._proto_
- Object.prototype.isPrototypeOf()
- Object.getPrototypeOf()
- Reflect.getPrototypeOf()
- instanceof
```

```
let exam = {}
let proxy = new Proxy({},{
    getPrototypeOf: function(target){
        return exam;
    }
})
Object.getPrototypeOf(proxy) // {}
```

注意，返回值必须是对象或者 null ，否则报错。另外，如果目标对象不可扩展（non-extensible），getPrototypeOf 方法必须返回目标对象的原型对象。

```
let proxy = new Proxy({},{
    getPrototypeOf: function(target){
        return true;
    }
})
Object.getPrototypeOf(proxy)
// TypeError: 'getPrototypeOf' on proxy: trap returned neither object // nor null
```



```
isExtensible(target)
```

用于拦截 Object.isExtensible 操作。

该方法只能返回布尔值，否则返回值会被自动转为布尔值。

```
let proxy = new Proxy({},{
    isExtensible:function(target){
        return true;
    }
})
Object.isExtensible(proxy) // true
```

注意：它的返回值必须与目标对象的isExtensible属性保持一致，否则会抛出错误。

```
let proxy = new Proxy({},{
    isExtensible:function(target){
        return false;
    }
})
Object.isExtensible(proxy)
// TypeError: 'isExtensible' on proxy: trap result does not reflect 
// extensibility of proxy target (which is 'true')
```

```
ownKeys(target)
```

用于拦截对象自身属性的读取操作。主要包括以下操作：

```
- Object.getOwnPropertyNames()
- Object.getOwnPropertySymbols()
- Object.keys()
- or...in
```

方法返回的数组成员，只能是字符串或 Symbol 值，否则会报错。

若目标对象中含有不可配置的属性，则必须将这些属性在结果中返回，否则就会报错。

若目标对象不可扩展，则必须全部返回且只能返回目标对象包含的所有属性，不能包含不存在的属性，否则也会报错。

```
let proxy = new Proxy( {
  name: "Tom",
  age: 24
}, {
    ownKeys(target) {
        return ['name'];
    }
});
Object.keys(proxy)
// [ 'name' ]f返回结果中，三类属性会被过滤：
//          - 目标对象上没有的属性
//          - 属性名为 Symbol 值的属性
//          - 不可遍历的属性
 
let target = {
  name: "Tom",
  [Symbol.for('age')]: 24,
};
// 添加不可遍历属性 'gender'
Object.defineProperty(target, 'gender', {
  enumerable: false,
  configurable: true,
  writable: true,
  value: 'male'
});
let handler = {
    ownKeys(target) {
        return ['name', 'parent', Symbol.for('age'), 'gender'];
    }
};
let proxy = new Proxy(target, handler);
Object.keys(proxy)
// ['name']
```

```
preventExtensions(target)
```

拦截 Object.preventExtensions 操作。

该方法必须返回一个布尔值，否则会自动转为布尔值。

```
// 只有目标对象不可扩展时（即 Object.isExtensible(proxy) 为 false ），
// proxy.preventExtensions 才能返回 true ，否则会报错
var proxy = new Proxy({}, {
  preventExtensions: function(target) {
    return true;
  }
});
// 由于 proxy.preventExtensions 返回 true，此处也会返回 true，因此会报错
Object.preventExtensions(proxy) 被// TypeError: 'preventExtensions' on proxy: trap returned truish but // the proxy target is extensible
 
// 解决方案
 var proxy = new Proxy({}, {
  preventExtensions: function(target) {
    // 返回前先调用 Object.preventExtensions
    Object.preventExtensions(target);
    return true;
  }
});
Object.preventExtensions(proxy)
// Proxy {}
```

```
setPrototypeOf
```

主要用来拦截 Object.setPrototypeOf 方法。

返回值必须为布尔值，否则会被自动转为布尔值。

若目标对象不可扩展，setPrototypeOf 方法不得改变目标对象的原型。

```
let proto = {}
let proxy = new Proxy(function () {}, {
    setPrototypeOf: function(target, proto) {
        console.log("setPrototypeOf");
        return true;
    }
}
);
Object.setPrototypeOf(proxy, proto);
// setPrototypeOf
```

```
Proxy.revocable()
```

用于返回一个可取消的 Proxy 实例。

```
let {proxy, revoke} = Proxy.revocable({}, {});
proxy.name = "Tom";
revoke();
proxy.name 
// TypeError: Cannot perform 'get' on a proxy that has been revoked
```

### Reflect

ES6 中将 Object 的一些明显属于语言内部的方法移植到了 Reflect 对象上（当前某些方法会同时存在于 Object 和 Reflect 对象上），未来的新方法会只部署在 Reflect 对象上。

Reflect 对象对某些方法的返回结果进行了修改，使其更合理。

Reflect 对象使用函数的方式实现了 Object 的命令式操作。

**静态方法**

```
Reflect.get(target, name, receiver)
```

查找并返回 target 对象的 name 属性。

```
let exam = {
    name: "Tom",
    age: 24,
    get info(){
        return this.name + this.age;
    }
}
Reflect.get(exam, 'name'); // "Tom"
 
// 当 target 对象中存在 name 属性的 getter 方法， getter 方法的 this 会绑定 // receiver
let receiver = {
    name: "Jerry",
    age: 20
}
Reflect.get(exam, 'info', receiver); // Jerry20
 
// 当 name 为不存在于 target 对象的属性时，返回 undefined
Reflect.get(exam, 'birth'); // undefined
 
// 当 target 不是对象时，会报错
Reflect.get(1, 'name'); // TypeError
```

```
Reflect.set(target, name, value, receiver)
```

将 target 的 name 属性设置为 value。返回值为 boolean ，true 表示修改成功，false 表示失败。当 target 为不存在的对象时，会报错。

```
let exam = {
    name: "Tom",
    age: 24,
    get info(){
        return this.name + this.age;
    }
}
Reflect.get(exam, 'name'); // "Tom"
 
// 当 target 对象中存在 name 属性的 getter 方法， getter 方法的 this 会绑定 // receiver
let receiver = {
    name: "Jerry",
    age: 20
}
Reflect.get(exam, 'info', receiver); // Jerry20
 
// 当 name 为不存在于 target 对象的属性时，返回 undefined
Reflect.get(exam, 'birth'); // undefined
 
// 当 target 不是对象时，会报错
Reflect.get(1, 'name'); // TypeError
```

```
Reflect.has(obj, name)
```

是 name in obj 指令的函数化，用于查找 name 属性在 obj 对象中是否存在。返回值为 boolean。如果 obj 不是对象则会报错 TypeError。

```
let exam = {
    name: "Tom",
    age: 24
}
Reflect.has(exam, 'name'); // true
```

```
Reflect.deleteProperty(obj, property)
```

是 delete obj[property\] 的函数化，用于删除 obj 对象的 property 属性，返回值为 boolean。如果 obj 不是对象则会报错 TypeError。

```
let exam = {
    name: "Tom",
    age: 24
}
Reflect.deleteProperty(exam , 'name'); // true
exam // {age: 24} 
// property 不存在时，也会返回 true
Reflect.deleteProperty(exam , 'name'); // true
```

```
Reflect.construct(obj, args)
```

等同于 new target(...args)。

```
function exam(name){
    this.name = name;
}
Reflect.construct(exam, ['Tom']); // exam {name: "Tom"}
```

```
Reflect.getPrototypeOf(obj)
```

用于读取 obj 的 \_proto\_ 属性。在 obj 不是对象时不会像 Object 一样把 obj 转为对象，而是会报错。

```
class Exam{}
let obj = new Exam()
Reflect.getPrototypeOf(obj) === Exam.prototype // true
```

```
Reflect.setPrototypeOf(obj, newProto)
```

用于设置目标对象的 prototype。

```
let obj ={}
Reflect.setPrototypeOf(obj, Array.prototype); // true
```

```
Reflect.apply(func, thisArg, args)
```

等同于 Function.prototype.apply.call(func, thisArg, args) 。func 表示目标函数；thisArg 表示目标函数绑定的 this 对象；args 表示目标函数调用时传入的参数列表，可以是数组或类似数组的对象。若目标函数无法调用，会抛出 TypeError 。

```
Reflect.apply(Math.max, Math, [1, 3, 5, 3, 1]); // 5
```

```
Reflect.defineProperty(target, propertyKey, attributes)
```

用于为目标对象定义属性。如果 target 不是对象，会抛出错误。

```
let myDate= {}
Reflect.defineProperty(MyDate, 'now', {
  value: () => Date.now()
}); // true
 
const student = {};
Reflect.defineProperty(student, "name", {value: "Mike"}); // true
student.name; // "Mike"
```

```
Reflect.getOwnPropertyDescriptor(target, propertyKey)
```

用于得到 target 对象的 propertyKey 属性的描述对象。在 target 不是对象时，会抛出错误表示参数非法，不会将非对象转换为对象。

```
var exam = {}
Reflect.defineProperty(exam, 'name', {
  value: true,
  enumerable: false,
})
Reflect.getOwnPropertyDescriptor(exam, 'name')
// { configurable: false, enumerable: false, value: true, writable:
// false}
 
 
// propertyKey 属性在 target 对象中不存在时，返回 undefined
Reflect.getOwnPropertyDescriptor(exam, 'age') // undefined
```

```
Reflect.isExtensible(target)
```

用于判断 target 对象是否可扩展。返回值为 boolean 。如果 target 参数不是对象，会抛出错误。

```
let exam = {}
Reflect.isExtensible(exam) // true
```

```
Reflect.preventExtensions(target)
```

用于让 target 对象变为不可扩展。如果 target 参数不是对象，会抛出错误。

```
let exam = {}
Reflect.preventExtensions(exam) // true
```

```
Reflect.ownKeys(target)
```

用于返回 target 对象的所有属性，等同于 Object.getOwnPropertyNames 与Object.getOwnPropertySymbols 之和。

```
var exam = {
  name: 1,
  [Symbol.for('age')]: 4
}
Reflect.ownKeys(exam) // ["name", Symbol(age)]
```

___

## 组合使用

Reflect 对象的方法与 Proxy 对象的方法是一一对应的。所以 Proxy 对象的方法可以通过调用 Reflect 对象的方法获取默认行为，然后进行额外操作。

```
let exam = {
    name: "Tom",
    age: 24
}
let handler = {
    get: function(target, key){
        console.log("getting "+key);
        return Reflect.get(target,key);
    },
    set: function(target, key, value){
        console.log("setting "+key+" to "+value)
        Reflect.set(target, key, value);
    }
}
let proxy = new Proxy(exam, handler)
proxy.name = "Jerry"
proxy.name
// setting name to Jerry
// getting name
// "Jerry"
```

### 使用场景拓展

**实现观察者模式**

```
// 定义 Set 集合
const queuedObservers = new Set();
// 把观察者函数都放入 Set 集合中
const observe = fn => queuedObservers.add(fn);
// observable 返回原始对象的代理，拦截赋值操作
const observable = obj => new Proxy(obj, {set});
function set(target, key, value, receiver) {
  // 获取对象的赋值操作
  const result = Reflect.set(target, key, value, receiver);
  // 执行所有观察者
  queuedObservers.forEach(observer => observer());
  // 执行赋值操作
  return result;
}
```

# 3.2.1 ES6 字符串

### 拓展的方法

### 子串的识别

ES6 之前判断字符串是否包含子串，用 indexOf 方法，ES6 新增了子串的识别方法。

-   **includes()**：返回布尔值，判断是否找到参数字符串。
-   **startsWith()**：返回布尔值，判断参数字符串是否在原字符串的头部。
-   **endsWith()**：返回布尔值，判断参数字符串是否在原字符串的尾部。

以上三个方法都可以接受两个参数，需要搜索的字符串，和可选的搜索起始位置索引。

```
let string = "apple,banana,orange";
string.includes("banana");     // true
string.startsWith("apple");    // true
string.endsWith("apple");      // false
string.startsWith("banana",6)  // true
```

**注意点：**

-   这三个方法只返回布尔值，如果需要知道子串的位置，还是得用 indexOf 和 lastIndexOf 。
-   这三个方法如果传入了正则表达式而不是字符串，会抛出错误。而 indexOf 和 lastIndexOf 这两个方法，它们会将正则表达式转换为字符串并搜索它。

### 字符串重复

repeat()：返回新的字符串，表示将字符串重复指定次数返回。

```
console.log("Hello,".repeat(2));  // "Hello,Hello,"
```

如果参数是小数，向下取整

```
console.log("Hello,".repeat(3.2));  // "Hello,Hello,Hello,"
```

如果参数是 0 至 -1 之间的小数，会进行取整运算，0 至 -1 之间的小数取整得到 -0 ，等同于 repeat 零次

```
console.log("Hello,".repeat(-0.5));  // "" 
```

如果参数是 NaN，等同于 repeat 零次

```
console.log("Hello,".repeat(NaN));  // "" 
```

如果参数是负数或者 Infinity ，会报错:

```
console.log("Hello,".repeat(-1));  
// RangeError: Invalid count value

console.log("Hello,".repeat(Infinity));  
// RangeError: Invalid count value
```

如果传入的参数是字符串，则会先将字符串转化为数字

```
console.log("Hello,".repeat("hh")); // ""
console.log("Hello,".repeat("2"));  // "Hello,Hello,"
```

### 字符串补全

-   **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
-   **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

以上两个方法接受两个参数，第一个参数是指定生成的字符串的最小长度，第二个参数是用来补全的字符串。如果没有指定第二个参数，默认用空格填充。

```
console.log("h".padStart(5,"o"));  // "ooooh"
console.log("h".padEnd(5,"o"));    // "hoooo"
console.log("h".padStart(5));      // "    h"
```

如果指定的长度小于或者等于原字符串的长度，则返回原字符串:

```
console.log("hello".padStart(5,"A"));  // "hello"
```

如果原字符串加上补全字符串长度大于指定长度，则截去超出位数的补全字符串:

```
console.log("hello".padEnd(10,",world!"));  // "hello,worl"
```

常用于补全位数：

```
console.log("123".padStart(10,"0"));  // "0000000123"
```

### 模板字符串

模板字符串相当于加强版的字符串，用反引号 \`,除了作为普通字符串，还可以用来定义多行字符串，还可以在字符串中加入变量和表达式。

**基本用法**

普通字符串

```
let string = `Hello'\n'world`;
console.log(string); 
// "Hello'
// 'world"
```

多行字符串:

```
let string1 =  `Hey,
can you stop angry now?`;
console.log(string1);
// Hey,
// can you stop angry now?
```

字符串插入变量和表达式。

变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式。

```
let name = "Mike";
let age = 27;
let info = `My Name is ${name},I am ${age+1} years old next year.`
console.log(info);
// My Name is Mike,I am 28 years old next year.
```

字符串中调用函数：

```
function f(){
  return "have fun!";
}
let string2= `Game start,${f()}`;
console.log(string2);  // Game start,have fun!
```

**注意要点**

模板字符串中的换行和空格都是会被保留的

```
innerHtml = `<ul>
  <li>menu</li>
  <li>mine</li>
</ul>
`;
console.log(innerHtml);
// 输出
<ul>
 <li>menu</li>
 <li>mine</li>
</ul>
```



### 标签模板

标签模板，是一个函数的调用，其中调用的参数是模板字符串。

```
alert`Hello world!`;
// 等价于
alert('Hello world!');
```

当模板字符串中带有变量，会将模板字符串参数处理成多个参数。

```
function f(stringArr,...values){
 let result = "";
 for(let i=0;i<stringArr.length;i++){
  result += stringArr[i];
  if(values[i]){
   result += values[i];
        }
    }
 return result;
}
let name = 'Mike';
let age = 27;
f`My Name is ${name},I am ${age+1} years old next year.`;
// "My Name is Mike,I am 28 years old next year."
 
f`My Name is ${name},I am ${age+1} years old next year.`;
// 等价于
f(['My Name is',',I am ',' years old next year.'],'Mike',28);
```

**应用**

过滤 HTML 字符串，防止用户输入恶意内容。

```
function f(stringArr,...values){
 let result = "";
 for(let i=0;i<stringArr.length;i++){
  result += stringArr[i];
   if(values[i]){
     result += String(values[i]).replace(/&/g, "&amp;")
               .replace(/</g, "&lt;")
               .replace(/>/g, "&gt;");
    }
 }
 return result;
}
name = '<Amy&MIke>';
f`<p>Hi, ${name}.I would like send you some message.</p>`;
// <p>Hi, &lt;Amy&amp;MIke&gt;.I would like send you some message.</p>
```

**国际化处理（转化多国语言）**

```
i18n`Hello ${name}, you are visitor number ${visitorNumber}.`;  
// 你好**，你是第**位访问者
```

# 3.2.2 ES6 数值

## 数值的表示

二进制表示法新写法: 前缀 0b 或 0B 。

```
console.log(0b11 === 3); // true
console.log(0B11 === 3); // true
```

八进制表示法新写法: 前缀 0o 或 0O 。

```
console.log(0o11 === 9); // true
console.log(0O11 === 9); // true
```

### 常量

```
Number.EPSILON
```

Number.EPSILON 属性表示 1 与大于 1 的最小浮点数之间的差。

它的值接近于 2.2204460492503130808472633361816E-16，或者 2-52。

测试数值是否在误差范围内:

```
0.1 + 0.2 === 0.3; // false
// 在误差范围内即视为相等
equal = (Math.abs(0.1 - 0.3 + 0.2) < Number.EPSILON); // true
```

### 属性特性

```
writable：false
enumerable：false
configurable：false
```

### 最大/最小安全整数

**安全整数**

安全整数表示在 JavaScript 中能够精确表示的整数，安全整数的范围在 2 的 -53 次方到 2 的 53 次方之间（不包括两个端点），超过这个范围的整数无法精确表示。

**最大安全整数**

安全整数范围的上限，即 2 的 53 次方减 1 。

```
Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2; // true
Number.MAX_SAFE_INTEGER === Number.MAX_SAFE_INTEGER + 1;     // false
Number.MAX_SAFE_INTEGER - 1 === Number.MAX_SAFE_INTEGER - 2; // false
```

**最小安全整数**

安全整数范围的下限，即 2 的 53 次方减 1 的负数。

```
Number.MIN_SAFE_INTEGER + 1 === Number.MIN_SAFE_INTEGER + 2; // false
Number.MIN_SAFE_INTEGER === Number.MIN_SAFE_INTEGER - 1;     // false
Number.MIN_SAFE_INTEGER - 1 === Number.MIN_SAFE_INTEGER - 2; // true
```

**属性特性**

```
writable：false
enumerable：false
configurable：false
```

### 方法

**Number 对象新方法**

```
Number.isFinite()
```

用于检查一个数值是否为有限的（ finite ），即不是 Infinity

```
console.log( Number.isFinite(1));   // true
console.log( Number.isFinite(0.1)); // true
 
// NaN 不是有限的
console.log( Number.isFinite(NaN)); // false
 
console.log( Number.isFinite(Infinity));  // false
console.log( Number.isFinite(-Infinity)); // false
 
// Number.isFinate 没有隐式的 Number() 类型转换，所有非数值都返回 false
console.log( Number.isFinite('foo')); // false
console.log( Number.isFinite('15'));  // false
console.log( Number.isFinite(true));  // false
Number.isNaN()
用于检查一个值是否为 NaN 。
console.log(Number.isNaN(NaN));      // true
console.log(Number.isNaN('true'/0)); // true
 
// 在全局的 isNaN() 中，以下皆返回 true，因为在判断前会将非数值向数值转换
// 而 Number.isNaN() 不存在隐式的 Number() 类型转换，非 NaN 全部返回 false
Number.isNaN("NaN");      // false
Number.isNaN(undefined);  // false
Number.isNaN({});         // false
Number.isNaN("true");     // false
```

**从全局移植到 Number 对象的方法**

逐步减少全局方法，用于全局变量的模块化。

方法的行为没有发生改变。

```
Number.parseInt()
```

用于将给定字符串转化为指定进制的整数。

```
// 不指定进制时默认为 10 进制
Number.parseInt('12.34'); // 12
Number.parseInt(12.34);   // 12
 
// 指定进制
Number.parseInt('0011',2); // 3
 
// 与全局的 parseInt() 函数是同一个函数
Number.parseInt === parseInt; // true
Number.parseFloat()
用于把一个字符串解析成浮点数。
Number.parseFloat('123.45')    // 123.45
Number.parseFloat('123.45abc') // 123.45
 
// 无法被解析成浮点数，则返回 NaN
Number.parseFloat('abc') // NaN
 
// 与全局的 parseFloat() 方法是同一个方法
Number.parseFloat === parseFloat // true
Number.isInteger()
用于判断给定的参数是否为整数。
Number.isInteger(value)
Number.isInteger(0); // true
// JavaScript 内部，整数和浮点数采用的是同样的储存方法,因此 1 与 1.0 被视为相同的值
Number.isInteger(1);   // true
Number.isInteger(1.0); // true
 
Number.isInteger(1.1);     // false
Number.isInteger(Math.PI); // false
 
// NaN 和正负 Infinity 不是整数
Number.isInteger(NaN);       // false
Number.isInteger(Infinity);  // false
Number.isInteger(-Infinity); // false
 
Number.isInteger("10");  // false
Number.isInteger(true);  // false
Number.isInteger(false); // false
Number.isInteger([1]);   // false
 
// 数值的精度超过 53 个二进制位时，由于第 54 位及后面的位被丢弃，会产生误判
Number.isInteger(1.0000000000000001) // true
 
// 一个数值的绝对值小于 Number.MIN_VALUE（5E-324），即小于 JavaScript 能够分辨
// 的最小值，会被自动转为 0，也会产生误判
Number.isInteger(5E-324); // false
Number.isInteger(5E-325); // true
Number.isSafeInteger()
用于判断数值是否在安全范围内。
Number.isSafeInteger(Number.MIN_SAFE_INTEGER - 1); // false
Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1); // false
```

___

## Math 对象的扩展

ES6 在 Math 对象上新增了 17 个数学相关的静态方法，这些方法只能在 Math 中调用。

**普通计算**

```
Math.cbrt
```

用于计算一个数的立方根。

```
Math.cbrt(1);  // 1
Math.cbrt(0);  // 0
Math.cbrt(-1); // -1
// 会对非数值进行转换
Math.cbrt('1'); // 1
 
// 非数值且无法转换为数值时返回 NaN
Math.cbrt('hhh'); // NaN
```

```
Math.imul
```

两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数。

```
// 大多数情况下，结果与 a * b 相同 
Math.imul(1, 2);   // 2
 
// 用于正确返回大数乘法结果中的低位数值
Math.imul(0x7fffffff, 0x7fffffff); // 1
```

```
Math.hypot
```

用于计算所有参数的平方和的平方根。

```
Math.hypot(3, 4); // 5
 
// 非数值会先被转换为数值后进行计算
Math.hypot(1, 2, '3'); // 3.741657386773941
Math.hypot(true);      // 1
Math.hypot(false);     // 0
 
// 空值会被转换为 0
Math.hypot();   // 0
Math.hypot([]); // 0
 
// 参数为 Infinity 或 -Infinity 返回 Infinity
Math.hypot(Infinity); // Infinity
Math.hypot(-Infinity); // Infinity
 
// 参数中存在无法转换为数值的参数时返回 NaN
Math.hypot(NaN);         // NaN
Math.hypot(3, 4, 'foo'); // NaN
Math.hypot({});          // NaN
```

```
Math.clz32
```

用于返回数字的32 位无符号整数形式的前导0的个数。

```
Math.clz32(0); // 32
Math.clz32(1); // 31
Math.clz32(0b01000000000100000000000000000000); // 1
 
// 当参数为小数时，只考虑整数部分
Math.clz32(0.5); // 32
 
// 对于空值或非数值，会转化为数值再进行计算
Math.clz32('1');       // 31
Math.clz32();          // 32
Math.clz32([]);        // 32
Math.clz32({});        // 32
Math.clz32(NaN);       // 32
Math.clz32(Infinity);  // 32
Math.clz32(-Infinity); // 32
Math.clz32(undefined); // 32
Math.clz32('hhh');     // 32
```

### 数字处理

```
Math.trunc
```

用于返回数字的整数部分。

```
Math.trunc(12.3); // 12
Math.trunc(12);   // 12
 
// 整数部分为 0 时也会判断符号
Math.trunc(-0.5); // -0
Math.trunc(0.5);  // 0
 
// Math.trunc 会将非数值转为数值再进行处理
Math.trunc("12.3"); // 12
 
// 空值或无法转化为数值时时返回 NaN
Math.trunc();           // NaN
Math.trunc(NaN);        // NaN
Math.trunc("hhh");      // NaN
Math.trunc("123.2hhh"); // NaN
```

```
Math.fround
```

用于获取数字的32位单精度浮点数形式。

```
// 对于 2 的 24 次方取负至 2 的 24 次方之间的整数（不含两个端点），返回结果与参数本身一致
Math.fround(-(2**24)+1);  // -16777215
Math.fround(2 ** 24 - 1); // 16777215
 
// 用于将 64 位双精度浮点数转为 32 位单精度浮点数
Math.fround(1.234) // 1.125
// 当小数的精度超过 24 个二进制位，会丢失精度
Math.fround(0.3); // 0.30000001192092896
// 参数为 NaN 或 Infinity 时返回本身
Math.fround(NaN)      // NaN
Math.fround(Infinity) // Infinity
 
// 参数为其他非数值类型时会将参数进行转换 
Math.fround('5');  // 5
Math.fround(true); // 1
Math.fround(null); // 0
Math.fround([]);   // 0
Math.fround({});   // NaN
```

### 判断

```
Math.sign
```

判断数字的符号（正、负、0）。

```
Math.sign(1);  // 1
Math.sign(-1); // -1
 
// 参数为 0 时，不同符号的返回不同
Math.sign(0);  // 0
Math.sign(-0); // -0
 
// 判断前会对非数值进行转换
Math.sign('1');  // 1
Math.sign('-1'); // -1  
 
// 参数为非数值（无法转换为数值）时返回 NaN
Math.sign(NaN);   // NaN 
Math.sign('hhh'); // NaN
```

### 对数方法

```
Math.expm1()
```

用于计算 e 的 x 次方减 1 的结果，即 Math.exp(x) - 1 。

```
Math.expm1(1);  // 1.718281828459045
Math.expm1(0);  // 0
Math.expm1(-1); // -0.6321205588285577
// 会对非数值进行转换
Math.expm1('0'); //0
 
// 参数不为数值且无法转换为数值时返回 NaN
Math.expm1(NaN); // NaN
```

```
Math.log1p(x)
```

用于计算1 + x 的自然对数，即 Math.log(1 + x) 。

```
Math.log1p(1);  // 0.6931471805599453
Math.log1p(0);  // 0
Math.log1p(-1); // -Infinity
 
// 参数小于 -1 时返回 NaN
Math.log1p(-2); // NaN
```

```
Math.log10(x)
```

用于计算以 10 为底的 x 的对数。

Math.log10(1); Math.log10('1'); Math.log10(0); Math.log10(\-1);

```
Math.log2()
```

用于计算 2 为底的 x 的对数。

```
Math.log10(1);   // 0
// 计算前对非数值进行转换
Math.log10('1'); // 0
// 参数为0时返回 -Infinity
Math.log10(0);   // -Infinity
// 参数小于0或参数不为数值（且无法转换为数值）时返回 NaN
Math.log10(-1);  // NaN
```

### 双曲函数方法

-   Math.sinh(x): 用于计算双曲正弦。
-   Math.cosh(x): 用于计算双曲余弦。
-   Math.tanh(x): 用于计算双曲正切。
-   Math.asinh(x): 用于计算反双曲正弦。
-   Math.acosh(x): 用于计算反双曲余弦。
-   Math.atanh(x): 用于计算反双曲正切。

### 指数运算符

```
1 ** 2; // 1
// 右结合，从右至左计算
2 ** 2 ** 3; // 256
// **=
let exam = 2;
exam ** = 2; // 4
```

# 3.2.3 ES6 对象

## 对象字面量

### 属性的简洁表示法

ES6允许对象的属性直接写变量，这时候属性名是变量名，属性值是变量值。

```
const age = 12;
const name = "Amy";
const person = {age, name};
person   //{age: 12, name: "Amy"}
//等同于
const person = {age: age, name: name}
```

### 方法名也可以简写

```
const person = {
  sayHi(){
    console.log("Hi");
  }
}
person.sayHi();  //"Hi"
//等同于
const person = {
  sayHi:function(){
    console.log("Hi");
  }
}
person.sayHi();//"Hi"
```

如果是Generator 函数，则要在前面加一个星号：

```
const obj = {
  * myGenerator() {
    yield 'hello world';
  }
};
//等同于
const obj = {
  myGenerator: function* () {
    yield 'hello world';
  }
};
```

### 属性名表达式

ES6允许用表达式作为属性名，但是一定要将表达式放在方括号内。

```
const obj = {
 ["he"+"llo"](){
   return "Hi";
  }
}
obj.hello();  //"Hi"
```

注意点：属性的简洁表示法和属性名表达式不能同时使用，否则会报错。

```
const hello = "Hello";
const obj = {
 [hello]
};
obj  //SyntaxError: Unexpected token }
 
const hello = "Hello";
const obj = {
 [hello+"2"]:"world"
};
obj  //{Hello2: "world"}
```

## 对象的拓展运算符

拓展运算符（...）用于取出参数对象所有可遍历属性然后拷贝到当前对象。

### 基本用法

```
let person = {name: "Amy", age: 15};
let someone = { ...person };
someone;  //{name: "Amy", age: 15}
```

### 可用于合并两个对象

```
let age = {age: 15};
let name = {name: "Amy"};
let person = {...age, ...name};
person;  //{age: 15, name: "Amy"}
```

### 注意点

自定义的属性和拓展运算符对象里面属性的相同的时候：**自定义的属性在拓展运算符后面，则拓展运算符对象内部同名的属性将被覆盖掉。**

```
let person = {name: "Amy", age: 15};
let someone = { ...person, name: "Mike", age: 17};
someone;  //{name: "Mike", age: 17}
```

自定义的属性在拓展运算度前面，则变成设置新对象默认属性值。

```
let person = {name: "Amy", age: 15};
let someone = {name: "Mike", age: 17, ...person};
someone;  //{name: "Amy", age: 15}
```

拓展运算符后面是空对象，没有任何效果也不会报错。

```
let a = {...{}, a: 1, b: 2};
a;  //{a: 1, b: 2}
```

拓展运算符后面是null或者undefined，没有效果也不会报错。

```
let b = {...null, ...undefined, a: 1, b: 2};
b;  //{a: 1, b: 2}
```

## 对象的新方法

### Object.assign(target, source\_1, ···)

用于将源对象的所有可枚举属性复制到目标对象中。

**基本用法**

```
let target = {a: 1};
let object2 = {b: 2};
let object3 = {c: 3};
Object.assign(target,object2,object3);  
// 第一个参数是目标对象，后面的参数是源对象
target;  // {a: 1, b: 2, c: 3}
```

-   如果目标对象和源对象有同名属性，或者多个源对象有同名属性，则后面的属性会覆盖前面的属性。
-   如果该函数只有一个参数，当参数为对象时，直接返回该对象；当参数不是对象时，会先将参数转为对象然后返回。

```
Object.assign(3);         // Number {3}
typeof Object.assign(3);  // "object"
```

因为 null 和 undefined 不能转化为对象，所以会报错:

```
Object.assign(null);       // TypeError: Cannot convert undefined or null to object
Object.assign(undefined);  // TypeError: Cannot convert undefined or null to object
当参数不止一个时，null 和 undefined 不放第一个，即不为目标对象时，会跳过 null 和 undefined ，不报错
Object.assign(1,undefined);  // Number {1}
Object.assign({a: 1},null);  // {a: 1}
 
Object.assign(undefined,{a: 1});  // TypeError: Cannot convert undefined or null to object
```

**注意点**

assign 的属性拷贝是浅拷贝:

```
let sourceObj = { a: { b: 1}};
let targetObj = {c: 3};
Object.assign(targetObj, sourceObj);
targetObj.a.b = 2;
sourceObj.a.b;  // 2
```

同名属性替换

```
targetObj = { a: { b: 1, c:2}};
sourceObj = { a: { b: "hh"}};
Object.assign(targetObj, sourceObj);
targetObj;  // {a: {b: "hh"}}
```

数组的处理

```
Object.assign([2,3], [5]);  // [5,3]
```

会将数组处理成对象，所以先将 \[2,3\] 转为 {0:2,1:3} ，然后再进行属性复制，所以源对象的 0 号属性覆盖了目标对象的 0。

### Object.is(value1, value2)

用来比较两个值是否严格相等，与（===）基本类似。

**基本用法**

```
Object.is("q","q");      // true
Object.is(1,1);          // true
Object.is([1],[1]);      // false
Object.is({q:1},{q:1});  // false
```

与（===）的区别

```
//一是+0不等于-0
Object.is(+0,-0);  //false
+0 === -0  //true
//二是NaN等于本身
Object.is(NaN,NaN); //true
NaN === NaN  //false
```

# 3.2.4 ES6 数组

## 数组创建

### Array.of()

将参数中所有值作为元素形成数组。

```
console.log(Array.of(1, 2, 3, 4)); // [1, 2, 3, 4]
 
// 参数值可为不同类型
console.log(Array.of(1, '2', true)); // [1, '2', true]
 
// 参数为空时返回空数组
console.log(Array.of()); // []
```

### Array.from()

将类数组对象或可迭代对象转化为数组。

```
// 参数为数组,返回与原数组一样的数组
console.log(Array.from([1, 2])); // [1, 2]
 
// 参数含空位
console.log(Array.from([1, , 3])); // [1, undefined, 3]
```

**参数**

```
Array.from(arrayLike[, mapFn[, thisArg]])
```

返回值为转换后的数组。

**arrayLike**

想要转换的类数组对象或可迭代对象。

```
console.log(Array.from([1, 2, 3])); // [1, 2, 3]
```

**mapFn**

可选，map 函数，用于对每个元素进行处理，放入数组的是处理后的元素。

```
console.log(Array.from([1, 2, 3], (n) => n * 2)); // [2, 4, 6]
```

**thisArg**

可选，用于指定 map 函数执行时的 this 对象。

```
let map = {
    do: function(n) {
        return n * 2;
    }
}
let arrayLike = [1, 2, 3];
console.log(Array.from(arrayLike, function (n){
    return this.do(n);
}, map)); // [2, 4, 6]
```

### 类数组对象

一个类数组对象必须含有 length 属性，且元素属性名必须是数值或者可转换为数值的字符。

```
let arr = Array.from({
  0: '1',
  1: '2',
  2: 3,
  length: 3
});
console.log(arr); // ['1', '2', 3]
 
// 没有 length 属性,则返回空数组
let array = Array.from({
  0: '1',
  1: '2',
  2: 3,
});
console.log(array); // []
 
// 元素属性名不为数值且无法转换为数值，返回长度为 length 元素值为 undefined 的数组  
let array1 = Array.from({
  a: 1,
  b: 2,
  length: 2
});
console.log(array1); // [undefined, undefined]
```

### 转换可迭代对象

**转换 map**

```
let map = new Map();
map.set('key0', 'value0');
map.set('key1', 'value1');
console.log(Array.from(map)); // [['key0', 'value0'],['key1',
// 'value1']]
```

**转换 set**

```
let arr = [1, 2, 3];
let set = new Set(arr);
console.log(Array.from(set)); // [1, 2, 3]
```

**转换字符串**

```
let str = 'abc';
console.log(Array.from(str)); // ["a", "b", "c"]let str = 'abc'; console.log(Array.from(str));
```

## 扩展的方法

### 查找

**find()**

查找数组中符合条件的元素,若有多个符合条件的元素，则返回第一个元素。

```
let arr = Array.of(1, 2, 3, 4);
console.log(arr.find(item => item > 2)); // 3
 
// 数组空位处理为 undefined
console.log([, 1].find(n => true)); // undefined
```

**findIndex()**

查找数组中符合条件的元素索引，若有多个符合条件的元素，则返回第一个元素索引。

```
let arr = Array.of(1, 2, 1, 3);
// 参数1：回调函数
// 参数2(可选)：指定回调函数中的 this 值
console.log(arr.findIndex(item => item == 2)); // 1
 
// 数组空位处理为 undefined
console.log([, 1].findIndex(n => true)); //0
```

### 填充

**fill()**

将一定范围索引的数组元素内容填充为单个指定的值。

```
let arr = Array.of(1, 2, 3, 4);
// 参数1：用来填充的值
// 参数2：被填充的起始索引
// 参数3(可选)：被填充的结束索引，默认为数组末尾
console.log(arr.fill(0,1,2)); // [1, 0, 3, 4]
```

**copyWithin()**

将一定范围索引的数组元素修改为此数组另一指定范围索引的元素。

```
// 参数1：被修改的起始索引
// 参数2：被用来覆盖的数据的起始索引
// 参数3(可选)：被用来覆盖的数据的结束索引，默认为数组末尾
console.log([1, 2, 3, 4].copyWithin(0,2,4)); // [3, 4, 3, 4]
 
// 参数1为负数表示倒数
console.log([1, 2, 3, 4].copyWithin(-2, 0)); // [1, 2, 1, 2]
 
console.log([1, 2, ,4].copyWithin(0, 2, 4)); // [, 4, , 4]
```

### 遍历

**entries()**

遍历键值对。

```
for(let [key, value] of ['a', 'b'].entries()){
    console.log(key, value);
}
// 0 "a"
// 1 "b"
 
// 不使用 for... of 循环
let entries = ['a', 'b'].entries();
console.log(entries.next().value); // [0, "a"]
console.log(entries.next().value); // [1, "b"]
 
// 数组含空位
console.log([...[,'a'].entries()]); // [[0, undefined], [1, "a"]]
```

**keys()**

遍历键名。

```
for(let key of ['a', 'b'].keys()){
    console.log(key);
}
// 0
// 1
 
// 数组含空位
console.log([...[,'a'].keys()]); // [0, 1]
```

**values()**

遍历键值。

```
for(let value of ['a', 'b'].values()){
    console.log(value);
}
// "a"
// "b"
 
// 数组含空位
console.log([...[,'a'].values()]); // [undefined, "a"]
```

### 包含

**includes()**

数组是否包含指定值。

注意：与 Set 和 Map 的 has 方法区分；Set 的 has 方法用于查找值；Map 的 has 方法用于查找键名。

```
// 参数1：包含的指定值
[1, 2, 3].includes(1);    // true
 
// 参数2：可选，搜索的起始索引，默认为0
[1, 2, 3].includes(1, 2); // false
 
// NaN 的包含判断
[1, NaN, 3].includes(NaN); // true
```

### 嵌套数组转一维数组

**flat()**

```
console.log([1 ,[2, 3]].flat()); // [1, 2, 3]
 
// 指定转换的嵌套层数
console.log([1, [2, [3, [4, 5]]]].flat(2)); // [1, 2, 3, [4, 5]]
 
// 不管嵌套多少层
console.log([1, [2, [3, [4, 5]]]].flat(Infinity)); // [1, 2, 3, 4, 5]
 
// 自动跳过空位
console.log([1, [2, , 3]].flat());<p> // [1, 2, 3]
```

**flatMap()**

先对数组中每个元素进行了的处理，再对数组执行 flat() 方法。

```
// 参数1：遍历函数，该遍历函数可接受3个参数：当前元素、当前元素索引、原数组
// 参数2：指定遍历函数中 this 的指向
console.log([1, 2, 3].flatMap(n => [n * 2])); // [2, 4, 6]
```

## 数组缓冲区

数组缓冲区是内存中的一段地址。

定型数组的基础。

实际字节数在创建时确定，之后只可修改其中的数据，不可修改大小。

### 创建数组缓冲区

通过构造函数创建:

```
let buffer = new ArrayBuffer(10);
console.log(buffer.byteLength); // 10
分割已有数组缓冲区
let buffer = new ArrayBuffer(10);
let buffer1 = buffer.slice(1, 3);
console.log(buffer1.byteLength); // 2
```

### 视图

视图是用来操作内存的接口。

视图可以操作数组缓冲区或缓冲区字节的子集,并按照其中一种数值数据类型来读取和写入数据。

DataView 类型是一种通用的数组缓冲区视图,其支持所有8种数值型数据类型。

创建:

```
// 默认 DataView 可操作数组缓冲区全部内容
let buffer = new ArrayBuffer(10);
    dataView = new DataView(buffer); 
dataView.setInt8(0,1);
console.log(dataView.getInt8(0)); // 1
 
// 通过设定偏移量(参数2)与长度(参数3)指定 DataView 可操作的字节范围
let buffer1 = new ArrayBuffer(10);
    dataView1 = new DataView(buffer1, 0, 3);
dataView1.setInt8(5,1); // RangeError
```

## 定型数组

数组缓冲区的特定类型的视图。

可以强制使用特定的数据类型，而不是使用通用的 DataView 对象来操作数组缓冲区。

### 创建

通过数组缓冲区生成

```
let buffer = new ArrayBuffer(10),
    view = new Int8Array(buffer);
console.log(view.byteLength); // 10
```

通过构造函数

```
let view = new Int32Array(10);
console.log(view.byteLength); // 40
console.log(view.length);     // 10
 
// 不传参则默认长度为0
// 在这种情况下数组缓冲区分配不到空间，创建的定型数组不能用来保存数据
let view1 = new Int32Array();
console.log(view1.byteLength); // 0
console.log(view1.length);     // 0
 
// 可接受参数包括定型数组、可迭代对象、数组、类数组对象
let arr = Array.from({
  0: '1',
  1: '2',
  2: 3,
  length: 3
});
let view2 = new Int16Array([1, 2]),
    view3 = new Int32Array(view2),
    view4 = new Int16Array(new Set([1, 2, 3])),
    view5 = new Int16Array([1, 2, 3]),
    view6 = new Int16Array(arr);
console.log(view2 .buffer === view3.buffer); // false
console.log(view4.byteLength); // 6
console.log(view5.byteLength); // 6
console.log(view6.byteLength); // 6
```

### 注意要点

length 属性不可写，如果尝试修改这个值，在非严格模式下会直接忽略该操作，在严格模式下会抛出错误。

```
let view = new Int16Array([1, 2]);
view.length = 3;
console.log(view.length); // 2
```

定型数组可使用 entries()、keys()、values()进行迭代。

```
let view = new Int16Array([1, 2]);
for(let [k, v] of view.entries()){
    console.log(k, v);
}
// 0 1
// 1 2
```

find() 等方法也可用于定型数组，但是定型数组中的方法会额外检查数值类型是否安全,也会通过 Symbol.species 确认方法的返回值是定型数组而非普通数组。concat() 方法由于两个定型数组合并结果不确定，故不能用于定型数组；另外，由于定型数组的尺寸不可更改,可以改变数组的尺寸的方法，例如 splice() ，不适用于定型数组。

```
let view = new Int16Array([1, 2]);
view.find((n) > 1); // 2
```

所有定型数组都含有静态 of() 方法和 from() 方法,运行效果分别与 Array.of() 方法和 Array.from() 方法相似,区别是定型数组的方法返回定型数组,而普通数组的方法返回普通数组。

```
let view = Int16Array.of(1, 2);
console.log(view instanceof Int16Array); // true
```

定型数组不是普通数组，不继承自 Array 。

```
let view = new Int16Array([1, 2]);
console.log(Array.isArray(view)); // false
```

定型数组中增加了 set() 与 subarray() 方法。 set() 方法用于将其他数组复制到已有定型数组, subarray() 用于提取已有定型数组的一部分形成新的定型数组。

```
// set 方法
// 参数1：一个定型数组或普通数组
// 参数2：可选，偏移量，开始插入数据的位置，默认为0
let view= new Int16Array(4);
view.set([1, 2]);
view.set([3, 4], 2);
console.log(view); // [1, 2, 3, 4]
 
// subarray 方法
// 参数1：可选，开始位置
// 参数2：可选，结束位置(不包含结束位置)
let view= new Int16Array([1, 2, 3, 4]), 
    subview1 = view.subarray(), 
    subview2 = view.subarray(1), 
    subview3 = view.subarray(1, 3);
console.log(subview1); // [1, 2, 3, 4]
console.log(subview2); // [2, 3, 4]
console.log(subview3); // [2, 3]
```

## 扩展运算符

### 复制数组

```
let arr = [1, 2],
    arr1 = [...arr];
console.log(arr1); // [1, 2]
 
// 数组含空位
let arr2 = [1, , 3],
    arr3 = [...arr2];
console.log(arr3); [1, undefined, 3]
```

合并数组

```
console.log([...[1, 2],...[3, 4]]); // [1, 2, 3, 4]
```

# 4.1 ES6 函数

## 函数参数的扩展

### 默认参数

基本用法

```
function fn(name,age=17){
 console.log(name+","+age);
}
fn("Amy",18);  // Amy,18
fn("Amy","");  // Amy,
fn("Amy");     // Amy,17
```

注意点：使用函数默认参数时，不允许有同名参数。

```
// 不报错
function fn(name,name){
 console.log(name);
}
 
// 报错
//SyntaxError: Duplicate parameter name not allowed in this context
function fn(name,name,age=17){
 console.log(name+","+age);
}
```

只有在未传递参数，或者参数为 undefined 时，才会使用默认参数，null 值被认为是有效的值传递。

```
function fn(name,age=17){
    console.log(name+","+age);
}
fn("Amy",null); // Amy,null
```

函数参数默认值存在暂时性死区，在函数参数默认值表达式中，还未初始化赋值的参数值无法作为其他参数的默认值。

```
function f(x,y=x){
    console.log(x,y);
}
f(1);  // 1 1
 
function f(x=y){
    console.log(x);
}
f();  // ReferenceError: y is not defined
```

### 不定参数

不定参数用来表示不确定参数个数，形如，...变量名，由...加上一个具名参数标识符组成。具名参数只能放在参数组的最后，并且有且只有一个不定参数。

基本用法

```
function f(...values){
    console.log(values.length);
}
f(1,2);      //2
f(1,2,3,4);  //4
```

## 箭头函数

箭头函数提供了一种更加简洁的函数书写方式。基本语法是：

```
参数 => 函数体
```

基本用法：

```
var f = v => v;
//等价于
var f = function(a){
 return a;
}
f(1);  //1
```

当箭头函数没有参数或者有多个参数，要用 () 括起来。

```
var f = (a,b) => a+b;
f(6,2);  //8var f = (a,b) => a+b; f(6,2);
```

当箭头函数函数体有多行语句，用 {} 包裹起来，表示代码块，当只有一行语句，并且需要返回结果时，可以省略 {} , 结果会自动返回。

```
var f = (a,b) => {
 let result = a+b;
 return result;
}
f(6,2);  // 8var f = (a,b) => { let result = a+b; return result; } f(6,2);
```

当箭头函数要返回对象的时候，为了区分于代码块，要用 () 将对象包裹起来

```
// 报错
var f = (id,name) => {id: id, name: name};
f(6,2);  // SyntaxError: Unexpected token :
 
// 不报错
var f = (id,name) => ({id: id, name: name});
f(6,2);  // {id: 6, name: 2}
```

注意点：没有 this、super、arguments 和 new.target 绑定。

```
var func = () => {
  // 箭头函数里面没有 this 对象，
  // 此时的 this 是外层的 this 对象，即 Window 
  console.log(this)
}
func(55)  // Window 
 
var func = () => {    
  console.log(arguments)
}
func(55);  // ReferenceError: arguments is not defined
```

箭头函数体中的 this 对象，是定义函数时的对象，而不是使用函数时的对象。

```
function fn(){
  setTimeout(()=>{
    // 定义时，this 绑定的是 fn 中的 this 对象
    console.log(this.a);
  },0)
}
var a = 20;
// fn 的 this 对象为 {a: 18}
fn.call({a: 18});  // 18
```

不可以作为构造函数，也就是不能使用 new 命令，否则会报错

### 适合使用的场景

ES6 之前，JavaScript 的 this 对象一直很令人头大，回调函数，经常看到 var self = this 这样的代码，为了将外部 this 传递到回调函数中，那么有了箭头函数，就不需要这样做了，直接使用 this 就行。

```
// 回调函数
var Person = {
    'age': 18,
    'sayHello': function () {
      setTimeout(function () {
        console.log(this.age);
      });
    }
};
var age = 20;
Person.sayHello();  // 20
 
var Person1 = {
    'age': 18,
    'sayHello': function () {
      setTimeout(()=>{
        console.log(this.age);
      });
    }
};
var age = 20;
Person1.sayHello();  // 18
```

所以，当我们需要维护一个 this 上下文的时候，就可以使用箭头函数。

### 不适合使用的场景

定义函数的方法，且该方法中包含 this

```
var Person = {
    'age': 18,
    'sayHello': ()=>{
        console.log(this.age);
      }
};
var age = 20;
Person.sayHello();  // 20
// 此时 this 指向的是全局对象
 
var Person1 = {
    'age': 18,
    'sayHello': function () {
        console.log(this.age);
    }
};
var age = 20;
Person1.sayHello();   // 18
// 此时的 this 指向 Person1 对象
```

需要动态 this 的时候

```
var button = document.getElementById('userClick');
button.addEventListener('click', () => {
     this.classList.toggle('on');
});
```

button 的监听函数是箭头函数，所以监听函数里面的 this 指向的是定义的时候外层的 this 对象，即 Window，导致无法操作到被点击的按钮对象。

# 4.3 ES6 Class 类

## 概述

在ES6中，class (类)作为对象的模板被引入，可以通过 class 关键字定义类。

class 的本质是 function。

它可以看作一个语法糖，让对象原型的写法更加清晰、更像面向对象编程的语法。

## 基础用法

### 类定义

类表达式可以为匿名或命名。

```
// 匿名类
let Example = class {
    constructor(a) {
        this.a = a;
    }
}
// 命名类
let Example = class Example {
    constructor(a) {
        this.a = a;
    }
}
```

### 类声明

```
class Example {
    constructor(a) {
        this.a = a;
    }
}
```

注意要点：不可重复声明。

```
class Example{}
class Example{}
// Uncaught SyntaxError: Identifier 'Example' has already been 
// declared
 
let Example1 = class{}
class Example{}
// Uncaught SyntaxError: Identifier 'Example' has already been 
// declared
```

### 注意要点

类定义不会被提升，这意味着，必须在访问前对类进行定义，否则就会报错。

类中方法不需要 function 关键字。

方法间不能加分号。

```
new Example(); 
class Example {}
```

### 类的主体

**属性**

`prototype`

ES6 中，prototype 仍旧存在，虽然可以直接自类中定义方法，但是其实方法还是定义在 prototype 上的。 覆盖方法 / 初始化时添加方法

```
Example.prototype={
    //methods
}
```

添加方法

```
Object.assign(Example.prototype,{
    //methods
})
```

静态属性

静态属性：class 本身的属性，即直接定义在类内部的属性（ Class.propname ），不需要实例化。 ES6 中规定，Class 内部只有静态方法，没有静态属性。

```
class Example {
// 新提案
    static a = 2;
}
// 目前可行写法
Example.b = 2;
```

公共属性

```
class Example{}
Example.prototype.a = 2;
```

实例属性

实例属性：定义在实例对象（ this ）上的属性。

```
class Example{}
Example.prototype.a = 2;
```

name 属性

返回跟在 class 后的类名(存在时)。

```
let Example=class Exam {
    constructor(a) {
        this.a = a;
    }
}
console.log(Example.name); // Exam
 
let Example=class {
    constructor(a) {
        this.a = a;
    }
}
console.log(Example.name); // Example
```

**方法**

constructor 方法

constructor 方法是类的默认方法，创建类的实例化对象时被调用。

class Example{ constructor(){ console.log('我是constructor'); } } new Example();

返回对象

class Test { constructor(){ } } console.log(new Test() instanceof Test); class Example { constructor(){ return new Test(); } } console.log(new Example() instanceof Example);

静态方法

class Example{ static sum(a, b) { console.log(a+b); } } Example.sum(1, 2);

原型方法

class Example { sum(a, b) { console.log(a + b); } } let exam = new Example(); exam.sum(1, 2);

实例方法

class Example { constructor() { this.sum = (a, b) => { console.log(a + b); } } }

### 类的实例化

**new**

class 的实例化必须通过 new 关键字。

class Example {} let exam1 = Example();

**实例化对象**

共享原型对象

class Example { constructor(a, b) { this.a = a; this.b = b; console.log('Example'); } sum() { return this.a + this.b; } } let exam1 = new Example(2, 1); let exam2 = new Example(3, 1); console.log(Object.getPrototypeOf(exam1) === Object.getPrototypeOf(exam2)); Object.getPrototypeOf(exam1).sub = function() { return this.a - this.b; } console.log(exam1.sub()); console.log(exam2.sub());

## decorator

decorator 是一个函数，用来修改类的行为，在代码编译时产生作用。

### 类修饰

一个参数

第一个参数 target，指向类本身。

function testable(target) { target.isTestable = true; } @testable class Example {} Example.isTestable;

多个参数——嵌套实现

function testable(isTestable) { return function(target) { target.isTestable\=isTestable; } } @testable(true) class Example {} Example.isTestable;

实例属性

上面两个例子添加的是静态属性，若要添加实例属性，在类的 prototype 上操作即可。

### 方法修饰

3个参数：target（类的原型对象）、name（修饰的属性名）、descriptor（该属性的描述对象）。

class Example { @writable sum(a, b) { return a + b; } } function writable(target, name, descriptor) { descriptor.writable = false; return descriptor; }

修饰器执行顺序

由外向内进入，由内向外执行。

class Example { @logMethod(1) @logMethod(2) sum(a, b){ return a + b; } } function logMethod(id) { console.log('evaluated logMethod'+id); return (target, name, desctiptor) => console.log('excuted logMethod '+id); }

## 封装与继承

### getter / setter

定义

class Example{ constructor(a, b) { this.a = a; this.b = b; } get a(){ console.log('getter'); return this.a; } set a(a){ console.log('setter'); this.a = a; } } let exam = new Example(1,2); class Example1{ constructor(a, b) { this.a = a; this.b = b; } get a(){ console.log('getter'); return this.\_a; } set a(a){ console.log('setter'); this.\_a = a; } } let exam1 = new Example1(1,2); console.log(exam1.\_a);

getter 不可单独出现

class Example { constructor(a) { this.a = a; } get a() { return this.a; } } let exam = new Example(1);

getter 与 setter 必须同级出现

class Father { constructor(){} get a() { return this.\_a; } } class Child extends Father { constructor(){ super(); } set a(a) { this.\_a = a; } } let test = new Child(); test.a = 2; console.log(test.a); class Father1 { constructor(){} get a() { return this.\_a; } set a(a) { this.\_a = a; } } class Child1 extends Father1 { constructor(){ super(); } } let test1 = new Child1(); test1.a = 2; console.log(test1.a);

### extends

通过 extends 实现类的继承。

class Child extends Father { ... }

### super

子类 constructor 方法中必须有 super ，且必须出现在 this 之前。

class Father { constructor() {} } class Child extends Father { constructor() {} } let test = new Child();

调用父类构造函数,只能出现在子类的构造函数。

class Father { test(){ return 0; } static test1(){ return 1; } } class Child extends Father { constructor(){ super(); } } class Child1 extends Father { test2() { super(); } }

调用父类方法, super 作为对象，在普通方法中，指向父类的原型对象，在静态方法中，指向父类

class Child2 extends Father { constructor(){ super(); console.log(super.test()); } static test3(){ return super.test1+2; } } Child2.test3();

### 注意要点

不可继承常规对象。

var Father = { } class Child extends Father { } Object.setPrototypeOf(Child.prototype, Father);	