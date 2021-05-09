1.Bootstrap3模板

```javascript
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <!-- 为了让IE浏览器运行在最新的渲染模式下 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!-- 国产浏览器高速模式渲染Webkit内核 -->
    <meta name="renderer" content="webkit">
    <!-- 为了保证移动端能正常显示 -->
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap Template</title>

    <!-- 导入Bootstrap的CSS -->
    <link rel="stylesheet" href="css/bootstrap.css">

    <!-- html5shiv.js和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!-- Ie条件注释，只有在ie浏览器才有效下方是ie9以下的浏览器 -->
    <!--[if lt IE 9]> 
      <script src="./js/html5shiv.js"></script>
      <script src="./js/respond.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>你好，世界！</h1>




    <!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
    <script src="js/jquery-1.12.4.min.js"></script>
    <!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
    <script src="js/bootstrap.js"></script>
  </body>
</html>
```

### 2.Bootstrap4模板

```javascript
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="css/bootstrap.css">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <script src="js/jquery-3.5.1.js"></script>
    <!-- 在bootstrap4中很多提示弹窗通过popper.min.js实现 -->
    <script src="js/popper.min.js"></script>
    <script src="js/bootstrap.js"></script>
  </body>
</html>
```

### 3.Bootstrap容器

```javascript
<!--
    1.Bootstrap容器
    1.1在Bootstrap中容器是响应式布局的基础, Bootstrap推荐将所有内容都定义在容器之中
    1.2并且容器是启用Bootstrap栅格系统必不可少的前置条件

    2. Bootstrap中提供了两个容器: container/container-fluid
    2.1container容器(固定容器):
    只要给标签添加了container类名, 这个标签就变成了Bootstrap的container容器
    只要这个标签变成了Bootstrap的container容器, 在不同视口大小下就会有不同的固定宽度

    2.2container-fluid(自适应宽度容器)
    只要给标签添加了container-fluid类名, 这个标签就变成了Bootstrap的container-fluid容器
    只要这个标签变成了Bootstrap的container-fluid容器, 那么容器的宽度永远都是100%自适应

    3.Bootstrap对视口划分
    Bootstrap4将视口划分为了5钟
    超小屏幕(xs): <576px
    小屏幕(sm): >=576px
    中等屏幕(md):>=768px
    大屏幕(lg): >=992px
    超大屏幕(xl): >= 1200px
-->






  <style>
        *{
            margin: 0;
            padding: 0;
        }
        .container {
            width: 100%;
            padding-right: 15px;
            padding-left: 15px;
            margin-right: auto;
            margin-left: auto;
        }

        @media (min-width: 576px) {
            .container {
                max-width: 540px;
            }
        }

        @media (min-width: 768px) {
            .container {
                max-width: 720px;
            }
        }

        @media (min-width: 992px) {
            .container {
                max-width: 960px;
            }
        }

        @media (min-width: 1200px) {
            .container {
                max-width: 1140px;
            }
        }
        div{
            height: 100px;
            background: red;
        }
    </style>
</head>
<body>
<div class="container"></div>
</body>
```

### 4.Bootstrap4栅格系统的基本使用

```javascript
   <style>
        *{
            margin: 0;
            padding: 0;
        }
        body>div{
            height: 100px;
            background: red;
        }
        .container>.row{
            height: 100%;
            background: blue;
        }
        .row>div{
            background: skyblue;
        }
        .row>div:nth-child(2){
            background: deeppink;
        }
        .row>div:nth-child(3){
            background: orangered;
        }
    </style>
</head>
<body>
<div class="container">
    <span class="row">
        <div class="col-6">我是第1列</div>
        <div class="col-4">我是第2列</div>
        <div class="col-6">我是第3列</div>
    </span>
</div>
<!--
    1.Bootstrap栅格系统
    Bootstrap的栅格系统使用一系列的"行"和"列"来实现复杂的响应式布局
    默认情况下栅格系统会将一行的内容等分为12份,
    然后我们可以通过绑定类名的方式指定这一行中的每一列占用多少分

    2.Bootstrap栅格系统格式
    <容器>
        <行>
            <列>我们的内容</列>
            <列>我们的内容</列>
            ... ...
        </行>
    </容器>

   3.Bootstrap栅格系统特点
   3.1默认情况下行的宽度和所在容器一样
   3.2默认情况下所有列的宽度是等分所在行的宽度
   3.3可以通过col-num方式指定当前列占用12分之几
   3.4如果一行中内容的宽度超过了12分, 那么将自动换行
-->
<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.1.1.js"></script>
<!--在Bootstrap4中很多的提示/弹窗都是通过popper.min.js实现的, 所以需要导入-->
<script src="js/popper.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.js"></script>
</body>
```

### 5.Bootstrap4栅格系统的实现原理

