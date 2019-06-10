#### [1、CSS相对布局和绝对布局。](https://blog.csdn.net/gnail_oug/article/details/77564684)
  
  - absolute：使元素绝对定位，相对于static定位以外的最近的一个祖先元素进行定位。元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。
  - relative：使元素相对定位，相对于自己的正常位置进行定位。
  - flex：使元素绝对定位，相对于浏览器窗口进行定位。元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。

#### [2、CSS动画](https://www.cnblogs.com/smyhvae/p/8435182.html)

#### 3、盒模型注意点。

  - inline:
    - margin-top和margin-bottom无效
    - margin-left和margin-right有效
    - padding-left和padding-right有效
    - padding-top和padding-bottom无效

  - inline-block:
  
  - block:
  

#### [4、垂直居中对齐的方式。](https://www.cnblogs.com/zhouhuan/p/vertical_center.html)

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
  
