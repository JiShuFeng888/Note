# 	JavaScript_third

## ES6 筑基

==重要: 调试代码是<font color="red">哪一行</font>输出的非常有用!!!==

### 数组与字符串进阶

#### 数组高级 API

##### 遍历数组

###### 朴素 for

```js
let arr = [1, 3, 5, 7, 9];

for(let i = 0; i < arr.length; i++){
    console.log(arr[i]);
}
```

###### 不推荐 for\..\.in

**注意点**:

- for\.\.\.in 循环就是专门用于遍历无序的东西的, 所以不推荐使用 for\.\.\.in 循环来遍历数组 (MDN 说的)

```js
for(let key in arr){
    // console.log(key);
    console.log(arr[key]);
}
```

###### ES6 新增 for\.\.\.of

for\.\.\.of 也可以迭代数组

```js
let arr = [1, 3, 5, 7, 9];

for(let value of arr){
    console.log(value);
}
```

###### Array.forEach()

forEach 方法会**自动调用传入的函数**

每次调用都会将**当前遍历到的元素**和**当前遍历到的索引**和**当前被遍历的数组**传递给这个函数

```js
let arr = [1, 3, 5, 7, 9];

arr.forEach(function (currentValue, currentIndex, currentArray) {
    console.log(currentValue, currentIndex, currentArray);
});
```

###### 实现一个 myForEach

```js
let arr = [1, 3, 5, 7, 9];

Array.prototype.myForEach = function (fn) {
    // this === [1, 3, 5, 7, 9]
    for(let i = 0; i < this.length; i++){
        fn(this[i], i, this);
    }
};

arr.myForEach(function (currentValue, currentIndex, currentArray) {
    console.log(currentValue, currentIndex, currentArray);
});
```

##### 数组索引

###### 原始的 API

```js
let arr = [3, 2, 6, 7, 6];

// 从左往右查找, 找到返回索引, 找不到返回-1
let index1 = arr.indexOf(6);
console.log(index1); // 2
// 从右至左查找, 找到返回索引, 找不到返回-1
let index2 = arr.lastIndexOf(6);
console.log(index2); // 4
// 从左往右查找, 找到返回true, 找不到返回false
let result = arr.includes(6);
console.log(result); // true
```

###### find

findIndex 方法返回索引, find 方法返回找到的元素

find 方法如果**找到了就返回找到的元素, 如果找不到就返回undefined**

```js
let arr = [3, 2, 6, 7, 6];

let value = arr.find(function (currentValue, currentIndex, currentArray) {
    // console.log(currentValue, currentIndex, currentArray);
    if(currentValue === 6){
        return true; // 注意到这个 true 是 return 到 find 方法上的
    }
});
console.log(value); // 6
```

###### 实现一个 myFind

```js
Array.prototype.myFind = function (fn) {
    for(let i = 0; i < this.length; i++){
        let result = fn(this[i], i, this);
        if(result){
            return this[i];
        }
    }
    return undefined;
}

let arr = [3, 2, 6, 7, 6];
let value = arr.myFind(function (currentValue, currentIndex, currentArray) {
    // console.log(currentValue, currentIndex, currentArray);
    if(currentValue === 6){
        return true;
    }
});
console.log(value);
```

###### findIndex

findIndex方法: 定制版的 indexOf, **找到返回索引, 找不到返回 -1**

```js
let arr = [3, 2, 6, 7, 6];

let index = arr.findIndex(function (currentValue, currentIndex, currentArray) {
    // console.log(currentValue, currentIndex, currentArray);
    if(currentValue === 6){
        return true;
    }
});
console.log(index); // 2
```

###### 实现一个 myFindIndex

```js
Array.prototype.myFindIndex = function (fn) {
    for(let i = 0; i < this.length; i++){
        let result = fn(this[i], i, this);
        if(result){
            return i;
        }
    }
    return -1;
}

let arr = [3, 2, 6, 7, 6];
let index = arr.myFindIndex(function (currentValue, currentIndex, currentArray) {
    // console.log(currentValue, currentIndex, currentArray);
    if(currentValue === 6){
        return true;
    }
});
console.log(index); // 2
```

##### 筛选数组元素

###### filter

数组的filter方法: 将满足条件的元素添加到一个新的恰好够长度的数组中

```js
let arr = [1, 2, 3, 4, 5];

let newArray = arr.filter(function (currentValue, currentIndex, currentArray) {
    // console.log(currentValue, currentIndex, currentArray);
    if(currentValue % 2 === 0){
        return true;
    }
});
console.log(newArray); // [2, 4]
```

###### 实现一个 myFilter

```js
Array.prototype.myFilter = function (fn) {
    let newArray = [];
    for(let i = 0; i < this.length; i++){
        let result = fn(this[i], i, this);
        if(result){
            newArray.push(this[i]);
        }
    }
    return newArray;
}
```

###### map

数组的map方法: 将满足条件的元素映射到一个新的和原来数组长度相同的数组中

```js
let arr = [1, 2, 3, 4, 5];

let newArray = arr.map(function (currentValue, currentIndex, currentArray) {
    // console.log(currentValue, currentIndex, currentArray);
    if(currentValue % 2 === 0){
        return currentValue;
    }
});
console.log(newArray); // [undefined, 2, undefined, 4, undefined]
```

###### 实现一个 myMap

```js
Array.prototype.myMap = function (fn) {
    let newArray = new Array(this.length);
    newArray.fill(undefined); // fill 居然真的是有用的
    for(let i = 0; i < this.length; i++){
        let result = fn(this[i], i, this);
        if(result !== undefined){
            newArray[i] = result;
        }
    }
    return newArray;
}
```

##### 删除数组元素

<font color="red">**注意点**</font>: 要考虑删除元素后**坑位还在不在的问题**

###### 正着 for 结合 splice 不行

```js
let arr = [1, 2, 3, 4, 5];

console.log(arr);
for(let i = 0; i < arr.length; i++){
    // console.log(arr.length); // 5, 4, 3
	arr.splice(i, 1);
}
console.log(arr);
```

###### 把 len 固定下来也不行

这个和上面内个不行的原因: **splice 不光切走了元素, 还截短了数组**

```js
let arr = [1, 2, 3, 4, 5];

console.log(arr);
let len = arr.length;
for(let i = 0; i < len; i++){
        // console.log(len); // 5
        arr.splice(i, 1); // array.splice(start[, deleteCount[, item1[, item2[, ...]]]])	
}
console.log(arr);
```

小声bb: 数组会自动扩充却还是有长度的概念, 这就很不直观令人困惑, 不学正统语言的定长数组就接触这个会气死人

###### 反着 for 可以

```js
let arr = [1, 2, 3, 4, 5];

let len = arr.length;
for(let i = len - 1; i >= 0; i--){
    arr.splice(i, 1);
}
console.log(arr);
```

###### 反着这样都行

虽然不推荐, 毕竟反复计算了数组长度

```js
let arr = [1, 2, 3, 4, 5];

for(let i = arr.length; i >= 0; i--){
    arr.splice(i, 1);
}
console.log(arr);
```

###### delete 可以

与 splice 不同, delete 只删除元素, 不会截短数组

```js
let arr = [1, 2, 3, 4, 5];

for(let i = 0; i < arr.length; i++){
    console.log(arr.length);
    // 注意点: 通过delete来删除数组中的元素, 数组的length属性不会发生变化
    delete arr[i];
}
console.log(arr);
```

##### 自己实现的关键

```js
for(let i = 0; i < this.length; i++){
    let result = fn(this[i], i, this);
    . . .
}

// 所以 this 还是很重要的
```

##### 排序 – sort

- 如果 compareFunction(a, b) 小于 0， 那么 a 会被排列到 b 之前；
- 如果 compareFunction(a, b) 等于 0， a 和 b 的相对位置不变。
- 如果 compareFunction(a, b) 大于 0， b 会被排列到 a 之前
- **注意点**:
  - 如果元素是字符串类型, 那么比较的是字符串的 Unicode 编码, 字符串排前面的字母优先级高
  - sort 本质是根据一套规则来排序, 默认有一套升序的规则, 但使用者可以改写排序规则以实现想要的排序

```js
let arr = ["c", "a", "b"];
arr.sort();
console.log(arr); // ["a", "b", "c"]
```

```js
let arr = ["c", "a", "b"];

arr.sort(function (a, b) { // b 下标是 a 下标 +1
    if(a > b){
        return 1;
    }else if(a < b){
        return -1;
    }else{
        return 0;
    }
});
console.log(arr); // ["a", "b", "c"]
```

- 只是比较数字类型

```js
let arr = [3, 4, 2, 5, 1];

arr.sort(function (a, b) {
    return a - b;
});
console.log(arr); // [ 1, 2, 3, 4, 5 ]
```

- 比较字符串

