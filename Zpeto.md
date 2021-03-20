### 1.Zepto的基本使用

```javascript

    1. Zepto?
    Zepto 是一个轻量级的针对现代高级浏览器的 JavaScript库，
    它与jQuery有着类似的api, 如果你会用jQuery，那么你也会用Zepto

    2.既然和jQuery差不多, 为什么还需要Zepto?
    2.1jQuery更多是在PC端被应用，Zepto更多是在移动端被应用；
       也正是因为jQuery用在PC端, 所以jQuery考虑了很多低级浏览器的的兼容性问题, ,所以代码更多体积更大；
       也正是因为Zepto用在移动端, 所以Zepto则是直接抛弃了低级浏览器的适配问题 , 所以代码更少体积更小；
    2.2综上所述: Zepto其实就是专门用于移动端的轻量级的jQuery

    3.官方网址:
    英文版：http://zeptojs.com/
    中文版：http://www.css88.com/doc/zeptojs_api/

    
    let oBtn = document.querySelector("button");
    oBtn.onclick = function () {
        $("div").css({backgroundColor: "red"});
    }
 
    4.Zepto的特点
    Zepto采用了模块化的开发, 将不同的功能放到了不同的模块中,
    在使用的过程中我们可以按需导入, 也就是需要什么功能就导入什么模块
  
    $("button").click(function () {
        $("div").css({backgroundColor: "red"});
    });
  
    5.Zepto注意点
    如果是从官方网站下载的, 那么已经包含了默认的一些模块
    如果是从github下载的, 那么需要我们自己手动导入每一个模块
    当然后续学习了NodeJS后, 我们也可以自己定制
	
   
```

### 2.Zepto选择器

```javascript
	<script src="js/zepto.js"></script>
    <script src="js/event.js"></script>
    <script src="js/selector.js"></script>

    <body>
    <button>我是按钮</button>
    <div></div>
    <div class="one"></div>
    <div id="two"></div>
    <script>
        /*
        1.Zepto选择器
        Zepto是模块化开发的, zepto.js核心模块中只包含了基础功能
        如果想使用高级的选择器必须引入高级选择器模块
        * */
        $("button").click(function () {
            // $("div").css({backgroundColor: "yellow"});
            // $(".one").css({backgroundColor: "yellow"});
            // $("#two").css({backgroundColor: "yellow"});
            $("div:first").css({backgroundColor: "yellow"});
        });
    </script>
    </body>
```

### 3.Zepto动画

```javascript
 	<script src="js/zepto.js"></script>
    <script src="js/event.js"></script>
    <script src="js/fx.js"></script>
    <script src="js/fx_methods.js"></script>
    <!--<script src="js/jquery-3.1.1.js"></script>-->




	/*
    1.zepto动画
    Zepto是模块化开发的, zepto.js核心模块中只包含了基础功能
    如果想使用动画必须引入动画模块

    2.zepto动画注意点
    由于zepto是一个轻量级的针对现代高级浏览器的 JavaScript库
    不需要兼容低级浏览器, 所以zepto中的动画是通过CSS3属性来实现动画的
    而jQuery中是通过DOM来实现动画的
    * */
    $("button").click(function () {
        // $("div").animate({marginLeft: 500}, 2000);
        // $("div").hide(2000);
        // $("div").show(2000);
        $("div").toggle(2000);
    });
```

### 4.Zepto-tap事件

```javascript
    <!--<script src="js/jquery-3.1.1.js"></script>-->
    <script src="js/zepto.js"></script>
    <script src="js/event.js"></script>
    <script src="js/touch.js"></script>



<script>
    /*
    1.无论PC端还是移动端都支持click事件
    而且不仅仅是jQuery和Zepto支持, 原生的JS也支持
    * */
    /*
    let oDiv = document.querySelector("div");
    oDiv.onclick = function () {
        console.log("被点击了");
    }
    */
    /*
    $("div").click(function () {
        console.log("被点击了");
    });
    */
    /*
    2.移动端click事件注意点
    在企业开发中如果需要在移动端监听点击事件, 一般不会使用click来监听
    因为移动端的事件很多(单击/双击/轻扫/捏合/拖拽等等)
    所以如果通过click来监听,系统需要花费100~300毫秒判断到底是什么事件
    而移动端对事件的响应速度要求很高, 事件响应越快用户体验就越好
    所以如果需要在移动端监听点击事件, 那么请使用tap事件

    3.tap事件
    tap事件是Zepto自己封装的一个事件, 解决了原生click事件100~300毫秒的延迟问题
    * */
    $("div").tap(function () {
        console.log("被点击了");
    });
</script>
```

