# JavaScript_fourth

## BOM

BOM 包含 window 对象, 从而包含 DOM

### BOM 简介

1. 什么是BOM?
   - DOM就是一套操作HTML标签的API(接口/方法/属性)
   - BOM就是一套操作浏览器的API(接口/方法/属性)
2. BOM中常见的对象
   - window: 代表整个浏览器窗口 (注意: window是BOM中的一个对象, 并且是一个顶级的对象(全局))
   - navigator: 代表当前浏览器的信息, 通过这个对象我们就能判断用户当前是什么浏览器
   - location: 代表浏览器地址栏的信息, 通过这个对象我们就能设置或者获取当前地址信息
   - history:  代表浏览器的历史信息, 通过这个对象来实现刷新/上一步/下一步
     注意点: 出于隐私考虑, 我们并不能拿到用户所有的历史记录, **只能拿到当前的历史记录**
   - screen:  代表用户的屏幕信息 ()

### BOM 的常用对象

#### navigator

代表当前浏览器的信息, 通过 navigator.userAgent 我们就能判断用户当前是什么浏览器

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-Navigator</title
  </head>
  <body>
    <script>
      // console.log(window.navigator);
      var agent = window.navigator.userAgent;
      if (/chrome/i.test(agent)) {
        alert("当前是谷歌浏览器");
      } else if (/firefox/i.test(agent)) {
        alert("当前是火狐浏览器");
      } else if (/msie/i.test(agent)) {
        alert("当前是低级IE浏览器");
      } else if ("ActiveXObject" in window) {
        alert("当前是高级IE浏览器");
      }
    </script>
  </body>
</html>
```

#### location

代表浏览器地址栏的信息, 通过 location.href 我们就能设置或者获取当前地址信息

- 给 location.href 赋值可以实现跳转到指定网址, 这里**无法**只在地址栏赋值而不跳转
- location.reload()
- location.reload(true)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-Location</title>
  </head>
  <body>
    <button id="btn1">获取</button>
    <button id="btn2">设置</button>
    <button id="btn3">刷新</button>
    <button id="btn4">强制刷新</button>
    <script>
      let oBtn1 = document.querySelector("#btn1");
      let oBtn2 = document.querySelector("#btn2");
      let oBtn3 = document.querySelector("#btn3");
      let oBtn4 = document.querySelector("#btn4");
      // 获取当前地址栏的地址, 一般就是网址嘛
      oBtn1.onclick = function () {
        console.log(window.location.href);
      };
      // 设置当前地址栏的地址, 这里 return false 不管用
      oBtn2.onclick = function () {
        window.location.href = "http://www.it666.com";
        return false;
      };
      // 刷新页面, 作用相当于按 F5
      oBtn3.onclick = function () {
        window.location.reload();
      };
      // 强制刷新页面, 作用相当于按 ctrl + F5
      oBtn4.onclick = function () {
        window.location.reload(true);
      };
    </script>
  </body>
</html>
```

#### history

代表浏览器的历史信息, 通过History来实现刷新/前进/后退

- history.forward()
- history.back()
- **history.go(number)**

注意点:

- 只有当前**访问过**其它的界面**且有后退**, 才能通过 forward/go 方法前进
- 只有当前访问过其它的界面且有得退, 才能通过 back/go 方法后退
- 如果给 go 方法传递 **1**, 就代表前进 1 个界面, 传递 2 就代表进行 2 个界面
  如果给 go 方法传递 **-1**, 就代表后退 1 个界面, 传递 -2 就代表后退 2 个界面
  如果给 go 方法传递 **0**, 就代表刷新

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-History1</title>
</head>
<body>
<h1>我是第一个界面</h1>
<button id="btn1">前进</button>
<button id="btn2">刷新</button>
<a href="JavaScript-History2.html">新的界面222</a>
<script>
    let oBtn1 = document.querySelector("#btn1");
    let oBtn2 = document.querySelector("#btn2");
    oBtn1.onclick = function () {
        // window.history.forward();
        window.history.go(1);
    }
    // 如果给go方法传递0, 就代表刷新
    oBtn2.onclick = function () {
        window.history.go(0);
    }