```js
let arr = ["1234", "21", "54321", "123", "6"];
arr.sort(function (str1, str2) {
    return str1.length - str2.length;
});
console.log(arr); // [ '6', '21', '123', '1234', '54321' ]
```

- 根据对象某一属性作比较

```js
let students = [
    {name: "zs", age: 34},
    {name: "ls", age: 18},
    {name: "ww", age: 22},
    {name: "mm", age: 28},
];
students.sort(function (o1, o2) {
    return o1.age - o2.age;
});
console.log(students);
```

#### 字符串

##### 常用的字符串 API

**在 js 中字符串可以看做一个特殊的数组**, (注意注意! string 是基本数据类型, 数组是引用类型==!!!==)
所以==大部分==数组的属性/方法字符串都可以使用,
但一般字符串有自己的方法, 虽然作用相同, 但用字符串专属方法显得专业

###### 获取字符串长度

.length

```js
let str = "abcd";
console.log(str.length);
```

###### 通过索引获取字符

charAt

```js
let str = "abcd";
// let ch = str[1]; // 与 charAt 作用一致, 低级浏览器不支持这么用
let ch = str.charAt(1);
console.log(ch); // b
```

###### 通过字符获取索引

indexOf/ lastIndexOf/ includes (和数组的一样的呀) ==传的是字符串也行嗷== 

```js
let str = "vavcd";
let index1 = str.indexOf("v");
console.log(index1); // 0
let index2 = str.lastIndexOf("v");
console.log(index2); // 2
let result = str.("p");	
console.log(result); // false
```

###### 拼接字符串

\+/ concat (用加号好, concat 留给数组用, 最佳实践呐)

```js
let str1 = "www";
let str2 = "it666";
let str3 = str1 + str2; // 推荐
let str4 = str1.concat(str2);
console.log(str3); // wwwit666
console.log(str4); // wwwit666
```

###### 截取子字符串

slice/ substring/ substr__废弃__ (居然没驼峰) 

这仨都**不会改变原数组**

```js
let str = "abcdef";
let subStr = str.slice(1, 3); // str.slice(beginIndex[, endIndex])
console.log(subStr); // bc
```

```js
let str = "abcdef";	
let subStr = str.substring(1, 3); // str.substring(indexStart[, indexEnd])
console.log(subStr); // bc
```

```js
let str = "abcdef";
let subStr = str.substr(1, 3); // str.substr(start[, length])
console.log(str);
console.log(subStr); // bcd
```

###### 切割字符串

- join

数组的 join 方法能用指定的符号拼接数组元素为字符串

```js
let arr = [1, 3, 5];
let str = arr.join("-");
console.log(str); // 1-3-5
```

- split

split 能将字符串用指定的符号(包括空格)来切割字符串为数组
**注意点**: 得到的数组的每个元素也都是字符串

```js
let str = "1-3-5";
let arr = str.split("-");
console.log(arr);
```

###### 验证字符串开头

- startWith

```js
let str = "http://www.it666.com";
let result = str.startsWith("www");
console.log(result); // true
```

###### 验证字符串结尾

- endWith

```js
let str = "fhs.jpg";
let result = str.endsWith("png");
console.log(result);
```

##### 模板字符串

反引号包着的和引号包着的**都是**字符串, 但是反引号有一些花哨的操作, 通常也比较省事儿

```js
let str = `www.it666.com`;
console.log(str); // www.it666.com
console.log(typeof str); // string
```

- 一般字符串用单引号`‘’`或双引号`“”`括起来

  ```js
  let str =   "<ul>\n" +
              "    <li>我是第1个li</li>\n" +
              "    <li>我是第2个li</li>\n" +
              "    <li>我是第3个li</li>\n" +
              "</ul>";
  ```

  ```js
  let name = "fhs";
  let age = 23;
  let str = "我的名字是" + name + ",我的年龄是" + age;
  console.log(str); // 我的名字是fhs,我的年龄是23
  ```

  - 模板字符串用反引号==``==括起来 (省事儿)	

  ```js
  let str = `<ul>
                  <li>我是第1个li</li>
                  <li>我是第2个li</li>
                  <li>我是第3个li</li>
              </ul>`;
  ```

  - 原来 js 的原生美元符 `${}` 是跟模板字面量结合使用的嗷

  ```js
  let name = "fhs";
  let age = 23;
  let str = `我的名字是${name},我的年龄是${age}`;
  console.log(str); // 我的名字是fhs,我的年龄是23
  ```

### 重要的对象们

js 中凡引用类型都是对象,
函数是引用类型因而也是对象,
重要的对象自然也就包括了重要的构造函数即类,
因为 js 的类是通过函数来实现的 

#### 包装类型

```js
let a = new String("word");
console.log(typeof a); // object
```

1. 有哪些基本数据类型?
   字符串类型 / 数值类型 / 布尔类型 / 空类型 / 未定义类型/ symbol

2. 通过字面量创建的**基本数据类型**的数据都是常量

3. 常量的特点和注意点

   - <font color="red">常量是不能被修改</font>的

     ```js
     let str = "abc";
     str[1] = "m";
     console.log(str); // abc
     ```

   - 每次‘修改’或者拼接都是**生成一个新的**

     ```js
     let str = "abc";
     let newStr = str.replace("b", "m");
     console.log(str); // abc
     console.log(newStr); // amc
     ```

4. 基本类型特点

   - 没有属性和方法

     ```js
     let str = "lnj";
     str.age = 34;
     str.say = function () {
         console.log("hello");
     }
     console.log(str.age); // undefined
     str.say(); // str.say is not a function
     ```

5. 对象类型的特点

   - 有属性和方法

6. 以前之所以能够访问基本数据类型的属性和方法, 是因为

   - 在运行的时候系统自动将基本数据类型包装成了对象类型

   - String() / Number() / Boolean()

     ```js
     let str = "www.it666.com";
     // let str = new String(str); // 底层不是 string 基本类型而是 String 类 new 出来的对象在调方法
     console.log(str.length);
     str.split(".");
     ```

#### 三大对象

JavaScript中提供三种自带的对象, 分别是:

1. 本地对象
2. 内置对象
   1. Global
   2. Math
   3. JSON
3. 宿主对象

什么是宿主?

- 宿主就是指JavaScript运行环境, js 可以在浏览器中运行, 也可以在服务器上运行

##### 本地对象

- **与宿主无**关，无论在浏览器还是服务器中都有的对象
- 就是 ECMAScript 标准中定义的类(构造函数) 生产的对象
- 在使用过程中**需要我们手动 new 创建**
- 例如：Boolean、Number、String、Array、Function、Object、Date、RegExp 等

##### 内置对象

- 与宿主无关，无论在浏览器还是服务器中都有的对象
- JavaScript 已经帮我们创建好的对象。
- 在使用过程中**无需**我们手动 new 创建
- 例如：Global、Math、JSON、 Date

##### 宿主对象

- 对于嵌入到网页中的JS来说，其宿主对象就是浏览器, 所以宿主对象就是浏览器提供的对象
- 包含: Window和Document等
- 所有的 DOM 和 BOM 对象都属于宿主对象, 只浏览器宿主提供 DOM 和 BOM

#### 内置对象们 

##### Math

Math.floor() | 向下取整

Math.ceil() | 向上取整

Math.round() | 四舍五入

Math.abs() | 绝对值

Math.random() | 生成随机数

经典应用 (可不简单嘞!):

```js
// 需求: 要求生成一个1~10的随机数
function getRandomIntInclusive(min, max) {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值
}
let value = getRandomIntInclusive(0, 10);
console.log(value);

/*
分析一波:
10 - 0 + 1 = 11
Math.random() 是生产从零到一左闭右开区间内的所有浮点数
Math.random() * 11 得到从零到十一左闭右开的平均概率密度的区间
十一个数字恰分出十小段, 每段的可能性是相等的, 因为 random 恰取到整数的概率趋近于 0

*/
```

##### Date

###### 基操

1. 获取当前时间
   new 出来的对象有一个标准格式 我们一般不用这个默认的格式

   ```js
   let date = new Date();
   console.log(date); // 2020-11-07T10:10:34.483Z
   console.log(typeof date); // object 
   ```

2. 获取当前时间距离1970年1月1日（世界标准时间）起的毫秒

   - 方法一

     ```js
     console.log(Date.now());
     ```

   - 方法二

     ```js
     // 日记对象进行计算时底层就是调用这个 .valueof
     let date = new Date();
     console.log(date.valueOf());
     ```

3. 创建指定时间

   - 方法一

     ```js
     // 年月日时分秒 
     let date = new Date("2020-11-07 10:10:34");
     console.log(date);
     ```

   - 方法二
     **注意点**: 在创建指定时间的时候, **如果月份是单独传入的, 那么会多一个月**

     ```js
     let date = new Date(2020, 10, 07, 9, 8, 7);
     console.log(date);
     ```

