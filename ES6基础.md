# 目录

## 前言

​	ES6（ECMAScript 6），也被称为ES2015，是JavaScript的第六个版本.它于2015年发布，并在现代JavaScript开发中扮演了重要的角色.

___

## let 和 const

-   const和let是在ES6中引入的两个新的变量声明关键字，用于声明变量的作用域。

1.  const：const用于声明一个**常量**，其值在**声明后不能被修改**。常量必须**在声明时进行初始化**，而且不能再次赋值。例如：
    
    ```javascript
    const PI = 3.14159;
    PI = 3.14; // 报错，常量不能再次赋值
    ```
    

-   常量适合用于保存不可变的值，如数学常数、配置项等。

2.  let：let用于声明块级作用域的变量，它与var相比具有更小的作用域范围。在块级作用域内部声明的变量只在该块级作用域内有效，而且不会被提升到函数作用域。例如：
    
    ```javascript
    function example() {
      let x = 10;
      if (true) {
        let x = 20;
        console.log(x); // 输出 20
      }
      console.log(x); // 输出 10
    }
    ```
    

-   在使用块级作用域时，可以避免变量之间的命名冲突和问题。

3.  var：var是ES5中使用的变量声明关键字，它存在一些作用域上的问题。var声明的变量属于**函数作用域或全局作用域**，而不是块级作用域，因此在循环或条件语句中声明的变量会被提升到外部函数作用域。
    
    ```javascript
    function example() {
      var x = 10;
      if (true) {
        var x = 20;
        console.log(x); // 输出 20
      }
      console.log(x); // 输出 20，而不是 10
    }
    ```
    

-   var声明的变量存在变量提升的问题，在变量声明之前就可以访问到变量，可能导致意外的结果。

___

## 块级作用域

-   块级作用域指的是在代码中由**花括号{}包围的部分**，这个部分内部声明的变量只在该块级作用域内有效，超出该作用域范围就无法访问。在ES6之前，JavaScript只有全局作用域和函数作用域，没有块级作用域。
    
-   使用块级作用域可以提供更细粒度的变量作用范围，避免变量的冲突和污染。块级作用域可以用于if语句、for循环、while循环等语句中的代码块，以及函数中的代码块。
    
    ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/999a59423114c4d81ebbc1f8704bc7f0.png)
    

___

## 模板字符串

### 一.模板字符串是什么

