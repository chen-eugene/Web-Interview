#### 1、let和var的区别。

  1. 先声明，后使用：let必须先声明再使用，否则会报错。
  2. let重复声明会报错；var后声明的变量值将会覆盖先声明的值。
  3. 作用域：let的作用域为代码块内，而var的作用域为函数体。
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

#### 2、ES5没有块级作用域，只有全局作用域和函数作用域，ES6新增了块级作用域。
  
<br>

#### 3、const本质。
  
&nbsp;&nbsp;`const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。

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



