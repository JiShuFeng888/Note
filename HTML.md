# HTML 标签

## 基本概念

URL: IP + 端口 + 资源名称。

HTML 作用: 为文本条件语义且**只应该**用来为文本添加语义。
在 html 中, 标签/标记/元素都是指 html 中的标签
一切 html 可用于修改样式的标签或者 attribute 都不推荐使用,这一原则到处都适用。

HTML: DTD 文档声明不是不是标签，现在是 HTML5 时代。

单标签闭合是 XHTML 的要求，html5 是向下兼容的，不闭合也行。

有个翻译是把 HTML 得 attribute 翻译为特性, 用于区分 property (翻译为属性), 但李南江老师不管这个, 管标签特性叫标签属性, 也并没有影响我理解, 反而是我记笔记总想着‘特性不能写成属性’而反复修改笔记, 这很没必要.
不如都叫属性, 标签属性就是标签属性, css 属性就是 css 属性, js 属性就是 js 属性, 指令就是 Vue 提供的标签属性, 只要主体明确, 就没问题, 就好像不同的类可以有同名属性而不会混淆一样

```html
<!-- 这是 html 用的注释的格式 -->
<!DOCTYPE html>
```

不推荐在行内元素中放块级元素 

## 常用标签

```html
<!--
这一大块儿包括:
标题, 段落, 水平线, 图像,
换行, 锚链, 基, 无序列表,
有序列表, 定义列表族, 表格族
-->

<h1></h1> <h2></h2> <h3></h3> <h4></h4> <h5></h5> <h6></h6>
<p></p>
<hr />
或者可以不闭合
<hr />

<img src="" width="" height="" title="" alt="" />
<!-- 
img 标签是行内块元素。
相对路径：同级就是图片和 .html 文件在同一文件夹。相对路径不能跨盘符。
绝对路径：每次都从指定的盘符开始查找，开发中不会用。
title 是悬停提示
-->

<br />
br加一次换一行，这个标签实际生产时用的少，p 用的多。

<a href="" target="" title=""></a> anchor 的缩写
<!--
href 属性既可以指定网络地址也可以指定本地 html 文件地址,
甚至可以指定页面内对应的 id 标签（但这个没有动画）。
若为 url 地址必须在前加上 http:// 或者 https://
target 属性值有 _self，_blank， #， javascript:void
-->
<base target="_blank" />
<!--
上面这个标签在 head 标签对中使用一次就能起到和在所有 a 标签中添加 target="_blank" 的效果
这个优先级比直接在 a 标签中指定 target 低
-->
```

### 列表标签

li 是块级元素, 啥都能往里装

```html
<!-- 无序列表 -->
<ul> <!-- li 是块级元素, 水平标签块常用 li 的浮动来做 -->
  <li></li>
</ul>

<!-- 有序列表 -->
<ol>
  <li></li>
</ol>

<!-- 定义列表 -->
<dl>
  <!-- definition list, definition title, definition description -->
  <dt></dt>
  <dd></dd>
  <!-- 推荐一个 dt 对应一个 dd	 -->
  <dt></dt>
  <dd></dd>
</dl>
<!-- 用来做网站尾部相关信息和图文混排 -->
<!--
ul 和 ol 的儿子们(最好)只能是 li，li 里面可以嵌 ul，ol。ul 用的多。
这几个都能用 type 设置外观，但是强烈建议用 css 去设置
-->
```

### 表格标签

```html
<!-- 表格是一种数据呈现方式,当数据量非常大时,这种形式被认为是最为清晰的一种展现形式 -->
<table border="" cellspacing="">
  <!-- 这俩特性值可后缀单位px也可不后缀 -->
  <caption>
    表格标题标签,这个标签只能写在 table 标签的 tr
    标签之前,写在这里面的会自动相对于表格去居中
  </caption>
  <thead>
    <tr>
      <!-- th 标签和 td 标签居然同级 -->
      <th>这里放表格表头内容,用这个会自动加粗和水平居中</th>
    </tr>
  </thead>
  <tbody>
    <tr align="">
      <td colspan="">
        colspan 是向后跨列合并. 从自身数起往后合并值个格子
        若有n列,其中m列合为一格,则该行应只剩 n-(m-1) 格(我牛逼)
      </td>
    </tr>
  </tbody>
  <tfoot>
    <tr align="">
      <td rowspan="">rowspan 是向下跨行合并,涉及下一个 tr 的td,哎哎,挺麻烦</td>
    </tr>
  </tfoot>
</table>
<!--
上面这个 table 是完整表格结构,其中浏览器会自动加 tbody, thead 和 tfoot 实际上很少用(04 年的新浪都不用了),这俩包着的不受 table 中设置的 height 属性影响
-->

<!-- 要通过设置标签特性做到 1px 纯色表格线,须如下设置 -->
<table bgcolor="black" cellspacing="1px">
  <tr bgcolor="white">
    <!-- 也就是 table 和 tr 标签设置背景颜色,再调整单元格间隙 -->
    <td></td>
    <!-- table,tr,td 都有 bgcolor 特性,bgcolor 结合不同标签有不同效果 -->
  </tr>
</table>
<!-- 表格标题指整个表格的标题,表头指表格的第一行 -->
<!-- 小结:完整表格包括标题,表头,主体,页尾.这个标签了解一下就好了 -->
```

