### 1.原生JS-侧边菜单栏

```javascript
 <script>
        let oDiv=document.querySelector("div");
        let oUl=document.querySelector("ul");
        let startY=0;
        let offsetY=0;
        let currentY=0;
        let maxOffsetY=150;
        let minOffsetY=oDiv.offsetHeight-oUl.offsetHeight;
        


        oDiv.ontouchstart=function(event){
            startY=event.targetTouches[0].clientY;
        }
        oDiv.ontouchmove=function(event){
            let moveY=event.targetTouches[0].clientY;
            offsetY=moveY-startY;
            if((currentY+offsetY)>=(maxOffsetY)){
                return;
            }else if((currentY+offsetY)<=(minOffsetY-100)){
                return;
            }
            oUl.style.top=currentY+offsetY+"px";
        }
        oDiv.ontouchend=function(event){
            currentY+=offsetY;
            //保存已经移动出去的偏移位
            if(currentY>maxOffsetY){
                currentY=maxOffsetY;
                oUl.style.top=0+"px";
            }else if(currentY<minOffsetY){
                currentY=minOffsetY;
                oUl.style.top=minOffsetY+"px";
            }

        }
    </script>
```

### 2.IScorll基本使用

```javascript
 <style>
        *{
            margin: 0;
            padding: 0;
            touch-action: none;
        }
        div{
            width: 100%;
            height: 300px;
            border: 1px solid #000;
            box-sizing: border-box;
            overflow: hidden;
        }
        dl>dt{
            line-height: 30px;
            text-align: center;
            border-bottom: 1px solid #000;
        }
    </style>
    <script src="js/iscroll.js"></script>
</head>
<body>
<div class="box">
    <dl>
        <dt>我是标题1</dt>
        <dt>我是标题2</dt>
        <dt>我是标题3</dt>
        <dt>我是标题4</dt>
        <dt>我是标题5</dt>
        <dt>我是标题6</dt>
        <dt>我是标题7</dt>
        <dt>我是标题8</dt>
        <dt>我是标题9</dt>
        <dt>我是标题10</dt>
        <dt>我是标题11</dt>
        <dt>我是标题12</dt>
        <dt>我是标题13</dt>
        <dt>我是标题14</dt>
        <dt>我是标题15</dt>
        <dt>我是标题16</dt>
        <dt>我是标题17</dt>
        <dt>我是标题18</dt>
        <dt>我是标题19</dt>
        <dt>我是标题20</dt>
        <dt>我是标题21</dt>
        <dt>我是标题22</dt>
        <dt>我是标题23</dt>
        <dt>我是标题24</dt>
        <dt>我是标题25</dt>
        <dt>我是标题26</dt>
        <dt>我是标题27</dt>
        <dt>我是标题28</dt>
        <dt>我是标题29</dt>
        <dt>我是标题30</dt>
    </dl>
</div>
<script>
    /*
    1.什么是iScroll?
    iScroll是一个高性能，资源占用少，无依赖，多平台的javascript滚动插件。
    iScroll不仅仅是滚动。在你的项目中包含仅仅4kb大小的iScroll，能让你的项目便拥有滚动，缩放，平移，无限滚动，视差滚动，旋转功能

    2.iScroll基本使用
    2.1按照iScroll的规定搭建HTML结构
    2.2引入iScroll
    2.3创建iScroll对象, 告诉它谁需要滚动
    */
    /*
    3.iScroll的版本
    针对iScroll的优化。为了达到更高的性能，iScroll分为了多个版本。你可以选择最适合你的版本。
    3.1iscroll.js，这个版本是常规应用的脚本。它包含大多数常用的功能，有很高的性能和很小的体积。
    3.2iscroll-lite.js，精简版本。它不支持快速跳跃，滚动条，鼠标滚轮，快捷键绑定。但如果你所需要的是滚动(特别是在移动平台) iScroll 精简版 是又小又快的解决方案。
    3.3iscroll-probe.js，探查当前滚动位置是一个要求很高的任务,这就是为什么我决定建立一个专门的版本。如果你需要知道滚动位置在任何给定的时间,这是iScroll给你的。（我正在做更多的测试,这可能最终在常规iscroll.js脚本，请留意）。
    3.4iscroll-zoom.js，在标准滚动功能上增加缩放功能。
    3.5iscroll-infinite.js，可以做无限缓存的滚动。处理很长的列表的元素为移动设备并非易事。 iScroll infinite版本使用缓存机制,允许你滚动一个潜在的无限数量的元素。
    * */
    let myScroll = new IScroll('.box');
```