```javascript
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .container {
            width: 100%;
            padding-right: 15px;
            padding-left: 15px;
            margin-right: auto;
            margin-left: auto;
        }

        @media (min-width: 576px) {
            .container {
                max-width: 540px;
            }
        }

        @media (min-width: 768px) {
            .container {
                max-width: 720px;
            }
        }

        @media (min-width: 992px) {
            .container {
                max-width: 960px;
            }
        }

        @media (min-width: 1200px) {
            .container {
                max-width: 1140px;
            }
        }
        div{
            height: 100px;
            background: red;
        }
        .row{
            display: flex;
            flex-wrap: wrap;
            margin-left: -15px;
            margin-right: -15px;
        }
        .container>.row{
            height: 100%;
            background: blue;
        }

        .col{
            flex: 1;
        }
        .row>div{
            background: skyblue;
        }
        .row>div:nth-child(2){
            background: deeppink;
        }
        .row>div:nth-child(3){
            background: orangered;
        }
        .col-6{
            flex-basis: 50%;
        }
    </style>
</head>
<body>
<div class="container">
    <span class="row">
        <div class="col-6">我是第1列</div>
        <div class="col">我是第2列</div>
        <div class="col">我是第3列</div>
    </span>
</div>
</body>
```

### 6.Bootstrap4栅格系统尺寸设置

```javascript
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        body>div{
            height: 100px;
            background: red;
        }
        .container>.row{
            height: 100%;
            background: blue;
        }
        .row>div{
            background: skyblue;
        }
        .row>div:nth-child(2){
            background: deeppink;
        }
        .row>div:nth-child(3){
            background: orangered;
        }
    </style>
</head>
<body>
<div class="container">
    <span class="row">
        <!--<div class="col-6">我是第1列</div>
        <div class="col-4">我是第2列</div>
        <div class="col-2">我是第3列</div>-->
        <!--<div class="col-xl-6">我是第1列</div>
        <div class="col-xl-4">我是第2列</div>
        <div class="col-xl-2">我是第3列</div>-->
        <div class="col-lg-2 col-xl-6">我是第1列</div>
        <div class="col-lg-4 col-xl-4">我是第2列</div>
        <div class="col-lg-6 col-xl-2">我是第3列</div>
    </span>
</div>
<!--
    1.栅格系统列的尺寸设置
    1.1Bootstrap的固定宽度容器提供了5种响应的尺寸,
       同样Bootstrap也给列提供了5种响应的尺寸
    col-*:   设置超小屏幕
    col-sm-*:设置小屏幕
    col-md-*:设置中等屏幕
    col-lg-*:设置大屏幕
    col-xl-*:设置超大屏幕

    2.栅格系统列的尺寸特点
    1.如果只设置了小屏幕的大小, 那么大屏幕也会采用小屏幕设置的大小
    2.如果值设置了大屏幕的大小, 那么小屏幕默认100%
    3.如果大小屏幕都设置了大小, 那么在什么屏幕就显示什么尺寸
-->
```

### 7.Bootstrap4栅格系统沟槽

```javascript
<!--<div class="container px-0">
    <span class="row no-gutters">
        <div class="col-6">我是第1列</div>
        <div class="col-2">我是第2列</div>
        <div class="col-2">我是第3列</div>
    </span>
</div>-->

1.栅格系统-沟槽
    BootStrap默认的栅格和列间有间隙沟槽，一般是左右-15px的margin或padding处理，您可以使用.no-gutters类来消除它，这将影响到.row行、列平行间隙及所有子列
```

### 8.Bootstrap4栅格系统对齐方式

```javascript
栅格系统列-对齐方式
    Bootstrap4的格栅系统是使用伸缩布局实现的, 所以也可以通过类名快速的设置伸缩项的在主轴和侧轴对齐方式


<div class="container">
    <!--<span class="row justify-content-between">-->
    <span class="row align-items-center">
        <div class="col-6">我是第1列</div>
        <div class="col-2">我是第2列</div>
        <div class="col-2">我是第3列</div>
    </span>
</div>
```

### 9.Bootstrap4栅格系统的偏移和排序

```javascript
<div class="container">
    <span class="row justify-content-center">
        <div class="col-2">1</div>
        <div class="col-2">2</div>
        <div class="col-2">3</div>
    </span>
</div>

<div class="container" style="margin-top: 20px">
    <span class="row">
        <div class="col-2 offset-3">1</div>
        <div class="col-2">2</div>
        <div class="col-2">3</div>
    </span>
</div>
-->
<!--
<div class="container">
    <span class="row justify-content-between">
        <div class="col-2">1</div>
        <div class="col-2">2</div>
    </span>
</div>
<div class="container" style="margin-top: 20px">
    <span class="row">
        <div class="col-2">1</div>
        <div class="col-2 offset-8">2</div>
    </span>
</div>
-->
<div class="container">
    <span class="row">
        <div class="col-2 order-3">1</div>
        <div class="col-2 order-2">2</div>
        <div class="col-2 order-1">3</div>
    </span>
</div>

<!--
    1.栅格系统-列偏移
    offset-*: 但前列偏移多少份位置
    注意点: 写在那一列就是那一列偏移

    2.栅格系统列-列排序
    order-*: 从小到大顺序排序, 小的在前面, 大的在后面
    注意点: 没有排序的列位置不会发生变化, 只有排序的列才参与位置变化
-->
```

### 10.Bootstrap4公共样式