### 表单标签

```html
<!-- 表单是用来收集用户信息的,浏览器中所有表单标签都有特殊外观和默认功能 -->
<form action="">
  <!-- action 特性用于指定 submit 的提交地址,有 name 特性的标签数据才会被提交 -->
    <!--
        这里输入的文字会与后面的"input的id值与该标签for值相同的"input标签绑定,
        绑定的意义是点文字实现输入框聚焦 
    -->
    <label for="xx">
        输入框前面的文字
    </label>
    <input
           type=""
           value=""
           id="xx"
           />
    <!-- 将 input 包裹在label 标签里就可以不需要 for,id 特性对 -->
<!--
这里 input 的 type 值就有很多种了,分别是 		   	  text,password,radio,checkbox,button,reset,submit,hidden
text(明文), password(暗文), radio(单选), checkbox(多选), button(按钮), reset(默认显示重置二字的按钮,作用是清空表单), submit(默认是显示提交二字, 作用是提交表单, 使用时需指明提交地址[与form标签的action特性搭配]和提交内容[与输入标签的name特性值搭配,以键值对的方式提交]), hidden 用于提交一些用户不可见的信息
-->
  <!-- value 值即为浏览器 input 框中默认值,reset 和 submit 也可改 value -->

<!--
type 值为 radio 时要与 name 特性搭配使用才起到单选框效果,value值是被提交的内容, checked 则是起到浏览器中默认选中的效果 
-->
  <input type="radio" name="gender" value="male" />male
  <input type="radio" name="gender" value="female" />female
  <input type="radio" name="gender" value="secret" checked="checked" />secret
  <!-- 这里 checked 特性名与特性值相同, 可只写一个 -->
  <!-- 收音机是按一个键其他键都会跳起来的设定,所以 radio 标签是单选框 -->
  <!-- checked 也可以结合 checkbox 使用起默认多个选中的效果 -->

  <!-- button type 结合 src 可以使按钮长成想要的图片的样子 -->
  <input type="button" src="" />male

  <input
    type=""
    list="oo"
  /><!-- 这一块儿的作用是通过 list,id 特性对实现输入框与一些数据的绑定 -->
  <datalist id="oo">
    <!-- 老浏览器对这些新标签的支持不太行 -->
    <option>天</option>
    <option>地</option>
    <option>人</option>
  </datalist>

  <!-- 新增的 input type 还有email,url,number,range,date,search,color,这些都相当于预置正则 -->
</form>

<!-- 以下是表单标签的非 input 标签 -->
<form>
  <select>
    <!-- 这个标签比 datalist标签早很多,差别是 select 不需要绑定而且只可选不可输入 -->
    <optgroup label="分组名称">
      <!-- 怪不得觉得绕,label 既是标签又是特性,没老师傅带很容易懵逼 -->
      <option></option>
      <option selected="selected"></option>
      <!-- 效果和 input 的 checked 类似,且也能只写一个单词 -->
    </optgroup>
    <!-- 这个是给选项分组,用处举例:特定城市有特定的区 -->
  </select>

  <!-- 这个是多行输入框, input 标签是单行输入框 -->
  <textarea col="" rows="">
    <!-- 指定行数列数后输入字数仍无限制 -->
    输入在这里的会显示在可编辑区域里面,而且可编辑.
    textarea 默认可以拉伸,通过修改 css 样式可使其不可拉伸
   </textarea>
</form>

<form>
  <fieldset>
    <!-- 这个是在表单外边包框框 -->
    <legend><!-- 这个是嵌在框框里的字 --></legend>
  </fieldset>
</form>
```

