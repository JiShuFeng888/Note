# CSS_third

CSS3 中新增的三个重磅模块:

1. 过渡 transition
2. 转换 transform
3. 动画 animation

## 前置知识

### `a`标签的伪类选择器

`a`标签存在多个状态, 默认是蓝色, 长按是红色, 访问后是紫色

`a`标签的伪类选择器就是用来修改`a`标签不同状态的样式的

**最佳实践**: 

1. 在设置完`a`标签的样式后再设置该标签伪类选择器的样式
2. `a`是行元素, 转为块元素后其宽高等都放在标签选择器而非伪类选择器中来设置
3. 文字和背景都放在伪类选择器中来使用

```css
a:link{ /* 修改默认样式用的,其余的都能见名知意 */
    background-color: ;
    color: ;
    text-decoration: ;
}
a:visited{
    color: ;
}
a:hover{
    color: ;
    background-color: ;
}
a:active{
    color: ;
}
/* 如上, 有四种状态样式, 都可以自定义, 可省略, 但出现时要严格按照顺序设置, 否则可能不生效 */
/* love, hate 原则: link, visited, hover, active 必须依次出现 */
```

```css
/* 如果默认和已访问颜色相同, 可简写为如下形式 */
a{
    color: ;
}
a:hover{
    color: ;
    background-color: ;
}
a:active{
    color: ;
}
/* 但是如果默认和已访问有专门设置, a 这种简写格式是不能替代 hover 和 active 的 */
```

### 补充

**注意到**:

1. 同一个选择器内(99-反转菜单那里关于这点有惊喜), 属性名相同会出现后面出现的覆盖前面出现的同名属性的情况
2. 对同一个选择器用同族属性的连写形式时各值之间**用空格而非逗号**隔开
3. opacity 在做动画效果时常用, 动画里用 display: none; 和 display: block; 不合适

## 过渡

**过渡三要素**:

1. 发生过渡效果**的属性**
2. 过渡前后状态有不同, 一般结合 :hover 伪类选择器设置后状态
3. 过渡效果持续时间

### transiton 属性族

这个族是设置在**动画前的那个样式**里面的
:hover 伪类选择器不仅可以用于`a`标签, 还可以用于所有标签, 但行元素在转为块元素或者脱标之前不能设置宽高.
:hover 伪类选择器可以改变相应元素样式, 但没有过渡, 此时 CSS3 过渡模块派上用场

也就是说: property 和 duration 是一定要有的, 速度变化方式和延迟启动是可以没有的

```css
/* 过渡模块的四个属性 */

selector{ /* 这里面设置的是前状态样式 */
    /* 告诉系统哪个属性需要执行过渡效果,一般是宽高 */
	transition-property: property1(,property2)(,property3)(...可以有多个);
    /* 告诉系统过渡效果持续的时长 */
    transition-duration: propertyDurationTime1(,propertyDurationTime2)											 (,propertyDurationTime3)
						 (...可以有多个, 与 transition-property 值一一对应);
	/* 告诉系统过渡动画的运动的速度变化方式 */
    /* 可选属性, 取值可以是 linear, ease, ease-in, ease-out, ease-in-out, cubic-bezier(n,n,n,n) */
    transition-timing-function: ;
    /* 可选属性, 告诉系统延迟多少秒之后才开始过渡动画 */
    transition-delay: delayTime;
}
```

```css
/* 过渡模块的连写 */
selector{
    transition: property1 duration1 (timing-function1) (delay1)
				(,property2 durationTime2 (timing-function2) (delay2))
        		(...可以有多个);
}
/* 代码短布局就难以精细 */
selector{
    transition: all duration;
}
```

### 写过渡的最佳实践

1. 不要管过渡, 先编写基本界面
2. 修改我们认为需要修改的属性
3. 再回过头去给被修改属性的那个元素添加过渡即可

## 转换

### 2D 转换

1. 旋转
2. 平移
3. 缩放

**注意**: 2D 转换模块会修改元素的坐标系

#### transform 属性各值

这个属性让人不适应的地方在于属性值还要取值.
不过这并不是 transform 属性独有, transition-duration 属性的 cubic-bezier(n,n,n,n) 属性值也是要取值的

```css
/* 分开写的样子 */

selector{
	transform: rotate( deg); /* deg 是单位, 意思是 degree, 前面要有数值 */
    transform: translate( px, px); /* 两个值, 单位是 px, 分别指定水平和竖直方向移动距离 */
    /* 两个值,没有单位, 值默认为 1, 分别指定水平和垂直方向拉伸倍数, 简写一个则是同时指定水平和竖直方向 */
    transform: scale( , );
}
```

