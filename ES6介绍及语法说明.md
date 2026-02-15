# ES6介绍及语法说明

## ES6介绍

​	ECMAScript 6（ES6），又称 ECMAScript 2015，是 JavaScript 的一个重要版本，引入了许多新特性，使得开发者能够编写更加简洁、优雅和高效的代码。本文将介绍 ES6 的一些关键特性，并通过代码示例展示其用法。

## 1、变量声明

在 `ES6` 之前，`JavaScript` 只有 `var` 用于变量声明。`ES6` 引入了 `let` 和 `const`，它们提供了块级作用域和不可变的变量。

### 1.1 let关键字

let关键字用于声明可变的变量，它的作用范围限定在当前的块级作用域内，包括花括号（{}）内部的任何代码块。在同一个作用域内，不能重复声明同名的let变量。

在以前使用 `var` 声明变量会存在：`越域`、`重复声明`、`变量提升`等问题，我们来看看代码演示

**跨域问题**

```javascript
// var 越域的问题
if (true) {
    var x = 10;
}
console.log(x); // 输出 ：10，变量 x 泄露到了全局作用域

// let 的块级作用域
if (true) {
    let y = 20;
}
console.log(y); // ReferenceError: y is not defined
```

**重复声明**

```javascript
// var 可以声明多次
// let 只能声明一次
var a = 1
var a = 2
let b = 3
let b = 4
console.log(a) // 2
console.log(b) // Identifier 'n' has already been declared
```

**变量提升**

```javascript
// var 会变量提升
// let 不存在变量提升
console.log(x); // undefined
var x = 10;
console.log(y); //ReferenceError: y is not defined
let y = 20;
```

### 1.2 const关键字

`const` 关键字用于声明常量，它的作用范围也是在当前的块级作用域内，`const` 声明的变量是不可变的

```javascript
// 1. 声明之后不允许改变
// 2. 一但声明必须初始化，否则会报错
const a = 1;
a = 3; //Uncaught TypeError: Assignment to constant variable.
```

## 2、箭头函数

学过 java 的小伙伴一定知道 `lambda` 表达式，与之一样箭头函数提供了一种更简洁的函数定义方式，并且不会绑定自己的 this

```javascript
// 传统函数
function sum(a, b) {
    return a + b;
}

// 箭头函数
const sum = (a, b) => a + b;

console.log(sum(2, 3)); // 5

// 只有一个参数
const square = x => x * x;
console.log(square(4)); // 16

// 没有参数
const greet = () => 'Hello, World!';
console.log(greet()); // Hello, World!
```

**使用箭头函数需要注意以下几点：**

### 2.1 没有自己的 this 绑定

箭头函数没有自己的 `this` 绑定，它会捕获其所在上下文的 `this` 值。对于处理回调函数中的 this 问题非常有用

```javascript
function Person() {
    this.age = 0;
    // 传统函数需要额外绑定 this
    setInterval(function growUp() {
        this.age++;
    }.bind(this), 1000);
}

function Person() {
    this.age = 0;
    // 箭头函数自动捕获外部 this
    setInterval(() => {
        this.age++;
    }, 1000);
}
```

### 2.2 没有 arguments 对象

箭头函数没有 `arguments` 对象，但可以使用 `rest` 参数（`...args`）代替

```javascript
const showArgs = (...args) => {
    console.log(args);
};

showArgs(1, 2, 3); // [1, 2, 3]
```

### 2.3 不能用作构造函数

箭头函数不能使用 `new` 关键字来实例化对象，因为它没有 `[[Construct]]` 方法

```javascript
const Foo = () => {};
const bar = new Foo(); // TypeError: Foo is not a constructor

```

### 2.4 没有 prototype 属性

箭头函数没有 `prototype` 属性，因此不能用于定义类的方法。

```javascript
const Foo = () => {};
console.log(Foo.prototype); // undefined
```

## 3、模板字符串

模板字符串使用反引号定义，可以嵌入变量和表达式。使用 `${}` 语法，在模板字符串中嵌入表达式或变量

```javascript
const name = 'John';
const age = 25;

// 普通字符串拼接
let info = "你好，我的名字是：【"+name+"】，年龄是：【"+age+"】"
console.log(info);

// 模板字符串的写法
let info = `你好，我的名字是：${name}，年龄是：${age}`
console.log(info);
```

## 4、解构赋值

解构赋值允许从数组或对象中提取值，并赋给变量。

### 4.1 数组解构

```javascript
let arr = [1, 2, 3];
//以前获取 通过使用角标  
console.log(arr[0]); // 1

const [a, b] = [1, 2];
console.log(a); // 1
console.log(b); // 2
```

### 4.2 对象解构

```javascript
const person = {
    name: "jack",
    age: 21,
    hobby: ['唱', '跳', 'rap']
}
// 解构表达式获取值，将 person 里面每一个属性和左边对应赋值
const {name, age, hobby} = person;
// 等价于下面
// const name = person.name;
// const age = person.age;
// const language = person.hobby;

// 可以分别打印
console.log(name);
console.log(age);
console.log(hobby);

//扩展：如果想要将 name 的值赋值给其他变量，可以如下,nn 是新的变量名
const {name: nn, age, hobby} = person;
console.log(nn);
console.log(age);
console.log(hobby);
```

## 5、默认参数

默认参数允许在函数定义时为参数指定默认值，这样可以简化函数的调用，避免出现`undefined`的情况

```javascript
function greet(name = 'Guest') {
    return `Hello, ${name}!`;
}

console.log(greet()); // Hello, Guest!
console.log(greet('Alice')); // Hello, Alice!


//还可以使用表达式
function multiply(a, b = 2 * a) {
  return a * b;
}
 
console.log(multiply(5)); // 输出：50
console.log(multiply(5,2)); // 输出：10
```