### 5.移动端touch事件

```javascript
 /*
    1.Zepto是如何实现tap事件的?
    虽然tap事件是Zepto自己封装的事件, 但是无论如何封装肯定都是通过原生JS来实现的
    在原生的JS中专门为移动端新增了几个事件
    touchstart: 手指按下
    touchmove:  手指在元素上移动
    touchend :  手指抬起

    2.注意点:
    这几个事件只支持移动端, 不支持PC端
    * */
    let oDiv = document.querySelector("div");
    oDiv.ontouchstart = function () {
        console.log("手指按下");
    }
    oDiv.ontouchend = function () {
        console.log("手指抬起");
    }
    oDiv.ontouchmove = function () {
        console.log("手指移动");
    }
```

### 6.移动端touch事件对象

```javascript
 /*
    1.Touch事件对象
    移动端的touch事件也是一个事件, 所以被触发的时候系统也会自动传递一个事件对象给我们

    2.移动端touch事件对象中比较重要的三个子对象
    touches:        当前屏幕上所有手指的列表
    targetTouches:  保存了元素上所有的手指里列表
    changedTouches: 当前屏幕上刚刚接触的手指或者离开的手指
    */
    /*
    let oDiv1 = document.querySelector(".box1");
    oDiv1.ontouchstart = function (event) {
        console.log("touches1", event.touches);
        console.log("targetTouches1", event.targetTouches);
    }
    let oDiv2 = document.querySelector(".box2");
    oDiv2.ontouchstart = function (event) {
        console.log("touches2", event.touches);
        console.log("targetTouches2", event.targetTouches);
    }
    */
    /*
    let oDiv1 = document.querySelector(".box1");
    oDiv1.ontouchstart = function (event) {
        // console.log("touches1", event.touches);
        console.log("targetTouches1", event.targetTouches);
    }
    oDiv1.ontouchend = function (event) {
        // console.log("touches1", event.touches);
        console.log("targetTouches1", event.targetTouches);
    }
    */
    let oDiv1 = document.querySelector(".box1");
    oDiv1.ontouchstart = function (event) {
        console.log("按下", event.changedTouches);
    }
    oDiv1.ontouchend = function (event) {
        console.log("抬起", event.changedTouches);
    }
    /*
    touches和targetTouches
    如果都是将手指按到了同一个元素上, 那么这两个对象中保存的内容是一样的
    如果是将手指按到了不同的元素上, 那么这个两个对象中保存的内容不一样
    touches保存的是所有元素中的手指, 而targetTouches保存的是当前元素中的手指

    changedTouches
    在ontouchstart中保存的是刚刚新增的手指
    在ontouchend中保存的是刚刚离开的手指
    * */
```

### 7.移动端touch事件位置

```javascript
  /*
    1.手指的位置
    1.screenX/screenY是相对于屏幕左上角的偏移位
    2.clientX/clientY是相对于可视区域左上角的偏移位
    3.pageX/pageY是相对于内容左上角的偏移位
    * */
    let oDiv = document.querySelector("div");
    oDiv.ontouchstart = function (event) {
        // console.log(event.targetTouches[0]);
        // console.log(event.targetTouches[0].screenX);
        // console.log(event.targetTouches[0].screenY);
        console.log(event.targetTouches[0].clientX); // 11
        console.log(event.targetTouches[0].clientY); // 63
        console.log(event.targetTouches[0].pageX);  // 686
        console.log(event.targetTouches[0].pageY);  // 63
    }
```

### 8.移动手指位置练习

```
/*需求: 通过手指拖拽div*/
    let oDiv = document.querySelector("div");
    let startX = 0;
    let startY = 0;
    let flag = false;
    oDiv.ontouchstart = function (event) {
        if(flag){return}
        flag = true;
        startX = event.targetTouches[0].clientX;
        startY = event.targetTouches[0].clientY;
    }
    oDiv.ontouchmove = function (event) {
        let moveX = event.targetTouches[0].clientX;
        let moveY = event.targetTouches[0].clientY;
        let offsetX = moveX - startX;
        let offsetY = moveY - startY;
        oDiv.style.transform = `translate(${offsetX}px, ${offsetY}px)`;
    }
```

### 9.tap事件原理