### 3.IScorll高级使用

```javascript
 <style>
        *{
            margin: 0;
            padding: 0;
            touch-action: none;
        }
        div{
            width: 50%;
            height: 300px;
            border: 1px solid #000;
            box-sizing: border-box;
            overflow: hidden;
            position: relative;
        }
        dl>dt{
            line-height: 30px;
            text-align: center;
            border-bottom: 1px solid #000;
        }
        .iScrollVerticalScrollbar{
            width: 30px;
            height: 100%;
            background: deepskyblue;
            position: absolute;
            top: 0;
            right: 0;
            z-index: 999;
        }
        .iScrollIndicator{
            width: 100%;
            background: pink;
        }
    </style>
    <script src="js/iscroll.js"></script>
</head>
<body>
<div class="box">
    <dl>
        <dt>我是标题1</dt>
        <dt>我是标题2</dt>
        <dt>我是标题3</dt>
        <dt>我是标题4</dt>
        <dt>我是标题5</dt>
        <dt>我是标题6</dt>
        <dt>我是标题7</dt>
        <dt>我是标题8</dt>
        <dt>我是标题9</dt>
        <dt>我是标题10</dt>
        <dt>我是标题11</dt>
        <dt>我是标题12</dt>
        <dt>我是标题13</dt>
        <dt>我是标题14</dt>
        <dt>我是标题15</dt>
        <dt>我是标题16</dt>
        <dt>我是标题17</dt>
        <dt>我是标题18</dt>
        <dt>我是标题19</dt>
        <dt>我是标题20</dt>
        <dt>我是标题21</dt>
        <dt>我是标题22</dt>
        <dt>我是标题23</dt>
        <dt>我是标题24</dt>
        <dt>我是标题25</dt>
        <dt>我是标题26</dt>
        <dt>我是标题27</dt>
        <dt>我是标题28</dt>
        <dt>我是标题29</dt>
        <dt>我是标题30</dt>
    </dl>
</div>
<script>
    let myScroll = new IScroll('.box', {
        mouseWheel: true,
        // scrollbars: true
        scrollbars: 'custom'
    });
    myScroll.on("beforeScrollStart", function () {
        console.log("滚动之前");
    });
    myScroll.on("scrollStart", function () {
        console.log("开始滚动");
    });
    /*myScroll.on("scroll", function () {
        console.log("正在滚动");
    });*/
    myScroll.on("scrollEnd", function () {
        console.log("滚动结束");
    });
```

### 4.IScorll-侧边栏菜单

```javascript
   <script src="js/iscroll.js"></script>

</head>
<body>
<div class="box">
    <ul>
        <li>热门推荐</li>
        <li>指趣学院</li>
        <li>手机数码</li>
        <li>家用电脑</li>
        <li>电脑办公</li>
        <li>计生情趣</li>
        <li>美妆护肤</li>
        <li>个护清洁</li>
        <li>汽车用品</li>
        <li>京东超市</li>
        <li>男装</li>
        <li>男鞋</li>
        <li>女装</li>
        <li>女鞋</li>
        <li>母婴童装</li>
        <li>图书音像</li>
        <li>运动户外</li>
        <li>内衣配饰</li>
        <li>食品生鲜</li>
        <li>酒水饮料</li>
        <li>家具家装</li>
        <li>箱包手袋</li>
        <li>钟表珠宝</li>
        <li>玩具乐器</li>
        <li>医疗保健</li>
        <li>宠物生活</li>
        <li>礼品鲜花</li>
        <li>生活旅行</li>
        <li>奢侈品</li>
        <li>艺术邮币</li>
        <li>二手商品</li>
    </ul>
</div>
<script>
    new IScroll(".box");
</script>
```