4. 获取指定时间年月日时分秒

   ```js
   	x 1let date = new Date();2console.log(date.getFullYear());34// 注意点; 通过getMonth方法获取到的月份会少一个月5console.log(date.getMonth() + 1);67console.log(date.getDate()); // 拿几号8console.log(date.getHours());9console.log(date.getMinutes());10console.log(date.getSeconds());1112// 此外还有13console.log(date.getMilliseconds());14console.log(date.getDay()); // 拿周几js
   ```

5. 时间格式化

   ```js
   let date = new Date();
   let res = formatDate(date);
   
   console.log(res); // 2020-11-7 18:30:46
   
   function formatDate(date) {
       return `${date.getFullYear()}-${date.getMonth() + 1}-${date.getDate()} ${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;
   }
   ```

###### 计算时间差

拿到两个时间点的毫秒值, 算出两个时间点相差几天几小时几分几秒

```js
	 1// 1000毫秒 = 1秒   60秒 = 1分钟  60分钟 = 1小时  24小时 = 1天2// 以下两个时间相差值 10天1小时29分40秒3let curDate = new Date("2020-4-19 22:30:20");4let remDate = new Date("2020-4-30 00:00:00");5// 1.得到两个时间之间的差值(毫秒)6let differTime = remDate - curDate;7// let differTime = remDate.valueOf() - curDate.valueOf();8// 2.得到两个时间之间的差值(秒)9let differSecond = differTime / 1000;10// 3.利用相差的总秒数 / 每一天的秒数 = 相差的天数11let day = Math.floor(differSecond / (60 * 60 * 24));12console.log(day);13// 4.利用相差的总秒数 / 小时 % 24;14let hour = Math.floor(differSecond / (60 * 60) % 24);15console.log(hour);16// 5.利用相差的总秒数 / 分钟 % 60;17let minute = Math.floor(differSecond / 60 % 60);18console.log(minute);19// 6.利用相差的总秒数 % 秒数20let second = differSecond % 60;21console.log(second);2223// 用 parseInt 不合适( IDE 会给警告), 因为 parseInt 应该接收字符串, 尽管是弱类型语言, 啥类干啥事最好还是分清楚    js
```



### 闭包与循环索引同步

#### 闭包 (新奇的解释)

1. 什么是闭包(closure)?
   - 闭包是一种特殊的函数。
2. 如何生成一个闭包?
   - 当一个内部函数引用了外部函数的数据(变量/函数)时, 那么内部的函数就是闭包
   - 所以只要满足**"是函数嵌套"、"内部函数引用外部函数数据"**
3. 闭包特点:
   - **只要闭包还在使用外部函数的数据, 那么外部的数据就一直不会被释放**
   - 也就是说可以延长外部函数数据的生命周期
4. 闭包注意点:
   - 当后续不需要使用闭包时候, 一定要手动将闭包设置为null, 否则会出现内存泄漏

```js
// 常规函数
function test() {
    var i = 666; // 局部变量
} // 只要代码执行到了大括号结束, i这个变量就会自动释放
console.log(i); // i is not defined
```

```js
function test() {
    var i = 666;
    // 由于demo函数满足闭包的两个条件, 所以demo函数就是闭包
    return function demo() {
        console.log(i);
    }
}
let fn = test();
fn(); // 666
```

#### 循环索引同步

- 要拎清: 函数**定义**和函数**执行**

##### 最基本的认识

- JavaScript 是单线程的

##### var

- 默认情况下**通过 var 定义的变量, 只要不是定义在函数中都是==全局变量==**

###### <s>for 循环用 var, for 完调函数</s>

for 完了才执行到 test, 此时全局变量 i 已经是 3 了, **我们称这种情况为循环索引==不同步==**

```js
for(var i = 0; i < 3; i++){ // 0 1 2 3
    function test() {
        console.log(i); // 3
    }
}
test();
```

###### for 循环用 var, for 里面调函数

```js
for (var i = 0; i < 3; i++) {
    function test() {
        console.log(i); // 0 // 1 // 2
    }
    test();
}
```

###### for 循环里面用立即执行函数

```js
for(var i = 0; i < 3; i++){
    (function test() {
        console.log(i); // 0 // 1 // 2
    })();
}
```
##### 闭包结合 var 循环索引同步

###### for 内调函数, 同义变体

```js
for(var i = 0; i < 3; i++){
    // function test(index) {
    //     console.log(index); // 0 // 1 // 2
    // }
    // test(i);
    (function test(index) {
        console.log(index); // 0 // 1 // 2
    })(i);
}
```

这样==就能==点第几个按钮就在控制台输出几 (从零开始)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>22-JavaScript-循环索引同步练习</title>
</head>
<body>
<button>我是按钮1</button>
<button>我是按钮2</button>
<button>我是按钮3</button>
<script>
    // 不能同步, 原理与 for 完调函数相同, for 才有 "每个 button 上都绑定了 onclick 事件", 此时 i 已经是 3
    /*
    let oBtns = document.querySelectorAll("button");
    for(var i = 0; i < oBtns.length; i++){
        let btn = oBtns[i];
        btn.onclick = function () {
            console.log(i); // 3
        }
    }
    */

    // 可以同步
    /*
    for(var i = 0; i < 3; i++){
        (function test(index) { // var index = i;
            console.log(index); // 0 1 2
        })(i);
    }
    */
    let oBtns = document.querySelectorAll("button");
    for(var i = 0; i < oBtns.length; i++) {
        let btn = oBtns[i];
        (function test(index) { // var index = i;
            // console.log(index); // 0 1 2
            // 注意点: onclick对应的方法由于满足了闭包的条件, 所以onclick对应的方法也是一个闭包
            btn.onclick = function () {
                console.log(index);
            }
        })(i);
    }
</script>
</body>
</html>
```

==这样又不行==, 个中差别**只在于**是否立即执行,
给参数赋值 (上面那种) 是 js 立即就干了的,
而触发点击事件却不是. 妈欸好鬼酷哦

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>22-JavaScript-循环索引同步练习</title>
  </head>
  <body>
    <button>我是按钮1</button>
    <button>我是按钮2</button>
    <button>我是按钮3</button>
    <script>
      // 不能同步
      let oBtns = document.querySelectorAll("button");
      for (var i = 0; i < oBtns.length; i++) {
        let btn = oBtns[i];
        (function test() {
          btn.onclick = function () {
            console.log(i);
          };
        })();
      }
    </script>
  </body>
</html>

```


##### let 天然可以循环索引同步

- 在ES6中如果在循环中通过 let 定义的变量, 那么这个变量是一个==局部变量==
- 由于 i 是局部变量, 所以每次执行完循环体都会重新定义一个 i 变量,
  且这个 i 并不对之前的 i 进行覆盖, 相互之间并不相干
- 在 ES6 中由于 {} 是块级作用域, 所以只要在块级作用域中定义了一个函数
  并且这个函数中用到了块级作用域中的数据, 那么这个函数就是闭包

```js
var list = [];
// 这里的i是全局变量
for(var i = 0; i < 3; i++){
    var fn = function test() {
        console.log(i); // 3 // 3 // 3
    }
    list.push(fn);
}

console.log(i); // 3
list[0]();
list[1]();
list[2]();
```

```js
let list = [];
for (let i = 0; i < 3; i++) {
    let fn = function test() {
        console.log(i); // 0 // 1 // 2
    };
    list.push(fn);
}

// console.log(i); // Uncaught ReferenceError: list is not defined
list[0]();
list[1]();
list[2]();
```

##### var 与 let 搞笑区别

- 在ES6中由于 {} 是块级作用域, 所以只要在块级作用域中定义了一个函数
- 并且这个函数中用到了块级作用域中的数据, 这个函数就是闭包

```js
for(var i = 0; i < 3; i++){ // 0 1 2 3
    function test() {
        console.log(i); // 3
    }
}
test();
```

```js
for(let i = 0; i < 3; i++){
    function test() {
        console.log(i); // 2
    }
}
test();
```

##### 闭包与 let, 优雅现代

- {} 的块级只能通过 let 来达成, 用了 let 后 {} 包着的函数 prone to 形成闭包
- 在ES6中
  1. for循环中通过let定义的变量是一个局部变量
  2. 2.for循环中通过let定义的变量每次执行循环体都会重新定义一个新的属于自己的变量
  3. for循环中如果定义了函数, 这个函数用到了通过let定义的变量, 那么这个函数是一个闭包

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>22-JavaScript-循环索引同步练习</title>
</head>
<body>
<button>我是按钮1</button>
<button>我是按钮2</button>
<button>我是按钮3</button>
<script>
    let oBtns = document.querySelectorAll("button");
    for(let i = 0; i < oBtns.length; i++){
        let btn = oBtns[i];
        btn.onclick = function () {
            console.log(i);
        }
    }
</script>
</body>
</html>
```




## DOM (了解即可)

### 从 window 到 DOM

**注意点**:

