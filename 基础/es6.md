#### 1、let和var的区别。

  1. 先声明，后使用：let必须先声明再使用，否则会报错。
  2. let不能重复申明；var后声明的变量值将会覆盖先声明的值。
  3. 作用域：let的作用域为代码块内，而var会发生变量提升（ES5没有块级作用域，只有全局作用域和函数作用域，ES6新增了块级作用域。）。
  ```
  function() {
    var varTest = 'test var OK.';
    let letTest = 'test let OK.';

    {
      var varTest = 'varTest changed.';
      let letTest = 'letTest changed.';
    } 

    console.log(varTest); //输出"varTest changed."，内部"{}"中声明的varTest变量覆盖外部的letTest声明
    console.log(letTest); //输出"test let OK."，内部"{}"中声明的letTest和外部的letTest不是同一个变量
  }
  ```
<br>

#### 2、const本质。
  
&emsp;&emsp;`const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。

  - 对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。

  - 对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，const只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。
  
  ```
  const foo = {};

  // 为 foo 添加一个属性，可以成功
  foo.prop = 123;
  foo.prop // 123

  // 将 foo 指向另一个对象，就会报错
  foo = {}; // TypeError: "foo" is read-only
  ```
  
<br>

#### 3、扩展运算符。
  
  - 合并数组：
  ```
  console.log(...[1, 2, 3])
  // 1 2 3

  console.log(1, ...[2, 3, 4], 5)
  // 1 2 3 4 5

  [...arr1, ...arr2, ...arr3]
  // [ 'a', 'b', 'c', 'd', 'e' ]
  ```
  
  - 对象的扩展：对象的扩展运算符（...）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。
  ```
  {...{}, a: 1}
  // { a: 1 }
  let aWithOverrides = { ...a, x: 1, y: 2 };
  // 等同于
  let aWithOverrides = { ...a, ...{ x: 1, y: 2 } };
  // 等同于
  let x = 1, y = 2, aWithOverrides = { ...a, x, y };
  // 等同于
  let aWithOverrides = Object.assign({}, a, { x: 1, y: 2 });
  ```
  
  
  
  
  
<br>

#### 4、对象属性的遍历。

  - `for...in`：循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）
  
  - `Object.keys(obj)`：返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名
  
  - `Object.getOwnPropertyNames(obj)`：返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名
  
  - `Object.getOwnPropertySymbols(obj)`：返回一个数组，包含对象自身的所有 Symbol 属性的键名
  
  - `Reflect.ownKeys(obj)`：返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举

<br>

#### 6、Symbol，新的原始数据类型
  
&emsp;&emsp;ES5 的对象属性名都是字符串，这容易造成属性名的冲突，ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

&emsp;&emsp;Symbol 值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

<br>

#### 5、Promise：异步编程的一种解决方案。

  - 对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）
  
  - 一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。

&emsp;&emsp;ES6以前的异步回调：
  ```
  //最原始的写法-同步写法

  f1(); //耗时很长，严重堵塞
  f2(); 
  f3(); //导致f3执行受到影响


  //改进版-异步写法
  function f1(callback){
　 　setTimeout(function () {
　 　　　// f1的任务代码
　 　　　callback();
　 　}, 1000);
  }

  f1(f2); //

  f3();
  ```
  
  


















