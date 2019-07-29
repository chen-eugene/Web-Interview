目录：       
&emsp;[第一章-第五章](#第一章-第五章)          
&emsp;[第六章 面向对象的程序设计](#第六章面向对象的程序设计)      
&emsp;[第七章-第八章](#第七章-第八章)    
&emsp;[第十章 DOM](#第十章DOM)    


### 第一章-第五章


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
   
#### 2、数据类型。

  - 基本数据类型：Undefined、Null、Boolean、Number、String
  - 复杂数据类型：Object，本质上是由一组无序的名值对组成的
  
  type操作符：
  - "undefined"——如果这个值未定义
  - "boolean"——如果这个值是布尔值
  - "string"——如果这个值是字符串
  - "number"——如果这个值是数值
  - "object"——如果这个值是对象或 null
  - "function"——如果这个值是函数
  
  Object:
  - constructor：保存着用于创建当前对象的函数。
  - hasOwnProperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名(propertyName)必须以字符串形式指定(例 如:o.hasOwnProperty("name"))。
  - isPrototypeOf(object)：用于检查传入的对象是否是传入对象的原型。
  - propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用for-in语句来枚举。与 hasOwnProperty()方法一样，作为参数的属性名必须以字符串形式指定。
  - toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应。
  - toString()：返回对象的字符串表示。
  - valueOf()：返回对象的字符串、数值或布尔值表示。通常与 toString()方法的返回值相同。
  
  相等和全等的区别：全等在比较之前不转换操作数，相等会在比较值钱转换成数值。
<br>

#### [3、执行环境及作用域链的理解。](https://segmentfault.com/a/1190000015782315)

   - 执行环境：每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被推入一个环境栈中。 而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。
   
   &emsp;&emsp;在 Web 浏览器中，全局执行环境被认为是 window 对象，因此所有的全局变量和函数都是作为window对象的属性和方法创建。全局执行环境直到应用程序退出——例如关闭网页或浏览器——时才会被销毁。
   
   - 作用域链：当代码在一个环境中执行时，会创建变量对象的一个作用域链。它保证了执行环境对所有变量和函数的有序访问。
   
   &emsp;&emsp;作用域链的前端，始终都是当前执行的代码所 在环境的变量对象。如果这个环境是函数，则将其**活动对象(activation object)** 作为变量对象。活动对象在最开始时只包含一个变量，即 arguments 对象(这个对象在全局环境中是不存在的)。
<br>

#### [4、call、apply和bing的作用。](https://www.cnblogs.com/coco1s/p/4833199.html)
  
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
<br>

#### 5、引用数据类型

   - Array:数组的每一项都可以保存任何类型的数据。
      - 当作栈使用：push()、pop()
      - 当作队列使用：shift()、push()、unshift()【与shift方法相反，同时使用unshifit和pop可以从末端移除项】
      - 排序方法：reverse、sort
      - 操作方法：
         - concat：根据当前数组生成新的数组，`var colors2 = colors.concat("yellow", ["black", "brown"]);`
         - slice：截取数组`var colors3 = colors.slice(1,4);`
         - splice(起始位置，要删除的向，...)：如splice(2,1,"red","green");会删除当前数组位置 2 的项，然后再从位置 2 开始插入字符串 "red"和"green"。
      - 位置方法：
         - indexOf()
         - lastIndexOf()：从数组的末尾开始向前查找
      - 迭代方法：
         - every()：如果该函数对每一项都返回 true，则返回 true
         - filter()：返回该函数会返回 true 的项组成的数组
         - forEach()：
         - map()：
         - some()：如果该函数对任一项返回 true，则返回 true
      - 归并方法：
         - reduce()：从数组的第一项开始，逐个遍历到最后
         - reduceRight()：从数组的最后一项开始，向前遍历到第一项
         ```
         var values = [1,2,3,4,5];
         //prev:前一个值 cur:当前值 index:索引 array:数组对象
         var sum = values.reduce(function(prev, cur, index, array){
             return prev + cur;
         });
         alert(sum); //15
         ```

   - Function类型：每个函数都是Function类型的实例。
      
      - 函数没有重载
      
      - 函数声明和函数表达式
      ```
      alert(sum(10,10));
      //函数声明
      function sum(num1, num2){
         return num1 + num2;
      }
      
      alert(sum(10,10)); //运行期间会产生错误
      //函数表达式
      var sum = function(num1, num2){
         return num1 + num2;
      };
      ```
     &emsp;&emsp; 解析器会率先读取函数声明，并使其在执行任何代码之前可用(可以访问);至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。
     
     - 函数内部属性：arguments、this
        - arguments：它是一个类数组对象，包含传入函数找那个的所有参数。
        - this：和Java中的this大致类似，指向的时候函数的执行环境对象。
        
     - 函数属性和方法：length、prototype
        - length：表示函数希望接受的命名参数的个数。
        - prototype：指向原型对象
        
        - apply()：接收两个参数：第一个为运行函数的作用域；第二个可以使Array实例，也可以是arguments对象。
        - call()：第一个参数为作用域，其余参数必须将函数的参数列举出来。     
<br>

#### 6、字面量
   
&emsp;&emsp;在编程语言中，字面量是一种表示值的记法。
   
   - 字符串字面量：是指双引号引住的一系列字符，双引号中可以没有字符，可以只有一个字符，也可以有很多个字符，`var test="hello world!"; "hello world!"就是字符串字面量，test是变量名`
   - 数组字面量：`var team=["tom","john","smith","kobe"]; ["tom","john","smith","kobe"]是数组字面量`
   - 对象字面量：`var person={name:"tom",age:"26",sex:"male"}; {name:"tom",age:"26",sex:"male"}为对象字面量`
   - 函数字面量：
   ```
   var person={
      name:"tom",
      age:"23",
      tell:function(){alert(name);}
   }
   ```
&emsp;&emsp;其中tell的值function{alert(name);}被认为是函数字面量，在调用时，函数不会执行，而是被当做数据来传递。

&emsp;&emsp;当然如果想把函数字面量当作函数来运行，可以使用eval(String)函数，让String里面的JavaScript执行运算：

&emsp;&emsp; 看到上面的示例，也许你会想到JSON（JavaScript Object Notation），对的，两者的确是有联系的。
JSON（JavaScript对象记法），它是一种用于描述文件和数组的记法，JSON由JavaScript字面量的一个子集组成。JSON可以用于交换数据，通常用它来替代xml。
<br>
<br>

---

### 第六章面向对象的程序设计


#### [1、理解原型对象和原型链。](https://www.cnblogs.com/wilber2013/p/4924309.html)

  - **所有的对象都有”__proto__“属性，该属性对应对象的原型**    
  
  "[[Prototype]]"作为对象的内部属性，是不能被直接访问的。所以为了方便查看一个对象的原型，Firefox和Chrome中提供了"__proto__"这个非标准（不是所有浏览器都支持）的访问器（ECMA引入了标准对象原型访问器"Object.getPrototype(object)"）。
  
 - **所有的函数对象都有"prototype"属性，该属性的值会被赋值给该函数创建的对象的"__proto__"**    
 
  每一个函数都有一个prototype属性，当一个函数被用作构造函数来创建实例时，该函数的prototype属性值将被作为原型赋值给所有对象实例（也就是设置实例的__proto__属性），也就是说，所有实例的原型引用的是函数的prototype属性。“prototype属性为函数对象特有的，如果不是函数对象，将不会有这个属性。”

  - **所有的原型对象都有一个"constructor"属性，这个属性对应创建所有指向该原型的实例的构造函数。**
  
  - **函数对象和原型对象通过"prototype"和"constructor"属性进行相互关联**
  
  当一个函数被当做构造函数来创建实例时，该函数的prototype属性值被作为原型赋值给所有对象实例（也就是设置实例的__proto__属性）
<br>
  
#### 2、原型链的缺点和对象冒充。

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
<br>

#### 3、对象创建的几种方式。

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
<br>
<br>

---

### 第七章-第八章


#### 1、递归
   
&emsp;&emsp;arguments.callee 是一个指向正在执行的函数的指针，因此可以用它来实现对函数的递归调用。
   ```
   function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * arguments.callee(num-1);
   } }
   ```
<br>

#### [2、this关键字的指向问题。](https://www.ibm.com/developerworks/cn/web/1207_wangqf_jsthis/index.html)

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
<br>

#### [2、JavaScript的this原理。](http://www.ruanyifeng.com/blog/2018/06/javascript-this.html)
<br>

#### 3、window对象

&emsp;&emsp;BOM的核心对象是 window，表示浏览器的一个实例。它既是通过 JavaScript 访问浏览器的一个接口，又是 ECMAScript 规定的 Global 对象。这就意味着在网页中定义的任何一个对象、变量和函数，都以 window 作为其 Global 对象。

   - 全局作用域
   
&emsp;&emsp;由于 window 对象同时扮演着 ECMAScript 中 Global 对象的角色，因此所有在全局作用域中声明的变量、函数都会变成 window 对象的属性和方法

   - 打开窗口：`window.open()`，接收四个参数
      - 要加载的URL（必须）
      - 窗口目标（和 <a> 标签的target属性一样）
      - 一个逗号分隔的设置字符串，表示在新窗口中都显示哪些特性
      - 一个表示新页面是否取代浏览器历史记录中当前加载也的布尔值（只在不打开新窗口的情况下使用）

   - 超时调用和间歇调用
      - setTimeout：接收两个参数：要执行的代码和时间
      ```
      setTimeout(function() {
         alert("Hello world!");
      }, 1000);
      ```
      - setInterval：
      ```
      var num = 0;
      var max = 10;
      var intervalId = null;
      
      function incrementNumber() {
         num++;
         //如果执行次数达到了 max 设定的值，则取消后续尚未执行的调用 
         if (num == max) {
            clearInterval(intervalId);
            alert("Done");
         }
      }
      intervalId = setInterval(incrementNumber, 500);      
      ```

   - 系统对话框
      - alert()：通常使用 alert()生成的“警告”对话框向用户显示一些他们无法控制的消息，例如错误消息。而 用户只能在看完消息后关闭对话框。
      - confirm()：与alert的区别，“确认”对话框除了显示 OK 按钮外，还会显示一个 Cancel(“取消”)按钮，两个按钮可以让用户决定是否执行给定的操作
      - prompt()：提示框中除了显示 OK 和 Cancel 按钮之外，还会显示一个文本输入域，以供用户在其中输入内容
<br>

#### 4、location对象
      
&emsp;&emsp;**每次修改 location 的属性(hash 除外)，页面都会以新 URL 重新加载。**
      
   ```
   //立即打开新URL并在浏览器的历史记录中生成一条记录
   location.assign("http://www.wrox.com");

   //和location.assign效果一样
   window.location = "http://www.wrox.com";
   location.href = "http://www.wrox.com";

   //假设初始 URL 为 http://www.wrox.com/WileyCDA/
   
   //将 URL 修改为"http://www.wrox.com/WileyCDA/#section1"
   location.hash = "#section1";
   
   //将 URL 修改为"http://www.wrox.com/WileyCDA/?q=javascript" 
   location.search = "?q=javascript";
   
   //将 URL 修改为"http://www.yahoo.com/WileyCDA/" 
   location.hostname = "www.yahoo.com";
   
   //将 URL 修改为"http://www.yahoo.com/mydir/" 
   location.pathname = "mydir";
   
   //将 URL 修改为"http://www.yahoo.com:8080/WileyCDA/" 
   location.port = 8080;

   ```
   <br>
   <br>
   
   ### 第十章DOM
   
   
   
   
   
  