```javascript
<body>
<!--
    1.文字颜色
    柔和灰（text-muted）
    主要蓝（text-primary）
    次要灰（text-secondary）
    成功绿（text-success）
    危险红（text-danger）
    警告黄（text-warning）
    危息绿（text-info）
    黑白对比（text-dark）
    注意点: .text-white 、 .text-muted这两个样式不支持链接上使用
-->
<p class="text-success">知播渔</p>
<p class="text-danger">知播渔</p>
<p class="text-warning">知播渔</p>
<!--
    2.背景颜色
    主要蓝（bg-primary）
    次要灰（bg-secondary）
    成功绿（bg-success）
    危险红（bg-danger）
    警告黄（bg-warning）
    危息绿（bg-info）
    黑白对比（bg-dark）
-->
<p class="bg-success">知播渔</p>
<p class="bg-danger">知播渔</p>
<p class="bg-warning">知播渔</p>

<!--
    3.边框相关
    3.1快速添加边框
    border / border-*
    3.2快速删除边框
    border-0 / border-*-0
    3.3快速指定边框颜色
    border-color
    3.4快速添加边框圆角
    rounded / rounded-*
-->
<!--<div class="border-top border-left border-warning"></div>-->
<div class="border border-warning rounded-circle"></div>











<!--
    1.显示模式
    d-*
    d-屏幕尺寸-*
-->
<!--<div class="bg-success d-inline d-sm-inline-block d-md-block">我是div</div>-->

<!--
    2.浮动和清除浮动
    float-*
    float-屏幕尺寸-*
    3.清除浮动
    clearfix
-->
<!--<div class="bg-success clearfix">
    <div class="float-left">左边</div>
    <div class="float-right">右边</div>
</div>-->

<!--
    3.定位
    position-*
-->
<div class="position-relative">我是div</div>







<!--
    1.在Bootstrap中可以通过m-* / p-* 快速添加间隙
    2.在Bootstrap中可以通过 list-unstyled 快速去除项目符号
    3.在Bootstrap中可以通过 img-fluid快速设置等比拉伸图片
    4.在Bootstrap中可以通过 img-thumbnail快速设置缩略图样式
-->
<!--<div class="bg-success m-auto" style="width: 200px; height: 200px"></div>-->
<!--<div class="bg-success pt-5" style="width: 200px; height: 200px">我是div</div>-->

<!--<ol class="list-unstyled">
    <li>我是第1个li</li>
    <li>我是第2个li</li>
    <li>我是第3个li</li>
</ol>-->

<!--<img src="images/img1.jpg" class="img-fluid">-->
<div class="bg-success">
    <img src="images/lnj.jpg" class="img-thumbnail">
</div>
```

### 11.Bootstrap4-提示框组件

```javascript
<!--
    1.什么是role?
    role属性用于增强语义性, 当现有的HTML标签不能充分表达语义性的时候，就可以借助role来说明
    比如用div做button，那么设置div 的 role=“button”，辅助工具就可以认出这实际上是个button

    2.什么是aria-xxx?
    aria全称: Accessible Rich Internet Applications
    这一套协定是w3和apple为了"残疾人士"无障碍使用网站的

    3.什么是aria-hidden?
    为了避免屏幕识读设备抓取非故意的和可能产生混淆的输出内容（尤其是当图标纯粹作为装饰用途时），我们为这些图标设置了 aria-hidden=“true” 属性
-->
<div class="alert alert-success" role="alert">
    A simple primary alert—check it out!
</div>

<div class="alert alert-warning alert-dismissible fade show" role="alert">
    <img src="images/ad.jpg" alt="">
    <!--
    data-dismiss="alert" 告诉bt需要关闭谁
    -->
    <button type="button" class="close" data-dismiss="alert">
        <span>&times;</span>
    </button>
</div>
```

### 12.Bootstrap4-按钮组件和按钮组组件

```javascript
<button type="button" class="btn btn-primary">Primary</button>
<input type="button" value="我是按钮" class="btn btn-success">
<a href="#" class="btn btn-danger">我是按钮</a>


<div class="btn-group">
    <button type="button" class="btn btn-secondary">1</button>
    <button type="button" class="btn btn-secondary">2</button>
    <button type="button" class="btn btn-secondary">3</button>
</div>
```

### 13.Bootstrap4-卡片组件

```javascript
<div class="card" style="width: 18rem;">
    <img class="card-img-top" src="images/img1.jpg">
    <div class="card-body">
        <h5 class="card-title">Card title</h5>
        <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
    </div>
</div>
```

### 14.Bootstrap4轮播图组件

```javascript
<body>
<!--
1.class="carousel slide" 创建一个轮播图组件
2.data-ride="carousel" 自动轮播
-->
<div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
    <!--
    1.class="carousel-indicators" 创建指示器
    2.data-target="#carouselExampleIndicators" 告诉bootstrap当前的索引属于哪一个轮播图
    3.data-slide-to="0" 指定当前指示器的索引
    4.class="active" 设置默认选中的指示器索引
    -->
    <ol class="carousel-indicators">
        <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
        <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
        <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
    </ol>
    <!--
    1.class="carousel-inner" 创建轮播图的内容部分
    2.class="carousel-item" 指定轮播图的每一页
    -->
    <div class="carousel-inner">
        <div class="carousel-item active">
            <img src="images/img1.jpg" class="d-block w-100" alt="...">
        </div>
        <div class="carousel-item">
            <img src="images/img2.jpg" class="d-block w-100" alt="...">
        </div>
        <div class="carousel-item">
            <img src="images/img3.jpg" class="d-block w-100" alt="...">
        </div>
    </div>
    <!--
    1.class="carousel-control-prev" 创建上一页的控制按钮
    2. href="#carouselExampleIndicators" 指定控制按钮可用控制哪一个轮播图
    -->
    <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
    </a>
</div>
<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.1.1.js"></script>
<!--在Bootstrap4中很多的提示/弹窗都是通过popper.min.js实现的, 所以需要导入-->
<script src="js/popper.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.js"></script>
<script>
    $('.carousel').carousel({
        interval: 1000
    });
</script>
</body>
```

