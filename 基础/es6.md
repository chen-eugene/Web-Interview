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
  



