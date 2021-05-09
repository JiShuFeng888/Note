### 1.SVG介绍

```javascript
<body>
<!--
1.注意点:
和canvas一样, svg也有默认的宽高, 并且默认的宽高和canvas都是一样的
默认的宽度是300px, 默认的高度是150px

2.注意点:
和canvas不一样的是, svg可以通过css设置宽高, 也可以通过行内的属性来设置宽高
-->
<svg width="500" height="500">
    <circle cx="100" cy="100" r="50" fill="transparent" stroke="#000"></circle>
</svg>
<script>
    /*
    1.什么是SVG?
    SVG英文全称为Scalable Vector Graphics，意思为可缩放的矢量图

    2.位图和矢量图
    在计算机中有两种图形, 一种是位图, 一种是矢量图
    2.1位图:
    传统的 jpg / png / gif图都是位图
    位图是一个个很小的颜色小方块组合在一起的图片。一个小方块代表1px
    2.2位图的优点和缺点:
    优点: 色彩丰富逼真
    缺点: 放大后会失真, 体积大

    2.3矢量图
    矢量图是用XML格式定义, 通过各种「路径」和「填充颜色」来描述渲染的的图片
    2.4矢量图优点和缺点:
    优点: 放大后不会失真, 体积小
    缺点: 不易制作色彩变化太多的图象
    * */
</script>
```

### 2.SVG使用方式

```javascript
<!--<svg width="500" height="500">
    <circle cx="100" cy="100" r="50" fill="transparent" stroke="#000"></circle>
</svg>-->
<!--<img src="circle.svg" alt="">-->
<div></div>
<script>
    /*
    1.SVG常见的四种使用方式
    1.内嵌到HTML中(直接在HTML中绘制)
    2.通过浏览器直接打开SVG文件
    注意点:
    如果需要将svg保存到一个单独的文件中, 并且需要通过浏览器直接打开, 那么就必须给svg添加一个属性
    xmlns="http://www.w3.org/2000/svg"
    3.在HTML的img标签中引用
    4.作为CSS背景使用
    * */
</script>
```

### 3.SVG绘制矩形

```javascript
<svg width="500" height="500">
    <!--
    x/y: 指定绘制的位置
    width/height: 指定绘制的大小
    fill: 修改填充的颜色
    stroke: 修改描边的颜色
    stroke-width: 修改描边的宽度
    rx/ry: 设置圆角的半径
    -->
    <!--<rect x="100" y="100" width="100" height="100"></rect>-->
    <!--<rect x="100" y="100" width="100" height="100" fill="blue"></rect>-->
    <!--<rect x="100" y="100" width="100" height="100" fill="blue" stroke="red"></rect>-->
    <!--<rect x="100" y="100" width="100" height="100" fill="blue" stroke="red" stroke-width="10"></rect>-->
    <rect x="100" y="100" width="100" height="100" fill="blue"  rx="10" ry="10"></rect>
</svg>
```

### 4.SVG绘制圆和椭圆

```javascript
<svg width="500" height="500">
    <!--<rect x="100" y="100" width="100" height="100" rx="50"></rect>-->
    <!--
    cx/cy: 圆绘制的位置(圆心的位置)
    r: 圆的半径
    -->
    <!--<circle cx="100" cy="100" r="50"></circle>-->

    <!--<rect x="100" y="100" width="200" height="100" rx="100" ry="50"></rect>-->

    <!--
    cx/cy: 椭圆绘制的位置(圆心的位置)
    rx: 水平方向的半径
    ry: 垂直方向的半径
    -->
    <!--<ellipse cx="100" cy="100" rx="100" ry="50"></ellipse>-->
</svg>
```

### 5.SVG绘制直线和折线

```javascript
<svg width="500" height="500">
    <!--绘制直线
    x1/y1: 设置起点
    x2/y2: 设置终点
    -->
    <!--<line x1="100" y1="100" x2="300" y2="100" stroke="#000"></line>-->

    <!--
    绘制折线
    points: 设置所有的点, 两两一对
    -->
    <!--<polyline points="100 100 300 100 300 300" stroke="#000" fill="none"></polyline>-->

    <!--<polyline points="100 100 300 100 300 300 100 100" stroke="#000" fill="none"></polyline>-->

    <!--
    绘制多边形
    polygon和polyline差不多, 只不过会自动关闭路径
    -->
    <polygon points="100 100 300 100 300 300" stroke="#000" fill="none"></polygon>
</svg>
```

### 6.SVG常用属性

