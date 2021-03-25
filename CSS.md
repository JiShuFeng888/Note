### BFC

![批注 2020-11-24 083714](C:\Users\阔乐c\Desktop\批注 2020-11-24 083714.png)

```javascript
只要元素满足下面任一条件即可触发 BFC 特性：

body 根元素
浮动元素：float 除 none 以外的值
绝对定位元素：position (absolute、fixed)
display 为 inline-block、table-cells、flex
overflow 除了 visible 以外的值 (hidden、auto、scroll)


1. 同一个 BFC 下外边距会发生折叠
2. BFC 可以包含浮动的元素（清除浮动）
3. BFC 可以阻止元素被浮动元素覆盖
```

margin-left:auto

style 标签只能放在 head 标签里, 与 title 标签是兄弟关系.

css 有**两大块知识点**: 选择器和属性.

开山名义: 盒模型由外到内包括外边距, 边框, 内边距, 内容. 英文写作 margin, border, padding, content

draggable:设置元素是否可以拖拽

## html 与 css 的关系

### 为什么强烈不建议 html 修改样式

1. 需要记忆哪些标签有哪些属性, 如果该标签没有这个属性, 那么设置了也没有效果
2. 当需求变更时我们需要修改大量的代码才能满足现有的需求
3. HTML**只有一个作用**就是用来添加语义

### 为什么使用 css 修改样式

1. 不用记忆哪些属性属于哪个标签
2. 当需求变更时我们不需要修改大量的代码就可以满足需求
3. 在前端开发中 CSS**只有一个作用**, 就是用来修改样式
4. body 标签内的标签都可以通过 css 设置样式, 一个 html 页面只应有一个 body 标签对

### 注意

css 属性值为数字时除非为零, 一定要带单位, 不可省略. 没单位的的才不用加
css3 很多属性非常有用,但由于是新事物,上古的浏览器可能无法解析
IDE 中换行或多空格对造成网页中的**单个**小空格

### 最佳实践

css 样式编写前, 一般要

1. 清空默认边距
2. 清空默认样式
3. 设置整个界面通用的文字信息
4. 在复杂布局的关键节点添加适当的注释

## css 格式

css 样式中值**不需要**双引号(写汉字就要了). 且注释的格式像是 js 中的段落注释.

### 行内样式

直接写在标签的**标签属性名为 style** 的值里

```html
<tag style="propertyname1: propertyValue1;..."></tag>
```

### 内联样式 (内嵌样式)

**注意**:
**style 标签**只能写在 head 标签里,
和 title 标签同级,
type 标签属性可以省略,
冒号不能省略,
分号大多数情况下也不能省略, 最佳实践就是一律不要省略

```css
/* 内联样式格式 */
<style type="text/css">
selector{
  propertyname: propertyValue;
  ...;
}
</style>
```

### 外联样式 (外链样式) (就用这个)

相比于内联样式, 就是**独立为一个文件**, 少了 style 标签

```css
/* 外链样式格式 */
selector{
  propertyname: propertyValue;
  ...;
}
```

```html
<!-- 只能写在 head 标签里 -->
<link rel="stylesheet" href="文件路径"></link>
```



### 导入样式

相比于外联样式, 首先就是形式上的区别, 还有**其他区别**:

