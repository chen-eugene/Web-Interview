#### 1、怎么提高页面的打开速度。
   
   &emsp;&emsp;**需要注意的是，带有 src 属性的<script>元素不应该在其<script>和</script>标签之间再包含额外的 JavaScript 代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码 会被忽略。**
  
  - 标签存放的位置：都把全部 JavaScript 引 用放在<body>元素中页面内容的后面
   
  - <script>标签的defer属性：延迟脚本，只适用于外部脚本
  ```
  <!DOCTYPE html>
    <html>
      <head>
        <title>Example HTML Page</title>
        <script type="text/javascript" defer="defer" src="example1.js"></script> 
        <script type="text/javascript" defer="defer" src="example2.js"></script>
      </head>
      <body>
        <!-- 这里放内容 --> 
      </body>
  </html>
  ```
&emsp;&emsp;其中包含的脚本将延迟到浏览器遇到</html>标签后再执行。HTML5 规范要求脚本按照它们出现的先后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于 DOMContentLoaded 事件(详见第 13 章) 9 执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发前执行，因此最好只包含一个延迟脚本。
  
  - <script>元素定义了 async 属性：异步脚本，只适用于外部脚本文件，标记为 async 的脚本并不保证按照指定它们的先后顺序执行。

<br>
<br>
<br>
<br>
<br>
<br>
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
  
  - ④ 原型模式
   - 优点：可以让所有对象实例共享它所包含的属性和方法。
   - 缺点：所有的实例在默认情况下豆浆取得相同的属性值。
  
  ```
  function Person(){}
  
  Person.prototype.name = "Nicholas";
  Person.prototype.age = 29;
  Person.prototype.job = "Software Engineer";
  Person.prototype.sayName = function(){
    alert(this.name);
  };
  ```

  - ⑤ 组合使用构造函数模式和原型模式
   
  优点：
  - 构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。
  - 这种组合模式还支持想构造函数传递参数
  
  ```
  function Person(name,age,job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.freinds = ["Shelby","Court"];
  }
  
  Person.prototype = {
    constructor : Person, //强制指向Person
    sayName : function(){
      alert(this.name);
    }
  }
  ```
  
  - ⑥ 动态原型模式
  
  优点：通过在构造函数中初始化原型（仅在必要的情况下），又保证了同事使用构造函数和原型的优点。
  
  ```
  function Person(name,age,job){
    this.name = name;
    this.age = age;
    this.job = job;
    
    if(typeof this.sayName != "function"){
      Person.prototype.sayName = function(){
        alert(this.name);
      };
    }
  }
  ```
  
  - ⑦ 寄生构造函数模式
  
  ```
  fuction Person(name,age,job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function(){
      alert(this.name);
    };
    return o;
  }
  ```
  
  - ⑧ 稳妥构造函数模式
  
  ```
  fuction Person(name,age,job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function(){
      alert(this.name);
    };
    return p;
  } 
  
  val freind = Person("Nicholas",29,"Software Engineer");
  
  ```

#### [4、理解原型对象和原型链。](https://www.cnblogs.com/wilber2013/p/4924309.html)

  - **所有的对象都有”__proto__“属性，该属性对应对象的原型**    
  
  "[[Prototype]]"作为对象的内部属性，是不能被直接访问的。所以为了方便查看一个对象的原型，Firefox和Chrome中提供了"__proto__"这个非标准（不是所有浏览器都支持）的访问器（ECMA引入了标准对象原型访问器"Object.getPrototype(object)"）。
  
 - **所有的函数对象都有"prototype"属性，该属性的值会被赋值给该函数创建的对象的"__proto__"**    
 
  每一个函数都有一个prototype属性，当一个函数被用作构造函数来创建实例时，该函数的prototype属性值将被作为原型赋值给所有对象实例（也就是设置实例的__proto__属性），也就是说，所有实例的原型引用的是函数的prototype属性。“prototype属性为函数对象特有的，如果不是函数对象，将不会有这个属性。”

  - **所有的原型对象都有一个"constructor"属性，这个属性对应创建所有指向该原型的实例的构造函数。**
  
  - **函数对象和原型对象通过"prototype"和"constructor"属性进行相互关联**
  
  当一个函数被当做构造函数来创建实例时，该函数的prototype属性值被作为原型赋值给所有对象实例（也就是设置实例的__proto__属性）

  