```css
/* 连写 */

selector{
	transform: rotate( deg) translate( px, px) scale( , )  
}

selector{
	transform: none; /* 清除过渡 */
}
```

```css
/* transform-origin 属性, 设置形变中心点 */ 

/*
默认情况下所有元素的旋转都是以自己的中心点为参考来进行旋转的,
可以通过 transform-origin 来修改对应元素的参考点
*/

selector{
    transform-origin: px px; 
    /* 
    两个值,取 0 和 0 即从左上角开始 
    取值有三种形式: 具体像素, 百分比, 特殊关键字(left center right, 这种用的多)
    */
}
/* 更改形变中心点对旋转, 平移和缩放都有影响, 但实际开发中考虑最多的还是对旋转的影响 */
```

```css
/* 旋转轴向 */

selector{
	transform: rotateZ( deg); /* 默认是这个,deg 是单位, 意思是 degree, 前面要有数值 */
}
selector{
	transform: rotateX( deg);
}
selector{
	transform: rotateX( deg);
}
```

#### 透视属性

透视属性结合 transform: rotateX( deg); 或者 transform: rotateX( deg); 就会呈现**近大远小**的效果

```css
/*
perspective 属性的取值单位是 px,
意思是在离屏幕多远的地方观察这个被旋转的元素,
距离越近效果越明显,
这个属性要放到需要呈现近大远小效果的元素的父元素或祖先元素选择器内,
一般取 500px 是比较合适的
*/

selector{
	transform: rotateZ( deg); /* 默认是这个,deg 是单位, 意思是 degree, 前面要有数值 */
    perspective: ;
}
selector{
	transform: rotateX( deg);
    perspective: ;
}
selector{
	transform: rotateX( deg);
    perspective: ;
}
```

### 3D 转换

3D 相比 2D 多了个厚度.

想看到某元素的 3D 效果, 只需要给他的父元素添加属性键值对 transform-style: preserve-3d;

父元素设置 transform-style: preserve-3d;
子元素通过 transform: rotate translate scale; 
一通操作, 可以做出丑丑的很简单的 3D 块块

## 动画

**动画三要素**:

1. 发生动画效果**的属性**
2. 动画前后状态有不同
3. 动画效果持续时间

**动画三状态**:

1. 执行前
2. 执行时
3. 执行后

过渡其实也算动画, 不过跟这里的动画有点**区别**: 过渡动画需要人为出发, 比如 hover, 而动画加载即执行

### animation 属性族

#### 核心属性

```css
/* 这一整套结合起来才能完成一组动画效果, 三要素一个都不能少 */

selector{
    animation-name: xxx; /* 自定义这个动画的名字 */
    animation-duration: ; /* 指定动画完成耗时, 单位是 s */
}
@keyframes xxx{
    from{
        propertyName: propertyValue;
    }
    to{
        propertyName: propertyValue;
    }
} 
```

#### 可选属性

```css
/* 其它可选属性 */

selector{
    animation-name: xxx;
    animation-duration: ;
    
    /* 可选属性 */
    animation-delay: ; /* 指定延迟启动的时长, 单位是 s */
    animation-iteration-time: ; /* 指定动画播放次数, 默认是 1, 没有单位, 可以是 infinity */
    /* 告诉系统过渡动画的运动的速度变化方式 */
    /* 取值可以是 linear, ease, ease-in, ease-out, ease-in-out, cubic-bezier(n,n,n,n) */
    animation-timing-function: ;
    animation-direction: ; /* 值为 normal 或 alternate, 作用见名知意 */
}
@keyframes xxx{ /* 这是只有初始和结束两帧的极简版本 */
    from{
        propertyName: propertyValue;
    }
    to{
        propertyName: propertyValue;
    }
} 

/* 值为 running 和 paused, 作用见名知意, 这个一般放在 hover 伪类选择器里 */
selector:hover{
    animation-state: ;
}
```

#### 进阶

虽然很炫酷, 但是企业开发里用的少