</script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-History2</title>
</head>
<body>
    <h2>我是第2222个界面</h2>
    <button id="btn1">后退</button>
    <script>
        let oBtn1 = document.querySelector("#btn1");
       	// 如果给go方法传递-1, 就代表后退1个界面, 传递-2就代表后退2个界面
        oBtn1.onclick = function () {
            // window.history.back();
            window.history.go(-1);
        }
    </script>
</body>
</html>
```


## 正则

### 简介

1. 什么是正则表达式?
   正则表达式就是对字符串操作的一种逻辑公式
2. 正则表达式的作用?
   1. 在字符串"**查找**"是否包含指定子串 (确认有没有)
   2. 从字符串中"**提取**"指定子串 (有就拿出来用)
   3. 对字符串中指定的内容进行"**替换**" (换掉)

### 匹配，提取，替换

#### 不含正则版本

1. 字符串查找

   ```js
   let str = "123abc456";
   let index = str.indexOf("abc");
   let index = str.lastIndexOf("abc");
   let flag = str.includes("abc");
   ```

2. 字符串提取

   ```js
   let str = "123abc456";
   let startIndex = str.indexOf("a");
   console.log(str.substr(startIndex, "abc".length));
   ```

3. 字符串替换

   ```js
   let str = "123abc456";
   str.replace("abc", "it666");
   ```

#### 正则登场

两种方式：

- 通过 RegExp 构造函数生成一个对象， 通过这个对象调方法

  - RegExp 构造函数的第二个参数传叫“标志”

- 通过字面量来创建正则表达式对象

  ```js
  let reg = /\d{4}-\d{1,2}-\d{1,2}/g;
  console.log(typeof reg); // object
  ```

  - 字面量没得传参，直接把标志缀在字面量末端即可

1. 字符串匹配 .test

   - 朴素的演示

   ```js
   let str = "123abc456";
   
   // 默认情况下在正则表达式中是区分大小写的
   let reg = new RegExp("A");
   let res = reg.test(str);
   console.log(res); // false
   ```

   ```js
   let str = "123abc456";
   
   // 加上标志是查找变成不区分大小写
   let reg = new RegExp("A", "i");
   let res = reg.test(str);
   console.log(res); // true
   ```

   - 搞个有技术含量的

   ```js
   let str = "abc2020-11-07def";
   
   // 通过构造函数创建正则表达式对象
   // let reg = new RegExp("\\d{4}-\\d{1,2}-\\d{1,2}");
   
   // 通过字面量来创建正则表达式对象
   let reg = /\d{4}-\d{1,2}-\d{1,2}/;
   let res = reg.test(str);
   console.log(res); // true
   ```

2. 字符串提取 .match

   ```js
   let str = "abc2020-11-07def2020-11-11fdjsklf";
   
   // 默认情况下在正则表达式中一旦匹配就会停止查找
   let reg = /\d{4}-\d{1,2}-\d{1,2}/;
   let res = str.match(reg);
   console.log(res); 
   /*伪数组
   [
     '2020-11-07',
     index: 3,
     input: 'abc2020-11-07def2020-11-11fdjsklf',
     groups: undefined
   ]
   */
   console.log(res[0]); // 2020-11-07
   console.log(res[1]); // undefined
   ```

   ```js
   let str = "abc2020-11-07def2020-11-11fdjsklf";
   
   // 加上标志 g，实现全局查找
   let reg = /\d{4}-\d{1,2}-\d{1,2}/g;
   let res = str.match(reg);
   console.log(res); // [ '2020-11-07', '2020-11-11' ]
   console.log(res[0]); // 2020-11-07
   console.log(res[1]); // 2020-11-11
   ```

3. 字符串替换 .replace

   ```js
   let str = "abc2020-11-07def2020-11-11fdjsklf";
   
   let reg = /\d{4}-\d{1,2}-\d{1,2}/g;
   let newStr = str.replace(reg, "it666");
   console.log(str); // abc2020-11-07def2020-11-11fdjsklf
   console.log(newStr); // abcit666defit666fdjsklf
   ```

4. 以上字面量赋给对象得操作可以省掉

   ```js
   let str = "abc2020-11-07def2020-11-11fdjsklf";
   
   let newStr = str.replace(/\d{4}-\d{1,2}-\d{1,2}/g, "it666");
   console.log(str); // abc2020-11-07def2020-11-11fdjsklf
   console.log(newStr); // abcit666defit666fdjsklf
   ```

### 常用正则

常用正则表达式合集:

验证数字：^[0-9]\*$

验证n位的数字：^\d{n}$

验证至少n位数字：^\d{n,}$

验证m-n位的数字：^\d{m,n}$

验证零和非零开头的数字：^(0|[1-9][0-9]\*)$

验证有两位小数的正实数：^[0-9]+(.[0-9]{2})?$

验证有1-3位小数的正实数：^[0-9]+(.[0-9]{1,3})?$

验证非零的正整数：^\+?[1-9][0-9]\*$

验证非零的负整数：^\-[1-9][0-9]\*$

验证非负整数（正整数 + 0） ^\d+$

验证非正整数（负整数 + 0） ^((-\d+)|(0+))$

验证长度为3的字符：^.{3}$

验证由26个英文字母组成的字符串：^[A-Za-z]+$

验证由26个大写英文字母组成的字符串：^[A-Z]+$

验证由26个小写英文字母组成的字符串：^[a-z]+$

验证由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$

验证由数字、26个英文字母或者下划线组成的字符串：^\w+$



验证用户密码:^[a-zA-Z]\w{5,17}$ 正确格式为：以字母开头，长度在6-18之间，只能包含字符、数字和下划线。

验证是否含有 ^%&',;=?$\" 等字符：\[^%&',;=?$\x22]+

验证汉字：^[\u4e00-\u9fa5],{0,}$

验证Email地址：^\w+[-+.]\w+)\*@\w+([-.]\w+)\*\.\w+([-.]\w+)\*$

验证InternetURL：^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]\*)?$ ；^[a-zA-z]+://(w+(-w+)\*)(.(w+(-w+)\*))\*(?S\*)?$

验证电话号码：^(\d3,4|\d{3,4}-)?\d{7,8}$：--正确格式为：XXXX-XXXXXXX，XXXX-XXXXXXXX，XXX-XXXXXXX，XXX-XXXXXXXX，XXXXXXX，XXXXXXXX。

验证身份证号（15位或18位数字）：^\d{15}|\d{}18$

验证一年的12个月：^(0?[1-9]|1[0-2])$ 正确格式为：“01”-“09”和“1”“12”

验证一个月的31天：^((0?[1-9])|((1|2)[0-9])|30|31)$  正确格式为：01、09和1、31。

整数：^-?\d+$

非负浮点数（正浮点数 + 0）：^\d+(\.\d+)?$

正浮点数  ^(([0-9]+\.[0-9]\*[1-9][0-9]\*)|([0-9]\*[1-9][0-9]\*\.[0-9]+)|([0-9]\*[1-9][0-9]\*))$

非正浮点数（负浮点数 + 0） ^((-\d+(\.\d+)?)|(0+(\.0+)?))$

负浮点数 ^(-(([0-9]+\.[0-9]\*[1-9][0-9]\*)|([0-9]\*[1-9][0-9]\*\.[0-9]+)|([0-9]\*[1-9][0-9]\*)))$

浮点数 ^(-?\d+)(\.\d+)?$

## 防抖与节流

### 函数防抖

1. 什么是函数防抖[debounce]?
   - 函数防抖是优化高频率执行 js 代码的一种手段
   - 可以让被调用的函数**在一次连续的高频操作过程中只被调用==一次==**
2. 函数防抖作用
   - 减少代码执行次数, 提升网页性能
3. 函数防抖应用场景
   - oninput / onmousemove / onscroll / onresize 等事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-函数防抖</title>
</head>
<body>
<input type="text">
<script>

    let oInput = document.querySelector("input");
    let timerId = null;
    oInput.oninput = function () {
        timerId && clearTimeout(timerId);
        timerId = setTimeout(function () {
            console.log("发送网络请求");
        }, 1000);
        // console.log(this.value);
        // console.log("发送网络请求");
    }
</script>
</body>
</html>
<!--
    第一次触发 oninput 事件就会生成一个定时器并赋引用给 timerId
    若一秒内又触发 oninput 事件, line14 与运算会清空上一个定时器并重设定时器
    直到第一次有"两次输入间间隔大于一秒", console.log 方法才会被执行
-->
```

