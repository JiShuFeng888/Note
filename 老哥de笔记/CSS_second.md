# CSS_second

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
8. 设置右边盒子的左外边距为负的自身的宽度
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