```css
selector{
    animation-name: xxx; /* 自定义这个动画的名字 */
    animation-duration: ; /* 指定动画完成耗时, 单位是 s */
    
    /* 特殊的可选属性, 这个属性要和多帧(不只有 from 和 to 的称为多帧)动画结合使用才合理 */
    animation-fill-mode: ;
    /*
    值可以是:
    none 默认取值即为 none
    forwards 意思是取最后一帧为结束状态 
    backwards 意思是取第一帧为执行前状态
    both 意思是取第一帧为执行前状态, 取最后一帧为结束状态 
    */
}
@keyframes xxx{ /* 百分比表示阶段, 数值可自定义 */
    0%{ /* 称为第一帧 */
        propertyName: propertyValue; /* 这里完全可以用 transform 属性 */
    }
    25%{
        propertyName: propertyValue;
    }
    50%{
        propertyName: propertyValue;
    }
    75%{
        propertyName: propertyValue;
    }
    100%{ /* 称为最后一帧 */
        propertyName: propertyValue;
    }
} 
```

#### 连写

```css
selector{
    /*
    依次是
		动画名称 动画时长 动画运动速度 延迟时间 执行次数 往返动画;
    注意: 只有动画名字, 动画持续时长和动画内容是必须有的
    */
    animation: animation-name animation-duration (animation-timing-function) 
        (animation-delay) (animation-iteration-time) (animation-derection) (animation-fill-mode);
}
@keyframes xxx{
    from{
        propertyName: propertyValue;
    }
    to{
        propertyName: propertyValue;
    }
```

**动画属性注意点**:

1. 动画中如果有和默认样式中同名的属性, 会覆盖默认样式中同名的属性
2. 在编写动画的时候, **固定不变的值写在前面**, 需要变化的值写在后面 (不这样的话效果会很魔幻)

## 从零到一搭个网站

### 编写网页的几个步骤

1. 新建**站点文件夹** (企业开发中站点文件夹一定不要写中文),
   里面应该包含css文件夹/js文件夹/images文件夹/index.html文件
   **注意点**:
   站点文件夹可以是中文, 但是其子文件夹或者子文件不能出现中文

2. 添加标签图标:
   在各大网站地址后缀 /favicon.ico 就能拿到该公司的 ico 格式的 logo 图标, 也就是网站标签页上的图标

   ```html
   <link rel="shortcut icon" href="favicon.ico"  type="image/x-icon"/>
   ```

3. 添加**网站优化三大标签**:

   1. title 标签
      - 网页中第一重要的标签, 是搜索引擎了解网页的入口, 和对网页主题归属的最佳判断点
      - 长度: 谷歌是 35 个中文, 百度是 **28** 个中文
      - **格式**: 网站名 (产品名) - 网站的介绍
      - **特点**: 越先出现的词语权重越高
   2. name 值为 keywords 的 meta 标签
   3. name 值为 description 的 meta 标签

   ```html
   <title>苏宁易购(Suning.com)-送货更准时、价格更超值、上新货更快</title>
   <meta name="keywords" content="苏宁易购网上商城,苏宁电器,Suning,手机,电脑,冰箱,洗衣机,相机,数码,家居用品,鞋帽,化妆品,母婴用品,图书,食品,正品行货"/>
   <meta name="description" content="苏宁易购-综合网上购物平台，商品涵盖家电、手机、电脑、超市、母婴、服装、百货、海外购等品类。送货更准时、价格更超值、上新货更快，正品行货、全国联保、可门店自提，全网更低价，让您放心去喜欢！" />    
   ```

4. 新建css文件, 在这个文件夹中做一些初始化操作 (一般是 reset.css 文件(或者 nomalize.css 文件) 和 base.css)

   1. 清空默认的样式
   2. 设置全局的样式
   3. 将新建的css文件和当前的index.html文件关联起来

5. 指导思想: 渐进增强(痛苦的起点), 优雅降级(这个常用)

   - **渐进增强**: 针对常用的低版本浏览器进行页面构建, 保证最基本功能,然后再针对高级浏览器进行效果和交互的改进和功能追加, 保证基础体验, 追求更好效果.
   - **优雅降级**: 一开始就在高级浏览器构建完整的功能, 然后再针对低版本浏览器进行兼容.

6. 摸清楚网页的基本骨架, 由于网页搭建应该从上到下, 从外到内,
   所以首先要确定上是什么, 下是什么, 外是什么, 内是什么.
   这里没有绝对的正确, 就像英语句子的词性划分标准并不唯一.
   要紧的是理出一条脉络, 知道应该从哪里下手

7. 按部就班, 合适的地方用合适的技术, 先做共性部分, 再对个性部分作调整

8. 开发经验