模板字符串是在JavaScript中使用的一种特殊字符串语法。它使用反引号（\`）包围，并允许在字符串中插入变量、表达式和换行符等。以下是一些模板字符串的特性：

1.  插入变量：通过`${}`语法，可以在字符串中插入变量。变量会被解析并替换为实际的值。示例代码如下：
    
    ```javascript
    const name = "Alice";
    const message = `Hello, ${name}!`;
    console.log(message); // 输出 "Hello, Alice!"
    ```
    
2.  执行表达式：在`${}`中除了可以插入变量外，还可以执行表达式。这样可以在字符串中进行复杂的运算或逻辑操作。示例代码如下：
    
    ```javascript
    const a = 10;
    const b = 5;
    const result = `The sum of ${a} and ${b} is ${a + b}.`;
    console.log(result); // 输出 "The sum of 10 and 5 is 15."
    ```
    
3.  多行字符串：在模板字符串中可以直接使用换行符，以方便创建多行文本。示例代码如下：
    
    ```javascript
    const multiLine = `This is a 
    multi-line
    string.`;
    console.log(multiLine);
    // 输出：
    // This is a
    // multi-line
    // string.
    ```
    

模板字符串更加灵活且易读，使得处理字符串的操作更加方便。它在与变量和表达式的结合使用时，特别有用。

### 二.模板字符串的注意事项

1.  反引号（\`）包围：模板字符串必须使用反引号（\`）而不是单引号或双引号来包围。
    
2.  字符串中的插入项：使用`${}`来包裹要插入的变量或表达式。注意，在`${}`中可以使用任何有效的JavaScript表达式。但是，要注意不要在其中放置具有副作用的代码，以免产生意想不到的结果。
    
3.  转义字符：如果字符串中需要使用反引号（\`），则需要使用转义字符（\\）进行转义。
    
4.  换行字符：模板字符串中的换行字符会被保留。如果希望字符串换行，可使用显式的换行符（\\n）。
    
5.  嵌套模板字符串：模板字符串可以嵌套在彼此之内，以创建更复杂的字符串结构。
    
6.  兼容性：模板字符串是ES6中引入的特性，因此在较旧的浏览器或环境中可能不被完全支持。为了兼容性考虑，可以使用转译工具（如Babel）将模板字符串转换为普通字符串。
    

### 三. 模板字符串的应用

> 1.  字符串拼接：使用模板字符串可以更方便地进行字符串拼接，特别是需要插入变量或执行表达式时。相比传统的字符串拼接方法（使用加号或concat函数），模板字符串更简洁易读。
>     
> 2.  动态HTML生成：通过将变量或表达式插入模板字符串中，可以动态生成包含动态数据的HTML片段。这对于基于数据生成复杂的HTML结构、动态更新网页内容等非常有用。
>     
> 3.  URL拼接：构建URL时，模板字符串可以方便地插入参数值，以生成完整的URL。
>     
> 4.  多语言支持：在多语言环境中，可以使用模板字符串来创建多语言文本模板，并根据需要插入对应语言的翻译。
>     
> 5.  格式化输出：通过在模板字符串中使用占位符和格式化规则，可以实现对输出结果的格式化控制，如日期格式化、货币格式化等。
>     
> 6.  生成代码：在某些情况下，可以使用模板字符串来生成动态的JavaScript代码。例如，根据用户输入生成动态的函数定义。
>     

___

## 箭头函数

### 一.箭头函数是什么

-   概念: 箭头函数是在ES6（ECMAScript 2015）中引入的一种新的函数声明语法。它提供了一种更简洁、更清晰的函数定义方式。
    
-   语法：
    

```javascript
(argument1, argument2, ...) => {
  // 函数体
}
```

其中，参数列表由圆括号包围，后面跟着一个箭头（=>），然后是函数体（可以是一个代码块或一个表达式）。

-   箭头函数的特点：
    
    1.  简洁的语法：相对于常规函数，箭头函数提供了更简洁的语法形式，减少了冗余的代码。
        
    2.  没有自己的this值：箭头函数没有自己的`this`上下文，继承了父级作用域的`this`值。这解决了常规函数中`this`指向的问题，使得箭头函数更易于理解和使用。
        
    3.  没有自己的arguments对象：箭头函数也没有自己的`arguments`对象，但可以通过使用`rest`参数（`...args`）来获取传递给函数的所有参数。
        
    4.  没有Constructor：由于没有自己的`this`值，箭头函数不能用作构造函数来创建对象实例，即无法使用`new`关键字调用箭头函数。
    
-   示例：
    
    ```javascript
    const add = (a, b) => {  //或者const add = (a, b) => a +b ;
      return a + b;
    };
    
    const greet = name => `Hello, ${name}!`;
    
    const numbers = [1, 2, 3, 4];
    const doubled = numbers.map(num => num * 2);
    ```
    

### 二.普通函数与箭头函数的转换

1.  判断函数是否有参数。如果有参数，需要使用小括号包裹参数列表。如果只有一个参数，则可以省略小括号。
    
    ```javascript
    // 普通函数
    function sum(a, b) {
      return a + b;
    }
    
    // 转换为箭头函数
    const sum = (a, b) => a + b;
    ```
    
2.  移除`function`关键字，并在参数和箭头之间添加一个箭头（`=>`）。
    
    ```javascript
    // 普通函数
    function sayHello() {
      console.log("Hello!");
    }
    
    // 转换为箭头函数
    const sayHello = () => {
      console.log("Hello!");
    };
    ```
    
3.  如果函数体只有一行代码，并且它是一个表达式，可以省略大括号和`return`关键字，并将该表达式放在箭头后面。
    
    ```javascript
    // 普通函数
    function square(x) {
      return x * x;
    }
    
    // 转换为箭头函数
    const square = (x) => x * x;
    ```
    
4.  如果函数只有一个返回值，并且没有参数，可以使用隐式返回，即省略大括号和`return`关键字，并且将返回值放在箭头后面。
    
    ```javascript
    // 普通函数
    function getPi() {
      return 3.14;
    }
    
    // 转换为箭头函数
    const getPi = () => 3.14;
    ```
    

-   注意:
    -   箭头函数没有自己的`this`绑定，它会捕获外部作用域中的`this`值，因此在转换函数时请特别留意函数内部是否使用了`this`关键字。
        
    -   在一些特殊情况下，如果需要更复杂的函数体或需要使用 `arguments` 对象，那么箭头函数可能不适合转换，因为它们缺少常规函数的一些特性。
        

### 三.this指向

#### 1\. 全局作用域中的 `this` 指向

-   在严格模式下，全局作用域中的 `this` 的值是 `undefined`。在非严格模式下，它会指向全局对象（浏览器中是 `window` 对象，Node.js 中是 `global` 对象）。
    
    -   使用严格模式可以通过在脚本文件或函数体的开头添加 `"use strict";` 来启用。以下示例演示了在严格模式下全局作用域中的 `this` 的行为：
    
    ```javascript
    "use strict";
    
    console.log(this); // undefined
    ```
    
-   在非严格模式下，则会输出全局对象：
    
    ```javascript
    console.log(this); // 全局对象（浏览器中是window对象，Node.js中是global对象）
    ```
    

#### 2\. 一般函数（非箭头函数）中的this指向

-   在对象的方法中，即使在严格模式下，方法中的 `this` 仍然会指向调用该方法的对象。严格模式主要影响到全局作用域下的 `this` 值的行为。
    
    ```javascript
    "use strict";
    
    const obj = {
      name: "Alice",
      sayHello: function() {
        console.log(this); // 指向obj对象
      }
    };
    
    obj.sayHello();
    ```
    
-   如果通过构造函数创建对象时，`this` 在严格模式下指向新创建的对象。但在非严格模式下，如果构造函数内部没有显式设置 `this` 的值，则 `this` 可能会指向全局对象。
    

#### 3.箭头函数中`this`指向

-   在箭头函数中，`this`的值是由定义箭头函数的词法作用域决定的，而不是根据函数调用方式或绑定调用者来改变。
    
-   换句话说，箭头函数没有自己的 `this` 绑定，它会捕获其外部的词法作用域中的 `this` 值，并沿用该值。因此，在箭头函数内部，`this` 的指向是固定的，指向定义箭头函数时所在的作用域中的 `this`。
    
-   示例:
    
    -   对象方法：
        
        ```javascript
        const obj = {
          name: "Alice",
          sayHello: () => {
            console.log(this.name); // 箭头函数没有自己的 this，沿用外部作用域中的 this，这里指向全局对象（浏览器中是 window，Node.js 中是 global）
          }
        };
        ```
        
    -   回调函数中的 `this` 绑定：
        
        ```javascript
        const button = document.querySelector("button");
        button.addEventListener("click", () => {
          console.log(this); // 箭头函数没有自己的 this，沿用外部作用域中的 this，取决于事件处理函数所在的上下文
        });
        ```
        

### 四.不适用箭头函数的场景

1.  **作为构造函数**
    
    -   由于箭头函数没有自己的 `this` 绑定，它无法通过 `new` 关键字创建实例对象。箭头函数的 `this` 始终指向其外部词法作用域中的 `this` 值，而不会根据调用方式或绑定调用者来改变。
        
        ```javascript
        // 错误示例
        const Person = () => {
          this.name = "Alice"; // 错误：箭头函数不能用作构造函数
        };
        
        const person = new Person();
        ```
    
2.  **需要 `this` 指向调用对象的情况**
    
    -   **对象方法**：当需要在对象中定义方法，并且需要通过 this 来引用对象自身时，箭头函数不适用。箭头函数的 this 始终继承自外部词法作用域，无法根据调用方式来动态绑定。
        
        ```javascript
        const obj = {
          name: "Alice",
          sayHello: () => {
            console.log(`Hello, ${this.name}!`); // 错误：箭头函数的 this 不是指向 obj
          }
        };
        
        ```
        
    -   **动态绑定 this**：如果需要根据调用方式动态绑定 this 的值，例如通过 `call()`、`apply()` 或 `bind()` 显式改变其 `this` 值，那么箭头函数就不适合使用。箭头函数的 this 始终保持不变。
        
        ```javascript
        
        const greet = () => {
          console.log(`Hello, ${this.name}!`); // 错误：箭头函数的 this 不会被显式绑定
        };
        
        const person = {
          name: "Alice"
        };
        
        greet.call(person); // 错误：this 在箭头函数中不会改变
        
        ```
    
3.  **需要使用函数的 `arguments` 对象**
    
    -   箭头函数没有自己的 `arguments` 对象，无法访问传递给函数的参数集合。
        
        ```javascript
        const sum = () => {
          console.log(arguments); // 错误：箭头函数没有自己的 arguments 对象
        };
        
        sum(1, 2, 3); // 错误：无法在箭头函数中访问 arguments
        ```
        

### 五.箭头函数的应用

1.  简化函数表达式：箭头函数提供了一种更简洁的函数表达式语法，特别适用于传递匿名函数或回调函数。
    
    ```javascript
    // 传统函数表达式
    const sum = function(a, b) {
      return a + b;
    };
    
    // 箭头函数
    const sum = (a, b) => a + b;
    ```
    
2.  数组遍历与转换：结合数组的`map()`、`filter()`和`reduce()`等方法，可以使用箭头函数对数组进行快速遍历、筛选和转换操作。
    
    ```javascript
    const numbers = [1, 2, 3, 4, 5];
    
    const doubled = numbers.map(num => num * 2);
    
    const evenNumbers = numbers.filter(num => num % 2 === 0);
    
    const sum = numbers.reduce((total, num) => total + num, 0);
    ```
    
3.  箭头函数作为回调函数：由于箭头函数没有自己的`this`值，因此常用于解决回调函数中`this`指向的问题。
    
    ```javascript
    const obj = {
      name: "Alice",
      sayHello: function() {
        setTimeout(() => {
          console.log(`Hello, ${this.name}!`); // this指向obj对象
        }, 1000);
      }
    };
    
    obj.sayHello();
    ```
    
4.  更简洁的函数嵌套：当需要在一个函数内部定义另一个函数时，可以使用箭头函数来简化语法。
    
    ```javascript
    function foo() {
      return (a, b) => a + b;
    }
    
    const add = foo();
    console.log(add(2, 3)); // 5
    ```
    
5.  对象方法的简洁定义：当定义对象方法时，可以使用箭头函数来简化语法。
    
    ```javascript
    const obj = {
      name: "Alice",
      sayHello: () => {
        console.log(`Hello, ${this.name}!`); // this指向全局对象
      }
    };
    
    obj.sayHello();
    ```
    

___

## 解构赋值

解构赋值是一种从数组或对象中提取值，并将其赋给变量的方式。

### 一. 数组的解构赋值

-   原理：
    -   数组解构赋值通过**模式匹配**，按照**索引位置**进行赋值。
    -   当进行解构赋值时，可以直接将一个数组\[\]赋给等号左侧的模式。
    -   可以使用默认值来指定缺失的元素取值。
-   示例代码：
    
    ```javascript
    // 基本用法
    const [a, b, c] = [1, 2, 3];
    console.log(a); // 输出: 1
    console.log(b); // 输出: 2
    console.log(c); // 输出: 3
    
    // 使用默认值
    const [x, y, z = 0] = [4, 5];
    console.log(x); // 输出: 4
    console.log(y); // 输出: 5
    console.log(z); // 输出: 0（默认值）
    ```
    

### 二. 对象的解构赋值

-   原理：
    
    -   对象解构赋值通过**模式匹配**，按照**属性名称**进行赋值。
    -   当进行解构赋值时，可以直接将一个对象{}赋给等号左侧的模式。
    -   可以使用默认值来指定缺失的属性取值。
-   示例代码：
    
    ```javascript
    // 基本用法
    const {name, age} = {name: "Alice", age: 20};
    console.log(name); // 输出: "Alice"
    console.log(age); // 输出: 20
    
    // 使用别名
    const {name: personName, age: personAge} = {name: "Bob", age: 25};
    console.log(personName); // 输出: "Bob"
    console.log(personAge); // 输出: 25
    
    // 使用默认值
    const {firstName = "Unknown", lastName = "Unknown"} = {firstName: "Charlie"};
    console.log(firstName); // 输出: "Charlie"
    console.log(lastName); // 输出: "Unknown"（默认值）
    ```
    
-   注意事项:
    
    -   将一个已经声明的变量用于解构赋值，整个赋值需在圆括号中进行
        
        -   因为 JavaScript 解析器会将以左花括号 `{` 开始的语句解析为一个代码块，而不是对象字面量。为了避免这种歧义，可以将解构赋值表达式放在圆括号中，明确告诉解析器这是一个赋值表达式。
            
            ```javascript
            let x, y;
            
            // 错误的写法：解析为代码块
            {x, y} = {x: 1, y: 2};
            
            // 正确的写法：圆括号中进行解构赋值
            ({x, y} = {x: 1, y: 2});
            
            console.log(x,y); // 输出: 1 2
            
            ```
        
    -   对象的解构赋值可以取到继承的属性或方法
        
        -   当进行对象解构赋值时，如果目标对象的属性并不存在，解构赋值表达式会继续向上查找该属性；如果目标对象的属性在原型链中存在，则可以成功提取到该属性的值。
        
        ```javascript
        function Person(name) {
          this.name = name;
        }
        
        Person.prototype.sayHello = function() {
          console.log(`Hello, ${this.name}!`);
        };
        
        function Student(name, grade) {
          Person.call(this, name);
          this.grade = grade;
        }
        
        Student.prototype = Object.create(Person.prototype);
        Student.prototype.constructor = Student;
        Student.prototype.study = function() {
          console.log(`${this.name} is studying in grade ${this.grade}.`);
        };
        
        const student = new Student('Alice', 10);
        
        // 对象解构赋值取到继承的属性
        const { name, grade } = student;
        console.log(name); // 输出: "Alice"
        console.log(grade); // 输出: 10
        
        // 解构赋值取到继承的方法
        const { sayHello, study } = student;
        sayHello(); // 输出: "Hello, Alice!"
        study(); // 输出: "Alice is studying in grade 10."
        ```
        

### 三. 其他数据类型的解构赋值

-   字符串的解构赋值：可以将字符串按照字符进行解构赋值。
    
    ```javascript
    const [a, b, c] = 'abc';
    console.log(a); // 输出: 'a'
    console.log(b); // 输出: 'b'
    console.log(c); // 输出: 'c'
    ```
    
-   数值和布尔值的解构赋值：会先将数值和布尔值**转换为对应的包装对象类型**（Number、Boolean），然后再进行解构赋值。
    
    示例代码：
    
    ```javascript
    const {toString: numToString} = 123;
    console.log(numToString === Number.prototype.toString); // 输出: true
    
    const {valueOf: boolValueOf} = true;
    console.log(boolValueOf === Boolean.prototype.valueOf); // 输出: true
    ```
    
-   undefined 和 null 的解构赋值：在解构赋值时，如果源值是 undefined 或者 null，则会使用默认值。
    
    示例代码：
    
    ```javascript
    const [x = 0, y] = [undefined, 2];
    console.log(x); // 输出: 0（默认值）
    console.log(y); // 输出: 2
    
    const {z = 'default'} = {z: null};
    console.log(z); // 输出: null（原始值）
    ```
    

注意: 在解构赋值中，如果目标没有对应的值，则可以使用默认值来指定默认取值。而 undefined 和 null 是不能进行解构赋值的 .

___

## 对象字面量的增强

### 一.属性和方法的简洁表示法

1.  **对象字面量**: 一种**创建和初始化对象的方式**，使用花括号 `{}` 来定义一个对象，并通过键值对来指定对象的属性和方法。
    
2.  **属性的简洁表示法**：当属性的键名与变量名相同时，可以使用简洁表示法来定义属性。简洁表示法**直接将变量名作为属性名，并自动将变量的值作为属性值。**
    
    ```javascript
    const name = 'Alice';
    const age = 25;
    
    const person = {
      name,   //使用简洁表示法将变量 `name` 和 `age` 直接作为对象 `person` 的属性
      age
    };
    
    console.log(person.name); // 输出: "Alice"
    console.log(person.age); // 输出: 25
    ```
    
3.  **方法的简洁表示法**：在对象字面量中，可以使用函数字面量来定义一个对象的方法。使用简洁表示法时，可以**省略冒号和 function 关键字，直接将函数体作为方法的值**。示例代码如下：
    
    ```javascript
    const person = {
      name: 'Alice',
      sayHello() {
        console.log(`Hello, my name is ${this.name}`);
      }
    };
    
    person.sayHello(); // 输出: "Hello, my name is Alice"
    ```
    

### 二.方括号表示法

-   方括号表示法是访问对象属性的一种语法，使用方括号 `[]` 来**引用属性名或计算属性**。这种表示法可以动态地获取和设置对象的属性。
    
-   用法：
    
    1.  **属性访问**：通过方括号表示法，可以使用变量或表达式作为属性名，从而**动态地获取对象的属性值**。示例代码如下：
        
        ```javascript
        const obj = {
          name: 'Alice',
          age: 25
        };
        
        const propertyName = 'name';
        
        console.log(obj[propertyName]); // 输出: "Alice"
        ```
        
    2.  **动态属性名**：方括号表示法还可以用于**动态地设置对象的属性名**，即使属性名是通过变量或表达式计算得到的。
        
        ```javascript
        const obj = {};
        
        const propertyName = 'name';
        
        obj[propertyName] = 'Alice';
        
        console.log(obj.name); // 输出: "Alice"
        ```
    
-   注意: 在使用方括号表示法访问属性时，属性名可以是任何字符串或能够被转换为字符串的表达式。方括号内的属性名会被解析为字符串，以便与对象的属性进行匹配。
    

___

## 函数参数的默认值

-   概念: 在定义函数时，为参数提供一个默认的初始值。这样，在调用函数时如果没有传递相应参数的值，就可以使用默认值作为参数的值。
    
-   用法: 函数参数的默认值可以在函数定义的括号内直接设置，使用 `=` 运算符来指定默认值。示例如下：
    
    ```javascript
    function greet(name = 'Alice') {
      console.log('Hello, ' + name);
    }
    
    greet(); // 输出: "Hello, Alice"
    greet('Bob'); // 输出: "Hello, Bob"
    ```
    
-   注意: 参数的默认值的应用是惰性求值的，即默认值在函数每次调用时都会被重新计算。
    
    1.  默认值的生效条件：
        
        -   默认值只会在参数值为 `undefined` 时生效。如果传递了参数但不为 `undefined`（例如 `null`、空字符串等），则默认值不会生效。
        -   当没有传递对应的参数（即没有提供参数值）时，默认值会生效。
        
        ```javascript
        function greet(name = 'Alice') {
          console.log('Hello, ' + name);
        }
        
        greet(); // 默认值生效，输出: "Hello, Alice"
        greet(undefined); // 默认值生效，输出: "Hello, Alice"
        greet(null); // 默认值不生效，输出: "Hello, null"
        greet('Bob'); // 默认值不生效，输出: "Hello, Bob"
        ```
        
    2.  默认值表达式：
        
        -   默认值可以是任何合法的表达式，包括调用函数、三元运算符、数学运算等。
        -   默认值表达式在定义函数时就会被计算，而不是在每次函数调用时计算。
        
        ```javascript
        function getDefaultValue() {
          console.log('Calculating default value...');
          return 'Default Value';
        }
        
        function func(param = getDefaultValue()) {
          console.log('Param:', param);
        }
        
        // 只有没有传递参数时，才会计算默认值
        func(); // 输出: "Calculating default value..."，"Param: Default Value"
        
        // 传递参数时，不计算默认值
        func('Custom Value'); // 输出: "Param: Custom Value"
        ```
        
    3.  设置默认值的小技巧：
        
        -   函数参数的默认值，最好从参数列表的右边开始设置
            
        -   默认值可以使用函数参数的默认值或其他局部变量。
            
        -   可以通过使用逻辑运算符（如 `||`）来提供默认值，如果左侧操作数为 `undefined`，那么返回右侧操作数。
            
        
        ```javascript
        // 使用其他局部变量作为默认值
        function combineStrings(str1, str2 = '') {
          const combinedString = str1 + ' ' + str2;
          console.log(combinedString);
        }
        
        combineStrings('Hello'); // 输出: "Hello "
        combineStrings('Hello', 'world!'); // 输出: "Hello world!"
        
        // 使用逻辑运算符设置默认值
        function greet(name) {
          name = name || 'Anonymous';
          console.log('Hello, ' + name);
        }
        
        greet(); // 输出: "Hello, Anonymous"
        greet('Alice'); // 输出: "Hello, Alice"
        ```
    
-   函数参数的默认值的应用
    
    ```javascript
      // 接收一个对象作为参数
      const logUser = ({usename = 'zhangsan',age = 0,sex = 'male'}={})=>console.log(usename,age,sex);
      logUser(); // 输出: zhangsan 0 male
    ```
    

## 剩余参数

-   剩余参数（Rest Parameters）是 ES6 中引入的一种语法，用于声明一个函数接收可变数量的参数，并将这些参数表示为一个数组。剩余参数使用三个点（…）在函数参数列表中表示。

1.  语法：
    
    在函数定义时，使用三个点（…）后跟一个参数名称来声明剩余参数。
    
    ```javascript
    function myFunction(...args) {
      // 函数体
    }
    ```
    
2.  使用范例：
    
    剩余参数以数组的形式表示传递给函数的所有多余参数。
    
    ```javascript
    function sum(...numbers) {
      let total = 0;
      for (let i = 0; i < numbers.length; i++) {
        total += numbers[i];
      }
      return total;
    }
    
    console.log(sum(1, 2, 3, 4, 5)); // 输出: 15
    ```
    
3.  结合其他参数使用：
    
    剩余参数可以与其他参数一起使用，但必须是最后一个参数。
    
    ```javascript
    function greet(greeting, ...names) {    // greet() 函数接收一个 `greeting` 参数和多个 `names` 参数。剩余参数 `names` 表示除第一个参数之外的所有其他参数，并将它们存储在一个数组中
      console.log(greeting + " " + names.join(", "));
    }
    
    greet("Hello", "Alice", "Bob", "Carl"); // 输出: Hello Alice, Bob, Carl
    ```
    

## 展开运算符

展开运算符（Spread Operator）是 ES6 中引入的一种语法，用于在某些上下文中**将数组或对象展开为单独的元素**。展开运算符使用三个点（…）作为前缀。

以下是展开运算符的用法：

1.  展开数组：
    
    在函数调用、数组字面量、数组解构赋值等场景中，可以使用展开运算符将数组展开为独立的元素。
    
    ```javascript
    const numbers = [1, 2, 3];
    console.log(...numbers); // 输出: 1 2 3
    
    const sum = (a, b, c) => a + b + c;
    console.log(sum(...numbers)); // 输出: 6
    ```
    
2.  合并数组：
    
    使用展开运算符还可以合并多个数组为一个新数组。
    
    ```javascript
    const arr1 = [1, 2, 3];
    const arr2 = [4, 5, 6];
    const mergedArray = [...arr1, ...arr2];
    console.log(mergedArray); // 输出: [1, 2, 3, 4, 5, 6]
    ```
    
3.  复制数组或对象：
    
    展开运算符可以用于浅复制数组或对象。
    
    ```javascript
    const originalArray = [1, 2, 3];
    const newArray = [...originalArray];
    console.log(newArray); // 输出: [1, 2, 3]
    
    const originalObject = { a: 1, b: 2 };
    const newObject = { ...originalObject };
    console.log(newObject); // 输出: { a: 1, b: 2 }
    ```
    
4.  合并对象属性：
    
    在对象字面量中，展开运算符可以用于合并多个对象的属性。
    
    ```javascript
    const obj1 = { a: 1, b: 2 };
    const obj2 = { c: 3, d: 4 };
    const mergedObject = { ...obj1, ...obj2 };
    console.log(mergedObject); // 输出: { a: 1, b: 2, c: 3, d: 4 }
    ```
    

注意: 展开运算符在数组和对象的浅复制（第一级）方面非常有用。如果展开的数组或对象包含嵌套的引用类型数据，仅会复制引用，而不是创建新的独立实例。

## set和map数据结构

-   Set 和 Map 是 ES6 中引入的两种新的数据结构，用于**存储和管理数据**。它们可以处理唯一性需求、键值对需求、去重需求等，适用于许多实际场景，如数据过滤、数据映射、缓存管理

1.  Set 数据结构：
    
    Set 是一种有序且唯一的**集合**，它的值可以是任何类型。
    
    Set 中的值是不重复的，重复的值将被自动去重。
    
    常见的 Set 操作方法如下：
    
    -   `add(value)`: 向 Set 中添加一个值。
    -   `delete(value)`: 删除 Set 中指定的值。
    -   `has(value)`: 检查 Set 中是否包含指定的值。
    -   `size`: 返回 Set 中的元素个数。
    -   `clear()`: 清空 Set 中的所有元素。
    
    ```javascript
    const mySet = new Set();
    
    mySet.add(1);
    mySet.add(2);
    mySet.add(3);
    mySet.add(2); // 重复值不会被添加
    
    console.log(mySet); // 输出: Set {1, 2, 3}
    console.log(mySet.has(2)); // 输出: true
    console.log(mySet.size); // 输出: 3
    
    mySet.delete(2);
    console.log(mySet); // 输出: Set {1, 3}
    
    mySet.clear();
    console.log(mySet); // 输出: Set {}
    ```
    
2.  Map 数据结构：
    
    Map 是一种用于**存储键值对的有序列表**，其中的键唯一且值可以是任意类型。
    
    常见的 Map 操作方法如下：
    
    -   `set(key, value)`: 向 Map 中添加一个键值对。
    -   `get(key)`: 获取指定键的值。
    -   `delete(key)`: 删除指定键的键值对。
    -   `has(key)`: 检查 Map 中是否包含指定的键。
    -   `size`: 返回 Map 中键值对的数量。
    -   `clear()`: 清空 Map 中所有的键值对。
    
    ```javascript
    const myMap = new Map();
    
    myMap.set('name', 'Alice');
    myMap.set('age', 25);
    myMap.set('gender', 'female');
    myMap.set('name', 'Bob'); // 覆盖已有的键值对
    
    console.log(myMap); // 输出: Map(3) {"name" => "Bob", "age" => 25, "gender" => "female"}
    console.log(myMap.get('age')); // 输出: 25
    console.log(myMap.size); // 输出: 3
    
    myMap.delete('gender');
    console.log(myMap); // 输出: Map(2) {"name" => "Bob", "age" => 25}
    
    myMap.clear();
    console.log(myMap); // 输出: Map {}
    ```
    

## 遍历器与for…of循环

遍历器（Iterator）和 `for...of` 循环是 JavaScript 中用于**遍历数据结构**的机制。

1.  遍历器（Iterator）：
    
    遍历器是一种接口，提供了一种统一的方式来**遍历数据结构中的元素**。它可以用于遍历`Array、String、Set、Map 、NodeList、arguments`等**可迭代对象**（Iterable) —— 具有内置符号`[Symbol.iterator]()` 方法的对象。
    
    -   遍历器具有一个 `next()` 方法，每次调用该方法都会返回一个包含 `value` 和 `done` 两个属性的对象。
    -   `value` 表示当前遍历到的值。
    -   `done` 表示遍历是否结束。结果为布尔值,`done: true`时结束
    
    ```javascript
    const iterable = [1, 2, 3];
    const it = iterable[Symbol.iterator]();
    
    console.log(it.next()); // 输出: { value: 1, done: false }
    console.log(it.next()); // 输出: { value: 2, done: false }
    console.log(it.next()); // 输出: { value: 3, done: false }
    console.log(it.next()); // 输出: { value: undefined, done: true }  
    ```
    
2.  `for...of` 循环：
    
    `for...of` 循环是一种语法结构，用于遍历支持遍历器的可迭代对象，如数组、字符串、Set、Map NodeList、arguments。
    
    ```javascript
    const iterable = [1, 2, 3];
    for (let item of iterable) {
      console.log(item);
    }
    // 输出: 1
    //       2
    //       3
    ```
    
    在 `for...of` 循环中，每次迭代都会自动调用可迭代对象的遍历器的 `next()` 方法，并将返回的 `value` 赋值给循环变量（这里是 `item`）。循环会在遍历器返回 `{ done: true }` 表示遍历结束时停止。
    

## ES6 新增方法

### 一. 字符串的新增方法

1.  `startsWith(searchString, position)`和 `endsWith(searchString, endPosition)`：判断一个字符串是否以指定的字符开头或结尾，并可指定起始位置或终止位置。
    
    ```javascript
    const str = "Hello, world!";
    console.log(str.startsWith("Hello")); // 输出: true
    console.log(str.endsWith("world!")); // 输出: true
    ```
    
2.  `includes(searchString, position)`：判断一个字符串是否包含指定的字符，并可指定起始位置。
    
    ```javascript
    const str = "Hello, world!";
    console.log(str.includes("o")); // 输出: true
    ```
    
3.  `repeat(count)`：复制并连接一个字符串的指定次数。
    
    ```javascript
    const str = "Hello";
    console.log(str.repeat(3)); // 输出: HelloHelloHello
    ```
    
4.  `padStart(targetLength, padString)` 和 `padEnd(targetLength, padString)`：用指定字符在字符串的开头或结尾填充到指定长度。
    
    ```javascript
    const str = "Hello";
    console.log(str.padStart(8, "X")); // 输出: XXXHello
    console.log(str.padEnd(8, "X")); // 输出: HelloXXX
    ```
    
5.  `trim()`：删除字符串开头和结尾的空格,常用于表单提交
    
    ```javascript
    const str = "  Hello, world!  ";
    console.log(str.trim()); // 输出: "Hello, world!"
    ```
    

### 二. 数组的新增方法

1.  `from(arrayLike, mapFn, thisArg)`：将一个类数组对象或可迭代对象转换成一个真正的数组。
    
    ```javascript
    const arr1 = Array.from("hello");
    console.log(arr1); // 输出: ["h", "e", "l", "l", "o"]
    
    const arr2 = Array.from([1, 2, 3], x => x * 2);
    console.log(arr2); // 输出: [2, 4, 6]
    ```
    
2.  `find(callback, thisArg)`：返回数组中满足条件的第一个元素;`findIndex(callback, thisArg)`：返回数组中满足条件的第一个元素的索引。
    
    ```javascript
    const arr = [5, 12, 8, 130, 44];
    const found = arr.find(element => element > 10);
    console.log(found); // 输出: 12
    console.log(foundIndex); // 输出: 1
    ```
    
3.  `includes(valueToFind, fromIndex)`：判断数组是否包含指定的元素。
    
    ```javascript
    const arr = [1, 2, 3, 4, 5];
    console.log(arr.includes(3)); // 输出: true
    ```
    
4.  `fill(value, start, end)`：使用指定的值填充数组的所有元素。
    
    ```javascript
    const arr = [1, 2, 3, 4, 5];
    arr.fill(0);
    console.log(arr); // 输出: [0, 0, 0, 0, 0]
    ```
    

### 三. 对象的新增方法

1.  `Object.assign(target, ...sources)`：用于将一个或多个源对象的属性复制到目标对象中。它返回目标对象。
    
    ```javascript
    const target = { a: 1 };
    const source = { b: 2, c: 3 };
    
    const result = Object.assign(target, source);
    console.log(result); // 输出: { a: 1, b: 2, c: 3 }
    ```
    
2.  `Object.keys(obj)`：返回一个数组，其中包含给定对象自身可枚举属性的名称。
    
    ```javascript
    const obj = { name: "John", age: 30, gender: "male" };
    const keys = Object.keys(obj);
    console.log(keys); // 输出: ["name", "age", "gender"]
    ```
    
3.  `Object.values(obj)`：返回一个数组，其中包含给定对象自身可枚举属性的值。
    
    ```javascript
    const obj = { name: "John", age: 30, gender: "male" };
    const values = Object.values(obj);
    console.log(values); // 输出: ["John", 30, "male"]
    ```
    
4.  `Object.entries(obj)`：返回一个数组，其中包含给定对象自身可枚举属性的键值对。
    
    ```javascript
    const obj = { name: "John", age: 30, gender: "male" };
    const entries = Object.entries(obj);
    console.log(entries); // 输出: [["name", "John"], ["age", 30], ["gender", "male"]]
    ```
    
5.  `Object.freeze(obj)`：冻结一个对象，使其属性不可修改、添加或删除。该方法返回被冻结的对象。
    
    ```javascript
    const obj = { name: "John" };
    Object.freeze(obj);
    
    obj.age = 30;
    console.log(obj); // 输出: { name: "John" }
    ```