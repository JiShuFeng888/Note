### 1.移动端JQ自动轮播图

```javascript
		*{
            margin: 0;
            padding: 0;
            touch-action: none;
        }
        div{
            width: 100%;
            position: relative;
            overflow: hidden;
        }
        ul{
            list-style: none;
            width: 500%;
            display: flex;
            justify-content: flex-start;
            position: relative;
            left: 0;
            top: 0;
        }
        ul>li{
            flex: 1;
        }
        ul>li>img{
            width: 100%;
            vertical-align: bottom;
        }
        div>p{
            width: 100%;
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            display: flex;
            justify-content: space-between;
            /*
            告诉浏览器当前元素不需要接收事件
            注意点: 如果父元素不接收事件, 那么默认子元素也不能接收事件
                    如果子元素需要接收事件, 那么必须单独设置为auto
            */
            pointer-events: none;
        }
        div>p>span{
            display: inline-block;
            width: 30px;
            height: 50px;
            line-height: 50px;
            text-align: center;
            font-weight: bold;
            font-size: 30px;
            color: #fff;
            background: rgba(0,0,0,0.3);
            pointer-events: auto;
        }
        ol{
            list-style: none;
            position: absolute;
            left: 50%;
            bottom: 20px;
            transform: translateX(-50%);
            display: flex;
            justify-content: flex-start;
        }
        ol>li{
            width: 20px;
            height: 20px;
            background: #fff;
            border-radius: 50%;
            margin: 0 5px;
        }
        ol>.active{
            background: #f40;
        }
    </style>
    <script src="js/zepto.js"></script>
    <script src="js/selector.js"></script>
    <script src="js/event.js"></script>
    <script src="js/touch.js"></script>
    <script src="js/fx.js"></script>
</head>
<body>
<div>
    <ul>
        <li><img src="images/img1.jpg" alt=""></li>
        <li><img src="images/img2.jpg" alt=""></li>
        <li><img src="images/img3.jpg" alt=""></li>
        <li><img src="images/img4.jpg" alt=""></li>
        <li><img src="images/img1.jpg" alt=""></li>
    </ul>
    <p>
        <span class="left-btn">&lt;</span>
        <span class="right-btn">&gt;</span>
    </p>
    <ol>
        <li class="active"></li>
        <li></li>
        <li></li>
        <li></li>
    </ol>
</div>
<script>
    (function($){
        $.extend($.fn, {
            stop: function(){
                this.css({transition: "none"});
                return this
            },
            isAnimation: function(){
                let time = $("ul").css("transition-duration");
                time = parseFloat(time);
                return time !== 0;
            }
        })
    })(Zepto)
</script>
<script>
    // 1.定义变量保存对当前的索引
    let currentIndex = 0;
    // 2.定义变量保存图片宽度
    let itemWidth = $("ul>li").width();
    // 3.定义变量保存最大的索引
    let maxIndex = $("ul>li").length - 1;
    // 4.监听按钮点击
    $(".left-btn").click(function () {
        clearInterval(timerId);
        if($(this).isAnimation()){return}
        currentIndex--;
        if(currentIndex < 0){
            $("ul").css({left: -maxIndex * itemWidth});
            currentIndex = maxIndex - 1;
        }
        $("ul").animate({left: -currentIndex * itemWidth}, 500, function () {
            autoPlay();
        });
        $("ol>li").eq(currentIndex).addClass("active").siblings().removeClass();
    });
    $(".right-btn").click(function () {
        clearInterval(timerId);
        if($(this).isAnimation()){return}
        currentIndex++;
        if(currentIndex > maxIndex){
            $("ul").css({left: 0});
            currentIndex = 1;
        }
        $("ul").animate({left: -currentIndex * itemWidth}, 500, function () {
            autoPlay();
        });
        let index = currentIndex === 4 ? 0 : currentIndex;
        $("ol>li").eq(index).addClass("active").siblings().removeClass();
    });
    /*
    注意点:
    在移动端中是没有移入和移出事件的
    * */
    /*
    let oUl = document.querySelector("ul");
    oUl.onmouseenter = function () {
        console.log("移入");
    }
    oUl.onmouseleave = function () {
        console.log("移出");
    }
    */
    // 5.实现自动轮播
    let timerId = null;
    function autoPlay() {
        timerId = setInterval(function () {
            $(".right-btn").click();
        }, 2000);
    }
    autoPlay();
    $("ul").get(0).ontouchstart = function () {
        clearInterval(timerId);
    }
    $("ul").get(0).ontouchend = function () {
        autoPlay();
    }
    // 6.实现轻扫切换
    $("ul").swipeLeft(function () {
        $(".right-btn").click();
    });
    $("ul").swipeRight(function () {
        $(".left-btn").click();
    });
</script>
```

### 2.Swiper基本使用

```javascript
 <title>02-swiper基本使用</title>
    <link rel="stylesheet" href="css/swiper.css">
    <script src="js/swiper.js"></script>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .swiper-container{
            width: 400px;
            height: 300px;
            border: 1px solid #000;
            margin: 100px auto;
        }
        .swiper-container>ul{
            list-style: none;
        }
    </style>
</head>
<body>
<div class="swiper-container">
    <ul class="swiper-wrapper">
        <li class="swiper-slide">Slide 1</li>
        <li class="swiper-slide">Slide 2</li>
        <li class="swiper-slide">Slide 3</li>
    </ul>
</div>
<script>
    /*
     1.什么是swiper?
     Swiper是纯javascript打造的滑动特效插件，面向PC、平板电脑等移动终端。
     Swiper能实现触屏焦点图、触屏Tab切换等常用效果。
     Swiper开源、免费、稳定、使用简单、功能强大，是架构移动终端网站的重要选择！
     
     2.如何使用:
     2.1引入swiper对应的css和js文件
     2.2按照框架的需求搭建三层结构
     2.3创建一个Swiper对象, 将容器元素传递给它
      */
    let mySwiper = new Swiper ('.swiper-container');
</script>
```

### 3.Swiper动画

```javascript
 <link rel="stylesheet" href="css/swiper.css">
    <link rel="stylesheet" href="css/swiper.animate.min.css">
    <script src="js/swiper.js"></script>
    <script src="js/swiper.animate1.0.3.min.js"></script>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        p{
            width: 200px;
            height: 200px;
            line-height: 200px;
            text-align: center;
            background: #f00;
            margin: 0 auto;
        }
        @keyframes myFadeIn {
            0% {
                opacity: 0;
                transform: scale(2);
            }

            100% {
                opacity: 1;
                transform: scale(0.5);
            }
        }

        .myFadeIn {
            -webkit-animation-name: myFadeIn;
            animation-name: myFadeIn
        }
    </style>
</head>
<body>
<div class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">
            <!--
            swiper-animate-effect：切换效果，例如 fadeInUp
            swiper-animate-duration：可选，动画持续时间（单位秒），例如 0.5s
            swiper-animate-delay：可选，动画延迟时间（单位秒），例如 0.3s
            -->
            <p class="ani" swiper-animate-effect="myFadeIn">内容</p>
        </div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
    </div>
</div>
<script>
    var mySwiper = new Swiper ('.swiper-container', {
        on:{
            init: function(){
                swiperAnimateCache(this); //隐藏动画元素 
                swiperAnimate(this); //初始化完成开始动画
            },
            slideChangeTransitionEnd: function(){
                swiperAnimate(this); //每个slide切换结束时也运行当前slide动画
            }
        }
    });
```