- 网页应该把公司 logo 用 h1 标签包裹起来

  - 在企业开发中, 一般情况下如果导入多个 CSS 文件, 都会将别人的 CSS 文件放在前, 自己的 CSS 文件放在后, 这样可以**避免**自己的 CSS 代码**被覆盖**

- object-fit: cover 和 background-size: cover 作用类似, 都能使背景图片(或视频)填满整个元素

- 绝对定位的父元素会使 hover 子元素的 a 标签不显示小手指, 解决方式是改大父元素的 z-index 值

- 如果对一行的块块设置 vertical-align: middle 后各个块块能垂直居中说明各块高度相同, 如果不能同时垂直居中且发现只有一个与其他块块高度不一致, 可以先设置行高, 再把特殊的块块与该行顶部对齐, 就能实现一行的垂直居中.

- 左浮动隐含着内容的左对齐, 所以浮动后没必要再设置 text-align: left;

- 在企业开发中, 如果元素是左浮动的, 就**不要**设置左边的 margin, 这样可以避免一些不必要的兼容性问题, 这时候 padding 就用得上了
  (还是 margin 方便, 不兼容的浏览器不会用我写的代码, 很稳)
  (没有一招鲜吃遍天的好事, 我清一色用 margin 导致翻车了)

- 一行有多个块一般是用 li 标签来做, 这算是最佳实践, 照着来错不了

- outline: none; 可以去除块块被点击后的蓝色框框
  outline （轮廓）是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。
  注释：轮廓线不会占据空间，也不一定是矩形

- 两个小块如果水平, 优先考虑放在同一个大的水平块块来做, 下面这块儿很好用

  ```css
  .clearfix::after{
      /*设置添加的子元素的内容为空*/
      content: "";
      /*设置添加的子元素为块级元素*/
      display: block;
      /*设置添加的子元素的高度为0*/
      height: 0;
      /*设置添加的子元素看不见*/
      visibility: hidden;
      /*给添加的子元素设置clear: both;*/
      clear: both;
  }
  .clearfix{
      /*兼容IE6*/
      *zoom:1;
  }
  ```

- 定位流导致 p 标签不再占据整行, 需要手动给宽度 一般给到 100%

- 水平排版其实可以浮动套浮动嗷, 很方便

- 可以用 dl 标签做图文混排

- **奇技淫巧**:

  1. 如果图片的宽度大于父元素的宽度, 使用 text-align: center; 是无法让图片居中的
     但配合上子元素的 margin: 0 -100%; 就能水平居中了
     这样写比用定位流方便多了
  2. -webkit-background-clip: text; 可以将所在块背景裁剪为文字的形状, 这对背景颜色和背景图片都生效
     (这个属性值只有内核为 webkit 或者 Blink的浏览器才能识别)

### 补充知识点

#### 设置页面最大最小宽度

```css
*{
 margin: 0;
 padding: 0;
}

body{
    min-width: ;
    max-width: ;
    margin: 0 auto;
}
```

#### iconfont

1. 图片有诸多优点, 但缺点也很明显
   - 图片会显著增大网页体积 (性能问题)
   - 多图片会增加访问页面时 HTTP 请求次数 (性能问题)
   - 图片过度缩放可能失真
2. **字体图片**
   **本质上是文字**(体积小), 但可起到和图片一样的效果
   而且可以方便的修改颜色、大小、透明度等\\\
3. 常用字体图标库
   https://www.iconfont.cn/ (阿里家的)
   https://icomoon.io/ (国外挺有名)
4. 字体图片的使用
   4.1 设计师提供 SVG 格式图标
   4.2 上传到对应字体图标网站
   4.3 下载生成的代码使用
   - 找到下载好的对应文件, 将所有的 iconfont 开头的文件放到项目的 font 文件夹下面
   - 新建一个 CSS 文件, 将 demo_index.html 对应的代码拷贝进去
   - 注意点: 拷贝之后需要将 @font-face 中的资源路径改为拷贝资源对应的路径
   - 具体用法有三种, 哎呀百度一下的事

#### 零碎

- 从零玩转HTML5+CSS3项目实战② 课时 47 有个关于 flex 的神奇知识点
- 从零玩转HTML5+CSS3项目实战② 课时 62 同一行的浮动中右浮放在左浮这个操作把我看得一愣一愣的, 神奇
- 从零玩转HTML5+CSS3项目实战② 课时 66 06:30 快速的讲了 iconfont 用法, 忘了用法就去看看 (全忘了就看课时 38)
- 从零玩转HTML5+CSS3项目实战② 课时 69 后半段讲了块块被 hover 后底边出图片的一种实现, 挺有启发性

