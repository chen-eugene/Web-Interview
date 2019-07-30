目录：    
&emsp;[第一章 Vue实例](#第一章Vue基础)

<br>

### 第一章Vue基础

#### 1、Vue生命周期函数。

  ![生命周期](https://github.com/chen-eugene/Web-Interview/blob/master/images/lifecycle.png)

 - 创建期间的生命周期函数：
    + beforeCreate：实例刚在内存中被创建出来，此时，还没有初始化好 data 和 methods 属性
    + created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
    + beforeMount：此时已经完成了模板的编译，但是还没有挂载到页面中
     + mounted：此时，已经将编译好的模板，挂载到了页面指定的容器中显示
     
 - 运行期间的生命周期函数：
 	  + beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
  	+ updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
    
 - 销毁期间的生命周期函数：
  	+ beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。
  	+ destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。
<br>

#### 2、计算属性和方法的区别
  ```
  <p>Reversed message: "{{ reversedMessage() }}"</p>
  
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
  
  methods: {
    reversedMessage: function () {
      return this.message.split('').reverse().join('')
    }
  }
  ```
&emsp;&emsp;计算属性是基于它们的响应式依赖进行缓存的。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。
<br>

#### 3、绑定Class和Style

**绑定class**

  - 传入对象
  ```
  //v-bind:class 指令也可以与普通的 class 属性共存
  //如果 isActive = true; hasError = true，class 列表将变为 "static active text-danger"。
  <div 
    class="static"
    v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>
  
  //绑定的数据对象不必内联定义在模板里
  //我们也可以在这里绑定一个返回对象的计算属性
  <div v-bind:class="classObject"></div>
  
  data: {
    classObject: {
      active: true,
      'text-danger': false
    }
  }
  ```
  
  - 传入数组：
  ```
  <div v-bind:class="[activeClass, errorClass]"></div>
  data: {
    activeClass: 'active',
    errorClass: 'text-danger'
  }
  
  //可以使用三目运算符
  <div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
  
  //可以在数组中添加对象
  <div v-bind:class="[{ active: isActive }, errorClass]"></div>
  ```
<br>

**绑定Style**

  ```
  <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
  data: {
    activeColor: 'red',
    fontSize: 30
  }
  
  //绑定一个样式对象
  <div v-bind:style="styleObject"></div>
  
  //绑定一个数组
  <div v-bind:style="[baseStyles, overridingStyles]"></div>
  ```
<br>

#### 4、组件之间元素的复用
  ```
  <template v-if="loginType === 'username'">
    <label>Username</label>
    <input placeholder="Enter your username" key="username-input">
  </template>
  <template v-else>
    <label>Email</label>
    <input placeholder="Enter your email address" key="email-input">
  </template>
  ```
  在两个组件之间切换，如果不使用key，Vue 会尽可能高效地渲染元素，label和input将会被复用，仅仅替换掉palceholder。如果使用了key，那么这两个input元素将会完全独立，不会进行复用。
<br>

#### 5、v-if和v-show的区别。
  
  - v-if：
    - v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
    - v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
    
  - v-show：不管初始条件是什么，元素总是会被渲染，v-show 只是简单地切换元素的 CSS 属性 display。
  
&emsp;&emsp;v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。  
<br>

#### 6、v-for的使用
  
  - 遍历数组：
  ```
    //第二个参数index为可选参数，即当前项的索引
    <li v-for="(item, index) in items">
      {{ parentMessage }} - {{ index }} - {{ item.message }}
    </li>
    
    data: {
      parentMessage: 'Parent',
      items: [
        { message: 'Foo' },
        { message: 'Bar' }
      ]
    }
  ```
  
  - 遍历对象
  ```
  //第二个的参数为属性名（可选参数）
  //第三个参数作为索引（可选参数）
  <div v-for="(value, name, index) in object">
    {{ index }}. {{ name }}: {{ value }}
  </div>
  
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
  ```

  - 使用key追踪元素：
&emsp;&emsp;v-for 渲染的元素列表时，它默认使用“就地更新”的策略。简单来说，如果数据项的顺序被改变，Vue 将不会更改DOM元素的位置顺序，而是更新元素的内容。
  
&emsp;&emsp; 使用key，用于强制替换元素/组件而不是重复使用它。
  ```
  <div v-for="item in items" v-bind:key="item.id"></div>
  ```
  - v-for和v-if不在同一个元素上使用
    - 为了过滤一个列表中的项目 (比如 `v-for="user in users" v-if="user.isActive"`)。在这种情形下，请将 users 替换为一个计算属性 (比如 activeUsers)，让其返回过滤后的列表。
    - 为了避免渲染本应该被隐藏的列表 (比如 `v-for="user in users" v-if="shouldShowUsers"`)。这种情形下，请将 v-if 移动至容器元素上 (比如 ul, ol)。
    
      用在同意元素时，v-for 比 v-if 具有更高的优先级，因此哪怕我们只渲染出一小部分用户的元素，也得在每次重渲染的时候遍历整个列表，不论活跃用户是否发生了变化。
<br>

#### 2、组件化和模块化。

  - 组件化：从UI的角度进行划分的，方便UI的复用。
  - 模块化：从代码功能的角度进行划分，方便代码分层开发，保证功能模块的只能单一，实现解耦。


#### 3、组件的定义方式。

  - 1、使用Vue.extend和Vue.component方法。
  ```
  var login = Vue.extend({
      template: '<h1>登录</h1>'
    });
  Vue.component('login', login);
  ```
  - 2、直接使用Vue.component方法。
  ```
  Vue.component('register', {
      template: '<h1>注册</h1>'
  });
  ```
  - 3、将模板字符串，定义到script标签中。
  ```
  <script id="tmpl" type="x-template">
      <div><a href="#">登录</a> | <a href="#">注册</a></div>
  </script>
  
  Vue.component('account', {
      template: '#tmpl'
  });
  ```
  - 4、使用 template元素，定义组件的html模板结构。
  ```
  
  <template id="tmp1">
    <div>
      <h1>这是通过template元素，在外部定义的组件结构，这个方式，有代码的智能提示和高亮</h1>
      <h4>好用，不错</h4>
    </div>
  </template>
  
  Vue.component("component",{
    template:"#tmpl"
  });

  ```
  

#### 4、组件中的data和Vue实例中的data的区别。
    
   - 组件中的data必须是一个function，并且放回一个对象。
   - Vue实例中的data可以是一个对象。
    
   **这样做的目的是避免组件之间的数据保持独立，互补影响。**
   
   
#### 5、什么是路由，前端路由和后端路由有什么区别。

  - 后端路由：对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源。
  - [前端路由](https://www.cnblogs.com/joyho/articles/4430148.html)：对于单页面应用程序来说，主要通过URL中的hash来实现不同页面之间切换，同时，hash有一个特点，HTTP请求中不会包含hash相关的内容，所以，单页面程序中的页面跳转主要通过hash实现。**在单页面应用程序中，这种通过hash改变来切换页面的方式，称作前端路由。**






  