### 函数节流

1. 什么是函数节流[throttle]?
   - 函数节流也是优化高频率执行js代码的一种手段
   - 可以**==减少==高频调用函数的执行次数**
2. 函数节流作用
   - 减少代码执行次数, 提升网页性能
3. 函数节流应用场景
   - oninput / onmousemove / onscroll / onresize等事件
4. 函数节流和函数防抖<font color="red">区别</font>
   - 函数节流是减少连续的高频操作函数执行次数 (例如连续调用10次, 可能只x执行3-4次)
   - 函数防抖是让连续的高频操作时函数只执行一次(例如连续调用10次, 但是只会执行1次)
   - 这个写法有瑕疵
     - 节流函数的计时器一旦启动就不应该被清除， 所以这花哨的与计算是无效的
     - 截留启动后并不更新入参， 理想状况应该是第二次触发用最新的入参
     - javascript.info 里面习题 6-9-4 就是比较完美的节流函数写法

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-函数节流封装</title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      div {
        width: 200px;
        height: 200px;
        background: red;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
      }
    </style>
  </head>
  <body>
    <div></div>
    <script>
      let oDiv = document.querySelector("div");
      function resetSize() {
        let { width, height } = getScreen();
        oDiv.style.width = width / 2 + "px";
        oDiv.style.height = height / 2 + "px";
      }
      resetSize();
      // 监听可视区域尺寸的变化
      window.onresize = throttle(function () { // 这种函数包裹函数的操作有点酷
        resetSize();
        console.log("尺寸的变化");
      }, 500);

      function throttle(fn, delay) { // 节流函数
        // fn = test
        let timerId = null;
        let flag = true;
        return function () {
          if (!flag) return; // 第一次触发之后, 计时器时间之内, 触发该函数没效果, 因为会 return 掉
          flag = false;
          let self = this;
          let args = arguments;
          timerId && clearTimeout(timerId);
          timerId = setTimeout(function () {
            flag = true;
            fn.apply(self, args);
          }, delay || 1000);
        };
      }
      function getScreen() { // 获得可视区域宽高的适配性写法
        let width, height;
        if (window.innerWidth) {
          width = window.innerWidth;
          height = window.innerHeight;
        } else if (document.compatMode === "BackCompat") {
          width = document.body.clientWidth;
          height = document.body.clientHeight;
        } else {
          width = document.documentElement.clientWidth;
          height = document.documentElement.clientHeight;
        }
        return {
          width: width,
          height: height,
        };
      }
    </script>
  </body>
