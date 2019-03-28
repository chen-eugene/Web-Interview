#### 1、let和var的区别。

  - 先声明，后使用：let必须先声明再使用，否则会报错。
  - let禁止重复声明，var后声明的变量值将会覆盖先声明的值。
  - 作用域：let的作用域为代码块内，而var的作用域为函数体。
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

#### 2、对象创建的几种方式。

  - ①字面量方式：
  ```
  let person = {
    name:"xiaoming",
    sayName:function(){
      console.log(this.name);
    }
    features:{
      height:"176cm",
      weight:"60kg",
    }
  }
  ```
  
  - ②Object构造函数创建：
  ```
  let person = new Object();
  person.name = "xiaoming";
  person.age = 21;
  ```
  
  - ③构造器模式：利用函数作用域使用自定义构造函数模式模仿类。
  ```
  function Person(name,age){
    this.name = name;
    this.age = age;
    this.print = function(){
      console.log(this.name + this.age)
    };
  }
  ```
  
  - ④原型模式


























