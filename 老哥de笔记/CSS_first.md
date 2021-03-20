# CSS_first

style 标签只能放在 head 标签里, 与 title 标签是兄弟关系.

css 有**两大块知识点**: 选择器和属性.

开山名义: 盒模型由外到内包括外边距, 边框, 内边距, 内容. 英文写作 margin, border, padding, content

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