```javascript
 /*
    1.单击事件特点
    1.1只有一根手指
    1.2按下和离开时间不能太久 100ms
    1.3按下和离开距离不能太远 5px
    * */
    let oDiv = document.querySelector("div");
    /*
    let startX = 0;
    let startY = 0;
    let startTime = 0;
    oDiv.ontouchstart = function (event) {
        // 1.判断当前元素中有几根手指
        if(event.targetTouches.length > 1){
            return;
        }
        // 2.拿到手指按下的位置
        startX = event.targetTouches[0].clientX;
        startY = event.targetTouches[0].clientY;
        // 3.拿到手指按下的时间
        startTime = Date.now();
    }
    oDiv.ontouchend = function (event) {
        // 1.判断有几根手指离开了
        if(event.changedTouches.length > 1){
            return;
        }
        // 2.拿到离开手指的位置
        let endX = event.changedTouches[0].clientX;
        let endY = event.changedTouches[0].clientY;
        // 3.判断手指离开的位置和按下位置的距离
        if(Math.abs(endX - startX) > 5 ||
            Math.abs(endY - startY) > 5){
            return;
        }
        // 4.拿到手指离开的时间
        let endTime = Date.now();
        // 5.判断手指离开的时间和按下的时间
        if(endTime - startTime > 100){
            return;
        }
        console.log("单击事件");
    }
    */
    Tap(oDiv, function () {
        console.log("点击事件");
    });
```

### 10.tap封装

```javascript
(function (window) {
    function Tap(dom, fn) {
        if(!(dom instanceof HTMLElement)){
            throw new Error("请传入一个DOM元素");
        }
        let startX = 0;
        let startY = 0;
        let startTime = 0;
        dom.ontouchstart = function (event) {
            // 1.判断当前元素中有几根手指
            if(event.targetTouches.length > 1){
                return;
            }
            // 2.拿到手指按下的位置
            startX = event.targetTouches[0].clientX;
            startY = event.targetTouches[0].clientY;
            // 3.拿到手指按下的时间
            startTime = Date.now();
        }
        dom.ontouchend = function (event) {
            // 1.判断有几根手指离开了
            if(event.changedTouches.length > 1){
                return;
            }
            // 2.拿到离开手指的位置
            let endX = event.changedTouches[0].clientX;
            let endY = event.changedTouches[0].clientY;
            // 3.判断手指离开的位置和按下位置的距离
            if(Math.abs(endX - startX) > 5 ||
                Math.abs(endY - startY) > 5){
                return;
            }
            // 4.拿到手指离开的时间
            let endTime = Date.now();
            // 5.判断手指离开的时间和按下的时间
            if(endTime - startTime > 100){
                return;
            }
            // console.log("单击事件");
            fn && fn();
        }
    }
    window.Tap = Tap;
})(window);
```

### 11.移动端点透问题

```javascript
 /*
    1.移动端点透问题
    当一个元素放覆盖了另一个元素, 覆盖的元素监听touch事件,而下面的元素监听click事件
    并且touch事件触发后覆盖的元素就消失了, 那么就会出现点透问题

    2.移动端点透问题出现的原因
    2.1当手指触摸到屏幕的时候，系统生成两个事件，一个是touch 一个是click
    2.2touch事件先执行,执行完后从文档上消失
    2.3click事件有100~300ms延迟, 所以后执行.
    2.4但click事件执行的时候触发的元素已经消失了, 对应的位置现在是下面的元素, 所以就触发了下面元素的click事件

    3.移动端点透问题解决方案
    在touch事件中添加event.preverDefault(); 阻止事件扩散
    * */
    let oClick = document.querySelector(".click");
    let oTap = document.querySelector(".tap");

    oTap.ontouchstart = function (event) {
        this.style.display = "none";
        event.preventDefault(); //  阻止事件扩散
    }
    oClick.onclick = function () {
        console.log("click");
    }





	    /*
    1.移动端点透问题三种解决方案
    1.1在touch事件中添加event.preverDefault(); 阻止事件扩散
    1.2使用Zepto, 但是需要注意老版本的Zepto也会出现点透问题
    1.3使用Fastclick, 最早解决点透问题的插件
    * */
    if ('addEventListener' in document) {
        document.addEventListener('DOMContentLoaded', function() {
            FastClick.attach(document.body);
        }, false);
    }

    let oClick = document.querySelector(".click");
    let oTap = document.querySelector(".tap");
    /*
    oTap.ontouchstart = function (event) {
        this.style.display = "none";
        // event.preventDefault(); //  阻止事件扩散
    }
    */
    /*
    $(oTap).tap(function () {
        oTap.style.display = "none";
    });
    */
    // 注意点: 这里的click事件并不是原生的click事件, 是使用的fastclick中的click
    //         这里的click事件已经解决了100~300ms延迟的问题
    oTap.addEventListener("click", function () {
        oTap.style.display = "none";
    });
    oClick.onclick = function () {
        console.log("click");
    }
```