### 15.Bootstrap4折叠面板

```javascript
<body>
<!--
1.data-toggle="collapse" 告诉bootstrap需要切换的是折叠面板
2.href="#collapseExample" 告诉bootstrap需要切换的是哪一个折叠面板
-->
<a class="btn btn-primary" data-toggle="collapse" href="#collapseExample" role="button">
    我是按钮
</a>
<!--
1.class="collapse" 创建一个折叠面板
注意点: 折叠面板默认情况下是不会显示的
-->
<div class="collapse bg-danger" id="collapseExample">
    <p>我是段落1</p>
    <p>我是段落2</p>
    <p>我是段落3</p>
    <p>我是段落4</p>
    <p>我是段落5</p>
</div>
<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.1.1.js"></script>
<!--在Bootstrap4中很多的提示/弹窗都是通过popper.min.js实现的, 所以需要导入-->
<script src="js/popper.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.js"></script>
</body>
```

### 16.Bootstrap4下拉菜单

```javascript
<body>
<!--
1.class="dropdown" 创建一个下拉菜单的容器
-->
<div class="dropdown">
    <!--
    1.dropdown-toggle: 指定菜单按钮的小箭头
    2.data-toggle="dropdown": 告诉bootstrap需要切换的是下拉菜单
    -->
    <button class="btn btn-secondary dropdown-toggle"  data-toggle="dropdown">
        我是按钮
    </button>
    <!--
    1.class="dropdown-menu": 创建一个弹出的下拉菜单
    2.class="dropdown-item": 指定菜单项
    -->
    <div class="dropdown-menu">
        <a class="dropdown-item" href="#">Action</a>
        <a class="dropdown-item" href="#">Another action</a>
        <a class="dropdown-item" href="#">Something else here</a>
    </div>
</div>
```

### 17.Bootstrap4-弹窗

```javascript
<body>
<!--
1.data-toggle="modal": 告诉bootstrap需要切换的是模态弹窗
2.data-target="#exampleModal": 告诉bootstrap需要切换的是哪一个模态弹窗
-->
<button class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
    我是按钮
</button>

<!--
class="modal fade": 创建模态弹窗的容器
-->
<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog">
    <!--
    1.class="modal-dialog": 创建真正弹出的内容
    -->
    <div class="modal-dialog" role="document">
        <div class="bg-danger">
            <p>我是段落1</p>
            <p>我是段落2</p>
            <p>我是段落3</p>
            <p>我是段落4</p>
            <p>我是段落5</p>
        </div>
    </div>
</div>

<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.1.1.js"></script>
<!--在Bootstrap4中很多的提示/弹窗都是通过popper.min.js实现的, 所以需要导入-->
<script src="js/popper.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.js"></script>

</body>
```

### 18.Bootstrap4提示气泡

```javascript
<body>

<div style="margin: 200px">
    <!--
    1.data-toggle="tooltip": 告诉bootstrap需要切换的是提示气泡
    2.data-placement="top": 告诉bootstrap提示气泡出现的位置
    3.title="Tooltip on top": 告诉bootstrap提示气泡中提示的内容是什么
    -->
    <!--
    <button class="btn btn-secondary" data-toggle="tooltip" data-placement="left" title="内容是什么">
        我是按钮
    </button>
    -->

    <!--
    1.data-container="body": 当你在一个父元素上有一些样式与提示框产生样式干扰，你可以指定一个自定义的container容器，这样提示框的HTML将出现在这个元素内部了。
    2.data-toggle="popover": 告诉bootstrap需要切换的是提示气泡
    3.data-placement="top": 告诉bootstrap提示气泡出现的位置
    4.data-content="": 告诉bootstrap提示气泡中提示的内容是什么
    -->
    <button class="btn btn-secondary" data-container="body" data-toggle="popover" data-placement="right" data-content="我是内容我是内容">
        我是按钮
    </button>
</div>


<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.1.1.js"></script>
<!--在Bootstrap4中很多的提示/弹窗都是通过popper.min.js实现的, 所以需要导入-->
<script src="js/popper.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.js"></script>
<script>
    /*
    $(function () {
        $('[data-toggle="tooltip"]').tooltip()
    })
    */
    $('button').popover()
</script>
</body>
```

### 19.Bootstrap4菜单栏

