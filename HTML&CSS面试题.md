# HTML

### 1. HTML5有哪些更新

1.语义化标签

- header:  定义文档的页眉（头部）；
- aside：定义其所处内容之外的内容（侧边）；
- nav：定义导航链接的部分；
- article：定义文章内容；
- section：定义文档中的节（语义化div）；
- footer：定义文档或节的页脚（底部）；

2.媒体标签

- audio:  音频

- video:  视频

3.DOM查询操作

- document.querySelector()
- document.querySelectorAll()

4.Web存储

- localStorage:  本地持久存储
- sessionStorage:  当前窗口本地存储

5.其他

- canvas:  画布

### 2. 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？

- 行内元素有：`a b span img input select strong`；
- 块级元素有：`div ul ol li dl dt dd h1 h2 h3 h4 h5 h6 p`；

空元素，即没有内容的HTML元素。空元素是在开始标签中关闭的，也就是空元素没有闭合标签：

- 常见的有：`<br>`、`<hr>`、`<img>`、`<input>`、`<link>`、`<meta>`；

### 3. Canvas和SVG的区别

- Canvas:  位图
- SVG:  矢量图

### 4. src和href的区别

src和href都是**用来引用外部的资源**，它们的区别如下：

- **src：** 它指向的内容会嵌入到当前标签所在的位置。
- **href：** 它指向一些网络资源的链接。

### 5.行内元素和块级元素

行内元素排在一行, 宽高无法设置,块级元素独占一行

### 6. script 标签中 defer 和 async 的区别？

- `async script` ：异步执行js脚本，有可能会阻塞 HTML 的解析。
- `defer script`：完全不会阻塞 HTML 的解析，解析完成之后再执行js脚本。



# CSS

### 1. CSS选择器及其优先级

| **选择器**     | **格式**      | **优先级权重** |
| -------------- | ------------- | -------------- |
| id选择器       | #id           | 100            |
| 伪类选择器     | li:last-child | 11             |
| 类选择器  | .classname     | 10   			|
| 属性选择器      | a[ref=“eee”]   | 10 				|
| 标签选择器     | div           | 1              |
| 伪元素选择器   | li:after      | 1              |
| 相邻兄弟选择器 | h1 + p        | 0              |
| 子选择器       | ul>li         | 0              |
| 后代选择器     | li a          | 0              |
| 通配符选择器   | *             | 0              |

对于选择器的**优先级**：

- 标签选择器、伪元素选择器：1
- 类选择器、属性选择器：10
- 伪类选择器:  11
- id 选择器：100
- 内联样式：1000

**注意事项：**

- !important声明的样式的优先级最高；
- 如果优先级相同，则最后出现的样式生效；
- 继承得到的样式的优先级最低；

### 2. 两栏布局的实现

一般两栏布局指的是**左边一栏宽度固定，右边一栏宽度自适应**，两栏布局的具体实现：

- 利用**浮动**，将左边元素宽度设置为200px，并且设置向左浮动。将右边元素的margin-left设置为200px。

```css
.left {
  float: left;
  width: 200px;
  background: tomato;
}
.right {
  margin-left: 200px;
  background: gold;
}
```

- 利用**浮动**，左侧元素设置固定大小，并左浮动，右侧元素设置overflow: hidden; 这样右边就**触发了BFC**，BFC的区域不会与浮动元素发生重叠，所以两侧就不会发生重叠。

```css
.left{
     width: 100px;
     background: red;
     float: left;
 }
 .right{
     background: blue;
     overflow: hidden;
 }
```

- 利用**flex布局**，将左边元素设置为固定宽度200px，将右边的元素设置为flex:1。

```css
.outer {
  display: flex;
}
.left {
  width: 200px;
  background: tomato;
}
.right {
  flex: 1; //相当于 flex-grow: 1;
  background: gold;
}
```

- 利用**绝对定位**，将父级元素设置为相对定位。左边元素宽度设置为200px，右边元素设置为绝对定位，左边定位为200px，其余方向定位为0。

```css
.outer {
  position: relative;
}
.left {
  width: 200px;
  background: tomato;
}
.right {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 200px;
  background: gold;
}
```

### 3. 三栏布局的实现

三栏布局一般指的是页面中一共有三栏，**左右两栏宽度固定，中间自适应的布局**，三栏布局的具体实现：