## 响应式网页

- 从零玩转HTML5+CSS3项目实战② 课时53 居然利用 浮动+清除浮动+伸缩布局 来做顶栏中的一行, 好炫酷!
- css 替换不了 img 标签的 src 标签属性, 但能**替换**块块的 background-image, 响应式网站利用了这一点
  ( js 能换 img 的 src, 现在一步步来 先用 css 来做)
- flex 很适合用来做自适应

### 获取浏览器宽度

有两种方式可以根据浏览器宽度的不同调整内容展示的样式, 要获取**浏览器宽度**有两种方式:

1. 通过 JavaScript 获取
2. 通过 CSS3 中新增的**媒体查询**技术, 也能获取当前浏览器的宽度

### 媒体查询

1. 什么是媒体查询?
   媒体查询就是**获取到当前浏览器的宽度**之后, **根据不同的宽度设置元素不同的样式**

2. 媒体查询的注意点
   由于媒体查询需要根据不同的浏览器宽度调整元素的样式, 所以**不适合用于比较复杂的网页**

3. 媒体查询的格式
   在**这里的 media 可以理解为 if**
   @media 条件{} 含义: 如果条件满足, 那么就执行后面{}中的代码
   3.1 内联格式: @media 条件{}
   3.2 外链格式: `<link rel="stylesheet" href="css/xxx.css" media="条件">`

   ```css
   *{
       margin: 0;
       padding: 0;
   }
   /*
   div{
   width: 500px;
   height: 500px;
   background: red;
   }
   */
   
   /*
   如果当前的网页是显示在电脑or平板or手机上的, 并且当前浏览器的宽度是大于等于1200px的,
   那么就执行后面大括号中的代码
   */
   @media screen and (min-width: 1200px){
       div{
           width: 500px;
           height: 500px;
           background: red;
       }
   }
   /*
   如果当前的网页是显示在电脑or平板or手机上的, 并且当前浏览器的宽度是小于等于1199px的,
   那么就执行后面大括号中的代码
   */
   @media screen and (max-width: 1199px){
       div{
           width: 300px;
           height: 300px;
           background: green;
       }
   }
   /*
   如果当前的网页是显示在电脑or平板or手机上的, 并且当前浏览器的宽度是小于等于768px的,
   那么就执行后面大括号中的代码
   */
   @media screen and (max-width: 768px){
       div{
           width: 100px;
           height: 100px;
           background: blue;
       }
   }
   ```

4. 在企业开发中, 如果需要分别给电脑/平板/手机分别设置样式, 那么我们会将电脑的样式写在前面, 平板的样式写在电脑的后面, 手机的样式写在平板的后面
   在**企业开发中媒体查询中指定的宽度不是固定的**, 指定的宽度是根据自己企业的需求来指定的,
   并没有一个固定的值代表电脑的,
   也没有一个固定的值代表平板的,
   也没有一个固定的值代表手机的

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>02-媒体查询基本使用2</title>
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <!-- 
   	<link rel="stylesheet" href="媒体查询CSS/index-pc.css" media="screen and (min-width: 1200px)">
   	改成第十一行能减少重复代码, 更改部分在十二三行写就好了. 选择器相下`同, 属性一样, 后写会覆盖先写.
   	-->
       <link rel="stylesheet" href="css/index.css">
       <link rel="stylesheet" href="媒体查询CSS/index-pad.css" media="screen and (max-width: 1199px)">
       <link rel="stylesheet" href="媒体查询CSS/index-phone.css" media="screen and (max-width: 768px)">
   </head>
   <body>
   <div></div>
   </body>
   </html>
   ```

5. 如上:

   1. 如果给电脑的 CSS  **添加条件**， 在平板和手机上所有的样式都**不会有**效果， 如果平板和手机上有和电脑上相同的样式也**不能**复用
   2. 所有我们**不要给电脑的 CSS 添加条件**， 这样无论浏览器的宽度是多少， 电脑的 CSS 文件**都会被执行**， 我们只需要在平板或者手机对应的 CSS 文件中通过相同的选择器覆盖掉不同的样式即可
   3. 降低了代码的冗余
   4. 企业开发中编写响应式网站的步骤
      1. 编写电脑版本的网页
      2. 编写平板版本的网页， 通过相同的选择器覆盖掉不同的样式
      3. 编写手机版本的网页， 通过相同的选择器覆盖掉不同的样式