### 12.Zepto-滑动事件

```javascript
    /*
    1.什么是轻扫事件?
    手指快速的往左边滑动/或者右边滑动/或者上边滑动/或者下边滑动
    * */
    // $("div").swipe(function () {
    //     console.log("轻扫");
    // });
    $("div").swipeLeft(function () {
        // console.log("向左边轻扫");
        $(this).animate({marginLeft: "0"}, 2000);
    });
    $("div").swipeRight(function () {
        // console.log("向右边轻扫");
        $(this).animate({marginLeft: "100px"}, 2000);
    });
    $("div").swipeUp(function () {
        // console.log("向上边轻扫");
        $(this).animate({marginTop: "0"}, 2000);
    });
    $("div").swipeDown(function () {
        // console.log("向下边轻扫");
        $(this).animate({marginTop: "100px"}, 2000);
    });
```

### 13.Zepto事件练习

```javascript
<style>
        *{
            margin: 0;
            padding: 0;
            /*禁用默认情况下移动端的一些事件*/
            touch-action: none;
        }
        .box{
            overflow: hidden;
        }
        .box-top{
            width: 100%;
            height: 50px;
        }
        .box-top>ul{
            list-style: none;
            width: 100%;
            height: 100%;
            display: flex;
        }
        .box-top>ul>li{
            flex-grow: 1;
            line-height: 50px;
            text-align: center;
            font-size: 20px;
            background: #6c6c6c;
        }
        .box-top>.line{
            width: 50%;
            height: 3px;
            background: #f40;
            position: relative;
            left: 0;
        }
        .box-top>ul>.active{
            color: #f40;
            background: #ccc;
        }
        .box-bottom{
            width: 200%;
            display: flex;
            position: relative;
            left: 0;
        }
        .box-bottom>ul{
            list-style: none;
            flex-grow: 1;
        }
    </style>
    <script src="js/zepto.js"></script>
    <script src="js/event.js"></script>
    <script src="js/touch.js"></script>
    <script src="js/fx.js"></script>
    <script src="js/selector.js"></script>
</head>
<body>
<div class="box">
    <div class="box-top">
        <ul>
            <li class="active">新闻</li>
            <li>军事</li>
        </ul>
        <p class="line"></p>
    </div>
    <div class="box-bottom">
        <ul class="list1">
            <li>我是新闻的内容1</li>
            <li>我是新闻的内容2</li>
            <li>我是新闻的内容3</li>
            <li>我是新闻的内容4</li>
            <li>我是新闻的内容5</li>
            <li>我是新闻的内容6</li>
            <li>我是新闻的内容7</li>
            <li>我是新闻的内容8</li>
            <li>我是新闻的内容9</li>
            <li>我是新闻的内容10</li>
        </ul>
        <ul class="list2">
            <li>我是军事的内容1</li>
            <li>我是军事的内容2</li>
            <li>我是军事的内容3</li>
            <li>我是军事的内容4</li>
            <li>我是军事的内容5</li>
            <li>我是军事的内容6</li>
            <li>我是军事的内容7</li>
            <li>我是军事的内容8</li>
            <li>我是军事的内容9</li>
            <li>我是军事的内容10</li>
        </ul>
    </div>
</div>
<script>
    // 1.监听按钮的点击
    $(".box-top li").on("nj:click",function () {
        $(this).addClass("active").siblings().removeClass();
        // console.log($(this).index());
        let currentIndex = $(this).index();
        $(".line").animate({left: currentIndex * $(this).width()}, 1000);
        $(".box-bottom").animate({left: -currentIndex * $(".list1").width()}, 1000);
    });
    $(".box-top li").click(function () {
        $(this).trigger("nj:click");
    });
    $(".box-bottom").swipeLeft(function () {
        $(".box-top li:last").trigger("nj:click");
    });
    $(".box-bottom").swipeRight(function () {
        $(".box-top li:first").trigger("nj:click");
    });
```