- DOM 是浏览器宿主提供的对象, 所以**相关代码要在浏览器中打开和调试**
- DOM 是根据 html 长出来的, DOM 相关的 js 代码都是结合 html 的在浏览器环境下运行的 js 代码

1. 什么是window?

   - window：是一个**全局对象**, 代表浏览器中一个打开的窗口, 每个窗口都是一个 window 对象

2. 什么是document?

   - document 是 window 的一个属性, 这个属性是一个对象的引用
   - document: 代表当前窗口中的整个网页
   - document对象保存了网页上所有的内容, 通过 document 对象就可以操作网页上的内容

3. 什么是DOM?

   - **DOM 定义了访问和操作 HTML 文档(网页)的标准方法**

   - DOM 全称: Document Object Model, 即文档模型对象

   - 所以学习 DOM 就是学习如何通过 document 对象操作网页上的内容

     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <title>Test</title>
     </head>
     <body>
         <script>
             console.log(window.document);
             console.log(typeof window.document);
             console.log(window.document.title);
         </script>
     </body>
     </html>
     ```

### 获取 DOM 元素或节点 

- 元素, element, 在 DOM 里指 html 标签的对应对象

- 节点, node, DOM对象以树的形式保存了界面上所有的内容

  HTML 页面<font color="red">每一部分</font>在 DOM 中都是有对应的节点 (标签(元素),==文本==,属性(已废弃)等等)

- **所以元素是节点的子集**

#### 老牌的 getXX 和现代的 queryXX

- 在 JavaScript 中 HTML 标签也称之为 DOM 元素
- 使用 document 的时候前面不用加 window

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Test</title>
</head>
<body>
    <script>
        var num = 666;
        console.log(window.num);
        console.log(num);

        // 同理可证
        console.log(window.document);
        console.log(document);
    </script>
</body>
</html>
```



1. 通过 id 获取指定元素 `.getElementById("idName");`
   - 由于 id 不可以重复, 所以找到了就会将找到的标签包装成**一个对象**返回给我们, 找不到就返回 **null**
   - **注意点**: DOM 操作**返回的是一个对象**, 这个对象是宿主类型对象(浏览器提供的对象)
2. 通过class名称获取 `.getElementsByClassName("className");`
   - 由于 class 可以重复, 所以找到了就返回**一个存储了标签对象的数组**, 找不到就返回**一个空数组**
3. 通过标签属性 name 值获取 `.getElementsByName("nameAttributeValue");`
   - 由于name可以重复, 所以找到了就返回一个存储了标签对象的数组, 找不到就返回一个空数组
   - **注意点**:
     - getElementsByName 在不同的浏览器其中工作方式不同
     - 在IE和Opera中，getElementsByName() 方法还会返回那些 id 为指定值的元素
4. 通过标签名称获取 `.getElementsByTagName("tagName");`
   - 由于标签名称可以重复, 所以找到了就返回一个存储了标签对象的数组, 找不到就返回一个空数组
5. 通过选择器获取 `.querySelector("");` (==**重点掌握**==)
   - querySelector 只会返回根据指定选择器找到的第一个元素
   - 类名用 ., id 名用 #, 各种选择器都用得
6. 通过选择器获取 `.querySelectorAll("");` (==**重点掌握**==)
   - querySelectorAll 会返回指定选择器找到的所有元素
   - 各种选择器都用得