```javascript
<body>
<!--
1.class="navbar": 告诉Bootstrap需要创建一个响应式的导航栏
2.class="navbar-expand-lg": 告诉Bootstrap在哪一种屏幕尺寸上需要展示完整的导航栏
3.class="navbar-light bg-light": 设置导航栏的主题样式
-->
<nav class="navbar navbar-expand-xl navbar-light bg-light">
    <!--
    1.class="navbar-brand": 指定导航栏中公司的品牌信息(公司名称/LOGO)
    -->
    <a class="navbar-brand" href="#">知播渔</a>
    <!--
    1.class="navbar-toggler": 创建一个移动端的菜单按钮
    2.data-toggle="collapse": 告诉bootstrap需要切换的是折叠面板
    3.data-target="#navbarSupportedContent": 告诉bootstrap需要切换的是哪一个折叠面板
    4.class="navbar-toggler-icon": 设置按钮的字体图标
    -->
    <button class="navbar-toggler"  data-toggle="collapse" data-target="#navbarSupportedContent">
        <span class="navbar-toggler-icon"></span>
    </button>
    <!--
    1.class="collapse": 创建一个折叠面板
    注意点: 折叠面板默认情况下是不会显示的
    2.class="navbar-collapse":用于通过父断点进行分组和隐藏导航列内容
    -->
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <!--
        1. class="navbar-nav": 创建导航栏的菜单
        2. class="nav-item": 创建导航来的菜单项
        -->
        <ul class="navbar-nav mr-auto">
            <li class="nav-item">
                <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item active">
                <a class="nav-link" href="#">Link</a>
            </li>
            <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    Dropdown
                </a>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <a class="dropdown-item" href="#">Action</a>
                    <a class="dropdown-item" href="#">Another action</a>
                    <div class="dropdown-divider"></div>
                    <a class="dropdown-item" href="#">Something else here</a>
                </div>
            </li>
            <li class="nav-item">
                <a class="nav-link disabled" href="#">Disabled</a>
            </li>
        </ul>
    </div>
</nav>

<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="js/jquery-3.1.1.js"></script>
<!--在Bootstrap4中很多的提示/弹窗都是通过popper.min.js实现的, 所以需要导入-->
<script src="js/popper.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="js/bootstrap.js"></script>
</body>
```

### 20.Bootstrap4-华为响应式官网

```javascript
bootstrap 默认会给p标签添加margin 

bootstrap 默认会给modal-footer标签添加d-flex 

class="rounded-pill" 边框圆角

class="w-100"       w100%

<input type="button" value="登录" class="btn"> 加btn变按钮

单选框框标签-都忘了怎么用
<form>
<label for="male">Male</label>
<input type="radio" name="sex" id="male" />
<br />
<label for="female">Female</label>
<input type="radio" name="sex" id="female" />
</form>

text-white 文字白色


```

### 21.GSAP动画库

```javascript
<div class="box"></div>
<script>
    /*
    1.什么是ScrollMagic?
    ScrollMagic是一个滚动视差插件
    ScrollMagic本身比较简单，只包含2个类：
    crollMagic.Controller 一个控制器类，用于总体的调度 ；
    ScrollMagic.Scene 一个场景类，用于设计具体的变换。

    需要注意的是，它本身并没有集成 animation的控制方法，动画的实现，需要引入插件 GSAP 或者是 Velocity
    * */
    /*
    1.什么是GSAP?
    GSAP(GreenSock Animation Platform)是一个从flash时代一直发展到今天的专业动画库

    2.GSAP优点
    1、速度快。GSAP专门优化了动画性能，使之实现和CSS一样的高性能动画效果。
    2、轻量与模块化。模块化与插件式的结构保持了核心引擎的轻量，TweenLite包非常小（基本上低于7kb）。GSAP提供了TweenLite, TimelineLite, TimelineMax 和 TweenMax不同功能的动画模块，你可以按需使用。
    3、没有依赖。
    4、灵活控制。不用受限于线性序列，可以重叠动画序列，你可以通过精确时间控制，灵活地使用最少的代码实现动画。

    3.GSAP版本
    GSAP提供4个库文件供用户使用
    1.TweenLite：这是GSAP动画平台的核心部分，使用它可以用来实现大部分的动画效果，适合来实现一些元素的简单动画效果。
    2.TimelineLite：一个强大的，轻量级的序列工具，它就如一个存放补间动画的容器，可以很容易的整体控制补间动画，且精确管理补间动画彼此之间的时间关系。比如动画的各种状态，Pause，reverse，restart，speed up，slow down，seek time，add labels等。它适合来实现一些复杂的动画效果。
    3.TimelineMax：扩展TimelineLite，提供完全相同的功能再加上有用的（但非必需）功能，如repeat，repeatDelay，yoyo，currentLabel()等。TimelineMax的目标是成为最终的全功能工具，而不是轻量级的。
    4.TweenMax：可以完成TimelineLite做的每一件事，并附加非必要的功能，如repeat，yoyo，repeatDelay(重复延迟)等。它也包括许多常见的插件，如CSSPlugin，这样您就不需自行载入多个文件。侧重于全功能的，而不是轻量级的。
    >>建议在开发中使用TweenMax这个全功能的js文件，它包括了GreenSock动画平台的所有核心的功能。

    官网地址：http://www.greensock.com/
    github地址：https://github.com/greensock/GreenSock-JS/
    中文网: https://www.tweenmax.com.cn/
    * */
    // 1.创建TweenMax对象
    /*
    第一个参数: 需要执行动画的元素
    第二个参数: 动画执行的时长
    第三个参数: 具体执行动画的属性
    * */
    // new TweenMax(".box", 3, {x: 500});
    // 2.利用静态方法执行动画
    // 从当前位置到指定位置
    // TweenMax.to(".box", 3, {x: 500});
    // 从指定位置到当前位置
    // TweenMax.from(".box", 3, {x: 500});
    // 从第一个指定的位置到第二个指定的位置
    TweenMax.fromTo(".box", 3, {x: 500}, {x: 200});
</script>
```

