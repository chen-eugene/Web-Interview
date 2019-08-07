#### [1、CSS选择器。](http://www.ruanyifeng.com/blog/2009/03/css_selectors.html)
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
  - E:link :               匹配所有未被点击的链接。
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

#### [4、浮动布局](https://www.cnblogs.com/iyangyuan/archive/2013/03/27/2983813.html)


#### 4、盒模型注意点。

  - inline:
    - margin-top和margin-bottom无效
    - margin-left和margin-right有效
    - padding-left和padding-right有效
    - padding-top和padding-bottom无效

  - inline-block:
  
  - block:
  <br>

#### [5、弹性布局](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
  
  - flex-direction　　容器内项目的排列方向(默认横向排列)　　
  - flex-wrap　　容器内项目换行方式
  - flex-flow　　以上两个属性的简写方式
  - justify-content　　项目在主轴上的对齐方式
  - align-items　　项目在交叉轴上如何对齐
  - align-content　　定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
<br>

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
<br> 
  
 #### [7、父元素与子元素的width的关系。](https://www.cnblogs.com/zhuzhenwei918/p/6389567.html)
 
  - 父子元素都是内联元素：宽度是由其内容撑起来的，故为auto。
  
  - 父子元素都是块级元素：对于块级元素，子元素的宽度默认为父元素的100%。
 <br>
 
 #### [8、inline、inline-block、block的区别。](https://www.cnblogs.com/KeithWang/p/3139517.html)
 
  - display:block
    - block元素会独占一行，多个block元素会各自新起一行。默认情况下，block元素宽度自动填满其父元素宽度。
    - block元素可以设置width,height属性。块级元素即使设置了宽度,仍然是独占一行。
    - block元素可以设置margin和padding属性。
  
  - display:inline
    - inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。
    - inline元素设置width,height属性无效。
    - inline元素的margin和padding属性，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果；但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。

  - display:inline-block
    - 简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性。
  
  
多个inline元素和inline-block元素同行展示时会出现间距问题:
  
  - 方法一：父元素设置font-size:0 
&nbsp;&nbsp;此种方法给父元素设置了font-size:0之后必须给该元素设置font-size

  - 方法二：给该元素float:left      
&nbsp;&nbsp;此种方法虽然可以实现取消间距，但是可能对布局产生影响，需要考虑布局

 - 方法三：letter-spacing:0
&nbsp;&nbsp;这里父元素需要设置letter-spacing属性的值为一个负值，具体值的大小看情况，但是我们可以无限写小，无妨碍，如letter-spacing：-1000px 
  
  
  
  
  
  
  
