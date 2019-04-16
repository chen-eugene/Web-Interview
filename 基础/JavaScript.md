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

  - ①字面量方式：使用Object构造函数和字面量会产生大量的重复代码。
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
  
  - ②工厂模式：没有解决对象的识别问题（即怎么知道一个对象的类型）
  ```
  function createPerson(name,age,job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayNamge = function(){
      alert(this.name);
    }
    return o;
  }
  ```

  
  - ③构造器模式：利用函数作用域使用自定义构造函数模式模仿类。构造器模式就是一种变相的工厂模式。
  ```
  function Person(name,age){
    this.name = name;
    this.age = age;
    this.print = function(){
      console.log(this.name + this.age)
    };
  }
  ```
  [new命令的作用，就是执行一个构造函数，并且返回一个对象实例。使用new命令时，它后面的函数调用就不是正常的调用，而是依次执行下面的步骤。](https://juejin.im/entry/584a1c98ac502e006c5d63b8)   
   - a：创建一个空对象，作为将要返回的对象实例。
   - b：将空对象的原型指向了构造函数的prototype属性。
   - c：将空对象赋值给构造函数内部的this关键字。
   - d：开始执行构造函数内部的代码。
   
   缺点：每个方法都要在每个实例上重新创建一遍。
  
  - ④原型模式
  ```
  function Person(){}
  
  Person.prototype.name = "Nicholas";
  Person.prototype.age = 29;
  Person.prototype.job = "Software Engineer";
  Person.prototype.sayName = function(){
    alert(this.name);
  };
  ```


#### 4、理解原型对象。

  