### 22.GSAP-Tween.stagger方法

```javascript
 <style>
        *{
            margin: 0;
            padding: 0;
        }
        div{
            width: 100px;
            height: 100px;
            background: red;
        }
        .box2{
            background: blue;
        }
        .box3{
            background: green;
        }
    </style>
</head>
<body>
<div class="box1"></div>
<div class="box2"></div>
<div class="box3"></div>
<script>
    // TweenMax.staggerTo([".box1", ".box2", ".box3"], 3, {x: 500}, 3);
    // TweenMax.staggerFrom([".box1", ".box2", ".box3"], 3, {x: 500}, 3);
    TweenMax.staggerFromTo([".box1", ".box2", ".box3"], 3, {x: 500}, {x: 200}, 3);
</script>
```

### 23.GSAP-Tween动画属性

```javascript
<script>
    new TweenMax(".box", 3, {
        // 设置动画开始之前的延迟时间
        // delay: 2,
        // 设置动画初识值
        startAt: {
            x: 100
        },
        // 设置动画结束值
        css: {
            x: 500,
        },
        // 设置动画重复执行的次数
        // 无限重复 -1
        repeat: 2,
        // 设置动画重复执行的往返动画
        yoyo: true,
        // 设置重复动画开始之前的延迟时间
        repeatDelay: 3,
        // 设置动画执行的节奏
        ease: Bounce.easeOut,
        yoyoEase: Bounce.easeOut
    });
</script>
```

### 24.GSAP循环动画

```javascript
<body>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
<script>
    let oDivs = document.querySelectorAll(".box");
    TweenMax.staggerTo(oDivs, 3, {
        cycle: {
            height: [100, 150, 200],
            backgroundColor: ["red", "green", "blue"]
        }
    }, 3);
</script>
</body>
```

### 25.GSAP动画常用事件

```javascript
<script>
    let obj = {name: "lnj"};
    TweenMax.to(".box", 3, {
        x: 500,
        delay: 3,
        onStart:function(a, b, c){
            // console.log("动画开始了", a, b, c);
            console.log(this);
        },
        onStartParams:["123", "456", "789"],
        onStartScope: obj,
    });
</script>
```

### 26.GSAP动画常用方法

```javascript
<div class="box"></div>
<button class="start">开始</button>
<button class="paused">暂停</button>
<button class="toggle">切换</button>
<button class="restart">重新开始</button>
<script>
    let tm = TweenMax.to(".box", 3, {
        x: 500,
        paused: true
    });
    // console.log(tm);
    let oStartBtn = document.querySelector(".start");
    oStartBtn.onclick = function () {
        tm.play();
    }

    let oPauseBtn = document.querySelector(".paused");
    oPauseBtn.onclick = function () {
        tm.pause();
    }

    let oToggleBtn = document.querySelector(".toggle");
    oToggleBtn.onclick = function () {
        // tm.paused(true);
        // tm.paused(false);
        // console.log(tm.paused());
        tm.paused(!tm.paused());
    }

    let oRestartBtn = document.querySelector(".restart");
    oRestartBtn.onclick = function () {
        tm.restart();
    }
</script>
```

### 27.GSAP动画管理

```javascript
<script>
    /*
    TweenMax.staggerTo([".box1", ".box2", ".box3"], 3, {
        x: 500
    }, 3);
    */
    /*
    TweenMax.to(".box1", 4, {
        x: 500
    });
    TweenMax.to(".box2", 3, {
        x: 400,
        delay:4
    });
    TweenMax.to(".box3", 3, {
        x: 300,
        delay:7
    });
    */
    let tm = new TimelineMax();
    tm.add(
        TweenMax.to(".box1", 4, {
            x: 500
        })
    );
    tm.add(
        TweenMax.to(".box2", 3, {
            x: 400
        })
    );
    tm.add(
        TweenMax.to(".box3", 3, {
            x: 300
        })
    );
</script>
```

### 28.Velocity

```javascript
<script>
    /*
    1.什么是Velocity?
    Velocity 是一个简单易用、性能极高、功能丰富的轻量级JS动画库。
    它能和 jQuery/Zepto 完美协作，并和$.animate()有相同的 API， 但它不依赖 jQuery，可单独使用。
    Velocity 不仅包含了 $.animate() 的全部功能， 还拥有：颜色动画、转换动画(transforms)、循环、 缓动、SVG 动画、和 滚动动画 等特色功能

    官方地址: https://github.com/julianshapiro/velocity
    中文文档: http://shouce.jb51.net/velocity/index.html

    2.GSAP基本使用
    1.1导入Velocity文件
    1.2利用Velocity实现动画
    * */
    // 1.单独使用
    /*
    let oDiv = document.querySelector(".box");
    Velocity(oDiv, {
        height: "300px"
    }, {
        duration: 3000
    });
    */

    // 2.配合jQuery使用
    // 注意点: 必须先导入jQuery, 再导入velocity
    $(".box").velocity({
        height: "300px"
    }, {
        duration: 3000
    });
</script>
```

### 29.Velocity常用配置