- 利用**绝对定位**，左右两栏设置为绝对定位，中间设置对应方向大小的margin的值。

```css
.outer {
  position: relative;
}

.left {
  position: absolute;
  width: 100px;
  background: tomato;
}

.right {
  position: absolute;
  top: 0;
  right: 0;
  width: 200px;
  background: gold;
}

.center {
  margin-left: 100px;
  margin-right: 200px;
  background: lightgreen;
}
```

- 利用**flex布局**，左右两栏设置固定大小，中间一栏设置为flex:1。

```css
.outer {
  display: flex;
}

.left {
  width: 100px;
  background: tomato;
}

.right {
  width: 100px;
  background: gold;
}

.center {
  flex: 1;
  background: lightgreen;
}
```

- 利用**浮动**，左右两栏设置固定大小，并设置对应方向的浮动。中间一栏设置左右两个方向的margin值，注意这种方式**，中间一栏的标签必须放到最后：**

```css
.left {
  float: left;
  width: 100px;
  background: tomato;
}

.right {
  float: right;
  width: 200px;
  background: gold;
}

.center {
  margin-left: 100px;
  margin-right: 200px;
  background: lightgreen;
}
```

### 4.水平垂直居中的方法

- 利用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过translate来调整元素的中心点到页面的中心。该方法需要考虑浏览器兼容问题。

```css
.parent {
  position: relative;
} 

.child {  
  position: absolute;    
  left: 50%;    
  top: 50%;    
  transform: translate(-50%,-50%);
}
```

- 使用flex布局，通过align-items:center和justify-content:center设置容器的垂直和水平方向上为居中对齐，然后它的子元素也可以实现垂直和水平的居中。该方法要考虑兼容的问题

```css
.parent {
    display: flex;
    justify-content:center;
    align-items:center;
}
```

### 5.清除浮动的方法

```css
// 伪元素
.clear::after{
    content: '';
    display: block;
    clear: both;
}
```

### 6.BFC

**理解:**

- BFC是一个独立的渲染容器，在这个容器中元素按照一定规则进行摆放，并且不会影响外界元素。

**创建BFC的常见条件：**

- 元素设置浮动：float 除 none 以外的值；
- 元素设置绝对定位：position (absolute、fixed)；
- overflow 值为：除visible以外的值;

**BFC的作用(使用场景)**:

- 解决margin重叠
- 解决高度塌陷

### 7.盒模型

标准盒模型和IE盒模型的区别在于设置width和height时，所对应的范围不同：

- 标准盒模型的width和height属性的范围只包含了content，
- IE盒模型的width和height属性的范围包含了border、padding和content。

可以通过修改元素的box-sizing属性来改变元素的盒模型：

- `box-sizeing: content-box`表示标准盒模型（默认值）
- `box-sizeing: border-box`表示IE盒模型（怪异盒模型）

### 8. position的属性有哪些，区别是什么

| 属性值   | 概述                                                         |
| -------- | ------------------------------------------------------------ |
| absolute | 生成绝对定位的元素，相对于static定位以外的一个父元素进行定位。元素的位置通过left、top、right、bottom属性进行规定。 |
| relative | 生成相对定位的元素，相对于其原来的位置进行定位。元素的位置通过left、top、right、bottom属性进行规定。 |
| fixed    | 生成绝对定位的元素，指定元素相对于屏幕视⼝（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变，⽐如回到顶部的按钮⼀般都是⽤此定位⽅式。 |
| static   | 默认值，没有定位，元素出现在正常的文档流中，会忽略 top, bottom, left, right 或者 z-index 声明，块级元素从上往下纵向排布，⾏级元素从左向右排列。 |
| inherit  | 规定从父元素继承position属性的值                             |

### 9. 隐藏元素的方法

1.`display：none`，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素。 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）

2.`visibility：hidden`，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已 经绑定的事件 ，隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

3.`opacity：0`，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定 一些事件，如click 事件，那么点击该区域，也能触发点击事件的

### 10. 实现三角形

```css
div {
    width: 0;
    border-bottom: 50px solid red;
    border-right: 50px solid transparent;
    border-left: 50px solid transparent;
}
```

### 11. CSS3中有哪些新特性

- 圆角 （border-radius:8px）
- 阴影（Shadow）
- 文字特效 （text-shadow）
- 文字渲染 （Text-decoration）
- 线性渐变 （gradient）
- 旋转 （transform）