## 6、扩展运算符

展开运算符（`...`）可以用来展开数组或对象，主要用于将一个可迭代对象（如数组、字符串或类数组对象）展开成多个元素

### 6.1 数组展开

```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5, 6];
console.log(arr2); // [1, 2, 3, 4, 5, 6]
```

### 6.2 对象展开

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };
console.log(obj2); // { a: 1, b: 2, c: 3 }
```

### 6.3 字符串展开

```javascript
const str = 'hello';
const chars = [...str];
console.log(chars); // 输出：['h', 'e', 'l', 'l', 'o']
```

## 7、模块化

ES6 模块允许将代码分割成小块，并通过 `import` 和 `export` 进行组织和重用,

### 7.1 导出模块

使用 `export` 暴露方法或变量等

```javascript
// 假设我们有一个名为 math.js 的模块
export function add(a, b) {
    return a + b;
}

export const PI = 3.14;
```

### 7.2 导入模块

我们可以使用 `import` 关键字导入 math.js 模块中的函数和变量

```javascript
// main.js
import { add, PI } from './math.js';

console.log(add(2, 3)); // 5
console.log(PI); // 3.14
```

## 8、Promise

`Promise` 是一种用于处理异步操作的对象，类似Java中的 `CompletableFuture`。它可以将异步操作封装成一个 `Promise` 对象，通过 `then()` 方法来添加回调函数，当异步操作完成时自动执行回调函数。

```javascript
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Success!');
    }, 1000);
});

promise.then((message) => {
    console.log(message); // Success!
}).catch((error) => {
    console.error(error);
});
```

使用 `Promise` 对象可以使异步操作的代码更加清晰、简洁，并且可以避免回调地狱的问题。

## 9、生成器函数

生成器函数使用 `function*` 语法，可以通过 yield 关键字多次返回值

```javascript
function* generator() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = generator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

定义了一个生成器函数 myGenerator，它包含三个 yield 表达式。我们通过调用该函数得到一个迭代器对象 generator，每次调用 generator.next() 都会执行一次函数体，并返回一个包含 value 和 done 两个属性的对象

## 10、原型 原型链

​	每一个对象从被创建开始就和另一个对象关联，从另一个对象上继承其属性，这个`另一个对象`就是 **原型**。

​	当访问一个对象的属性时，先在对象的本身找，找不到就去对象的原型上找，如果还是找不到，就去对象的原型（原型也是对象，也有它自己的原型）的原型上找，如此继续，直到找到为止，或者查找到最顶层的原型对象中也没有找到，就结束查找，返回`undefined`。

**这条由对象及其原型组成的链就叫做原型链。**

1. **原型存在的意义就是组成原型链**：引用类型皆对象，每个对象都有原型，原型也是对象，也有它自己的原型，一层一层，组成原型链。
2. **原型链存在的意义就是继承**：访问对象属性时，在对象本身找不到，就在原型链上一层一层找。说白了就是一个对象可以访问其他对象的属性。
3. **继承存在的意义就是属性共享**：好处有二：一是代码重用，字面意思；二是可扩展，不同对象可能继承相同的属性，也可以定义只属于自己的属性。

**在JavaScript中，原型分为显式原型和隐式原型两种：**

1. **显式原型（prototype）**：所有函数自带一个`prototype`属性，它指向一个对象，这个对象就是该函数的原型对象，用来存放可以被所有实例共享的属性和方法，实现数据共享节省内存。 
2. **隐式原型（\**proto\**）**：所有引用类型（对象、数组、函数）都自带`__proto__`属性，它指向创建自身的构造函数的显式原型，浏览器通过它来查找原型上的属性和方法，它不属于标准属性，可以直接通过实例调用原型上的内容。

```
// 定义构造函数
function Person(name) {
    this.name = name;
}
// 在显式原型上添加共享方法
Person.prototype.sayHi = function() {
    console.log(`你好，我是${this.name}`);
}
// 创建两个实例
const person1 = new Person("张三");
const person2 = new Person("李四");
// 实例直接调用原型上的方法
person1.sayHi(); // 输出：你好，我是张三
person2.sayHi(); // 输出：你好，我是李四
// 验证隐式原型指向
console.log(person1.__proto__ === Person.prototype); // 输出：true
```

原型链查找

```
function Person(name) {
    this.name = name;
}
Person.prototype.sayHi = function() {
    console.log(`你好，我是${this.name}`);
}

const person1 = new Person("张三");
// person1 本身没有toString方法，会沿原型链查找到Object.prototype.toString
console.log(person1.toString()); // 输出：[object Object]
// 验证原型链指向
console.log(person1.__proto__ === Person.prototype);         // true
console.log(Person.prototype.__proto__ === Object.prototype); // true
console.log(Object.prototype.__proto__); // 输出：null
```

## 11、Axios

​	Axios 是一个基于 Promise 的 HTTP 库，支持在浏览器和 Node.js 中跨平台使用，拥有同构特性，一套代码可同时适配前后端环境：浏览器端基于XMLHttpRequest实现请求，Node.js端则调用原生http模块。

它的核心优势在于：

1. **异步友好**：基于Promise封装，避免回调地狱，完美适配async/await语法
2. **功能强大**：支持请求/响应拦截、请求取消、自动JSON数据转换，还内置客户端CSRF防御能力
3. **配置灵活**：支持全局配置、实例配置和请求级配置，可以满足各类复杂请求场景

### 发起一个Get请求

```
const axios = require('axios');

// 向给定ID的用户发起请求
axios.get('/user?ID=12345')
  .then(function (response) {
    // 处理成功情况
    console.log(response);
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });

// 上述请求也可以按以下方式完成（可选）
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });  

// 支持async/await用法
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

### 发起一个Post请求

```
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```