```javascript
<script>
    $(".box").velocity({
        marginLeft: "500px"
    }, {
        duration: 3000,
        // 设置动画开始之前的延迟时间
        // delay: 2000,
        // 设置动画循环的次数
        // 注意点: 从初始位置到指定位置再到初始的位置算一次
        // loop: 2,
        // 设置动画运动的节奏
        // easing: "easeInOutQuint",
        // 设置动画结束之后元素的状态
        // display: "none",
        // visibility: "hidden"
        // 设置动画队列
        // 注意点: 只要设置了动画队列动画就不会自动执行
        queue: "a"
    });

    $(".box").velocity({
        marginTop: "500px"
    }, {
        duration: 3000,
        queue: "b"
    });
    $(".box").dequeue("a");
    setTimeout(function () {
        $(".box").dequeue("b");
    }, 3000)
</script>
```

### 30..Velocity常用事件

```javascript
<body>
<div class="box"></div>
<script>
    $(".box").velocity({
        marginLeft: "500px"
    }, {
        duration: 3000,
        delay: 2000,
        begin: function(elements) {
            console.log("动画开始了", elements);
        },
        complete: function(elements) {
            console.log("动画结束了", elements);
        },
        /*
        elements：当前执行动画的元素，可以用$(elements)来获取
        complete：整个动画过程执行到百分之多少，该值是递增的，注意：该值为一个十进制数值 并不带单位 (%)
        remaining：整个动画过程还剩下多少毫秒，该值是递减的
        start：动画开始时的绝对时间 (Unix time)
        tweenValue：动画执行过程中 两个动画属性之间的补间值
        * */
        progress: function(elements, complete, remaining, start, tweenValue) {
            // console.log("动画正在执行");
            console.log((complete * 100) + "%");
        }
    });
</script>
</body>
```

### 31.ScrollMagic滚动魔法基本使用

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>11-ScrollMagic开篇</title>
    <script src="js/ScrollMagic.js"></script>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        header{
            width: 100%;
            height: 100px;
            background: #000;
        }
        div{
            width: 100%;
            height: 200px;
        }
        .section1{
            background: red;
        }
        .section2{
            background: green;
        }
        .section3{
            background: blue;
        }
        .section4{
            background: deeppink;
        }
        footer{
            width: 100%;
            height: 2000px;
            background: #000;
        }
    </style>
</head>
<body>
<header></header>
<div class="section1"></div>
<div class="section2"></div>
<div class="section3"></div>
<div class="section4"></div>
<footer></footer>
<script>
    /*
    1.什么是ScrollMagic?
    ScrollMagic是一个神奇的滚动效果的插件.
    如果你想在特定的滚动位置开始一个动画，并且让动画同步滚动条的动作，
    或者把元素粘在一个特定的滚动位置，那么这款插件正是你需要的。
    使用 ScrollMagic，你可以很容易地让动画和滚动条的动作同步。
　　使用 ScrollMagic，你可以很容易地把视差效果添加到您的网站中。

    2.ScrollMagic特点:
    优化性能
    **轻量级（压缩后只有6KB）
    灵活可扩展
    **兼容移动设备
    强大的事件管理
    **支持响应式网页设计
    面向对象的编程方式和链式编程方式
    代码可读性强
    支持两个方向的滚动（even different on one page）
    支持在div容器中滚动（一个页面可以支持多个div）
    完善的调试和日志记录功能

    3.官网地址: http://ScrollMagic.io
    https://github.com/janpaepke/ScrollMagic
      官方文档: http://scrollmagic.io/docs/index.html
    * */
    // 1.创建一个控制器对象
    let controller = new ScrollMagic.Controller();
    // 2.创建一个场景对象
    let scene = new ScrollMagic.Scene({
        // 告诉ScrollMagic从什么位置开始当前的场景
        // offset: 100,
        offset: 0,
        // 告诉ScrollMagic当前的场景的有效范围
        duration: 200
    });
    // 告诉ScrollMagic哪一个元素需要固定
    // scene.setPin(".section1");
    scene.setPin(".section1", {pushFollowers: false});
    // 3.将场景对象添加到控制器对象
    controller.addScene(scene);
</script>
</body>
</html>
```

### 32.ScrollMagic滚动魔法基本使用场景配置

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>12-ScrollMagic场景配置</title>
    <script src="js/ScrollMagic.js"></script>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        header{
            width: 100%;
            height: 100px;
            background: #000;
        }
        div{
            width: 100%;
            height: 200px;
        }
        .section1{
            background: red;
        }
        .section2{
            background: green;
        }
        .section3{
            background: blue;
        }
        .section4{
            background: deeppink;
        }
        footer{
            width: 100%;
            height: 2000px;
            background: #000;
        }
    </style>
</head>
<body>
<header></header>
<div class="section1"></div>
<div class="section2"></div>
<div class="section3"></div>
<div class="section4"></div>
<footer></footer>
<script>
    // 官方文档: http://scrollmagic.io/docs/index.html
    // 1.创建一个控制器对象controller
    let controller = new ScrollMagic.Controller();
    // 2.创建一个场景对象scene
    let scene = new ScrollMagic.Scene({
        offset: 0,
        // 告诉ScrollMagic当前的场景从哪一个元素开始
        // triggerElement: "footer",
        // triggerElement: ".section3",
        triggerElement: "header",
        // 告诉ScrollMagic当前的场景从指定元素相对于视口的什么位置开始
        // triggerHook: "onEnter",
        // triggerHook: "onCenter",
        triggerHook: "onLeave",
        duration: 200,
        reverse: false,
    });
    // 告诉ScrollMagic哪一个元素需要固定
    // scene.setPin(".section1", {pushFollowers: false});
    scene.setPin(".section1"	);
    // 3.将场景对象添加到控制器对象
    controller.addScene(scene);
</script>
</body>
</html>
```