[html 标签集](https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/HTML5/HTML5_element_list) 哇,MDN 整理的又干净又好懂

### 音视频标签

```html
<!-- 特性名与特性值相同, 可只写一个 -->

<!-- 设置了 autoplay 特性则 preload 特性会失效 -->
<!-- 第一种格式 -->
<video src="" autoplay="autoplay" controls="controls" poster="poster" loop="loop" preload="preload" muted="muted" width="" height=""></video>
<!-- 第二种格式,这种格式的出现是因为各大浏览器对视频格式支持不一致 -->
<video>
    <source src="" type="video/文件格式"></source>
    <source src="" type=""></source>
</video>
<!--
另外,有些垃圾浏览器甚至不支持html5标签,这种情况下可以用 js 框架 html5media 来实现使用 vedio 标签
-->

<!-- audio 也有两种格式,原因和 video 有两种格式的原因相同 -->
<!-- audio 理所当然的不能设置宽高和封面 -->
<audio src="" autoplay="autoplay" controls="controls" loop="loop" preload="preload" muted="muted"></audio>
<audio>
    <source src="" type="audio/文件格式"></source>
</audio>
```

### 小甜点

```html
<details>
  <summary>概要信息</summary>
  详情信息
</details>

<marquee
  behavior="设置单项和弹反"
  direction="方向默认是左"
  scrollamount=""
  loop=""
  >这个标签不在标准内,但各大浏览器对这个标签的支持都很好.作用是形成滚动条.
  marquee 里面还能放图片</marquee
>
```

### 已废弃标签

```html
<!-- 已经被废弃的标签 -->
<!--
现代 html 标签的作用有且只有一个:添加语义,明确的语义. 因此以前一些生来就是为了设置样式的标签被废弃了
-->
<!-- 这些标签现在唯一的用处就是作为 css 的钩子(虽然能用) -->
<br />
<hr />
<font>
  <b>bold</b>
  <u>underline</u>
  <i>italic</i>
  <s>strike through</s></font
>
```

### 替代废弃标签的标签

```html
<!-- 替代被废弃的标签的标签,这些新标签的特点是: 语义鲜明 -->
<strong></strong>
<ins></ins>
<em></em>
<del></del>
```

### 字符实体

```html
<!-- 字符实体 -->
&nbsp; 就是一个字符实体.
<!-- nbsp 是 non-breaking space 的缩写 -->

在HTML中有的字符是被HTML保留的, 有的HTML字符在HTML中是有特殊含义的,
是不能在浏览器中直接显示出来的. 这些东西要想显示出来就必须通过字符实体.
```

## 与 css 结合才有威力的标签

### div 与 span

```html
<div>通过 div 标签和 css 样式设置, 可以很快搭出网页的基本框架</div>

<span>
  如果想更改一段文字的某一部分的样式, 可以用 span 标签讲这部分包裹起来, 用 css
  对 span 设置样式
</span>

<!-- label 是和 form 搭对使用的标签,虽然 label 的中文翻译也是标签, 但 html 中的标签英文是 tag -->

<!--
div 是容器级的标签, 可以嵌套其他所有标签. div 默认单独占一行.
span 是文本级的标签, 只能嵌套文字/超链接/图片. span 可多个挤一行. 
文本级标签放容器级标签不会报错, 但浏览器解析会导致问题. 
-->

<!--
容器级标签: div, h, ul, ol, dl, li... 容器级(块级)元素独占一行
文本级标签: span, p, buis, strong, em, ins, del... 文本级元素不独占一行
-->
```

### 块级元素和行内元素

#### 块级元素

- 独占一行
- 如果没有设置宽度, 那么默认和父元素一样宽
- 如果设置了宽高, 那么就按照设置的来显示

#### 行内元素

- 不会独占一行
- 如果没有设置宽度, 那么默认和内容一样宽
- 行内元素是不可以设置宽度和高度的

#### 行内块元素

- 为了能够让元素既能够不独占一行, 又可以设置宽度和高度, 那么就出现了行内块级元素
- img 标签就是原生行内块元素

#### 显示模式转换

块级元素,行内元素,行内块元素内通过设置 css 属性 display 的属性值来实现相互转换.
伸缩布局和格子布局也是通过 css 属性 display 来实现的.