</html>
```

### 完整掌握的工具方法

- 这些都是用来用一个方法兼容多类浏览器的

```js
(function () {
  function getScreen() {
    let width, height;
    if (window.innerWidth) {
      width = window.innerWidth;
      height = window.innerHeight;
    } else if (document.compatMode === "BackCompat") {
      width = document.body.clientWidth;
      height = document.body.clientHeight;
    } else {
      width = document.documentElement.clientWidth;
      height = document.documentElement.clientHeight;
    }
    return {
      width: width,
      height: height,
    };
  }
  function getPageScroll() {
    let x, y;
    if (window.pageXOffset) {
      x = window.pageXOffset;
      y = window.pageYOffset;
    } else if (document.compatMode === "BackCompat") {
      x = document.body.scrollLeft;
      y = document.body.scrollTop;
    } else {
      x = document.documentElement.scrollLeft;
      y = document.documentElement.scrollTop;
    }
    return {
      x: x,
      y: y,
    };
  }
  function addEvent(ele, name, fn) {
    if (ele.attachEvent) {
      ele.attachEvent("on" + name, fn);
    } else {
      ele.addEventListener(name, fn);
    }
  }
  function getStyleAttr(obj, name) {
    if (obj.currentStyle) {
      return obj.currentStyle[name];
    } else {
      return getComputedStyle(obj)[name];
    }
  }
  function debounce(fn, delay) {
    // fn = test
    let timerId = null;
    return function () {
      let self = this;
      let args = arguments;
      timerId && clearTimeout(timerId);
      timerId = setTimeout(function () {
        fn.apply(self, args);
      }, delay || 1000);
    };
  }
  function throttle(fn, delay) {
    // fn = test
    let timerId = null;
    let flag = true;
    return function () {
      if (!flag) return;
      flag = false;
      let self = this;
      let args = arguments;
      timerId && clearTimeout(timerId);
      timerId = setTimeout(function () {
        flag = true;
        fn.apply(self, args);
      }, delay || 1000);
    };
  }

  window.getScreen = getScreen; // 获得屏幕尺寸
  window.getPageScroll = getPageScroll; // 拿到滚出屏幕区域的长度
  window.addEvent = addEvent; // 给拿到的 dom 元素添加事件
  window.getStyleAttr = getStyleAttr; // 拿到 css 文件里设置的样式
  window.debounce = debounce; // 函数防抖, 连续的操作里其函数参数只被执行一次
  window.throttle = throttle; // 函数节流, 连续的操作里其函数参数有时间间隔的执行
})();
```



## 杂项

### 什么是上古浏览器

IE 自 9 起就相对地现代了， 在开发层面现代浏览器能跑的代码 IE9 基本也能跑， 不像 IE8 还有自己独特的方法名

### 术语

- 行内,内联,外链
- 关键字,保留字,标识符,函数,命名规范
- 函数声明,函数表达式
- 扩展运算符
- 作用域链,原型链
- DOM,BOM
- 同源,跨域,JSONP
- 异步
- 语法糖: class, catch
- 解构赋值

### this

- 闭包,对象,bind,call,apply

### 同源、跨域、JSONP

#### 同源

协议，域名，端口**都**相同,就是同源, 否则就是跨域
同源策略（Same origin policy）是一种约定，它是浏览器最核心也最基本的安全功能

#### 同源策略带来的问题

在同源策略下, 浏览器只允许Ajax请求同源的数据, **不允许**请求不同源**除 script 之外**的数据
但在企业开发中, 一般情况下为了提升网页的性能, 网页和数据都是单独存储在**不同服务器**上的
这时如果再通过Ajax请求数据就会**拿不到**跨域数据

#### 跨域解决方案

- **jsonp**
- document.domain+iframe
- location.hash + iframe
- window.name + iframe
- window.postMessage
- flash等第三方插件

#### JSONP

##### 名词解释

JSONP stands for **JSON with Padding**.

Requesting a file from another domain can cause problems, due to cross-domain policy.
Requesting an external *script* from another domain does not have this problem.
JSONP uses this advantage, and request files using the script tag **instead of** the `XMLHttpRequest` object.

##### JSONP实现跨域访问的原理

- 在同一界面中可以定义多个 script 标签
- 同一个界面中多个 script 标签中的数据**可以相互访问**
- 可以通过 script 的 src 属性导入其它资源
- 通过 src 属性导入其它资源的**本质就是**将资源**拷贝**到 script 标签中
- script 的 src 属性不仅能导入本地资源, 还**能导入远程资源**
- 由于 script 的 src 属性**没有同源限制**, 所以可以通过 script 的 src 属性来请求跨域数据

##### promise

如果 promise 的状态是失败,但没有对应失败的监听就会报错.
then 方法返回的 promise 会继承返回者的 state.

### 发现

ES6 之后,代码块和函数的区别小了一点.

好讨厌 var

形参不用声明欸!

关键字如 if、switch、while 等不是函数,其毗邻的大括号的作用域是块级作用域而非函数作用域.不同作用域的 var 和 let 定义的变量的作用域可能不一样,这 tm 简直狗.

ES6 之前没有块级作用域,但高级浏览器不对 {} 内函数进行提升.

预解析时.若函数名和变量名同名时,函数的优先级更高.

js 通过 prototype 实现继承.

js 除了“事件绑定的函数”和“回调函数”以外的代码都是同步的.

### 关于 map

Iteration over `Map` and `Set` is always in the insertion order, so we can’t say that these collections are unordered, but we can’t reorder elements or directly get an element by its number.