#### 1、CSS选择器。
  **基本选择器：**
  - '*' :     通用选择器，匹配所有元素。
  - E:        标签选择器，匹配使用E的标签。
  - .info:    class选择器，匹配所有class属性中包含info的元素。
  - #footer:  id选择器，匹配id为footer的元素。  
  
  **多元素的组合选择器：**
  - E,F:    多元素选择器，同时匹配所有E元素或F元素，E和F之间用逗号隔开。
  - E F:    后代元素选择器，匹配所有属于E元素后代的F元素，E和F之间用空格隔开。
  - E > F:  子元素选择器，匹配所有E元素的子元素F。
     
  **伪类选择器：**
  - E:fisrt-child:         匹配父元素的第一个子元素。
  - E:link:                匹配所有未被点击的链接。
  - E:visited:             匹配所有已被点击的链接。
  - E:active:              匹配所有鼠标已经按下，但是还没有释放的E元素。
  - E:hover:               匹配鼠标悬停其上的E元素。
  - E:focus:               匹配获得当前焦点的E元素。
  - E:lang(c):             匹配lang属性等于c的E元素。
  - E:first-line:          匹配E元素的第一行。
  - E:first-letter:        匹配E元素的第一个字母。
  - E:before:              在E元素之前插入生成的内容。
  - E:after:               在E元素之后插入生成的内容。
  - E:enabled:             匹配表单中激活的元素。
  - E:disabled:            匹配表单中禁用的元素。
  - E:checked:             匹配表单中被选中的Radio(单选框)或CheckBox(复选框)元素。
  - E::selection:          匹配用户当前选中的元素。
  - E:root:                匹配文档的根元素，对于HTML文档，就是HTML元素。
  - E:nth-child(n):        匹配其父元素的第n个子元素，第一个编号为1。
  - E:nth-lasht-child(n):  匹配其父元素的倒数第n个子元素，第一个编号为1。
  - E:nth-of-type(n):      与:nth-child()作用类似，但是仅匹配使用同种标签的元素。
  - E:nth-last-of-type(n): 与:nth-last-child() 作用类似，但是仅匹配使用同种标签的元素。
  - E:last-child:          匹配父元素的最后一个子元素，等同于:nth-last-child(1)。
  - E:first-of-type:       匹配父元素下使用同种标签的第一个子元素，等同于:nth-of-type(1)。
  - E:last-of-type:        匹配父元素下使用同种标签的最后一个子元素，等同于:nth-last-of-type(1)。
  - E:only-child:          匹配父元素下仅有的一个子元素，等同于:first-child:last-child或 :nth-child(1):nth-last-child(1)。
  - E:only-of-type:        匹配父元素下使用同种标签的唯一一个子元素，等同于:first-of-type:last-of-type或 :nth-of-type(1):nth-last-of-type(1)。
  - E:empty:               匹配一个不包含任何子元素的元素，注意，文本节点也被看作子元素。
  - E:not(s):              匹配不符合当前选择器的任何元素。
  - E:target:              匹配文档中特定"id"点击后的效果。



#### [2、CSS相对布局和绝对布局。](https://blog.csdn.net/gnail_oug/article/details/77564684)
  
  - absolute：使元素绝对定位，相对于static定位以外的最近的一个祖先元素进行定位。元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。
  - relative：使元素相对定位，相对于自己的正常位置进行定位。
  - flex：使元素绝对定位，相对于浏览器窗口进行定位。元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。

#### [3、CSS动画](https://www.cnblogs.com/smyhvae/p/8435182.html)

#### 4、盒模型注意点。

  - inline:
    - margin-top和margin-bottom无效
    - margin-left和margin-right有效
    - padding-left和padding-right有效
    - padding-top和padding-bottom无效

  - inline-block:
  
  - block:
  

#### [5、弹性布局](https://www.cnblogs.com/xuyuntao/articles/6391728.html)
  
  - flex-direction　　容器内项目的排列方向(默认横向排列)　　
  - flex-wrap　　容器内项目换行方式
  - flex-flow　　以上两个属性的简写方式
  - justify-content　　项目在主轴上的对齐方式
  - align-items　　项目在交叉轴上如何对齐
  - align-content　　定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。


#### [6、垂直居中对齐的方式。](https://www.cnblogs.com/zhouhuan/p/vertical_center.html)

  - 1、使用绝对定位和负外边距对块级元素进行垂直居中(必须提前知道被居中块级元素的尺寸，否则无法准确实现垂直居中。)
  ```
  <div id="box">
    <div id="child">我是测试DIV</div>
  </div>
  
  #box {
    width: 300px;
    height: 300px;
    background: #ddd;
    position: relative;
  }
  #child {
    width: 150px;
    height: 100px;
    background: orange;
    position: absolute;
    top: 50%;
    margin: -50px 0 0 0;
    line-height: 100px;
  }
  ```
  
  - 2、使用绝对定位和transform
  ```
  <div id="child">
    我是一串很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长的文本
  </div>
  
  #box {
    width: 300px;
    height: 300px;
    background: #ddd;
    position: relative;
  }
  #child {
    background: #93BC49;
    position: absolute;
    top: 50%;
    transform: translate(0, -50%);
  }
  ```
  
  - 3、使用flex布局。
  ```
  <div id="box">雾霾天气，太久没有打球了</div>
  
  #box {
    width: 300px;
    height: 300px;
    background: #ddd;
    display: flex;
    align-items: center;
  }
  
  flex-start:交叉轴的起点对齐；
　flex-end:交叉轴的终点对齐；
　center:交叉轴的中点对齐；
　baseline:项目第一行文字的基线对齐；
　stretch（该值是默认值）:如果项目没有设置高度或者设为了auto，那么将占满整个容器的高度。
  ```

  - 4、使用 line-height 和 vertical-align 对图片进行垂直居中
  ```
  #box{
    width: 300px;
    height: 300px;
    background: #ddd;
    line-height: 300px;
  }
  #box img {
    vertical-align: middle;
  }
  ```
  
  - 5、使用 display 和 vertical-align 对容器里的文字进行垂直居中
  ```
  <div id="box">
    <div id="child">我也是一段测试文本</div>
  </div>
  
  #box {
    width: 300px;
    height: 300px;
    background: #ddd;
    display: table;
  }
  #child {
    display: table-cell;
    vertical-align: middle;
  }
  ```
  