7. [关于 get 系和 query 系的区别](https://www.imooc.com/article/13027)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-获取DOM元素</title>
</head>
<body>
<div class="father">
    <form>
        <input type="text" name="test">
        <input type="password" name="test">
    </form>
</div>
<div class="father" id="box">我是div</div>

<script>
    let oDiv1 = document.getElementById("box");
    console.log(oDiv1);
    console.log(typeof oDiv1); // object

    let oDivs1 = document.getElementsByClassName("father");
    console.log(oDivs);

    let oDivs2 = document.getElementsByName("test");
    console.log(oDivs);

    let oDivs3 =  document.getElementsByTagName("div");
    console.log(oDivs);

    let oDiv4 = document.querySelector("#box");
    let oDiv5 = document.querySelector(".father");
    let oDiv6 = document.querySelector("div>form");

    let oDivs7 = document.querySelectorAll(".father");
    console.log(oDivs);
</script>
</body>
</html>
```

#### 通过元素(节点)拿其他元素(节点)

##### 获取父元素, 父节点

- 由于元素的父节点必然是元素, 所以下面俩方法作用是一样的

```js
let item = document.querySelector(".item");
console.log(item.parentElement);
console.log(item.parentNode);

// 火狐一开始不支持 .parentElement, 现在通用 .parentElement 就好啦
// let parentEle = item.parentElement || item.parentNode;
let parentEle = item.parentElement;
console.log(parentEle);
```

##### 获取子元素, 子节点

妈的这名字不能很好的见名知意, 差评!

1. 获取指定元素所有子代

   - .childNodes 拿所有节点
   - .children 拿所有元素

   ```js
   let oDiv = document.querySelector("div");
   
   // children属性获取到的是指定元素中所有的子元素
   // console.log(oDiv.children);
   
   // childNodes属性获取到的是指定元素中所有的节点
   // console.log(oDiv.childNodes);
   
   for(let node of oDiv.childNodes){
       // console.log(node.nodeType); // 3
       // if(node.nodeType === 1){ // 与第12行等价, 但不够炫酷
       if(node.nodeType === Node.ELEMENT_NODE){
           console.log(node);
       }
   }
   ```

2. 获取指定节点中的第一个子代

   - .firstChild 拿第一个子节点
   - .firstElementChild 拿第一个子元素

   ```js
   let oDiv = document.querySelector("div");
   console.log(oDiv.firstChild);
   console.log(oDiv.firstElementChild);
   ```

3. 获取指定节点中的最后一个子代

   - .lastChild 拿最后一个子节点
   - .lastElementChild 拿最后一个子元素

   ```js
   let oDiv = document.querySelector("div");
   console.log(oDiv.lastChild);
   console.log(oDiv.lastElementChild);
   ```

##### 获取兄弟元素, 获取兄弟节点

1. 获取指定节点的相邻上一个兄弟

   - .previousSibling 获取相邻上一个节点
   - .previousElementSibling 获取相邻上一个元素

   ```js
   let item = document.querySelector(".item");
   
   console.log(item.previousSibling);
   console.log(item.previousElementSibling);
   ```

2. 获取指定节点的相邻下一个兄弟

   - .nextSibling 获取相邻下一个节点
   - .nextElementSibling 获取相邻下一个元素

   ```js
   let item = document.querySelector(".item");
   
   console.log(item.nextSibling);
   console.log(item.nextElementSibling);
   ```

#### 增删改查

##### 元素节点增删改查

再提醒自己一波: DOM 里元素是节点的子集

1. 增
   - 创建: document.createElement("elementName");
   - 推入尾部: parentNode.appendChild(newChildNode);
   - 插入节点: parentNode.insertBefore(newChildNode, targetSiblingNode);
2. 删
   - 只能通过父节点删子节点: childNode.parentNode.removeChild(anotherChildNode);
3. 改是好大一块, 另外讲
4. 查就是 queryXX 啦

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-元素增删改查</title>
</head>
<body>
<div>
    <h1>我是标题</h1>
    <p>我是段落</p>
</div>
<script>
    // query 出来给增删改查用
    let oDiv = document.querySelector("div");
    let oH1 = document.querySelector("h1");
    let oP = document.querySelector("p");
    
    // 1.创建节点
    let oSpan = document.createElement("span");
    console.log(oSpan); // <span></span>
    console.log(typeof oSpan); // object

    // 2.添加节点	注意点: appendChild方法会将指定的元素添加到最后
    oDiv.appendChild(oSpan)
    let oA = document.createElement("a");
    oDiv.appendChild(oA);

    // 3.插入节点
    oDiv.insertBefore(oSpan, oH1);
    oDiv.insertBefore(oSpan, oP);

    // 5.删除节点	注意点: 在 js 中如果想要删除某一个元素, 只能通过对应的父元素来删除, 元素是不能够自杀的       
    console.log(oSpan.parentNode);
    oSpan.parentNode.removeChild(oSpan);
    // oDiv.parentNode.removeChild(oDiv); wrong play

    // 5.克隆节点	注意点: cloneNode方法默认不会克隆子元素, 如果想克隆子元素需要传递一个true
    // let newDiv =  oDiv.cloneNode();
    let newDiv =  oDiv.cloneNode(true);
    console.log(newDiv);
</script>
</body>
</html>
```

##### 属性节点增删改查 (废弃节点)

关键点:
元素节点的默认属性可以通过 . 操作来实现
但自定义属性的增改删查要用到 .setAttribute, .removeAttribute, .getAttribute

```html
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-元素属性操作</title>
</head>
<body>
<img src="images/1.jpg" alt="我是alt222" title="我是title" fhs="666">
<script>
    /*
    无论是通过document创建还是查询出来的标签,系统都会将元素包装成一个对象返回给我们,
    系统在包装这个对象的时候会自动将元素的属性都包装到这个对象中,
    所以只要拿到这个对象就可以拿到标签属性,操作标签属性
    */
    
    // let oImg = document.querySelector("img");
    let oImg = document.createElement("img");
    console.dir(oImg);

    // 1.如何获取元素属性
    let oImg = document.querySelector("img");
    // console.log(oImg.alt);
    // console.log(oImg.getAttribute("alt"));
    /*
    注意点: 
    通过对象.属性名称的方式无法获取到自定义属性的取值
    通过getAttribute方法可以获取到自定义属性的取值
	*/
    console.log(oImg.nj); // undefined
    console.log(oImg.getAttribute("fhs"));

    // 2.如何修改元素属性
    let oImg = document.querySelector("img");
    // oImg.title = "新的title";
    // oImg.setAttribute("title", "新的title222");
    // 注意点和获取元素属性一样
    // oImg.fhs = "123";
    oImg.setAttribute("fhs", "123");

    // 3.如何新增元素属性
    /*
    let oImg = document.querySelector("img");
    // oImg.it666 = "it";
    // 注意点: setAttribute方法如果属性不存在就是新增, 如果属性存在就是修改
    oImg.setAttribute("it666", "itzb");
    */

    // 4.如何删除元素属性 通过父元素节点删除子属性节点
    let oImg = document.querySelector("img");
    // oImg.alt = "";
    // oImg.removeAttribute("alt");
    // 注意点和获取元素属性一样
    // oImg.nj = ""; // 不管用
    oImg.removeAttribute("fhs");
</script>
</body>
</html>
```

#### 玩转元素

##### 操作元素内容

1. 获取元素内容
   - .innerHTML
   - .innerText
   - .textContent
   - innerText 和 textContext 作用是一样的, 只不过不同浏览器支持的方法名有不同
2. 给上面的属性赋值就好了

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-元素内容操作</title>
</head>
<body>
<div>
    我是div
    <h1>我是标题</h1>
    <p>我是段落</p>
</div>
<script>
   // 1.获取元素内容
   /*
   1.innerHTML获取的内容包含标签, innerText/textContent获取的内容不包含标签
   2.innerHTML/textContent获取的内容不会去除两端的空格, innerText获取的内容会去除两端的空格
   */
   let oDiv = document.querySelector("div");
   console.log(oDiv.innerHTML);
   console.log(oDiv.innerText);
   console.log(oDiv.textContent);

   // 2.设置元素内容
   /*
   共性:
   无论通过 innerHTML/innerText/textContent 设置内容, 新的内容都会覆盖原有的内容
   区别:
   如果通过 innerHTML 设置数据, 数据中包含标签, 会转换成标签之后再添加
   如果通过 innerText/textContent 设置数据, 数据中包含标签, 不会转换成标签, 会当做一个字符串直接设置
   */
    let oDiv = document.querySelector("div");
   // oDiv.innerHTML = "123";
   // oDiv.innerText = "456";
   // oDiv.textContent = "789";
   //  oDiv.innerHTML = "<span>我是span</span>";
   //  oDiv.innerText = "<span>我是span</span>";
   //  oDiv.textContent = "<span>我是span</span>";

    setText(oDiv, "www.it666.com");
    function setText(obj, text) {
        if("textContent" in obj){
            obj.textContent = text;
        }else{
            obj.innerText = text;
        }
    }
</script>
</body>
</html>
```

##### <font color="red">操作元素样式</font>

通过 JavaScript 设置 CSS 样式**注意点**:

- JS 可以通过**给元素添加类名**或**修改 style 对象相应属性值**的方式来设置 CSS 样式
  JS 通过 style 属性**只能拿到行内样式的值**, ==拿不到== CSS 文件中设置的样式
  JS 通过 window.getComputedStyle(selector); 可以==拿到==对应选择器的 css **对象**, 从而**修改外链样式**	
- CSS 中通过短杠连接的属性名在 JS 中以驼峰形式出现
- 通过 js 添加的 css 属性是行内样式, 优先级高于 css 文件设置的样式
  - .className
  - .style
  - .getComputedStyle(Element)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript-操作元素样式</title>
    <style>
        .box{
            width: 200px;
            height: 200px;
            background-color: red;
        }
    </style>
</head>
<body>
<div class="box"></div>
<script>
    // 1.设置元素样式
    /*
    let oDiv = document.querySelector("div");
    // 第一种方式
    // 注意点: 由于class在JS中是一个关键字, 所以叫做className
    // oDiv.className = "box";
    // 第二种方式
    // 注意点: 过去CSS中通过-连接的样式, 在JS中都是驼峰命名
    // 注意点: 通过JS添加的样式都是行内样式, 会覆盖掉同名的CSS样式
    oDiv.style.width = "300px";
    oDiv.style.height = "300px";
    oDiv.style.backgroundColor = "blue";
    */

    // 2.获取元素样式
    let oDiv = document.querySelector("div");
    // oDiv.style.width = "300px";
    // 注意点: 通过style属性只能过去到行内样式的属性值, 获取不到CSS设置的属性值
    // console.log(oDiv.style.width);
    // 注意点: 如果想获取到CSS设置的属性值, 必须通过getComputedStyle方法来获取
    // getComputedStyle方法接收一个参数, 这个参数就是要获取的元素对象
    // getComputedStyle方法返回一个对象, 这个对象中就保存了CSS设置的样式和属性值
    let style = window.getComputedStyle(oDiv);
    console.log(style.width);
</script>
</body>
</html>
```

##### 点击事件

1. 什么是事件?
   - **用户和浏览器之间的交互行为我们就称之为事件**, 比如：点击，移入/移出
2. 如何给元素绑定事件?
   - 在 JavaScript 中所有的HTML标签都可以添加事件
   - 元素.事件名称 = function(){};
   - 当对应事件被触发时候就会自动执行function中的代码
3. **注意点**:
   - 如果给元素添加了和系统同名的事件 (比如 a 标签的跳转), 我们添加的事件不会覆盖系统添加的事件
   - 通过 元素.事件名称 = function(){}; 的函数体里 return false; 可以禁用系统默认事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>08-JavaScript-DOM事件</title>
</head>
<body>
    <button>我是按钮</button>
    <a href="http://www.it666.com">我是a标签</a>
<script>
    let oBtn = document.querySelector("button");
    oBtn.onclick = function () {
        alert("按钮被点击了");
    }
    // 注意点: 如果给元素添加了和系统同名的事件, 我们添加的事件不会覆盖系统添加的事件
    let oA = document.querySelector("a");
    oA.onclick = function () {
        alert("a标签被点击了");
        // 以下代码的含义: 用我们添加的事件覆盖掉系统同名的事件
        return false;
    }
</script>
</body>
</html>
```

### 定时器

在JavaScript中有两种定时器, 一种是重复执行的定时器, 一种是只执行一次的定时器

1. 重复执行的定时器
   setInterval(function () {
   	// some code
   }, /* duration */);

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>09-JavaScript-定时器</title>
   </head>
   <body>
       <button id="start">开始</button>
       <button id="close">结束</button>
   <script>
       // setInterval(function () {
       //     console.log("随便写点");
       // }, 1000);
       let startBtn = document.querySelector("#start");
       let id = null;
       startBtn.onclick = function () {
           id = setInterval(function () {
               console.log("随便写点");
           }, 1000);
       }
       let closeBtn = document.querySelector("#close");
       closeBtn.onclick = function () {
           clearInterval(id);
       }
   </script>
   </body>
   </html>
   ```

2. 只执行一次的定时器
   window.setTimeout(function () {
   	// some code

   }, /* duration */);

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>09-JavaScript-定时器</title>
   </head>
   <body>
   <button id="start">开始</button>
   <button id="close">结束</button>
   <script>
       // window.setTimeout(function () {
       //     console.log("随便写点");
       // }, 5000);
       let startBtn = document.querySelector("#start");
       let closeBtn = document.querySelector("#close");
       let id = null;
       startBtn.onclick = function () {
           id = window.setTimeout(function () {
               console.log("随便写点");
           }, 5000);
       }
       closeBtn.onclick = function () {
           clearTimeout(id);
       }
   </script>
   </body>
   </html>
   ```

3. **注意点**:
   
   - 只要手速快, 可以做到在计时器第一次生效前就移除掉 
   - 对象里的计时器用箭头函数形式比较省事儿
   - 即使通过技巧使得计时器的 this 指向对象,
     计时器也不同于其他方法, 不随对象的销毁而销毁,
     需手动销毁, 否则可能因为 null 调方法而导致报错
   
4. 淦! 计时器的 this 和一般的函数也不一样
   <font color="red">不管是类还是构造函数, <br>只要是匿名函数形式的计时器, 其 this 就指向 window, <br>只要是箭头函数的计时器, 其 this 就指向这个类(或函数)</font>

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>令人震惊的 this</title>
   </head>
   <body>
   <script>   
   
       class Person{
           constructor(name){
               this.name = name;
               this.say = function(){
                   console.log(this);
                   console.log(`say--${this}`);
                   console.log("------------------------------------");
               }
           }
           hi(){
               console.log("+-+-+-+-+-+-");
               console.log(this);
               console.log(`hi--${this}`);
               console.log("======================================");
           }
           timer1 = setTimeout(()=>{
               console.log("+++++++++++++++++++++++++++++++++++++");
               console.log(this);
               console.log(`timer1--${this}`);
               console.log("<======================================>");
           }, 5000);
   
           timer2 = setTimeout(function(){
               console.log(this);
               console.log(`timer2--${this}`);
               console.log(">======================================<");
           }, 10000);
       }
   
       let a = new Person("fhs");
       console.log(a.say());
       console.log(a.hi());
   </script>
   </body>
   </html> 
   
   <!--
   Person
   say--[object Object]
   ------------------------------------
   undefined
   +-+-+-+-+-+-
   Person
   say--[object Object]
   ======================================
   undefined
   +++++++++++++++++++++++++++++++++++++
   Person
   timer1--[object Object]
   <======================================>
   Window
   timer2--[object Window]
   >======================================<
   -->
   
   <!--
   打了这么多条分界线, 我发现 undefined 全部是方法打出来的
   不管加不加严格模式, 是类还是构造函数, 
   方法的 this 都既有 Person 又有 undefined,
   而且是在输出完我打印的内容后 undefined 才出来.
   找到原因了! 方法没有返回值所以执行完方法后返回 undefined
   -->
   ```

### 事件

**<font color="red">注意点</font>**: 事件方法都是没有驼峰的

#### 移入， 移出， 移动

- .onmouseover .onmouseenter
- .onmouseout .onmouseleave
- .onmousemove
- 淦!居然没驼峰

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>13-JavaScript-移入移出事件</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        div{
            width: 300px;
            height: 300px;
            background: red;
        }
    </style>
</head>
<body>
<div></div>
<script>
    let oDiv = document.querySelector("div");
    // 1.移入事件
    // oDiv.onmouseover = function () {
    //     console.log("移入事件");
    // }
    // 注意点: 对于初学者来说, 为了避免未知的一些BUG, 建议使用onmouseenter
    oDiv.onmouseenter = function () {
        console.log("移入事件");
    }

    // 2.移出事件
    // oDiv.onmouseout = function () {
    //     console.log("移出事件");
    // }
    // 注意点: 对于初学者来说, 为了避免未知的一些BUG, 建议使用onmouseleave
    oDiv.onmouseleave = function () {
        console.log("移出事件");
    }
    3.移动事件
    oDiv.onmousemove = function () {
        console.log("移动事件");
    }
</script>
</body>
</html>
```

#### 表单焦点事件

- .onfocus
- .onblur
- .onchange (只在失焦后才能拿到修改后的数据)
- .oninput (实时获取到修改后的数据)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>17-JavaScript-焦点事件</title>
</head>
<body>
<input type="text">
<script>
    let oInput = document.querySelector("input");
    // 1.监听input获取焦点
    oInput.onfocus = function () {
        console.log("获取到了焦点");
    }
    // 2.监听input失去焦点
    oInput.onblur = function () {
        console.log("失去了焦点");
    }
    // 3.监听input内容改变
    // 注意点: onchange事件只有表单失去焦点的时候, 才能拿到修改之后的数据
    oInput.onchange = function () {
        console.log(this.value);
    }
    // oninput事件可以时时获取到用户修改之后的数据, 只要用户修改了数据就会调用(执行)
    // 注意点: oninput事件只有在IE9以上的浏览器才能使用
    // 在IE9以下, 如果想时时的获取到用户修改之后的数据, 可以通过onpropertychange事件来实现
    oInput.oninput = function () {
        console.log(this.value);
    }
</script>
</body>
</html>
```

#### 添加事件的三种方式

1. element.onxxx
2. element.attachEvent (上古, 了解即可)
3. element.addEventListener (现代，可选事件冒泡 or 捕获)

##### 方法一：onxxx

注意点: 

1. 由于是给属性赋值, 所以**后赋值的会覆盖先赋值**
2. 缺点很明显： 不能通过一个事件触发多个方法， 不利于维持方法的细粒度

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>onclick</title>
</head>
<body>
<button id="btn">我是按钮</button>
<script>
    // 这点击事件只会输出 777， 原理就是给对象属性重赋值会对原有的值进行覆盖
    var oBtn = document.getElementById("btn");

    oBtn.onclick = function () {
        alert("666");
    }
    oBtn.onclick = function () {
        alert("777");
    }
</script>
</body>
</html>
```

##### 方法二：attachEvent

注意点:

1. 事件名称必须加上on
2. 后添加的不会覆盖先添加的
3. **只支持低版本的浏览器**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>attachEvent</title>
</head>
<body>
<button id="btn">我是按钮</button>
<script>
    // 既输出 666 也输出 777，但现代浏览器已经摒弃了这个方法
    var oBtn = document.getElementById("btn");

    oBtn.attachEvent("onclick", function () {
        alert("666");
    });
    oBtn.attachEvent("onclick", function () {
        alert("777");
    });
</script>
</body>
</html>
```

##### 方法三：addEventListen

注意点:

1. 事件名称**不需要添加 on**
2. 后添加的**不会**覆盖先添加的
3. 只支持现代浏览器（其实完全足够了）
4. 这是三个里唯一可自定义事件是冒泡行为还是捕获行为的方法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>addEventListener</title>
</head>
<body>
<button id="btn">我是按钮</button>
<script>
    // 既输出 666 也输出 777，现代浏览器通用这个方法
    var oBtn = document.getElementById("btn");

    oBtn.addEventListener("click", function () {
        alert("666");
    });
    oBtn.addEventListener("click", function () {
        alert("777");
    });

</script>
</body>
</html>
```

##### 强行兼容

看似考虑周全，实则没有必要

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>加个判断</title>
</head>
<body>
<button id="btn">我是按钮</button>
<script>
    var oBtn = document.getElementById("btn");

    function addEvent(ele, name, fn) {
        if(ele.attachEvent){
            ele.attachEvent("on"+name, fn);
        }else{
            ele.addEventListener(name, fn);
        }
    }
</script>
</body>
</html>
```

#### 事件对象

- 事件对象就是一个系统自动创建的一个对象
- 当注册的事件被触发的时候, 系统就会自动创建事件对象
- 事件对象的属性海了去了

**注意点**：

1. 在高级版本的浏览器中, 会自动将事件对象传递给回到函数
2. 在低级版本的浏览器中, 不会自动将事件对象传递给回调函数, 需要通过 window.event 来获取事件对象



**关于阻止默认行为**：

1. event.preventDefault(); 只支持现代浏览器
2. event.returnValue = false; 只支持上古浏览器（了解即可， 这年头谁还用 IE8 啊）
3. return false; 通吃

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件对象</title>
</head>
<body>
<button id="btn">我是按钮</button>
<a href="http://www.baidu.com">百度首页</a>
<script>
   var oBtn = document.getElementById("btn");
   oBtn.onclick = function (event) {
       // 兼容性的写法
       event = event || window.event;
       // alert("666");
       console.log(event);
       console.log(typeof event);
   }

   let oA = document.querySelector("a");
    oA.onclick = function (event) {
        // 兼容性的写法
        event = event || window.event;

        alert("666");
        // 阻止默认行为
        return false; // 企业开发推荐

        // event.preventDefault(); // 高级浏览器
        // event.returnValue = false; // IE9以下浏览器
    }
</script>
</body>
</html>
```

#### 时间执行的三个阶段

##### 三个阶段

1. **捕获**阶段(从外向内的传递事件)
2. **当前**目标阶段
3. **冒泡**的阶段(从内向外的传递事件)

**注意点**:

- 三个阶段**只有两个会被同时执行**
- 要么捕获和当前, 要么当前和冒泡

> 为什么要么只能是捕获和当前, 要么只能是当前和冒泡?
>
> 这是JS处理事件的历史问题
>
> 早期各大浏览器厂商为争夺定义权, 以及对事件的理解不同， 产生了捕获和冒泡两种流向
>
> 后续W3C为了兼容, 将两种方式都纳入标准

##### 冒泡还是捕获

如何设置事件到底是捕获还是冒泡?

通过addEventListener方法, 这个方法接收三个参数

- 第一个参数: 事件的名称
- 第二个参数: 回调函数
- 第三个参数: ==false 冒泡== / ==true 捕获==

**注意点**：

- onXxx的属性, 不接收任何参数, 所以默认就是冒泡
- attachEvent方法, 只能接收两个参数, 所以默认就是冒泡

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>41-JavaScript-事件执行的三个阶段</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .father{
            width: 300px;
            height: 300px;
            background: red;
        }
        .son{
            width: 150px;
            height: 150px;
            background: blue;
        }
    </style>
</head>
<body>
<div class="father">
    <div class="son"></div>
</div>
<script>
    let oFDiv = document.querySelector(".father");
    let oSDiv = document.querySelector(".son");
    oFDiv.addEventListener("click", function () {
        console.log("father");
    }, false);
    oSDiv.addEventListener("click", function () {
        console.log("son");
    }, false);
</script>
</body>
</html>

<!--
默认就是 false，也就是冒泡
设置为 true 的元素及其子元素链条都变为捕获，且仅影响自身及其子代，不影响其父元素
-->
```

##### 关于冒泡的细节

IE6.0: div -> body -> html -> document

其他浏览器: div -> body -> html -> document -> window

**注意**： 不是所有的事件都能冒泡，有些事件不冒泡，如 blur、 focus、 load、 unload 等

#### 阻止事件冒泡 (强行兼容)

首先要明确：阻止的前提是有事件，阻止事件冒泡的操作是写在实践方法的回调函数里的

1. event.cancelBubble = true; (上古)
2. event.stopProgagation(); (现代，知道这个才要紧)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>43-JavaScript-阻止事件冒泡</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .father{
            width: 300px;
            height: 300px;
            background: red;
        }
        .son{
            width: 150px;
            height: 150px;
            background: blue;
        }
    </style>
</head>
<body>
<div class="father" id="father">
    <div class="son" id="son"></div>
</div>
<script>
    // 1.拿到需要操作的元素
    var oFDiv = document.getElementById("father");
    var oSDiv = document.getElementById("son");
    
    // 2.注册事件监听
    oFDiv.onclick = function () {
        console.log("father");
    }
    oSDiv.onclick = function (event) {
        event = event || window.event;
        // event.stopPropagation(); // 高级浏览器
        // event.cancelBubble = true; // 低级浏览器
        if(event.cancelBubble){
            event.cancelBubble = true;
        }else{
            event.stopPropagation();
        }
        console.log("son");
    }
</script>
</body>
</html>
```

#### 不同移入移出事件辨析

区别在于是否触发冒泡（或捕获）

1. onmouseover 和 onmouseenter 的区别
   - onmouseover 移入到子元素,父元素的移入事件也会被触发
   - onmouseenter 移入到子元素,父元素的移入事件不会被触发
2. onmouseout 和 onmouseleave 的区别
   - onmouseout 移出到子元素,父元素的移入事件也会被触发
   - onmouseleave 移出到子元素,父元素的移入事件不会被触发
3. 简单来说， enter 和 leave 比较干净不拖泥带水

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>44-JavaScript-移入移出事件区别</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .father{
            width: 300px;
            height: 300px;
            background: red;
        }
        .son{
            width: 150px;
            height: 150px;
            background: blue;
        }
    </style>
</head>
<body>
<div class="father">
    <div class="son"></div>
</div>
<script>
    let oFDiv = document.querySelector(".father");
    let oSDiv = document.querySelector(".son");
    /*
    oFDiv.onmouseover = function () {
        console.log("father");
    }
    oSDiv.onmouseover = function () {
        console.log("son");
    }
     */
    /*
    oFDiv.onmouseenter = function () {
        console.log("father");
    }
    oSDiv.onmouseenter = function () {
        console.log("son");
    }
     */
    oFDiv.onmouseleave = function () {
        console.log("father");
    }
    oSDiv.onmouseleave = function () {
        console.log("son");
    }
</script>
</body>
</html>
```

#### 通过事件获取元素位置

- offsetX/offsetY: 事件触发点相对于当前元素**自身以左上为原点**的位置
- clientX/clientY: 事件触发相对于浏览器**可视区域**的位置（上古浏览器不支持）
- 注意点:
  - 显示器区域**不包括**滚动出去的部分（这个开发中用的少）
- <s>screenX/screenY</s>: 事件触发相对于屏幕的位置
- 整个网页**包括**滚动出去的部分
  pageX/pageY: 事件触发相对于整个网页的位置（在页面不滚动时拿到的值和 clientX/clientY 是一样的）

#### 细节们

- 调用事件方法时 return false 可以禁用默认事件， 或者用 event.preventDefault() 也行

- 如果想获取 query 到的 input 标签对象中输入的内容, **只能通过其 value 属性**

  html 可以给标签设置**自定义标签属性**, 可以给 JS 用, 

  甚至可以通过 JS 给指定 DOM 添加自定义属性标签

- 在 JS 中如果 HTML 标签的属性名称和取值名称一样的时候, JS 会返回 true/false
  但如果是通过代码给 input 设置的数据, 那么不会触发 oninput 事件

- 对上古浏览器的兼容只需了解即可

### 排他

#### 什么是排他

排他操作指**清除其它非选中元素的样式, 只设置当前选中元素样式**.

**点击事件**中有频繁的用到排他.

#### 拙劣的排他

for 一把梭清掉样式再给指定 dom 节点添加样式, 次次都遍历, 效率属实不行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>25-JavaScript-排它思想</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        ul{
            width: 400px;
            border: 1px solid #000;
            margin: 100px auto;
        }
        .current{
            background: red;
        }
    </style>
</head>
<body>
<ul>
    <li class="current">我是第1个li</li>
    <li>我是第2个li</li>
    <li>我是第3个li</li>
    <li>我是第4个li</li>
    <li>我是第5个li</li>
</ul>
<script>
    for(let i = 0; i < oItems.length; i++){
        let item = oItems[i];
        item.onclick = function () {
            
            for(let j = 0; j < oItems.length; j++){
                let li = oItems[j];
                li.className = "";
            }

            this.className = "current";
        }
    }
</script>
</body>
</html>
```

#### 正经的排他

通过每次存上次被渲染的元素的索引, 每次更新只需清空指定元素的样式, 精确打击省子弹

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>25-JavaScript-排它思想</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        ul{
            width: 400px;
            border: 1px solid #000;
            margin: 100px auto;
        }
        .current{
            background: red;
        }
    </style>
</head>
<body>
<ul>
    <li class="current">我是第1个li</li>
    <li>我是第2个li</li>
    <li>我是第3个li</li>
    <li>我是第4个li</li>
    <li>我是第5个li</li>
</ul>
<script>
    let oItems = document.querySelectorAll("li");
    let previousIndex = 0;

    for(let i = 0; i < oItems.length; i++){
        let item = oItems[i];
        item.onclick = function () {
            // 排它
            let preItem = oItems[previousIndex];
            preItem.className = "";

            this.className = "current";
            
            // 更新当前选中节点的索引
            previousIndex = i;
        }
    }
</script>
</body>
</html>
```

#### 通过 event.target 做排他

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>25-JavaScript-排它思想</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        ul{
            width: 400px;
            border: 1px solid #000;
            margin: 100px auto;
        }
        .current{
            background: red;
        }
    </style>
</head>
<body>
<ul>
    <li class="current">我是第1个li</li>
    <li>我是第2个li</li>
    <li>我是第3个li</li>
    <li>我是第4个li</li>
    <li>我是第5个li</li>
</ul>
<script>
    let oUl = document.querySelector("ul");
    let oLi = document.querySelector(".selected");
    oUl.onclick = function (event) {
        event = event || window.event;
        // console.log(event.target); // 好鬼酷啊！！！
        oLi.className = "";
        let item = event.target;
        item.className = "selected";
        oLi = item;
    }
</script>
</body>
</html>
```



#### ES6 以前的正经排他

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>25-JavaScript-排它思想</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        ul{
            width: 400px;
            border: 1px solid #000;
            margin: 100px auto;
        }
        .current{
            background: red;
        }
    </style>
</head>
<body>
<ul>
    <li class="current">我是第1个li</li>
    <li>我是第2个li</li>
    <li>我是第3个li</li>
    <li>我是第4个li</li>
    <li>我是第5个li</li>
</ul>
<script>
    let oItems = document.querySelectorAll("li");
    let previousIndex = 0;

    for(var i = 0; i < oItems.length; i++) {
        var item = oItems[i];
        
        // 通过带参的立即执行函数实现排他
        (function (index) {
            item.onclick = function () {
                // 排它
                var preItem = oItems[previousIndex];
                preItem.className = "";

                this.className = "current";
                previousIndex = index;
            }
        })(i);
    }
</script>
</body>
</html>
```

​		

### 块块的宽高及偏移位

复习一下 CSS_first 的 background 模块: 盒模型刨去 margin, border, padding 后剩的就是 **content**

#### 花式获取元素宽高

> - style
> - getComputedStyle (这个好)
> - offsetWidth, offsetHeight
> - <s>currentStyle</s>

1. style (行内样式)

   通过style属性获取宽高

   1. 获取的宽高**只是** content 的宽高, 即不包括 padding 和 border (当然更没有 margin)
   2. 只能获取通过**行内样式**设置的宽高
   3. 可以获取也**可以设置**

2. getComputedStyle (重要)

   1. 获取的宽高不包括 边框和内边距
   2. 即可以获取行内设置的宽高也可以获取 CSS 设置的宽高
   3. 只支持获取, **不支持设置**
   4. 上古浏览器用不了这个

3. offsetWidth, offsetHeight

   1. 获取的宽高包含 ==border+padding+content==
   2. 即可以获取行内设置的宽高也可以获取 CSS 设置的宽高
   3. 只支持获取, 不支持设置

4. <s>currentStyle</s> (上古, 废弃)

   1. 获取的宽高不包括 边框和内边距
   2. 即可以获取行内设置的宽高也可以获取 CSS 设置的宽高
   3. 只支持获取, 不支持设置
   4. 只支持 IE9 以下浏览器
   5. **所以 <s>currentStyle</s> 是 getComputed 的上古版本**

#### 拿元素宽高四种方式的辨析

##### 宽高是哪部分的宽高

1. getComputedStyle/currentStyle/style
   获取的宽高只是 content 的宽高, **不包括** 边框和内边距
2. offsetWidth/offsetHeight (独特)
   获取的宽高包括 边框和内边距

##### 样式是哪里的样式

1. getComputedStyle/currentStyle/offsetXXX
   即可以获取行内,也可以获取外链和内联样式, 只支持获取, 不支持设置
2. style
   只能获取行内样式, 可以获取, 也可以设置

#### 元素不同的偏移位们

> 偏移位三个族
>
> - offsetLeft, offsetTop
> - clientLeft, clientTop
> - scrollTop (也有 scrollLeft, 但是比较少用)

##### offsetLeft, offsetTop

简单来说, offset 族都是**相对于最近层级的定位元素**的

- offsetLeft, offsetTop
  - 获取元素到第一个定位**祖先元素**之间的偏移位
  - 如果没有祖先元素是定位的, 获取到相对于 body 的偏移位
- offsetParent
  - 获取元素的第一个定位祖先元素
  - 如果没有祖先元素是定位的, 那么就是获取到的就是 body

```html
<!-- offsetLeft, offsetTop -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-获取元素位置-offsetLeft, offsetTop</title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      .father {
        width: 200px;
        height: 200px;
        margin-top: 100px;
        margin-left: 100px;
        background: blue;
        overflow: hidden;
        position: relative;
      }
      .son {
        width: 100px;
        height: 100px;
        margin-top: 100px;
        margin-left: 100px;
        background: red;
      }
    </style>
  </head>
  <body>
    <div class="father">
      <div class="son"></div>
    </div>
    <script>
      /*
       获取元素到第一个定位祖先元素之间的偏移位
       如果没有祖先元素是定位的, 那么就是获取到body的偏移位
      */
      let oSDiv = document.querySelector(".son");
      oSDiv.onclick = function () {
        console.log(oSDiv.offsetLeft); // 100
        console.log(oSDiv.offsetTop); // 100
      };
    </script>
  </body>
</html>
```

```html
<!-- offsetParent -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-offsetParent</title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      .grand-father {
        width: 300px;
        height: 300px;
        margin-top: 100px;
        margin-left: 100px;
        background: deeppink;
        overflow: hidden;
        position: relative;
      }
      .father {
        width: 200px;
        height: 200px;
        margin-top: 100px;
        margin-left: 100px;
        background: blue;
        overflow: hidden;
        position: relative;
      }
      .son {
        width: 100px;
        height: 100px;
        margin-top: 100px;
        margin-left: 100px;
        background: red;
      }
    </style>
  </head>
  <body>
    <div class="grand-father">
      <div class="father">
        <div class="son"></div>
      </div>
    </div>
    <script>
      let oSDiv = document.querySelector(".son");
      oSDiv.onclick = function () {
        console.log(oSDiv.offsetParent); // <div class="father">…</div>
      };
    </script>
  </body>
</html>
```

##### clientLeft, clientTop

- clientWidth, clientHeight
  - clientWidth = content+padding
  - clientHeight = content+padding
- clientLeft, clientTop
  - 左边框和顶部边框

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-client族</title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      div {
        width: 150px;
        height: 150px;
        padding: 100px;
        border: 50px solid #000;
        background: red;
        background-clip: content-box;
      }
    </style>
  </head>
  <body>
    <div id="box"></div>
    <script>
      let oDiv = document.querySelector("div");
      console.log(oDiv.clientWidth); // 350
      console.log(oDiv.clientHeight); // 350
      console.log(oDiv.clientLeft); // 50
      console.log(oDiv.clientTop); // 50
    </script>
  </body>
</html>
```

##### scrollTop

scrollWidth, scrollTop

- 内容没有超出元素范围时
  - scrollWidth = content+padding == clientWidth
  - scrollHeight = content+padding == clientHeight
- 内容超出元素范围时
  - 内容相对于初始位置的位移, **一旦开始滚动就会有输出**
  - 小意外: 这里第二个页面滚动条出现后宽度缩水了! 从 200 缩水到了 183.

```html
<!-- 内容没有超出块块的时候 -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-scroll属性</title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      div {
        width: 100px;
        height: 100px;
        padding: 50px;
        border: 50px solid #000;
        background: red;
        background-clip: content-box;
        color: deepskyblue;
        overflow: auto;
      }
    </style>
  </head>
  <body>
    <div id="box">
      我是内容<br />
      我是内容<br />
    </div>
    <script>
      let oDiv = document.querySelector("div");
      console.log(oDiv.scrollWidth); // 200
      console.log(oDiv.scrollHeight); // 200
      oDiv.onscroll = function () { // 没有滚动条
        console.log(oDiv.scrollTop);
      };
    </script>
  </body>
</html>
```

```html
<!-- 内容超出块块的时候 -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-scroll属性</title>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      div {
        width: 100px;
        height: 100px;
        padding: 50px;
        border: 50px solid #000;
        background: red;
        background-clip: content-box;
        color: deepskyblue;
        overflow: auto;
      }
    </style>
  </head>
  <body>
    <div id="box">
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
      我是内容<br />
    </div>
    <script>
      let oDiv = document.querySelector("div");
      console.log(oDiv.scrollWidth); // 183
      console.log(oDiv.scrollHeight); // 425	
      oDiv.onscroll = function () { // 一旦开始滚动, 就开始输出
        console.log(oDiv.scrollTop);
      };
    </script>
  </body>
</html>
```

#### 可视区域的宽高

> - window.innerWidth, window.innerHeight (现代, 只在 IE9 及以上浏览器可用)
> - <s>document.documentElement.clientWidth, document.documentElement.clientHeight</s> (上古标准模式)
> - <s>document.body.clientWidth, document.body.clientHeight</s> (上古怪异模式):warning:

注意点:

- 浏览器在渲染网页的时候有两种模式"标准模式"/"混杂(怪异)模式"
- 默认情况下都是以标准模式来进行渲染的 (CSS1Compat)
- 如果网页没有书写文档声明, 那么就会按照"混杂(怪异)模式"来进行渲染 的(BackCompat)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JavaScript-获取网页宽高</title>
  </head>
  <body>
    <script>
      let { width, height } = getScreen();
      console.log(width);
      console.log(height);

      function getScreen() {
        var width, height;
        if (window.innerWidth) {
          width = window.innerWidth;
          height = window.innerHeight;
        } else if (document.compatMode === "BackCompat") {
          console.log(document.compatMode);// BackCompat
          width = document.body.clientWidth;
          height = document.body.clientHeight;
        } else {
          console.log(document.compatMode);// CSS1Compat
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

- 关于 document 对象和 window 对象

  ```html
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>document 和 window</title>
      <script>
          console.log(window);
          console.log(document);
      </script>
    </head>
    <body>
        总之 window 是个大而全的对象, document 就是比较纯粹的 html 文档
    </body>
  </html>
  ```
  
    ```html
  <!-- 文档声明加和不加行为是一样的, 应该是浏览器优化过了 -->
  <!DOCTYPE html>
  <html lang="en">
    <head>
          <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
          <title>document.documentElement 和 window</title>
          <script>
              console.log(document); // 比 document.documentElement 多了个文档声明 (如果有的话)
              console.log(document.documentElement); // 和 line13 打印的数字相同
              console.log(document.documentElement.clientWidth); // 和 line14 打印的数字相同
              console.log(document.documentElement.clientHeight);
              console.log(window.innerWidth);
              console.log(window.innerHeight);
              // console.log(document.body.clientWidth); 这俩在现代浏览器里会报错
              // console.log(document.body.clientHeight);
          </script>
      </head>
      <body></body>
  </html>
    ```
  
  