### 33.ScorllMagic-GSAP结合使用

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>13-ScrollMagic-GSAP动画</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        header{
            width: 100%;
            height: 100px;
            background: #000;
        }
        div{
            width: 100%;
            height: 200px;
        }
        .section1{
            background: red;
        }
        .section2{
            background: green;
        }
        .section3{
            background: blue;
        }
        .section4{
            background: deeppink;
        }
        footer{
            width: 100%;
            height: 2000px;
            background: #000;
        }
        p{
            width: 100px;
            height: 100px;
            background: purple;
            margin: 0 auto;
        }
    </style>
    <script src="js/ScrollMagic.js"></script>
    <script src="js/TweenMax.js"></script>
    <script src="js/animation.gsap.js"></script>
</head>
<body>
<header></header>
<div class="section1">
    <p class="anim"></p>
</div>
<div class="section2"></div>
<div class="section3"></div>
<div class="section4"></div>
<footer></footer>
<script>
    // 1.创建一个控制器对象controller
    let controller = new ScrollMagic.Controller();
    // 2.创建一个场景对象scene
    let scene = new ScrollMagic.Scene({
        offset: 100,
        duration: 200,
    });
    // 告诉ScrollMagic哪一个元素需要固定
    scene.setPin(".section1");
    /*
    // 创建一个GSAP动画
    let tm = TweenMax.to(".anim", 3, {
        width: 200,
        height: 200
    });
    scene.setTween(tm);
    */
    scene.setTween(".anim", 3, {
        width: 200,
        height: 200
    });
    // 3.将场景对象添加到控制器对象
    controller.addScene(scene);
</script>
</body>
</html>
```

### 34.ScorllMagic-velocity结合使用

```javascript
企业开发中如果想要滚动和动画同步，就用ScorllMagic-GSAP
企业开发中如果想要滚动和不动画同步，就用ScorllMagic-velocity


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>14-ScrollMagic-Velocity动画</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        header{
            width: 100%;
            height: 100px;
            background: #000;
        }
        div{
            width: 100%;
            height: 200px;
        }
        .section1{
            background: red;
        }
        .section2{
            background: green;
        }
        .section3{
            background: blue;
        }
        .section4{
            background: deeppink;
        }
        footer{
            width: 100%;
            height: 2000px;
            background: #000;
        }
        p{
            width: 100px;
            height: 100px;
            background: purple;
            margin: 0 auto;
        }
    </style>
    <script src="js/ScrollMagic.js"></script>
    <script src="js/velocity.js"></script>
    <script src="js/animation.velocity.js"></script>
</head>
<body>
<header></header>
<div class="section1">
    <p class="anim"></p>
</div>
<div class="section2"></div>
<div class="section3"></div>
<div class="section4"></div>
<footer></footer>
<script>
    // 1.创建一个控制器对象controller
    let controller = new ScrollMagic.Controller();
    // 2.创建一个场景对象scene
    let scene = new ScrollMagic.Scene({
        offset: 100,
        // 注意点: 如果需要结合Velocity来使用, 那么在创建场景的时候就不能指定有效范围
        // duration: 200,
    });
    // 告诉ScrollMagic哪一个元素需要固定
    scene.setPin(".section1");
    scene.setVelocity(".anim", {
        width: "200px",
        height: "200px"
    }, {
        duration: 3000
    });
    // 3.将场景对象添加到控制器对象
    controller.addScene(scene);
</script>
</body>
</html>

```

### 35.ScorllMagic事件

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>15-ScrollMagic事件</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        header{
            width: 100%;
            height: 100px;
            background: #000;
        }
        div{
            width: 100%;
            height: 200px;
        }
        .section1{
            background: red;
        }
        .section2{
            background: green;
        }
        .section3{
            background: blue;
        }
        .section4{
            background: deeppink;
        }
        footer{
            width: 100%;
            height: 2000px;
            background: #000;
        }
    </style>
    <script src="js/ScrollMagic.js"></script>
    <script src="js/velocity.js"></script>
    <script src="js/animation.velocity.js"></script>
</head>
<body>
<header></header>
<div class="section1"></div>
<div class="section2"></div>
<div class="section3"></div>
<div class="section4"></div>
<footer></footer>
<script>
    // 1.创建一个控制器对象controller
    let controller = new ScrollMagic.Controller();
    // 2.创建一个场景对象scene
    let scene = new ScrollMagic.Scene({
        offset: 100,
        duration: 200,
    });
    // 告诉ScrollMagic哪一个元素需要固定
    scene.setPin(".section1");
    scene.on("start", function (event) {
        console.log("进入场景");
    });
    scene.on("end", function (event) {
        console.log("离开场景");
    });
    scene.on("progress", function (event) {
        console.log("场景执行过程中" + event.progress);
    });
    // 3.将场景对象添加到控制器对象
    controller.addScene(scene);
</script>
</body>
</html>
```