```javascript
<svg width="500" height="500">
    <!--
    fill: 修改填充颜色
    fill-opacity: 0~1 设置填充颜色的透明度
    stroke: 修改描边颜色
    stroke-width: 修改描边宽度
    stroke-opacity: 0~1 设置描边透明度
    stroke-linecap: butt/square/round  设置线段两端帽子
    stroke-dasharray: 设置虚线
    stroke-dashoffset: 设置虚线偏移位
    stroke-linejoin: miter/bevel/round 设置折线转角样式
    -->
    <!--<rect x="100" y="100" width="100" height="100" fill="blue"></rect>-->
    <!--<rect x="100" y="100" width="100" height="100" fill="blue" fill-opacity="0.5"></rect>-->
    <!--<line x1="100" y1="100" x2="300" y2="100" stroke="red"></line>-->
    <!--<line x1="100" y1="100" x2="300" y2="100" stroke="red" stroke-width="10"></line>-->
    <!--<line x1="100" y1="100" x2="300" y2="100" stroke="red" stroke-width="10" stroke-opacity="0.5"></line>-->
    <!--
    <line x1="100" y1="100" x2="300" y2="100" stroke="red" stroke-width="10" stroke-linecap="butt"></line>
    <line x1="100" y1="200" x2="300" y2="200" stroke="red" stroke-width="10" stroke-linecap="square"></line>
    <line x1="100" y1="300" x2="300" y2="300" stroke="red" stroke-width="10" stroke-linecap="round"></line>
    -->

    <!--
    注意点:
    在SVG中这些所有的常用属性都是可以直接在CSS中使用的
    -->
    <!--<line x1="100" y1="100" x2="300" y2="100"></line>-->

    <!--<line x1="100" y1="200" x2="300" y2="200" stroke="red" stroke-width="10" stroke-dasharray="10 20 30"></line>-->
    <!--<line x1="100" y1="200" x2="300" y2="200" stroke="red" stroke-width="10" stroke-dasharray="10 " stroke-dashoffset="15"></line>-->
    <!--<line x1="100" y1="300" x2="300" y2="300" stroke="red" stroke-width="10" stroke-dasharray="10 " stroke-dashoffset="-15"></line>-->

    <!--<polyline points="100 100 300 100 300 300" stroke="red" stroke-width="10" fill="none" stroke-linejoin="miter"></polyline>-->
    <!--<polyline points="100 100 300 100 300 300" stroke="red" stroke-width="10" fill="none" stroke-linejoin="bevel"></polyline>-->
    <polyline points="100 100 300 100 300 300" stroke="red" stroke-width="10" fill="none" stroke-linejoin="round"></polyline>
</svg>
```

### 7.SVG绘制路径

```javascript
<svg width="500" height="500">
    <!--
    1.什么是SVG路径
    SVG路径是一个比较牛X的东西, 可以绘制任意图形, 只不过比较复杂而已
    M = moveto  起点
    L = lineto  其它点
    H = horizontal lineto 和上一个点Y相等
    V = vertical lineto   和上一个点X相等
    Z = closepath  关闭当前路径
    -->
    <!--
    S = smooth curveto
    S(x2, y2, x, y)  从当前位置光滑的绘制三次贝塞尔曲线到指定位置

    T = smooth quadratic Bézier curveto
    T(x, y) 从当前位置光滑的绘制二次贝塞尔曲线到指定位置
    -->
    <!--<path d="M 100 100 L 300 100" stroke="red"></path>-->
    <!--<path d="M 100 100 L 300 100 L 300 300" stroke="red" fill="none" stroke-width="10"></path>-->
    <!--<path d="M 100 100 L 300 100 L 300 300 L 100 100" stroke="red" fill="none" stroke-width="10"></path>-->
    <!--<path d="M 100 100 L 300 100 L 300 300 Z" stroke="red" fill="none" stroke-width="10"></path>-->

    <!--<path d="M 100 100 H 300 V 300 Z" stroke="red" fill="none" stroke-width="10"></path>-->
    <!--
   2.路径指令注意点
   大写字母是绝对定位, 小写字母是相对定位
   绝对定位: 写什么位置就是什么位置
   相对定位: 相对上一次的位置, 在上一次位置基础上做调整
   -->
    <path d="M 100 100 l 300 100" stroke="red" stroke-width="10"></path>
</svg>
```

### 8.SVG绘制圆弧

```javascript
<svg width="500" height="500">
    <!--
    <path d="M 100 100 A 100 50 0 0 0 200 150" stroke="red" fill="none"></path>
    <path d="M 100 200 A 100 50 0 1 0 200 250" stroke="red" fill="none"></path>
    <path d="M 100 300 A 100 50 0 0 1 200 350" stroke="red" fill="none"></path>
    <path d="M 100 400 A 100 50 0 1 1 200 450" stroke="red" fill="none"></path>
    -->
    <path d="M 100 400 A 100 50 90 1 1 200 450" stroke="red" fill="none"></path>
</svg>
```

### 9.SVG

```javascript

```

### 10.SVG

```javascript

```

### 11.SVG

```javascript

```

### 12.SVG

```javascript

```

### 13.SVG

```javascript

```

### 14.SVG

```javascript

```

### 15.SVG

```javascript

```

