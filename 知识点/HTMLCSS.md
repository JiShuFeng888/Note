```
使用CSS3代码代替JS动画（尽可能避免重绘重排以及回流）
```

```
修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。
```

```
如何创建块级格式化上下文(block formatting context),BFC有什么用
BFC(Block Formatting Context)，块级格式化上下文，是一个独立的渲染区域，让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响

触发条件 (以下任意一条)

float的值不为none
overflow的值不为visible
display的值为table-cell、tabble-caption和inline-block之一
position的值不为static或则releative中的任何一个

.BFC布局与普通文档流布局区别 普通文档流布局:

浮动的元素是不会被父级计算高度
非浮动元素会覆盖浮动元素的位置
margin会传递给父级元素
两个相邻元素上下的margin会重叠
BFC布局规则:

浮动的元素会被父级计算高度(父级元素触发了BFC)
非浮动元素不会覆盖浮动元素的位置(非浮动元素触发了BFC)
margin不会传递给父级(父级触发BFC)
属于同一个BFC的两个相邻元素上下margin会重叠
开发中的应用

阻止margin重叠
可以包含浮动元素 —— 清除内部浮动(清除浮动的原理是两个 div都位于同一个 BFC 区域之中)
自适应两栏布局
可以阻止元素被浮动元素覆盖

父级div定义伪类:after和zoom
父级div定义overflow:hidden



.clearfix:after{
  content: ""; 
  display: block; 
  height: 0; 
  clear: both; 
  visibility: hidden;  
  }

.clearfix {
  /* 触发 hasLayout */ 
  zoom: 1; 
 	}
```

```
// 不换行
@mixin no-wrap(){
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}
// 限制行数
@mixin clamp($row){
  overflow:hidden;
  text-overflow:ellipsis;
  display:-webkit-box;
  -webkit-box-orient:vertical; 
  -webkit-line-clamp:$row;
}
```

```
flex: 1;   
    让所有弹性盒模型对象的子元素都有相同的长度，忽略它们内部的内容
	flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0%;	
```

```
垂直居中一个元素：
父元素relative

  margin:auto;
  position: absolute;        //父元素需要相对定位
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  
  
  
  如何垂直居中一个<img>?（用更简便的方法。）

#container     /**<img>的容器设置如下**/
{
    display:table-cell;
    text-align:center;
    vertical-align:middle;
}
```

```
em = 像素值 / 父级font-size
```

```
水平居中的方法
元素为行内元素，设置父元素text-align:center
如果元素宽度固定，可以设置左右margin为auto;
绝对定位和移动: absolute + transform
使用flex-box布局，指定justify-content属性为center
display设置为tabel-ceil

垂直居中的方法
将显示方式设置为表格，display:table-cell,同时设置vertial-align：middle
使用flex布局，设置为align-item：center
绝对定位中设置bottom:0,top:0,并设置margin:auto
绝对定位中固定高度时设置top:50%，margin-top值为高度一半的负值
文本垂直居中设置line-height为height值
```

```
左边宽度固定，右边自适应
使用flex布局

.outer {
    width: 100%;
    height: 500px;
    background-color: yellow;
    display: flex;
    flex-direction: row;
}
.left {
    width: 200px;
    height: 200px;
    background-color: red;
}
.right {
    height: 200px;
    background-color: blue;
    flex: 1;
}
```

```
 用纯CSS创建一个三角形的原理是什么
/* 把上、左、右三条边隐藏掉（颜色设为 transparent） */
#demo {
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent transparent red transparent;
}
```

```
为什么要初始化CSS样式
因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异
```

```
offsetWidth/offsetHeight,clientWidth/clientHeight与scrollWidth/scrollHeight的区别
offsetWidth/offsetHeight返回值包含content + padding + border，效果与e.getBoundingClientRect()相同
clientWidth/clientHeight返回值只包含content + padding，如果有滚动条，也不包含滚动条
scrollWidth/scrollHeight返回值包含content + padding + 溢出内容的尺寸
```

```
 <meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no" />
    // width    设置viewport宽度，为一个正整数，或字符串‘device-width’
    // device-width  设备宽度
    // height   设置viewport高度，一般设置了宽度，会自动解析出高度，可以不用设置
    // initial-scale    默认缩放比例（初始缩放比例），为一个数字，可以带小数
    // minimum-scale    允许用户最小缩放比例，为一个数字，可以带小数
    // maximum-scale    允许用户最大缩放比例，为一个数字，可以带小数
    // user-scalable    是否允许手动缩放
```