1. link 是 XHTML 标签，除了加载 CSS 外，还可以定义 [RSS](https://link.jianshu.com/?t=http://baike.baidu.com/link?url=kUew5P-VHsAgfZen83YoKmxqPaQLtGfzUchfFJ_nmTt414G3N8jdrN8S-Mz4jejHx6fQJ3UF02_JOiy2Y2WNX_) 等其他事务；@import 属于 CSS 范畴，只能加载 CSS
2. link 引用 CSS 时，在页面载入时**同时**加载；@import 需要页面网页完全载入以**后**加载
3. link 是 XHTML 标签，无兼容问题；@import 是在 CSS2.1 提出的，低版本的浏览器不支持
4. link 支持使用 Javascript 控制 DOM 去改变样式；而@import不支持

```css
/* 导入样式文件格式与外链样式文件格式无异 */
selector{
  propertyname: propertyValue;
  ...;
}
```

```html
<!-- 只能写在 head 标签里 -->
<style>
	@import "文件路径";
</style>
```

import 的各种变体:

1. @import '文件路径'
2. @import “文件路径”
3. @import url(文件路径)
4. @import url(‘文件路径’)
5. @import url(“文件路径”) (这种兼容性最好)

以上五种形式现代浏览器都能识别, 现代版茴字的三种写法hhh

## 常用 css 属性

### 文字属性

```css
/* ws 有很多好用的快捷键 */

font-style: /* 斜体或者正常 */ ;
font-weight: /* 值可以是特定单词(无需引号)也可以是特定数字 */ ;
font-size: /* 这个的单位是 px,这里一定要带单位! */ ;
font-family: "指定字体", "备选字体";
/*
这里的值是单词, 注意汉字外面要套英文引号(英文单词不需要,加了引号也能行).
设置的字体必须是电脑已经安装的字体,否则会显示默认字体.
在指定字体不生效时则备用字体生效. 中文字体可以处理英文,英文字体不能处理中文.
*/
/*
英文名的字体不一定是英文字体,中文字体一般也有英文名.
常用中文字体: 宋体/黑体/微软雅黑
常用英文字体: Times New Roman/Arial
*/

/* 上述四个属性可以简写为 font 属性,格式如下. */
font: (style值), (weight值), size值, family值;
/*
style和weight值可以省略或者交换位置,
size和family值不可省略,不可交换位置.
*/
```

### 文本属性

```css
/* 文本装饰 */
text-decoration: /* 下划线,贯穿线,上划线,无 */;

/* 文本水平对齐 */
text-align: /* 左中右 */;

/* 文本缩进 */
text-indent: /* 单位是 em 或 px,推荐用 em */;

文本文字颜色
color:
/*
值可以是英文颜色单词,
也可以是 rgb(值,值,值), 16^2 = 256,
也可以是 #六个十六进制数(ff0000 可以缩写为 f00, 类似的同理),
还可以是 rgba(值,值.值,值), rgba 是 css3 才推出的
*/;
```

**vertical-align**
设置元素的垂直对齐
**注意点**:

1. text-align 是设置给需要对齐元素的**父元素**
2. vertical-align 是设置给需要对齐的那个**元素本身**
3. vertical-align **只对行内元素有效**

```css
img{
    vertical-align: ;
}
/*
取值有 baseline, top, text-top, text-bottom, middle;
默认就是 baseline, 即图片底部与一行文字的基线对齐,基线即一行文字最短文字的底部
top 指图片顶部与父元素顶部对齐
bottom 指图片底部与父元素底部对齐
text-top 指图片顶部与文字顶部对齐
text-bottom 指图片顶部与文字底部对齐
middle 指图片中线与文字中线对齐 (文字中线并非文字正中间)
*/
```

[什么是文字基线](https://www.google.com/search?q=%E6%96%87%E5%AD%97%E5%9F%BA%E7%BA%BF&rlz=1C1SQJL_zh-TWNL904JP904&sxsrf=ALeKk00cw8gyynF4UvndS_JlR75rdl15Hg:1601787328425&source=lnms&tbm=isch&sa=X&ved=2ahUKEwiLn93lkprsAhWW9Z4KHYj3B40Q_AUoAXoECAwQAw&biw=1396&bih=693)

## 常用 css 选择器	

tagName, idName, className 都属于 selector

1. 标签选择器 

   ```css
   tagName{
     /* 只能选中所有标签,只能选中 html 中有的标签 */
   }
   ```

2. id 选择器,一个 html 页面内每个 idName 都应该是唯一的

   ```css
   #idName{
     /*
     id 名称只能有字母/数字、下划线, 且不能以数字开头.
     id 名称不能是 html 标签的名称 ,
     实际开发中 id 选择器并不用于设置样式, 而是留给 js 用
     */
   }
   ```

3. 类选择器

   ```css
   .className{
     /*
     每个 html 都可以同时绑定多个类名
     <tagName class="className1 className2">
     巧用类选择器和但标签多类的特性,可以提高 css 代码的复用性
     */
   }
   ```

4. 后代选择器,用空格连接

   ```css
   /* 子孙都算后代, 用后代选择器比一个个设相同 class 名要节省许多代码量 */
   /* 选择器可以是标签选择器、id 选择器、类选择器的任意个数任意组合,重点是空格隔开选择器 */
   tagName1 tagName2 {
     /* tagName1 所有标签名为 tagName2 的后代 */
     propertyname: propertyValue;
   }
   ```

5. 子元素选择器,用大于号连接

   ```css
   /* 选择器之间不能有空格 */
   /* 选择器可以是标签选择器、id 选择器、类选择器的任意个数任意组合,重点是大于号隔开选择器 */
   tagName1>tagName2{
     /* tagName1 标签中所有直接子元素标签名为 tagName2 的标签 */
   }
   ```

6. 交集选择器,紧密连接,没有任何连接符号

   ```css
   selector1selector2{
   	/* 这个企业开发中用的不多 */
   }
   ```

7. 并集选择器,选择器之间用逗号隔开,这个我觉得叫多选选择器更合适 

   ```css
   selector1,selector2{
   }
   ```

8. 兄弟选择器

   ```css
   /* 8.1 相邻兄弟选择器,css2推出,作用是给指定选择器后紧跟的那个选择器的标签设置属性,要挨着的标签 */
   selector1+selector2{
   }
   /* 8.2 通用兄弟选择器,css3推出,作用是选中 selector1 后面所有名为 selector2 的选择器 */
   selector1~selector2{
   }
   ```

9. 序选择器 

   ```css
   /*
   这个蛮常用,选的是标签. css3推出的,
   n 除了能是数字还能使 odd 或者 even, 甚至是 xn+y
   */
   /* 9.1 同名子元素的第几个 */
   tagName:nth-child(n){
     /* 若该级别 nth-child 标签名不是 tagName 就该花括号内样式就不生效 */
   }
   tagName:nth-last-child(n){
     /* 若该级别 nth-last-child 标签名不是 tagName 就该花括号内样式就不生效 */
   }
   tagName:only-child{
     /* 父元素有且仅有一个指定名称子元素且在子元素列表中排在第一 */
   }
   /* 9.2 同名子元素的第几个 */
   tagName:nth-of-type(n){
     /* 若该级别 nth-child 标签名不是 tagName 就就找到第一个出现的 tagName 再生效 */
   }
   tagName:nth-last-of-type(n){
     /* 若该级别 nth-child 标签名不是 tagName 就就找到第一个出现的 tagName 再生效 */
   }
   tagName:only-of-type{
     /* 父元素有且仅有一个指定名称子元素 */
   }
   ```

10. 属性选择器

    ```css
    /* 10.1 根据属性名选择 */
    tagName[attribute]{
    }
    /* 10.2 根据属性名和值 */
    tagName[attribute="value"]{
      /* 最常见的应用场景是区分 input 属性 */
    }
    /* 10.3 根据属性名和什么属性值开头 */
    tagName[attribute|="value"]{
      /* 了解即可 */
    }
    tagName[attribute^="value"]{
      /* css3推出的,用这个 */
    }
    /* 10.4 根据属性名和什么属性值结尾 */
    tagName[attribute$="value"]{
    }
    /* 10.5 根据属性名和包含什么属性值 */
    tagName[attribute~="value"]{
      /* 了解即可 */
    }
    tagName[attribute*="value"]{
      /* css3推出的,用这个 */
    }
    ```

11. 通配符选择器,标签多时比较贵,开发中用的少

    ```css
    *{
    }
    ```

## css 三大特性

### 1. 继承性

1.1 以 color/font-/text-/line 开头的 css 属性才有继承性
1.2 后代皆可继承
1.3 **特殊情况**
  1.3.1 a 标签的文字颜色和下划线是不能继承的
  1.3.2 h 标签的文字大小不能继承
应用场景: 设置网页的共性样式

### 2. 层叠性

层叠性是 css 处理样式冲突时某个样式设置会覆盖其他样式设置的特性.
多个选择器选中同一个标签切设置了相同的属性, 这时称发生了重叠.

### 3. 优先级

3.1 优先级是 css 处理样式设置冲突的一套规则
3.2 优先级判断的三种方式
  3.2.1 样式是否源自继承,直选优于继承
  3.2.2 冲突的选择器相同,下面的覆盖上面的
  3.2.3 冲突的选择器不同,按选择器的优先级来层叠.
优先级排序: id>class>tagName>wildcard>inherited>browserDefault (通配居然大于继承)

#### 3.3 优先级提升: !important

注意点:
3.3.1 !important 只能用于直接选中,不能用于间接选中
3.3.2 通配符选择器属于直接选中
3.3.3 !important 只能写在属性值分号之后,只对设置了 !important 的那个属性生效
3.3.4 用法:

```css
selector{
    propertyName: propertyValue; !important
}
```

#### 3.4 权重问题

直接选中标签的 css 样式权重大,
优先级高的权重大,
**同优先级时选择器个数多的权重大**,
若以上计算值相等,放在下面的权重大.

## 显示模式转换

```html
<!DOCTYPE html>
<html>
  <!-- 行,块,行内块区别见 html 对应部分 -->
  <head>
    <title>块级元素,行内元素,行内块元素的相互转换</title>
  </head>
  <style>
    blockElemnt{
      /* 块元素转行元素 */
      display: inline;
    }
    inlineElement{
      /* 行元素转块元素 */
      display: block;
    }
    .className{
      /* 同一个类下的块元素或行元素转为行内块元素 */
      display: inline-block;
    }
  </style>
  <body>
    <details>
      <summary>新发现</summary>
      在 html 中常称标签为标签, 在 css 中常称标签为元素, 在 js 中常称标签为节点
    </details>
  </body>
</html>
```

## 背景图片相关属性

### css 背景和精灵图

注意和 img 标签区分开

```css
/* 1. 给标签设置背景颜色, 注意背景颜色默认从 border 区域开始 */
selector{
  background-color: ;
}

/* 2.
背景图片,注意和 img 标签区分开, 背景图片默认从 padding 区域开始
img 标签语义强但挤占其他内容,
css 背景图片设置方便
*/
selector{
  background-image: url();
  background-repeat: ; /* 图片默认会平铺占满对应块元素,合理利用平铺能减小网页体积 */
}

/* 3. 背景定位属性 */
/* 背景颜色和背景图片可以共存. 背景图片在背景色的上面,默认在左上角 */
selector{
  background-image: url();
  background-repeat: ;
  background-position: horizontalNum verticalNum;
  /* 值还可以是英文方位名词. 为数字时一定要有单位,水平值与垂直值用空格隔开,值可以为负 */
}

/* 4. 背景关联,这个用的少 */
selector{
  background-image: url();
  background-repeat: ;
  background-position: horizontalNum verticalNum;
  background-attachment: ; /* 默认是 scroll, 随着滚动会跑掉, fixed 就始终看得见 */
}

/* 5. 背景家族可以像 font 家族一样有个"一个属性设所有"的属性 */
selector{
  /* 任何一个都可以省略,但有的话要按顺序排才会生效 */
  background: (bgColor) (bgImg) (bgRepeat) (bgAttachment) (bgPosition);
}
/* 老师说,一般下方有滚动条的网站是比较垃圾的网站hhhh, b站躺枪,谷歌躺枪 */
```

精灵图(sprite)就是结合背景图片和背景定位来实现的. 精灵图整合多个小图标能起到减少请求服务器次数从而减轻服务器压力的作用.

### background-size

CSS3 新增了背景图片尺寸属性:  background-size
结合 background: url(“xxx”) no-repeat; 可以**规定背景图片大小及比例**

- background-size: 宽 高; (指定图片具体宽高, 单位是 **px**)
- background-size: 宽 高; (指定图片宽高占所在块宽高的百分比, 单位是 **%**)
- background-size: auto 高; (宽度与指定的高度**成比例**, 高可以是 px 也可以是 %)
- background-size: 宽 auto; (高度与指定的宽度**成比例**, 宽可以是 px 也可以是 %)
- background-size: cover; (能让图片等比拉伸至**整张图片填满**所在块块)
- background-size: contain; (能让图片等比拉伸至宽度**或**高度**填满**所在块块, 一旦其中一个填满就停止拉伸)

### background-origin

CSS3 新增了背景图片定位属性: background-origin
结合 background: url(“xxx”) no-repeat; 可以**规定背景图片从盒模型的哪个区域开始显示**
(之所以说“开始”, 是因为图片如果比所在块块大, 默认是要溢出的)

**前置知识**:
背景图片默认铺满 padding (内边距)区域, **而不只是** content (内容)区域

- background-origin: padding-box; (默认就是这个样子)
- background-origin: border-box; (使背景图片从 border (边框)区域开始显示)
- background-origin: content-box; (使背景图片从 content (内容)区域开始显示)

### background-clip

CSS3 新增了背景绘制区域属性: background-clip
结合 background: url(“xxx”) no-repeat; 可以**规定背景绘制区域** (跟背景图片居然**不是一回事**)

- background-clip: border-box; (默认就是这个样子)
- background-clip: padding-box; (使背景只绘制从  padding (内边距)区域往内部分)
- background-clip: content-box; (使背景只绘制  content (内容)区域)

### 渐变

渐变不是一个新的属性, 而是一个**取值**

**注意**:

1. 渐变首先要求有**至少两个**不同颜色, 否则没得变, 样式也不会生效, 但**可以有多个**
2. 渐变的背景**相当于图片**, 写 background 和 background-image 都可, 写成 background-color IDE 会报错

**线性渐变**: background: linear-gradient();
**径向渐变**: background: radial-gradient();

#### 线性渐变

**默认**情况下线性渐变是**从上至下**的渐变
我们可以通过在颜色的前面添加 to xxx 修改渐变的方向
to top
to left
to right

```css
selector{
    background: linear-gradient(red, green);
}

selector{
    background-image: linear-gradient(to top right, red, blue);
    background-image: linear-gradient(to left ,red 0%, red 30%,blue 30%, blue 60%, green 60%, green 100%);
}
```

除了可以通过关键字控制渐变的方向以外, 还可以**通过角度来控制渐变的方向**, 
角度是以从下往上为零度, 按照**顺时针**旋转

```css
selector{
    background-image: linear-gradient(200deg, red, blue);
}
```

默认情况下系统自动计算纯色和渐变色的范围, 但也可自定义
这里只指定了一个颜色的纯色范围, 其实后面的 blue 也可以指定, 有多个颜色时也能分别指定
**但**除了第一个是指定纯色范围, 其余的都是指定渐变的范围

```css
selector{
    /* 前一百个像素都是纯色 */
    background-image: linear-gradient(red 100px, blue); 
}

selector{
    /*30%以前不渐变, 从30%开始慢慢渐变到下一个颜色*/
    background-image: linear-gradient(red 30%, blue);
}
```

多色渐变

```css
/* 注意到这里有从蓝色到蓝色, 这段等于没有渐变, 就是纯色 */

selector{
    background-image:
		linear-gradient(red 0%, red 30%,blue 30%, blue 60%, green 60%, green 100%);
}
```

#### 径向渐变

**径向渐变**:
指从一个点开始, 向四周扩散的渐变,
径向渐变默认从块块中心点向四周扩散

可以在颜色前面添加 **at 关键字**跟**方位名词**来指定从什么位置开始渐变

```css
selector{
    background-image: radial-gradient(at left top,red, blue);
}
```

除了可以通过方位名词指定从什么位置开始渐变以外, 还可以通过添加at关键字跟**具体像素**来指定从什么位置开始渐变

```css
selector{
    background-image: radial-gradient(at 50px 50px,red, blue);
}
```

也可以在颜色前面**直接加上一个具体的像素**来指定渐变的范围

```css
/* 这里指的是从中心点开始半径为 150px 内有渐变效果 */
selector{
    background-image: radial-gradient(150px ,red, blue);
}
```

如果既要指定**扩散的范围**, 又要指定**起始位置**,
那么把**扩散的范围写在前面**, 而起始位置(仍可以是具体数值)写在后面

```css
selector{
    background-image: radial-gradient(50px at right bottom ,red, blue);
}
```

### 注意

background-origin(指**背景图片**) 和 background-clip(指**背景色**) 不是一回事,
二者可以共同作用于一个块块, 也就是可以**共存**,
**图片的优先级高于背景颜色的优先级**

### 多重背景图片

CSS3 新增多重背景图片, 没有新属性, 而是对 background 属性进行了加强
有了多重背景做动画就比较容易了

**用法**:
多张背景图片之间用逗号隔开即可

**注意点**:
**先添加**的背景图片会**盖住后添加**的背景图片
**建议**在编写多重背景时**拆开编写** (目的是使代码便于阅读)

```css
/*
background: url("images/animal1.png") no-repeat left top,
			url("images/animal2.png") no-repeat right top,
			url("images/animal3.png") no-repeat left bottom,
			url("images/animal4.png") no-repeat right bottom,
			url("images/animal5.png") no-repeat center center;
*/
background-image: url("images/animal1.png"),url("images/animal2.png"),url("images/animal3.png");
background-repeat: no-repeat, no-repeat, no-repeat;
background-position: left top, right top, left bottom;
```

## padding, border, margin

- 边框, 就是环绕在标签宽度和高度周围的线条
- 内外边距的四条边的宽度都叫做边框宽度,这跟矩形的宽高的宽不一样嗷,这一点要注意
- 通过设置外边框能得到三角形! 创意十足服气服气

### 边框 border

#### width, style, color

**边框三要素**:

1. 宽度 | border-width
2. 样式 | border-style (连写时唯一不可省略的属性)
3. 颜色 | border-color

```css
/* 1. 非连写:分开设置,每个属性名都是"方向+样式". 非常费代码量,企业中几乎不用 */
/* 1.1 分开设置各边宽度 */
blockElement{
  border-top-width: top (right) (bottom) (left);
  border-right-width: ;
  border-bottom-width: ;
  border-left-width: ;
}
/* 1.2 分开设置各边样式 */
blockElement{
  border-top-style: top (right) (bottom) (left);
  border-right-style: ;
  border-bottom-style: ;
  border-left-style: ;
}
/* 1.3 分开设置各边颜色 */
blockElement{
  border-top-color: top (right) (bottom) (left);
  border-right-color: ;
  border-bottom-color: ;
  border-left-color: ;
}

/* 2. 连写:一条设所有 */
/* 2.1 属性名只有方向 */
blockElement{
  /* 值为 none 时就没了对应的外边框 */
  border-top: (width) style (color); /* 样式不可省略. 颜色和宽度可省略,颜色默认为黑. */
  border-right: ;
  border-bottom: ;
  border-left: ;
}
/* 2.2 属性名只有样式 */
blockElement{
  /*
  任一个属性都可省略.
  属性值从顶部按顺时针取值,可省略,被省略的值取对边边框相应属性值.
  只设上边的值时则上右下左相应属性取值都一样.
  */
  border-width: top (right) (bottom) (left);
  border-style: top (right) (bottom) (left);
  border-color: top (right) (bottom) (left);
}
/* 2.3 属性名非常不具体,灵活性就小一些 */
blockElement{
  /* 宽度可省略倒是有点出乎意料 */
  border: (width) style (color);
}

/*
小记录:
1. style 中文可以是样式
2. 我们称 width style color 是边框的样式
3. 这就造成了歧义,很烦
*/
```

#### radius

边框圆角的**作用**: 将原始的直角变为圆角

**格式**:

- border-radius: 左上 右上 右下 左下; (设置每个角边框是半径为指定数值的四分之一圆, 单位是 px)
- border-radius: 左上 右上&左下 右下; (只写三个的话, 第二个既是右上角的又是左下角的)
- border-radius: 左上&右下 右上&左下; (只写两个的话, 第一个值负责主对角线, 第二个值负责副对角线)
- border-radius: 四个角; (只写一个就负责四个角)
- border-radius: 50%; (做个圆)
- 所以想只设置某角的话, 应该四个都写, 不设圆角的写 0
  或者这样写**单独设置**左上角(其余角同理):
  border-top-left-radius: 水平 垂直;
  (这是专门设置某角的属性, 第一个值是圆心离左边框距离, 第二个值是圆心距离顶部边框距离, 这样可以设**椭圆**)
  border-top-left-radius: 水平&垂直;
  (这个属性的简写)

此外有个**规律**:
如果边框的宽度**小于**圆角的半径, 那么内圆和外圆都是圆弧形状
如果边框的宽度**大于或者等于**圆角的半径, 那么内圆就会变成直角而不是圆角

#### box-shadow & text-shadow

1. 给盒子添加阴影
   **box-shadow**: h-shadow v-shadow blur spread color inset;
   盒子阴影: 水平偏移 垂直偏移 模糊度 阴影扩展 阴影颜色 内外阴影;
   **注意点**:
   1. 盒子的阴影分为内外阴影, 默认情况下就是外阴影
   2. 快速添加阴影只需要编写三个参数即可
   3. box-shadow: 水平偏移 垂直偏移 模糊度
   4. 默认情况下阴影的颜色和盒子内容的颜色一致
2. 给文字添加阴影文字阴影: 
   **text-shadow**: h-shadow v-shadow blur-radius color;
   水平偏移 垂直偏移 模糊度 阴影颜色 ;

```css
selector{
	box-shadow: h-shadow v-shadow blur spread color inset;
}

selector{
	text-shadow: h-shadow v-shadow blur-radius color;    
}
```

#### border-image (花里胡哨)

- border-image-source: url(“文件路径”);
  (指定作为边框的图片, 若只有这个属性, 图片会被放到边框四个点上, 边框图片的优先级高于边框颜色且不共存)
- border-image-slice: 距上 距右 距底 距左 (fill); (**不需要单位**, 作用是把作为边框的图片切成了九块, 一般写一个)
- border-image-width: ; (设置这个后边框宽度 border-width 还是原来的数值(浏览器调试可见)但不生效)
- border-image-repeat: ; 
  (指定除四角外的边框位置被图片如何填充, 值有 stretch, repeat, round, 作用见名知意)
- border-image-outset: 往上 往右 往下 往左; (指定边往外移动多少, **单位是 px**)

**连写**:

- border-image: 资源地址 切割方式 填充模式;

**作用**: 替代之前的滑动门方案, 实现拉伸不变性的效果

### 内边距 padding

- 边框和内容之间的距离就是内边距
- 给标签设置内边距之后,标签占有的宽度发生变化 (设置了 box-sizing: border-box; 就不会了)
- 内边距也会有背景颜色

```css
/* 1. 内边距 padding */
/* 1.1 非连写: 分别设置各边内边距 */
blockElement{
  padding-top: ;
  padding-right: ;
  padding-bottom: ;
  padding-left: ;
}
/* 1.2 连写: 一条设所有 */
blockElement{
  /* 省略的效果同边框 */
  padding: top (right) (bottom) (left);
}
```

### 外边距 margin

- 标签与标签之间的距离就是外边距
- 外边距没有背景颜色

```css
/* 2. 外边距 margin */
/* 2.1 非连写: 分别设置各边外边距 */
blockElement{
  margin-top: ;
  margin-right: ;
  margin-bottom: ;
  margin-left: ;
}
/* 1.2 连写: 一条设所有 */
blockElement{
  /* 省略的效果同边框 */
  margin: top (right) (bottom) (left);
}
```

#### 外边距合并(塌陷)现象 collapse

- 垂直方向上相邻的 **margin** 会合并, 结果是只有 margin 值大的才生效

  - 注意: 只有垂直方向才有外边距合并现象, 水平方向没有

    ## 盒模型

    - 内容(content)
    - 宽度/高度: 默认指定的是可以存放内容的区域
    - 内边距(padding): 填充物
    - 边框(border): 盒子厚度
    - 外边距(margin): 盒子和盒子之间的间隙
    - 盒子是包裹内容的, 而非内容本身

    ### 明确宽度和高度

    1. **内容**的宽度和高度:
       就是通过 width/height 属性设置的宽度和高度
    2. **元素**的宽度和高度
       宽度 = 左边框 + 左内边距 + width + 右内边距 + 右边框
       高度 同理可证
    3. **元素空间**的宽度和高度
       宽度 = 左外边距 + 左边框 + 左内边距 + width + 右内边距 + 右边框 + 右外边距
       高度 同理可证

    为啥叫元素啊,叫盒子不是更合适吗,名字这么花里胡骚做什么

    ### box-sizing 属性

    padding, border, margin 都会影响元素空间的宽高.

    1. CSS3 中新增了一个 box-sizing 属性
       这个属性可以保证我们给盒子新增 padding 和 border 之后, 盒子元素的宽度和高度不变
    2. box-sizing 属性是如何保证增加 padding 之后, 盒子元素的宽度和高度不变?
       和我们前面学习的原理一样, 增加 padding 和 border 之后要想保证盒子元素的宽高不变, 那么就必须减去一部分内容的宽度和高度
       惊奇发现：如果内容、内边距和边框之和大于设置的 width、height，box-sizing就失效了
    3. box-sizing 取值
       3.1 content-box <!— 这是默认取值 ->
       元素的宽高 = 边框 + 内边距 + 内容宽高
       3.2 **border-box**
       元素的宽高 = width/height 的宽高

    ```css
    blockElement {
      /* 省略的效果同边框 */
      box-sizing: ; /* 设置为 border-box 后 width/height 的宽高指的是元素的宽高 */
    }
    ```

    ### margin 注意点

    1. 如果两个盒子是嵌套关系, 那么设置了里面一个盒子顶部的外边距, 外面一个盒子也会被顶下来
       有趣的是,  子元素的 margin-top 能带动父元素往下, 子元素的 margin-left **却不能**带动父元素往右
    2. 如果外面的盒子不想被一起顶下来,那么可以给外面的盒子添加一个边框属性 (或者加 overflow: hidden;)
    3. 在企业开发中, 一般情况下如果需要控制嵌套关系盒子之间的距离
       应该**首先考虑 padding**, 其次再考虑 margin
    4. margin 本质上是用于控制**兄弟关系**之间的间隙的
    5. 在嵌套关系的盒子中, 我们可以利用`margin: 0 auto;`的方式来让里面的盒子在外面的盒子中水平居中
    6. margin: 0 auto; **只对水平方向有效**, 对垂直方向无效

    ### 盒子知识点零碎

    #### 内容水平居中与盒子水平居中

    - 内容居中: text-align:center; 作用是使盒子内容相对于盒子居中
    - 盒子居中: margin:0 auto; 作用是使盒子相对于父盒子水平居中

    #### 清空默认边距

    为了使开发人员的布局不受默认设置干扰,一般清零浏览器自带的默认内外边距值.

    ```css
    /* 1. 通配符选择器非常费性能,不推荐,上课才这么用 */
    *{
       margin: 0;
       padding: 0;
    }
    
    /* 2. 企业开发中标准的清空默认内外边距设置的写法 */
    body,div,dl,dt,dd,ul,ol,li,
    h1,h2,h3,h4,h5,h6,pre,code,
    form,fieldset,legend,input,
    textarea,p,blockquote,th,td{
       margin:0;padding:0
    }
    ```

    #### 行高

    - 行高: 指一行内容的高度 | line-height: ; | 文字默认在行高中垂直居中 (注意这是设置给文字**父元素**的)
    - 盒子高度: 整个标签高度 | height: ; | 不设置的话会被内容撑开,设置后即固定. 内容可能跑出盒子
    - 企业开发中
      - 常将盒子高度与行高设置为相同, 这样就可以保证*一行文字*在盒子的高度是垂直居中的,
        或者只设置行高, 这样父盒子也会被行高撑开, 这样就省了一行代码
      - 用 padding 属性与 box-sizing: border-box; 结合实现*多行文字*在盒子中垂直居中

    #### 字体与字号

    1. 在企业开发中, 如果一个盒子中存储的是文字, 那么一般情况下我们会以盒子左边的内边距为基准,
       不会以右边的内边距为基准, 因为这个**右边的内边距有误差**
       右边内边距的误差从何而来? 右边如果放不下一个文字, 那么文字就会换行显示, 所以文字和内边距之间的距离就有了误差
    2. 顶部的内边距并不是边框到文字顶部的距离, 而是**边框到行高顶部**的距离

    ## 网页布局方式

    1. **标准流(文档流/普通流)**排版方式
       1.1 浏览器默认的排版方式就是标准流的排版方式
       1.2 在CSS中将元素分为三类, 分别是块级元素/行内元素/行内块级元素
       1.3 在标准流中有两种排版方式, 一种是垂直排版, 一种是水平排版

       - 垂直排版, 如果元素是块级元素, 那么就会垂直排版
       - 水平排版, 如果元素是行内元素/行内块级元素, 那么就会水平排版

    2. **浮动流**排版方式
       2.1 浮动流是一种"*半脱离*标准流"的排版方式
       2.2 浮动流*只有一种排版方式, 就是水平排版*. 它*只能*设置某个元素*左对齐*或者*右对齐*
       *注意点*:

       - 浮动流中没有居中对齐, 也就是*没有center*这个取值
       - 在浮动流中不可以使用margin: 0 auto;

    - 水平排版中间有间隙时用 float 要找 margin-right 值很麻烦的, 可以考虑 flex

      - 浮动是对要浮动**元素本身**设置 float 属性, 伸缩(弹性)布局是对**父元素**设置 display: flex;

      *特点*:

    - 浮动流中的元素和标准流中的行内块级元素很像

      - 在浮动流内**没有了**块,行内,行内块的区分

    3. **定位流**排版方式

    4. **伸缩布局**排版方式
       4.1 伸缩布局是**先**按主轴方向顺序排好伸缩项, **再**按指定对齐方式对齐

    5. 补充: 浮动和定位中的绝对定位都是脱离标准流的, 脱离标准流的标签**都能**设置宽高

    ### 脱标

    - 脱标: 脱离标准流, 像是从标准流中删除了, *不再*占据标准流的位置
    - **脱标后的标签**都类似行内块, 比如 span 浮动后可以设置宽高
    - 脱标后的元素的子行元素还是行元素, 也就是说脱标是不可继承的
    - 浮动是半脱标, 浮动之后的位置, 由浮动元素浮动之前在标准流中的位置来确定
    - 定位中的绝对定位和相对定位都是**就地脱标**

    ### 浮动流

    #### 浮动的排序规则

    1. 先浮动的排前面, 最先左浮排最左, 最先右浮排最右, 按顺序来
    2. **半脱离标准流**:
       浮动元素,
       浮动后.

    #### 浮动元素的贴靠现象

    1. 如果父元素的宽度能够显示所有浮动元素, 那么浮动的元素会并排显示
    2. 如果父元素的宽度不能显示所有浮动元素, 那么会从最后一个元素开始往前贴靠
    3. 如果贴靠了前面所有浮动元素之后都不能显示, 最终会贴靠到父元素的左边或者右边,
       靠到最后还不行就*顶出来*了

    #### 浮动元素的自围现象

    虽然浮动元素盖住没有浮动的元素, 但没有盖住非浮动元素的文字内容.

    #### 浮动流的布局

    垂直方向用标准流, 水平方向用浮动流.
    布局要从上到下, 从外到内.
    浮动还有使得水平的多个块块水平对齐的效果.

    #### 清除浮动

       震惊： 浮动后不设置 border 或者 overflow: hidden；子块也不会连带顶下父块了！！！

    ##### 浮动流的高度问题

    1. 在标准流中内容的高度可以撑起父元素的高度
    2. 在浮动流中浮动的元素是**无法撑起**父元素的高度的

    ##### 清除浮动的五种方式 (难点)

    1. 给前面一个父元素设置高度
       注意: 不推荐在企业开发中应用这种方式

    2. 设置 clear 属性, 让被设置的元素不去找**前面**的*往值方向*的浮动元素

       ```css
       selector{
           clear: ; /* 取值可以是 left, right, both, none. 默认是 none */
       }
       
       /*
       none: 默认取值, 按照浮动元素的排序规则来排序(左浮动找左浮动, 右浮动找右浮动)
       left: 不要找前面的左浮动元素
       right: 不要找前面的右浮动元素
       both: 不要找前面的左浮动元素和右浮动元素
       */
       ```

       **注意点**:
       当我们给某个元素添加 clear 属性之后, 那么这个属性的*margin属性会失效*, 原因是浮动元素的父元素没有边框. (我反复尝试， 确认并不失效)

    3. 隔墙法, 墙指的是额外添加的块级元素

       1. 外墙法
          1.1 在两个盒子中间添加一个额外的块级元素
          1.2 给这个额外添加的块级元素设置 clear: both;
          **注意点**:
          外墙法它可以让第二个盒子使用margin-top属性
          外墙法*不可以*让第一个盒子使用margin-bottom属性
          一般用外墙法时既不用块一的 margin-bottom 也不用块二的 margin-top, 而是设置这个额外块的高度
       2. 内墙法
          2.1 在第一个盒子中所有子元素最后添加一个额外的块级元素
          2.2 给这个额外添加的块级元素设置 clear: both;
          **注意点**:
          内墙法它可以让第二个盒子使用margin-top属性
          内墙法它可以让第一个盒子使用margin-bottom属性
       3. 外墙法和内墙法区别?
          外墙法*不能撑起第一个盒子的高度*, 而内墙法可以撑起第一个盒子的高度
       4. 在企业开发中*不常用*隔墙法来清除浮动, 原因有两个
          1. 只用 css 就设置了浮动却要用 css+html 来清除浮动
          2. 加了大量额外的空 div 块块

    4. 伪元素选择器添空块

       ```css
       /* 这效果跟内墙法是一样的，伪元素起到了元素的效果 */
       selector::after{
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
       selector{
           /*兼容IE6, 注意这两个 selector 是同一个*/
           *zoom:1;
       }
       ```

       浮动是通过 css 样式添加的, 清除浮动也用 css 显然更合理, 所以推荐企业开发中用这种清除浮动的方式

    5. overflow: hidden;

       **用法**:

       - 在浮动元素的**父元素中**设置 overflow: hidden;

       **作用**:

       1. 可以将超出标签范围的内容裁剪掉 (这是独有的能力)
       2. **清除浮动** (border 做不到)
       3. 可以通过 overflow: hidden;
          让里面的盒子设置margin-top之后, 外面的盒子**不被**顶下来, 这样就可以不用设置 border,
          (只有这点像 border)
       4. 此外, 设置了浮动的子块, 设置了 margin, 即使父块没有 border 或者 overflow: hidden,
          父块**也不会**被子块连带

       ```css
       /* 这效果跟内墙法是一样的 */
       selector{
           overflow: hidden;
          /* 兼容IE6 */
           *zoom:1;
       }
       ```

    ##### 伪元素选择器

    伪元素选择器是 CSS3 推出的, 作用就是给指定标签的**内容前面**添加一个子元素或者给指定标签的内容后面添加一个子元素, 这里设置 display: block; 之后,虽然没有添加 html 标签,但起到了添加一个块级元素的效果

    ```css
    tagName::before{
        content: "";
        width: ;
        height: ;
        background-color: ;
        display: ;
        visibility: ; /* 这里取值为 hidden 之后块块将不可见 */
    }
    
    tagName::after{
        content: "";
        width: ;
        height: ;
        background-color: ;
        display: ;
    }
    ```

    ### 定位流

    定位流分类:

    1. 相对定位
    2. 绝对定位
    3. 固定定位
    4. 静态定位: 每个元素默认就是静态定位

    #### 相对定位

    相对定位: **不脱离**标准流, 相对的是自己在标准流中的位置
    作用: 

    1. 给指定块块位置进行微调 (用的少)
    2. 配合 absolute 属性来使用

    ```css
    selector{
        position: relative;
        top: ;
        bottom: ;
        left: ;
        right: ;
    }
    /*
    同一个轴上定位方向的属性只能有一个
    给有 position: relative; 键值对的块设置 margin-top 之类的属性是在给这个块在标准流中根据 top 等属性跑走之前的位置设置
    */
    ```

    #### 绝对定位

    绝对定位: 

    1. **脱离**标准流
    2. 默认相对的是自己在页面首屏中的定位
    3. 如果有设置了*非静态定位*定位流的祖先, 则相对的是离自己最近的祖先中的定位
    4. 绝对定位会无视相对的那个元素的 padding, 但不会无视 border 和 margin

    **脱标后的标签**都类似行内块, 比如 span 浮动后可以设置宽高

    ```css
    selector{
        position: absolute;
        top: ;
        bottom: ;
        left: ;
        right: ;
    }
    ```

    ##### 绝对定位元素的水平居中

    在**绝对定位中** margin: 0 auto; 是无效的

    ```css
    selector{
        width: ;
        height: ;
        position: absolute;
        left: 50%;
        margin-left: /* 负的元素宽度的一半 */;
    }
    ```

    更花哨的方式 (不算花哨, 挺实用) 

    ```css
    selector{
        width: ;
        height: ;
        position: absolute;
        left: 50%;
        /* margin-left: 负的元素宽度的一半; */
        transform: translateX(-50%);
    }
    ```

    垂直居中还能这么写 (transform 在一个选择器里只能出现一次, 但可以有多值, 顺序可以去 MDN 查)

    ```css
    selector{
        width: ;
        height: ;
        position: absolute;
        top: 50%;
        /* margin-left: 负的元素宽度的一半; 奇技淫巧 */
        transform: translateY(-50%);
    }
    ```

    

    #### 子绝父相

    一般常见的开发方式是子块设置为绝对定位, 父级设置为相对定位

    这样用的原因:

    - 相对定位不脱离标准流, 布局较麻烦
    - 绝对定位没有定位流祖先会相对于页面首屏定位, 分辨率一变就要出大问题

    结合相对定位父块的绝对定位的子块, 既不占用标准流位置, 也不会因为分辨率的调整而乱套, 是最佳实践

    一图盖住另一图这种情况第一时间要想到定位流和子绝父相	

    #### 固定定位

    固定定位:

    1. 脱离标准流
    2. 固定定位和前面学习的背景关联方式很像, 背景定位可以让背景图片不随着滚动条的滚动而滚动, 
       而固定定位可以让某个盒子不随着滚动条的滚动而滚动
    3. IE6 不支持固定定位

    作用: 做导航条, 侧边牛皮癣小广告

    ```css
    selector{
        position: fixed;
        top: ;
        bottom: ;
        left: ;
        right: ;
    }
    ```

    #### 定位流 z-index 属性

    z-index: 默认情况下每个元素的 z-index 属性值都是 0

    **作用**: 专门用于控制定位流元素的覆盖关系的

    **覆盖规则**:

    1. 默认情况下定位流的元素盖住标准流的元素
    2. 默认情况下定位流的元素**后面**编写的会**盖住前面**编写的
    3. 如果定位流的元素设置了 z-index 属性, 则 z-index 属性**值大的显示在上**面
    4. **从父现象**:
       如果两个元素的父元素设置了z-index属性, 那么子元素的z-index属性就会失效,
       也就是说谁的父元素的z-index属性比较大谁就会显示在上面

    ### 伸缩布局

    #### 简介

    ##### 容器与项

    设置了 display: flex; 的元素称为**伸缩容器**, 其**子元素**成为**伸缩项**

    ##### 主轴与侧轴

    - 在伸缩布局中, 默认伸缩项是从左至右的排版的, 主轴与侧轴**一定相互垂直**
    - **默认水平向右**方向就是**主轴**方向, 竖直向下方向就是侧轴方向
    - 主轴起点在伸缩容器左边, 主轴终点在伸缩容器右边
    - 侧轴起点在伸缩容器顶边, 侧轴终点在伸缩容器底边
    - 主轴侧轴方向是可以修改的

    **小声叨叨**: 毗邻真是个好词, 比紧挨着文雅多了, 也不难懂, 没有歧义, 真好真好

    #### 伸缩容器属性

    ##### flex-direction

    用于**修改主轴**方向, 伸缩项谁先谁后由主轴决定

    ```css
    selector{
        display: flex;
        flex-direction: ;
        /*
        值可以是 row, row-reverse, column, column-reverse
        默认就是 row, 主轴水平向右
        row-reverse 使得主轴水平向左
        column 使得主轴竖直向下
        column-reverse 使得主轴竖直向上
        */
    }
    ```

    ##### justify-content

    指定**伸缩项的水平对齐**方式, 这个属性**只**指定对齐方式
    space-between 指两端对齐, space-around 指环绕对齐

    ```css
    selector{
        display: flex;
        flex-direction: row;
        justify-content: ;
        /*
        值可以是 flex-start, flex-end, center, space-between, space-around
        flex-start, flex-end, center 伸缩项间无间隙
        默认就是 flex-start, 伸缩项与主轴起点对齐
        flex-end 使得伸缩项与主轴终点对齐 (和右浮动大不相同)
        center 使得伸缩项与主轴中点对齐
        
        space-between, space-around 伸缩项间有间隙
        space-between 使得伸缩项均匀分布在主轴, 左右边无间隙
        space-around 使得伸缩项均匀分布在主轴, 每个伸缩项左右间隙相等, 伸缩项相邻时间隙叠加
        */
    }
    ```

    ##### align-items

    指定**伸缩项的垂直对齐**方式
    侧轴跟主轴的对齐方式相比, **少了**两端对齐和环绕对齐, 多了基线对齐和拉伸对齐

    ```css
    selector{
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: ;
        /*
        值可以是 flex-start, flex-end, center, baseline, stretch
        默认就是 flex-start, 伸缩项与侧轴起点对齐
        flex-end 使得伸缩项与侧轴终点对齐
        center 使得伸缩项与侧轴中点对齐
        
        baseline 使得所有伸缩项基线在一条直线上对齐
        stretch 使得所有伸缩项的高度变为侧轴的高度, 前提是伸缩项不能设置高度
        */
    }
    ```

    ##### flex-wrap & align-content

    指定**伸缩布局的换行与换行对齐**方式
    默认情况下如果伸缩容器的一行放不下所有的伸缩项, 系统会自动等比压缩所有伸缩项

    ```css
    selector{
        display: flex;
        flex-direction: row;
        justify-content: flex;
        align-items: flex-start;
     	flex-wrap: ;
        /*
        值可以是 nowrap, wrap, wrap-reverse
        默认就是 nowrap, 所有伸缩项挤一行
        wrap 使得放不下就换行, 不压缩
        wrap-reverse 使得不压缩换行后以行为单位进行反转
        */
    }
    ```

     指定**换行之后行与行的对齐**方式, 只在伸缩项发生**换行后**这个属性**才会**生效

    ```css
    selector{
        display: flex;
        flex-direction: row;
        justify-content: flex;
        align-items: flex-start;
     	flex-wrap: wrap; /* 上面都是默认值, 只有这个不是 */
        align-content: ;
        /*
        值可以是 flex-start, flex-end, center, space-between, space-around, stretch
        默认就是 stretch (居然不是默认为 flex-start, 差评)
        flex-start 使得行与行毗邻, 行与侧轴起点对齐
        flex-end 使得行与行毗邻, 行与侧轴终点对齐
        center 使得行与行毗邻, 行与侧轴中点对齐
        space-between 使得行与行两端对齐, 端当然指侧轴起止点
        space-around 使得行与行环绕对齐
        
        这里 stretch 不同于 align-items 或 align-self 的 stretch
        是以行为单位进行拉伸, 拉伸的部分以空白填充, 保证拉伸之后所有的行加起来能填满侧轴
        */
    }
    ```

    #### 伸缩项属性

    ##### align-self

    align-items 修改侧轴的对齐方式, 是**修改所有伸缩项**侧轴的对齐方式
    通过 align-self 修改侧轴的对齐方式, 是**单独修改当前伸缩项**侧轴的对齐方式
    取值与 align-items 相同

    ##### order

    **伸缩项排序**属性:
    每个伸缩项都有 order 属性, 默认值为 **0**,
    在 order 值相等时按元素**从上到下**依次排序,
    在 order 值不相等时按值**从小到大**依次排序

    ##### flex-grow

    **伸缩项扩充**属性:
    每个伸缩项都有 flex-grow 属性, 默认值为 **0**, (设为 0 的意思是此块不形变)
    **只在**当所有伸缩项宽度的总和小于伸缩容器的宽度时,  flex-grow 属性**才会**生效
    给每个伸缩项的 flex-grow 属性都设置相应的值, 数值大的会更宽, 但**数值并不是比例**

    flex-grow **计算公式**

    1. 剩余的空间 = 伸缩容器宽度 - 所有伸缩项的宽度
    2. 每份剩余空间的宽度 = 剩余空间 / 需要的份数
    3. 每个伸缩项**最终的宽度** = 伸缩项的宽度 + 需要的份数 * 每份的宽度

    ##### flex-shrink

    **伸缩项收缩**属性:
    每个伸缩项都有 flex-shrink 属性, 默认值为 **1**, (设为 0 的意思是超出父块也不缩小, ,默认是 1, 即等比缩小)
    **只在**当所有伸缩项宽度的总和大于伸缩容器的宽度时,  flex-shrink 属性**才会**生效
    给每个伸缩项的 flex-shrink 属性都设置相应的值, 数值大的会更加收缩, 但**数值并不是比例**

    flex-shrink **计算公式**

    1. 溢出的宽度 = 所有伸缩项的宽度总和 - 伸缩容器的宽度
    2. 总权重 = Σ每个伸缩项需要的份数 * 每个伸缩项的宽度
    3. 当前伸缩项**需要压缩的宽度** = 溢出的宽度 *((需要的份数 * 当前伸缩项原宽度) / 总权重) (加了括号逻辑更顺)
    4. 当前伸缩项**最终的宽度**  = 当前伸缩项原宽度 - 当前伸缩项需要压缩的宽度

    ##### flex-basis

    **伸缩项宽度**属性: 指定伸缩项的宽度

    如果是伸缩布局, 除了可以通过元素的width属性来设置宽度以外, 还可以通过flex-basis属性来设置伸缩项的宽度

    **注意点**:

    1. width 属性可以设置宽度, flex-basis **也可以**设置宽度, flex-basis 优先级高于 width
    2. flex-basis 属性是**专门提供给伸缩布局使用**的, 且只在伸缩布局中才有效
    3. 但如果同时通过这两个属性设置了宽度, 但是其中一个是auto, 那么系统会**按照具体值**来设置

    ##### 关于伸缩项宽度

    - 发现 flex-grow 和 flex-shrink 值为 0 都代表此块在需扩充(或收缩)不发生形变, 但 flex-shrink 值默认是 1 嗷
    - 前面说 flex-grow 和 flex-shrink 宽度扩充或缩小**并不严谨**, 也可能是高度, 具体是哪个, 还得看主轴在哪个方向
      主轴水平就扩缩宽度, 主轴竖直就扩缩高度
    - 如果没有给伸缩项指定宽度, 伸缩项的宽度由内容撑开

    ##### 伸缩项属性连写

    ```css
    selector{
        /* flex: flex-grow flex-shrink flex-basis;    */
        flex: 0 1 auto; /* 这就是默认值 */
    }
    /*
    注意点:
    在连写格式中, flex-shrink flex-basis是可以省略的, 只剩这一个值时它真就是比例了
    补充:
    如果只指定 flex-grow 和 flex-shrink, flex-basis 默认是 auto, 格子会被内容撑大
    */
    selector{
    	flex: 1;   
    }
    ```

    ### 两种重要布局

    #### 圣杯布局

    **圣杯布局**: 左中右三栏布局, 左右固定, 中间自适应

    **圣杯布局的步骤**:

    1. 搞一个容器, 里面放三个盒子
    2. 设置两侧盒子的宽度 (**固定**)
    3. 设置中间盒子的宽度等于容器的宽度 (100%)
    4. 让三个盒子都在同一个方向上浮动
    5. 设置容器的 padding 等于两侧盒子的宽度
    6. 设置左边盒子的左外边距为 **-100%**
    7. 通过定位调整左边的盒子, 让左边的盒子不要盖住中间的区域
    8. ###### 设置右边盒子的左外边距为负的自身的宽度
    9. 通过定位调整右边的盒子, 让右边的盒子不要盖住中间的区域
    10. 给容器设置一个最小的宽度, 防止缩小后变形

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>144-圣杯布局</title>
        <style>
            *{
                margin: 0;
                padding: 0;
            }
            .left, .right{
                width: 200px;
                height: 200px;
                background: red;
                float: left;
            }
            .center{
                width: 100%;
                height: 200px;
                background: skyblue;
                float: left;
            }
            .box{
                min-width: 400px;
                padding: 0 200px;
                background: purple;
                overflow: hidden;
            }
            .left{
                margin-left: -100%;
                position: relative;
                left: -200px;
            }
            .right{
                margin-left: -200px;
                position: relative;
                left: 200px;
            }
        </style>
    </head>
    <body>
    <div class="box">
        <div class="center">
    		中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容
            中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容
    		中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容
        </div>
        <div class="left"></div>
        <div class="right"></div>
    </div>
    </body>
    </html>
    ```

    圣杯布局在容器小到一定程度后会变形, 所以要设置个最小宽度, 保证效果

    #### 双飞翼布局

    圣杯布局的升级版, 实现上比圣杯布局容易一点, 少了 relative 定位调整, 中间盒子多了个子盒子
    而且总能自适应, 所以不需要设置最小宽度

    **双飞翼布局的实现步骤**:

    1. 搞一个容器, 里面放三个盒子
    2. 设置两侧盒子的宽度 (固定)
    3. 设置中间盒子的宽度等于容器的宽度 (100%)
    4. 让三个盒子都在同一个方向上浮动
    5. **给中间的盒子添加一个子盒子** (这一步是圣杯布局没有的)
    6. 给子盒子设置 margin 0 两侧盒子的宽度
       由于是给子盒子设置 margin,所以不会对父盒子排版产生任何影响
    7. 设置左边盒子的左外边距为 -100%
    8. 设置右边盒子的左外边距为负的自身宽度

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>145-双飞翼布局</title>
        <style>
            *{
                margin: 0;
                padding: 0;
            }
            .left, .right{
                width: 200px;
                height: 200px;
                background: red;
                float: left;
            }
            .center{
                width: 100%;
                height: 200px;
                background: skyblue;
                float: left;
            }
            .center>.center-in{
                margin: 0 200px;
                height: 200px;
                background: yellow;
            }
            .left{
                margin-left: -100%;
            }
            .right{
                margin-left: -200px;
            }
            .box{
                background: purple;
                overflow: hidden;
            }
        </style>
    </head>
    <body>
    <div class="box">
        <div class="center">
            <div class="center-in">
                中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容
    			中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容
    			中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容中间的内容	
            </div>
        </div>
        <div class="left"></div>
        <div class="right"></div>
    </div>
    </body>
    </html>
    ```

    



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