#### 5、原型链的缺点和对象冒充。

  **所有引用类型默认都继承了Object，这个继承也是通过原型链实现的。**
  
  **所有函数的默认原型都是Object的实例，因此默认原型都会包含一个内部指针，指向Object.prototype。**
  
  **原型链的问题：**
  - 属性共享问题：通过原型来实现继承时，原型实际上会变成另一个类型的实例。于是，原先的实例属性也就顺理成章地成了现在的原型属性了。
  - 在创建子类型的实例时，不能向超类型的构造函数中传递参数。即没有办法在不影响所有对象实例的情况下，给超类型的构造函数传递参数。

  **对象冒充：**
  ```
  function SuperType(name){
    this.name = name;
    this.colors = ["red","blue","green"];
  }
  
  function SubType(){
    //继承了SuperType，同时传递了参数
    SuperType.call(this,"Nicholas");
  }
  
  val instance1 = new SubType();
  alert(instance.name);    //"Nicholas";
  instance1.colors.push("black");
  alert(instance1.colors);    //"red,blue,green,black"
  
  var instance2 = new SubType();
  alert(instance2.colors);    //"red,blue,green"
  ```
  **对象冒充无法避免构造函数模式存在的问题，仅仅解决了传参和属性共享问题，但是不能解决函数的复用问题。**
  
  **组合继承：指的是将原型链和借用构造函数的技术组合到一块。思路是使用原型链实现对原型属性和方 法的继承，而通过借用构造函数来实现对实例属性的继承。**
  
  ```
  function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
  }
  
  SuperType.prototype.sayName = function(){
    alert(this.name);
  };
  
  function SubType(name, age){
    //继承属性 SuperType.call(this, name);
    this.age = age;
  }
  ```
  
  
#### [6、call、apply和bing的作用。](https://www.cnblogs.com/coco1s/p/4833199.html)
  
  ```
  function fruits(){}
  
  fruits.prototype = {
    color : "red";
    say : function(){
      console.log("My color is" + this.color);
    }
  }
  
  var apple = new fruits();
  apple.say(); //My color is red
  
  var banana = {
    color : "yellow";
  }
  
  apple.say.call(banana); //My color is yellow
  apple.say.apply(banana); //My color is yellow
  ```
  
  call和apply的作用完全一样，都是改变被调用函数的作用域。不同的是call传递参数的时候是把所有参数依次传递进去，而apply则是将参数封装成数组。
  

 #### [7、this关键字的指向问题。](https://www.ibm.com/developerworks/cn/web/1207_wangqf_jsthis/index.html)

  - 作为对象方法：指向当前对象
  ```
  var point = { 
    x : 0, 
    y : 0, 
    moveTo : function(x, y) { 
      this.x = this.x + x; 
      this.y = this.y + y; 
    } 
  }; 
 
  point.moveTo(1, 1)//this 绑定到当前对象，即 point 对象
  ```
  - 作为函数调用：指向window全局对象
  ```
  function makeNoSense(x) { 
    this.x = x; 
  } 
 
  makeNoSense(5); 
  x;// x 已经成为一个值为 5 的全局变量
  ```
  - 对象函数的内部函数：指向window全局对象
  ```
  var point = { 
    x : 0, 
    y : 0, 
    moveTo : function(x, y) { 
      var that = this;
      // 内部函数
      var moveX = function(x) { 
          that.x = x; //that 指向当前对象
      }; 
      // 内部函数
      var moveY = function(y) { 
          this.y = y; //this 指向window对象
      }; 
 
      moveX(x); 
      moveY(y); 
    } 
  }; 
  point.moveTo(1, 1); 
  point.x; //==>0 
  point.y; //==>0 
  x; //==>1 
  y; //==>1
  ```
  - 作为构造函数调用：指向创建的新对象
  ```
  function Point(x, y){ 
     this.x = x; 
     this.y = y; 
  }
  ```

#### [8、JavaScript的this原理。](http://www.ruanyifeng.com/blog/2018/06/javascript-this.html)

  




