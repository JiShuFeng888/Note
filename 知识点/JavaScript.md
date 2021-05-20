### 	 1.闭包

```javascript
首先在函数内再嵌套函数，闭包就是里面能够读取外部函数的变量的函数

没有let出现之前，会污染全局变量，导致维护困难，所以通过立即执行函数和闭包避免全局变量的污染，也就是设计私有的方法和变量

另外参数和变量不会被垃圾回收，会造成内存消耗过大，解决方法就是在退出函数之前，将不使用的局部变量全部删除

var name = "外部name";
var init = (function(){
    var name = "内部name";
    function callName(){
        console.log(name);
        //打印name
    }
    return function(){
        callName();
        //形成接口
    }
}());
init();
```

### 2.作用域链

```javascript
作用域链的变量只能向上访问，变量访问到window对象即被终止，作用域链向下访问变量是不被允许的
```

### 3.原型链

```javascript
        function Person(myName, myAge) {
            // let obj = new Object();  // 系统自动添加的
            // let this = obj; // 系统自动添加的
            this.name = myName;
            this.age = myAge;
            // this.say = fns.mySay;
            // return this; // 系统自动添加的
        }
		//保存公共方法和属性  
		//Person.prototype是一个对象
        Person.prototype = {
			currentType="人",
            say: function () {
                console.log("hello world");
            }
        }
        let obj1 = new Person("lnj", 34);
        obj1.say();
        let obj2 = new Person("zs", 44);
        obj2.say();
        console.log(obj1.say === obj2.say); // true
    
```

```
        1.对象中__proto__组成的链条我们称之为原型链
		//注意！！！原型链
        2.对象在查找属性和方法的时候, 会先在当前对象查找
          如果当前对象中找不到想要的, 会依次去上一级原型对象中查找
         如果找到Object原型对象都没有找到,Object原型对象指向空null,就会报错
```

### 4.new 原理

```java
let New = function (P) {
        let o = {};
        let arg = 				Array.prototype.slice.call(arguments,1);
   // 还能写成 let arg = [...arguments].slice(1)
   arguments 是一个对应于传递给函数的参数的类数组对象，不能使用数组的方法。
        o.__proto__ = P.prototype;
       	// 绑定 this,执行构造函数
        let result=P.apply(o,arg);
         // 确保 new 出来的是个对象
        return typeof result === 'object' ? result : o
}  
> 这里有一个坑，如果我创建一个对象，更改它的原型，`constructor`就会变得不可靠了
```
```javascript
function Fn(){};

Fn.prototype=new Array();

var f=new Fn();

console.log(f.constructor===Fn);    // false
console.log(f.constructor===Array); // true 
只要只new出来实例的它自身都没有constructor属性
```

### 5.继承

```javascript
 function Person(myName, myAge) {
            // let per = new Object();
            // let this = per;
            // this = stu;
            this.name = myName; // stu.name = myName;
            this.age = myAge; // stu.age = myAge;
            // return this;
        }
        Person.prototype.say = function () {
            console.log(this.name, this.age);
        }
        function Student(myName, myAge, myScore) {
            Person.call(this, myName, myAge);
            this.score = myScore;
            this.study = function () {
                console.log("day day up");
            }
        }
        /*
        弊端:
        1.由于修改了Person原型对象的constructor属性, 所以破坏了Person的三角恋关系
        2.由于Person和Student的原型对象是同一个, 所以给Student的元素添加方法, Person也会新增方法
         */
        // Student.prototype = Person.prototype;
		//重点！！！！！！！！！！！！！！！！
        Student.prototype = new Person();
        Student.prototype.constructor = Student;
        Student.prototype.run = function(){
            console.log("run");
        }

        let per = new Person();
        per.run();

        /*
        1.1在子类的构造函数中通过call借助父类的构造函数
        1.2将子类的原型对象修改为父类的实例对象
        */
        // let stu = new Student("ww", 19, 99);
        // console.log(stu.score);
        // stu.say();
        // stu.study();
```

### 6.bind/call/apply

```javascript
        这三个方法都是用于修改函数或者方法中的this的
        2.1.bind方法作用
        修改函数或者方法中的this为指定的对象, 并且会返回一个修改之后的新函数给我们
        注意点: bind方法除了可以修改this以外, 还可以传递参数, 只不过参数必须写在this对象的后面
        2.2.call方法作用
        修改函数或者方法中的this为指定的对象, 并且会立即调用修改之后的函数
        注意点: call方法除了可以修改this以外, 还可以传递参数, 只不过参数必须写在this对象的后面
        2.3.apply方法作用
        修改函数或者方法中的this为指定的对象, 并且会立即调用修改之后的函数
        注意点: apply方法除了可以修改this以外, 还可以传递参数, 只不过参数必须通过数组的方式传递
```

```javascript
Function.prototype.myCall = function(context) {
  if (typeof this !== 'function') {
    throw new TypeError('Error')
  }
  context = context || window
  context.fn = this
  const args = [...arguments].slice(1)
  const result = context.fn(...args)
  delete context.fn
  return result
}

- 首先 `context` 为可选参数，如果不传的话默认上下文为 `window`
- 接下来给 `context` 创建一个 `fn` 属性，并将值设置为需要调用的函数
- 因为 `call` 可以传入多个参数作为调用函数的参数，所以需要将参数剥离出来
- 然后调用函数并将对象上的函数删除
```

```javascript
Function.prototype.myApply = function(context) {
  if (typeof this !== 'function') {
    throw new TypeError('Error')
  }
  context = context || window
  context.fn = this
  let result
  // 处理参数和 call 有区别
  if (arguments[1]) {
    result = context.fn(...arguments[1])
  } else {
    result = context.fn()
  }
  delete context.fn
  return result
}
```

```javascript
Function.prototype.myBind = function (context) {
  if (typeof this !== 'function') {
    throw new TypeError('Error')
  }
  const _this = this
  const args = [...arguments].slice(1)
  // 返回一个函数
  return function F() {
    // 因为返回了一个函数，我们可以 new F()，所以需要判断
    if (this instanceof F) {
		//还能继承person的原型
      return new _this(...args, ...arguments)
    }
    return _this.apply(context, 			args.concat(...arguments))
  }
}

- 前几步和之前的实现差不多，就不赘述了
- `bind` 返回了一个函数，对于函数来说有两种方式调用，一种是直接调用，一种是通过 `new` 的方式，我们先来说直接调用的方式
- 对于直接调用来说，这里选择了 `apply` 的方式实现，但是对于参数需要注意以下情况：因为 `bind` 可以实现类似这样的代码 `f.bind(obj, 1)(2)`，所以我们需要将两边的参数拼接起来，于是就有了这样的实现 `args.concat(...arguments)`
- 最后来说通过 `new` 的方式，在之前的章节中我们学习过如何判断 `this`，对于 `new` 的情况来说，不会被任何方式改变 `this`，所以对于这种情况我们需要忽略传入的 `this`
```

### 7.instanceof

```javascript
-   `instanceof`  可以准确地判断复杂引用数据类型，但是不能正确判断基础数据类型；
-   而  `typeof`  也存在弊端，它虽然可以判断基础数据类型（`null`  除外），但是引用数据类型中，除了  `function`  类型以外，其他的也无法判断
function myInstanceof(left, right) {
  let prototype = right.prototype
  left = left.__proto__
  while (true) {
    if (left === null || left === undefined)
      return false
    if (prototype === left)
      return true
    left = left.__proto__
  }
}
```

### 8.Ajax

```
/** 1. 创建连接 **/
var xhr = null;
xhr = new XMLHttpRequest()
/** 2. 连接服务器 **/
xhr.open('get', url, true)
/** 3. 发送请求 **/
xhr.send(null);
/** 4. 接受请求 **/
xhr.onreadystatechange = function(){
	if(xhr.readyState == 4){
		if(xhr.status == 200){
			success(xhr.responseText);
		} else { 
			/** false **/
			fail && fail(xhr.status);
		}
	}
}
```

### 9.零食知识点

```javascript
JS的基本数据类型和引用数据类型
基本数据类型：undefined、null、boolean、number、string、symbol
引用数据类型：object、array、function

js有哪些内置对象
Object 是 JavaScript 中所有对象的父对象
数据封装类对象：Object、Array、Boolean、Number 和 String
其他对象：Function、Arguments、Math、Date、RegExp、Error

栈：原始数据类型（Undefined，Null，Boolean，Number、String）
堆：引用数据类型（对象、数组和函数）
两种类型的区别是：存储位置不同；
原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储； 
引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其
在栈中的地址，取得地址后从堆中获得实体

forEach 无法遍历对象

vue.js 则是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调

JSON.stringify(obj)==JSON.stringify(obj2);//true
判断对象内容是否相等


### 判断是否是数组

-   `Array.isArray(arr`
-   `Object.prototype.toString.call(arr) === '[Object Array]'`
-   `arr instanceof Array`
-   `array.constructor === Array`



（1）for...in**

> `for...in`循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

**（2）Object.keys(obj)**

> `Object.keys`返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

date-xxx=""  自定义属性名
通过元素.dataset.xxx获取
```

### 10.正则表达式

```javascript
正则表达式构造函数var reg=new RegExp(“xxx”)与正则表达字面量var reg=//有什么不同？匹配邮箱的正则表达式？

当使用RegExp()构造函数的时候，不仅需要转义引号（即\”表示”），并且还需要双反斜杠（即\\表示一个\）。使用正则表达字面量的效率更高
邮箱的正则匹配：

var regMail = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((.[a-zA-Z0-9_-]{2,3}){1,2})$/;

匹配除了 [...] 中字符的所有字符，例如 [^aeiou] 匹配字符串 "google runoob taobao" 中除了 e o u a 字母的所有字母。

匹配所有。\s 是匹配所有空白符，包括换行，\S 非空白符，不包括换行。

匹配字母、数字、下划线。等价于 [A-Za-z0-9_]

```

### 11.数组去重

```javascript
方法一：利用ES6 Set去重（ES6中最常用）
function unique (arr) {
  return Array.from(new Set(arr))
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
 //[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]

[...new Set(arr)]
//代码就是这么少----（其实，严格来说并不算是一种，相对于第一种方法来说只是简化了代码）
```

```javascript
方法二：利用for嵌套for，然后splice去重（ES5中最常用）
function unique(arr){            
        for(var i=0; i<arr.length; i++){
            for(var j=i+1; j<arr.length; j++){
             
                if(arr[i]==arr[j]){         //第一个等同于第二个，splice方法删除第二个
                    arr.splice(j,1);
                    j--;
                }
            }
        }
	return arr;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
    //[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}]     //NaN和{}没有去重，两个null直接消失了
```

### 12.深浅拷贝

```javascript
浅拷贝：
	首先可以通过 Object.assign 来解决这个问题，很多人认为这个函数是用来深拷贝的。其实并不是，Object.assign 只会拷贝所有的属性值到新的对象中，如果属性值是对象的话，拷贝的是地址，所以并不是深拷贝

另外我们还可以通过展开运算符 ... 来实现浅拷贝
    let a = {
      age: 1
    }
    let b = { ...a }
    a.age = 2
    console.log(b.age) // 1
    
    
    
    
    
深拷贝：

    这个问题通常可以通过JSON.parse(JSON.stringify(object)) 来解决。

    let a = {
      age: 1,
      jobs: {
        first: 'FE'
      }
    }
    let b = JSON.parse(JSON.stringify(a))
    a.jobs.first = 'native'
    console.log(b.jobs.first) // FE
    但是该方法也是有局限性的：

    会忽略 undefined
    会忽略 symbol
    不能序列化函数(将json格式的对象转为json格式的字符串)
    不能解决循环引用的对象
    他无法实现对函数 、RegExp等特殊对象的克隆
    会抛弃对象的constructor,所有的构造函数会指向Object
    对象有循环引用,会报错
    let obj = {
      a: 1,
      b: {
        c: 2,
        d: 3,
      },
    }
    obj.c = obj.b
    obj.e = obj.a
    obj.b.c = obj.c
    obj.b.d = obj.b
    obj.b.e = obj.b.c
    let newObj = JSON.parse(JSON.stringify(obj))
    console.log(newObj)






        function depCopy(target, source) {
            // 1.通过遍历拿到source中所有的属性
            for(let key in source){
                // console.log(key);
                // 2.取出当前遍历到的属性对应的取值
                let sourceValue = source[key];
                // console.log(sourceValue);
                // 3.判断当前的取值是否是引用数据类型
                if(sourceValue instanceof Object){
                    // console.log(sourceValue.constructor);
                    // console.log(new sourceValue.constructor);
                    let subTarget = new sourceValue.constructor;
                    target[key] = subTarget;
                    depCopy(subTarget, sourceValue);
                }else{
                    target[key] = sourceValue;
                }
            }
        }

运用递归实现深拷贝，先遍历要拷贝对象的属性，判断该属性的值是否是引用数据类型，如果值是的话就new 这个属性的constructor 赋值给要拷贝的对象的属性，再用递归把属性的值赋值给它，不是的话就直接赋值
```

### 13.防抖节流

```javascript
防抖是将多次执行变为最后一次执行，节流是将多次执行变成每隔一段时间执行
function debounce(fn,delay){
	let timeId=null
	return function (){
		timeId&&clearTimeout(timeId)
		timeId=setTimeout(()=>{
			//没有指定谁调用默认就是window，所以要修改fn函数内正确的this指向，以及传入的参数（例如事件对象）
			fn.apply(this,arguments)
            //以下是两个错误例子
            //fn.apply(null,arguments)
			//fn(...arguments)
		},delay||200)
	}
}

function throttle(fn,delay){
	let flag=true
	return function (){
		if(!flag){
			return
		}
		flag=false
		setInterval(()=>{
			flag=true
			fn.apply(this,arguments)
            //fn(...arguments)
		},delay||500)
	}
}
```

### 14.Set/Map

```
Set本身是一个构造函数，用来生成 Set 数据结构。

const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
上面代码通过add()方法向 Set 结构加入成员，结果表明 Set 结构不会添加重复的值

```

### 15.slice/splice

```
**`slice`**

> “读取”数组指定的元素，不会对原数组进行修改

-   语法：`arr.slice(start, end)`
-   `start`  指定选取开始位置（含）
-   `end`  指定选取结束位置（不含）

**splice**

-   “操作”数组指定的元素，会修改原数组，返回被删除的元素
-   语法：`arr.splice(index, count, [insert Elements])`
-   `index`  是操作的起始位置
-   `count = 0`  插入元素，`count > 0`  删除元素
-   `[insert Elements]`  向数组新插入的元素
```

### 16.Symbol

```javascript
避免覆盖框架中同名的属性和方法，独一无二的值
let a=Symbol("name")
如果想使用变量作为对象属性的名称，必须加上[],[name]
a不能转成数值类型

Symbol不能for in 遍历
Object.getOwnPropertySymbols(obj)返回所有Symbol属性的数组
```

### 17.Iterator

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>46-Iterator基本概念</title>
</head>
<body>
<script>
    /*
    1.什么是Iterator?
    Iterator又叫做迭代器, 是一种接口
    这里的接口和现实中接口一样, 是一种标准一种规范
    例如: 电脑的USB接口有电脑USB接口的标准和规范, 正式因为有了标准和规范
          所以A厂商生成的USB线可以插到B厂商电脑的USB接口上

    它规定了不同数据类型统一访问的机制, 这里的访问机制主要指数据的遍历
    在ES6中Iterator接口主要供for...of消费

    2.默认情况下以下数据类型都实现的Iterator接口
    Array/Map/Set/String/TypedArray/函数的 arguments 对象/NodeList 对象
    */
    /*
    1.只要一个数据已经实现了Iterator接口, 那么这个数据就有一个叫做[Symbol.iterator]的属性
    2.[Symbol.iterator]的属性会返回一个函数
    3.[Symbol.iterator]返回的函数执行之后会返回一个对象
    4.[Symbol.iterator]函数返回的对象中又一个名称叫做next的方法
    5.next方法每次执行都会返回一个对象{value: 1, done: false}
    6.这个对象中存储了当前取出的数据和是否取完了的标记
    */
    /*
    // let arr = [1, 3, 5];
    // console.log(arr[Symbol.iterator]);
    // let it = arr[Symbol.iterator]();
    // console.log(it);
    // console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());

    // for(let value of arr){
    //     console.log(value);
    // }

    // let obj = {
    //     name: "lnj",
    //     age: 34,
    //     gender: "man"
    // }
    // console.log(obj[Symbol.iterator]);
    // for(let value of obj){
    //     console.log(value);
    // }
    */

    class MyArray{
        constructor(){
            for(let i = 0; i < arguments.length; i++){
                // this[0] = 1;
                // this[1] = 3;
                // this[2] = 5;
                this[i] = arguments[i];
            }
            this.length = arguments.length;
        }
        [Symbol.iterator](){
            let index = 0;
            let that = this;
            return {
                next(){
                    if(index < that.length){
                        return {value: that[index++], done: false}
                    }else{
                        return {value: that[index], done: true}
                    }
                }
            }
        }
    }
    let arr = new MyArray(1, 3, 5);
    // console.log(arr);
    // console.log(arr[0]);
    // arr[0] = 666;
    // console.log(arr);
    for(let value of arr){
        console.log(value);
    }
    // console.log(arr[Symbol.iterator]);
    // let it = arr[Symbol.iterator]();
    // console.log(it);
    // console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());
</script>
</body>
</html>
```

```
解构赋值和扩展运算符用到了iterator
```

### 18.Generator

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>48-Generator函数基本概念</title>
</head>
<body>
<script>
    /*
    1.什么是Generator函数?
    Generator 函数是 ES6 提供的一种异步编程解决方案
    Generator 函数内部可以封装多个状态, 因此又可以理解为是一个状态机

    2.如何定义Generator函数
    只需要在普通函数的function后面加上*即可

    3.Generator函数和普通函数区别
    3.1调用Generator函数后, 无论函数有没有返回值, 都会返回一个迭代器对象,
    3.2调用Generator函数后, 函数中封装的代码不会立即被执行

    4.真正让Generator具有价值的是yield关键字
    4.1在Generator函数内部使用yield关键字定义状态
    4.2并且yield关键字可以让 Generator内部的逻辑能够切割成多个部分。
    4.3通过调用迭代器对象的next方法执行一个部分代码,
       执行哪个部分就会返回哪个部分定义的状态

    5.在调用next方法的时候可以传递一个参数, 这个参数会传递给上一个yield
    */
    function* gen() {
        console.log("123");
        let res = yield "aaa";

        console.log(res);
        console.log("567");
        yield 1 + 1;

        console.log("789");
        yield true;
    }
    let it = gen();
    // console.log(it);
    console.log(it.next());
    console.log(it.next("it666"));
    // console.log(it.next());
    // console.log(it.next());

    // 注意点: yield关键字只能在Generator函数中使用, 不能在普通函数中使用
    // function say() {
    //     yield "abc";
    // }
    // say();
</script>
</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>49-Generator函数应用场景</title>
</head>
<body>
<script>
    /*
    应用场景, 让函数返回多个值
    * */
    /*
    function calculate(a, b) {
        let sum = a + b;
        let sub = a - b;
        return [sum, sub];
    }
    */
    function* calculate(a, b) {
        yield a + b;
        yield a - b;
    }
    let it = calculate(10, 5);
    console.log(it.next().value);
    console.log(it.next().value);
</script>
</body>
</html>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>50-Generator函数应用场景</title>
</head>
<body>
<script>
    /*
    1. 应用场景: 利用 Generator 函数，可以在任意对象上快速部署 Iterator 接口
    */
    /*
    Generator 函数特点
    1.Generator 函数也是一个函数
    2.Generator 函数会返回一个迭代器对象
    3.迭代器对象有next方法
    4.next方法每次执行都会返回一个对象{value: xxx, done: false}
    */
    /*
    function* gen() {
        yield "aaa";
        yield "bbb";
        yield "ccc";
    }
    let it = gen();
    // console.log(it);
    console.log(it.next());
    */

    /*
   1.必须有一个叫做[Symbol.iterator]的属性
   2.[Symbol.iterator]的属性会返回一个函数
   3.[Symbol.iterator]返回的函数执行之后会返回一个可迭代对象
   4.[Symbol.iterator]函数返回的对象中又一个名称叫做next的方法
   5.next方法每次执行都会返回一个对象{value: xxx, done: false}
   */
    /*
    let obj = {
        name: "lnj",
        age: 34,
        gender: "man",
        [Symbol.iterator](){
            let keys = Object.keys(this);
            // console.log(keys);
            let index = 0;
            let that = this;
            return {
                next(){
                    if(index < keys.length){
                        return {value: that[keys[index++]], done: false};
                    }else{
                        return {value: undefined, done: true};
                    }
                }
            }
        }
    }
    // console.log(obj[Symbol.iterator]);
    // let it = obj[Symbol.iterator]();
    // console.log(it);
    // console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());
    // console.log(it.next());
    for(let value of obj){
        console.log(value);
    }
    */

    let obj = {
        name: "lnj",
        age: 34,
        gender: "man"
    }
    function* gen(){
        let keys = Object.keys(obj);
        for(let i = 0; i < keys.length; i++){
            yield obj[keys[i]];
        }
    }
    obj[Symbol.iterator] = gen;
    // console.log(obj[Symbol.iterator]);
    let it = obj[Symbol.iterator]();
    // console.log(it);
    console.log(it.next());
    console.log(it.next());
    console.log(it.next());
    console.log(it.next());
</script>
</body>
</html>
```

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>51-Generator函数应用场景</title>
</head>
<body>
<script>
    /*
    应用场景: 用同步的流程来表示异步的操作
    */
    /*
    function request(fn) {
        setTimeout(function () {
            fn("拿到的数据");
        }, 1000);
    }
    request(function (data) {
        console.log("1", data);
        request(function (data) {
            console.log("2", data);
            request(function (data) {
                console.log("3", data);
            });
        });
    });
    */
    function request() {
        return new Promise(function (resolve, reject) {
            setTimeout(function () {
                resolve("拿到的数据");
            }, 1000);
        });
    }
    /*
    request().then(function (data) {
        console.log(data, 1);
        return request();
    }).then(function (data) {
        console.log(data, 2);
        return request();
    }).then(function (data) {
        console.log(data, 3);
    });
    */
    function* gen() {
        yield request();
        yield request();
        yield request();
    }
    let it = gen();
    // console.log(it.next().value);
    it.next().value.then(function (data) {
        console.log(data, 1);
        return it.next().value;
    }).then(function (data) {
        console.log(data, 2);
        return it.next().value;
    }).then(function (data) {
        console.log(data, 3);
    });
</script>
</body>
</html>
```

### 19.Promise

```javascript
    1.Promise特点
    1.1创建时必须传入一个函数, 否则会报错
    1.2会给传入的函数设置两个回调函数
    1.3刚创建的Promise对象状态是pending
    1.4状态一旦发生改变就不可再次改变
    1.5可以通过then来监听状态的改变
    1.5.1如果添加监听时状态已经改变, 立即执行监听的回调
    1.5.2如果添加监听时状态还未改变, 那么状态改变时候再执行监听回到
    1.5.3同一个Promise对象可以添加多个then监听, 状态改变时所有的监听按照添加顺序执行

    1.Promise特点
    1.1then方法每次执行完毕都会返回一个新的Promise对象
    1.2上一个Promise对象的then可以给下一个Promise的then传递数据
    1.2.1无论上一个是在成功的回调还是失败的回调传递的（return的参数）都会传递给下一个成功的回调
    1.2.2如果上一个return的是Promise对象, 那么传给下一个的成功还是失败由传递的Promise状态决定

    1.Promise特点
    1.1then方法返回的Promise对象的状态和前一个Promise的状态默认相同
    1.2后一个Promise对象的then可以捕获前一个Promise then的异常（不是一个对象）
    1.3catch方法就是then方法的语法糖 then(undefined, function(){});
```

```javascript
<script>
    // 定义常量保存对象的状态
    const PENDING = "pending";
    const FULFILLED = "fulfilled";
    const REJECTED = "rejected";

    class MyPromise{
        constructor(handle){
            // 0.初始化默认的状态
            this.status = PENDING;
            // 定义变量保存传入的参数
            this.value = undefined;
            this.reason = undefined;
            // 定义变量保存监听的函数
            // this.onResolvedCallback = null;
            // this.onRejectedCallback = null;
            this.onResolvedCallbacks = [];
            this.onRejectedCallbacks = [];
            // 1.判断是否传入了一个函数, 如果没有传入就抛出一个异常
            if(!this._isFunction(handle)){
                throw new Error("请传入一个函数");
            }
            // 2.给传入的函数传递形参(传递两个函数)
            handle(this._resolve.bind(this), this._reject.bind(this));

        }
        then(onResolved, onRejected){
            return new MyPromise((nextResolve, nextReject) => {
                // 1.判断有没有传入成功的回调
                if(this._isFunction(onResolved)){
                    // 2.判断当前的状态是否是成功状态
                    if(this.status === FULFILLED){
                        try {
                            // 拿到上一个promise成功回调执行的结果
                            let result = onResolved(this.value);
                            // console.log("result", result);
                            // 判断执行的结果是否是一个promise对象
                            if(result instanceof MyPromise){
                                result.then(nextResolve, nextReject);
                            }else{
                                // 将上一个promise成功回调执行的结果传递给下一个promise成功的回调
                                nextResolve(result);
                            }
                        }catch (e) {
                            nextReject(e);
                        }
                    }
                }
                // 1.判断有没有传入失败的回调
                // if(this._isFunction(onRejected)){
                try {
                    // 2.判断当前的状态是否是失败状态
                    if(this.status === REJECTED){
                        let result = onRejected(this.reason);
                        if(result instanceof MyPromise){
                            result.then(nextResolve, nextReject);
                        }else if(result !== undefined){
                            nextResolve(result);
                        }else{
                            nextReject();
                        }
                    }
                }catch (e) {
                    nextReject(e);
                }
                // }
                // 2.判断当前的状态是否是默认状态
                if(this.status === PENDING){
                    if(this._isFunction(onResolved)){
                        // this.onResolvedCallback = onResolved;
                        this.onResolvedCallbacks.push(() => {
                            try {
                                let result = onResolved(this.value);
                                if(result instanceof MyPromise){
                                    result.then(nextResolve, nextReject);
                                }else{
                                    nextResolve(result);
                                }
                            }catch (e) {
                                nextReject(e);
                            }
                        });
                    }
                    // if(this._isFunction(onRejected)){
                    // this.onRejectedCallback = onRejected;
                    this.onRejectedCallbacks.push(() => {
                        try {
                            let result = onRejected(this.reason);
                            if(result instanceof MyPromise){
                                result.then(nextResolve, nextReject);
                            }else if(result !== undefined){
                                nextResolve(result);
                            }else{
                                nextReject();
                            }
                        }catch (e) {
                            nextReject(e);
                        }
                    });
                    // }
                }
            });
        }
        catch(onRejected){
            return this.then(undefined, onRejected);
        }
        _resolve(value){
            // 这里是为了防止重复修改
            if(this.status === PENDING){
                this.status = FULFILLED;
                this.value = value;
                // this.onResolvedCallback(this.value);
                this.onResolvedCallbacks.forEach(fn => fn(this.value));
            }
        }
        _reject(reason){
            if(this.status === PENDING) {
                this.status = REJECTED;
                this.reason = reason;
                // this.onRejectedCallback(this.reason);
                this.onRejectedCallbacks.forEach(fn => fn(this.reason));
            }
        }
        _isFunction(fn){
            return typeof fn === "function";
        }
        static all(list){
            return new MyPromise(function (resolve, reject) {
                let arr = [];
                let count = 0;
                for(let i = 0; i < list.length; i++){
                    let p = list[i];
                    p.then(function (value) {
                        arr.push(value);
                        count++;
                        if(list.length === count){
                            resolve(arr);
                        }
                    }).catch(function (e) {
                        reject(e);
                    });
                }
            });
        }
        static race(list){
            return new MyPromise(function (resolve, reject) {
                for(let p of list){
                    p.then(function (value) {
                        resolve(value);
                    }).catch(function (e) {
                        reject(e);
                    });
                }
            })
        }
    }
</script>
```

### 20.Promise-all

```javascript
要么一起成功，要么一起失败
static all(list){
            return new MyPromise(function (resolve, reject) {
                let arr = [];
                let count = 0;
                for(let i = 0; i < list.length; i++){
                    let p = list[i];
                    p.then(function (value) {
                        arr.push(value);
                        count++;
                        if(list.length === count){
                            resolve(arr);
                        }
                    }).catch(function (e) {
                        reject(e);
                    });
                }
            });
        }
```

### 21.Promise-race

```javascript
谁先返回听返回的
       static race(list){
            return new MyPromise(function (resolve, reject) {
                for(let p of list){
                    p.then(function (value) {
                        resolve(value);
                    }).catch(function (e) {
                        reject(e);
                    });
                }
            })
        }
```

### 22.class

```javascript
2.从ES6开始系统提供了一个名称叫做class的关键字, 这个关键字就是专门用于定义类的
        class Person{
            // 当我们通过new创建对象的时候, 系统会自动调用constructor
            // constructor我们称之为构造函数
			//ES6中定义实例属性必须写在constructor中!!!!!!
            constructor(myName, myAge){
                this.name = myName;
                this.age = myAge;
            }
            // 实例属性 错误写法
            // name = "lnj";
            // age = 34;

            // 实例方法 写在constructor外会被添加到原型中 不想的话就写在constructor里面!!!!!
            say(){
                console.log(this.name, this.age);
            }
            // 静态属性 错误写法
            //static num = 666;
            
            // 静态方法!!!!!
            static run() {
                console.log("run");
            }
        }
        // let p = new Person();
        let p = new Person("zs", 18);
		p.num=666; //静态属性
        p.say();
        console.log(Person.num);
        Person.run();



        class Person{
            constructor(myName, myAge){
                this.name = myName;
                this.age = myAge;
                this.hi = function () {
                    console.log("hi");
                }
            }
            run(){
                console.log("run");
            }
        }
        // Person.prototype.type = "人";
        // Person.prototype.say = function () {
        //     console.log(this.name, this.age);
        // };

        let p = new Person("lnj", 34);
        console.log(p);

        /*
        注意点:
		//注意！！！！！！！！！！！！！！！！！！！！！！！
        如果通过class定义类, 那么不能自定义这个类的原型对象
        如果想将属性和方法保存到原型中, 只能动态给原型对象添加属性和方法
        */
```

### 23.自动无缝轮播图

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>37-JavaScript-自动轮播</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box{
            width: 670px;
            height: 300px;
            border: 1px solid #000;
            margin: 100px auto;
            position: relative;
            overflow: hidden;
        }
        ul{
            list-style: none;
            display: flex;
        }
        p{
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 100%;
            display: flex;
            justify-content: space-between;
        }
        p>span{
            width: 30px;
            height: 60px;
            line-height: 60px;
            text-align: center;
            background: rgba(0,0,0,0.5);
            color: #fff;
            font-size: 40px;
        }
    </style>
    <script src="js/animation.js"></script>
</head>
<body>
<div class="box">
    <ul>
        <li><img src="images/ad1.jpg" alt=""></li>
        <li><img src="images/ad2.jpg" alt=""></li>
        <li><img src="images/ad3.jpg" alt=""></li>
        <li><img src="images/ad1.jpg" alt=""></li>
    </ul>
    <p>
        <span class="left">&lt;</span>
        <span class="right">&gt;</span>
    </p>
</div>
<script>
	window.onload = function(){
	// 1.拿到需要操作的元素
		let oBox = document.querySelector(".box");
		let oLeft = document.querySelector(".left");
		let oRight = document.querySelector(".right");
		let oUl = document.querySelector("ul");
		let oItems = document.querySelectorAll("ul>li");
		let imgWidth = parseFloat(getComputedStyle(oItems[0]).width);
		let currentIndex = 0;

		// 2.监听按钮的点击
		oRight.onclick = function () {
			currentIndex++;
			if(currentIndex > oItems.length - 1){
				currentIndex = 0;
				// 快速的跳转到第一张
				oUl.style.marginLeft = -currentIndex * imgWidth + "px";
				currentIndex++;
			}
			easeAnimation(oUl, -currentIndex * imgWidth);
		}
		oLeft.onclick = function () {
			currentIndex--;
			if(currentIndex < 0){
				currentIndex = oItems.length - 1;
				// 快速的跳转到最后一张
				oUl.style.marginLeft = -currentIndex * imgWidth + "px";
				currentIndex--;
			}
			easeAnimation(oUl, -currentIndex * imgWidth);
		}

		// 3.自动轮播
		let id = setInterval(function () {
			oRight.onclick();
		}, 2000);
		oBox.onmouseenter = function(){
			// 关闭定时器
			clearInterval(id);
		};
		oBox.onmouseleave = function(){
			// 重新开启定时器
			id = setInterval(function () {
				oRight.onclick();
			}, 2000);
		};
	}
</script>
</body>
</html>
```

```javascript
		let timerId = null;
		function linearAnimation(ele, target) {
			clearInterval(timerId);
			timerId = setInterval(function () {
				// 1.拿到元素当前的位置
				let begin = parseInt(ele.style.marginLeft) || 0;
				// 2.定义变量记录步长
				//         0  -  500 = -500    13
				//         500 -  200 = 300    -13
				let step = (begin - target) > 0 ? -13 : 13;
				// 3.计算新的位置
				begin += step;
				console.log(Math.abs(target - begin), Math.abs(step));
				if(Math.abs(target - begin) <= Math.abs(step)){
					clearInterval(timerId);
					begin = target;
				}

				// 4.重新设置元素的位置
				ele.style.marginLeft = begin + "px";
			}, 100);
		}
		function easeAnimation(ele, target) {
			clearInterval(timerId);
			timerId = setInterval(function () {
				// 1.拿到元素当前的位置
				let begin = parseInt(ele.style.marginLeft) || 0;
				// 2.定义变量记录步长
				// 公式: (结束位置 - 开始位置) * 缓动系数(0 ~1)
				let step = (target - begin) * 0.3;
				console.log(step);
				// 3.计算新的位置
				begin += step;
				if(Math.abs(Math.floor(step)) <= 1){
					clearInterval(timerId);
					begin = target;
				}
				// 4.重新设置元素的位置
				ele.style.marginLeft = begin + "px";
			}, 100);
		}
```

```javascript
    function linearAnimation(ele, obj, fn) {
        clearInterval(timerId);
        timerId = setInterval(function () {
            // flag变量用于标记是否所有的属性都执行完了动画
            let flag = true;
            for(let key in obj){
                let attr = key;
                let target = obj[key];

                // 1.拿到元素当前的位置
                // let begin = parseInt(ele.style.width) || 0;
                let style = getComputedStyle(ele);
                // let begin = parseInt(style.width) || 0;
                let begin = parseInt(style[attr]) || 0;
                // 2.定义变量记录步长
                let step = (begin - target) > 0 ? -13 : 13;
                // 3.计算新的位置
                begin += step;
                if(Math.abs(target - begin) > Math.abs(step)){
                    flag = false;
                }else{
                    begin = target;
                }
                // 4.重新设置元素的位置
                // ele.style.width = begin + "px";
                ele.style[attr] = begin + "px";
            }
            if(flag){
                clearInterval(timerId);
                // if(fn){
                //     fn();
                // }
                fn && fn();
            }
        }, 100);
    }
```

### 24.拖拽效果

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>62-JavaScript-大图展示</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box{
            width: 400px;
            height: 400px;
            border: 1px solid #000;
            margin-top: 100px;
            margin-left: 100px;
            position: relative;
        }
        .small-box>span{
            display: inline-block;
            width: 200px;
            height: 200px;
            background: rgba(0,0,0,0.5);
            position: absolute;
            left: 0;
            top: 0;
            display: none;
        }
        .big-box{
            width: 400px;
            height: 400px;
            border: 1px solid #000;
            overflow: hidden;
            position: absolute;
            left: 410px;
            top: 0;
            display: none;
        }
        .big-box>img{
            position: absolute;
            left: 0;
            top: 0;
        }
    </style>
</head>
<body>
<div class="box">
    <div class="small-box">
        <img src="images/small.jpg" alt="">
        <span></span>
    </div>
    <div class="big-box">
        <img src="images/big.jpg" alt="">
    </div>
</div>
<script>
    // 1.拿到需要操作的元素
    let oSmallDiv = document.querySelector(".small-box");
    let oBigDiv = document.querySelector(".big-box");
    let oMask = document.querySelector("span");
    let oBoxDiv = document.querySelector(".box");
    let oBigImg = document.querySelector(".big-box>img");
    // 2.监听小图的移入移出事件
    oSmallDiv.onmouseenter = function () {
        oMask.style.display = "block";
        oBigDiv.style.display = "block";
    }
    oSmallDiv.onmouseleave = function () {
        oMask.style.display = "none";
        oBigDiv.style.display = "none";
    }
    // 3.监听鼠标在小图中的移动事件
    oSmallDiv.onmousemove = function (event) {
        event = event || window.event;
        // 1.获取鼠标当前在小图中的位置
        let mouseX = event.pageX - oBoxDiv.offsetLeft;
        let mouseY = event.pageY - oBoxDiv.offsetTop;

        // 2.重新计算鼠标的位置
        let maskWidth = oMask.offsetWidth;
        let maskHeight = oMask.offsetHeight;
        mouseX = mouseX - maskWidth / 2;
        mouseY = mouseY - maskHeight / 2;

        // 3.安全校验
        mouseX = mouseX < 0 ? 0 : mouseX;
        mouseY = mouseY < 0 ? 0 : mouseY;

        let smallWidth = oSmallDiv.offsetWidth;
        let smallHeight = oSmallDiv.offsetHeight;
        let maxMouseX = smallWidth - maskWidth;
        let maxMouseY = smallHeight - maskHeight;

        mouseX = mouseX > maxMouseX ? maxMouseX : mouseX;
        mouseY = mouseY > maxMouseY ? maxMouseY : mouseY;

        // 4.将鼠标当前在小图中的位置设置给蒙版
        oMask.style.left = mouseX +"px";
        oMask.style.top = mouseY +"px";

        // 5.计算大图移动的距离
        // 蒙版移动的距离 / 蒙版最大能移动的距离 = 大图移动的距离 / 大图最大能移动的距离
        // 蒙版移动的距离 / 蒙版最大能移动的距离 * 大图最大能移动的距离 = 大图移动的距离
        let maxBigX = oBigDiv.offsetWidth - oBigImg.offsetWidth;
        let maxBigY = oBigDiv.offsetHeight - oBigImg.offsetHeight;

        let bigX = mouseX / maxMouseX * maxBigX;
        let bigY = mouseY / maxMouseY * maxBigY;

        // 6.设置大图移动的位置
        oBigImg.style.left = bigX + "px";
        oBigImg.style.top = bigY + "px";
    }
</script>
</body>
</html>
```

### 25.工具类

```javascript
    function getScreen() {
        let width, height;
        if(window.innerWidth){
            width = window.innerWidth;
            height = window.innerHeight;
        }else if(document.compatMode === "BackCompat"){
            width = document.body.clientWidth;
            height = document.body.clientHeight;
        }else{
            width = document.documentElement.clientWidth;
            height = document.documentElement.clientHeight;
        }
        return {
            width: width,
            height: height
        }
    }
    function getPageScroll() {
        let x, y;
        if(window.pageXOffset){
            x = window.pageXOffset;
            y = window.pageYOffset;
        }else if(document.compatMode === "BackCompat"){
            x = document.body.scrollLeft;
            y = document.body.scrollTop;
        }else{
            x = document.documentElement.scrollLeft;
            y = document.documentElement.scrollTop;
        }
        return {
            x: x,
            y: y
        }
    }
    function addEvent(ele, name, fn) {
        if(ele.attachEvent){
            ele.attachEvent("on"+name, fn);
        }else{
            ele.addEventListener(name, fn);
        }
    }
    function getStyleAttr(obj, name) {
        if(obj.currentStyle){
            return obj.currentStyle[name];
        }else{
            return getComputedStyle(obj)[name];
        }
    }
```

### 26.楼层效果

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>67-JavaScript-楼层效果</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        html,body{
            width: 100%;
            height: 100%;
        }
        ul{
            width: 100%;
            height: 100%;
        }
        ul>li{
            list-style: none;
            width: 100%;
            height: 100%;
            font-size: 100px;
            text-align: center;
        }
        ol{
            position: fixed;
            left: 10px;
            top: 50%;
            transform: translateY(-50%);
        }
        ol>li{
            list-style: none;
            width: 100px;
            line-height: 40px;
            text-align: center;
            border: 1px solid #000;
        }
        .selected{
            background: deepskyblue;
        }
    </style>
</head>
<body>
<ul>
    <li>我是第1层</li>
    <li>我是第2层</li>
    <li>我是第3层</li>
    <li>我是第4层</li>
    <li>我是第5层</li>
</ul>
<ol>
    <li class="selected">第1层</li>
    <li>第2层</li>
    <li>第3层</li>
    <li>第4层</li>
    <li>第5层</li>
</ol>
<script src="js/animation2.js"></script>
<script src="js/tools.js"></script>
<script>
    // 1.初始化楼层的颜色
    let oPages = document.querySelectorAll("ul>li");
    let colorArr = ['green', 'blue', 'purple', 'red', 'yellow'];
    for(let i = 0; i < oPages.length; i++){
        let page = oPages[i];
        page.style.background = colorArr[i];
    }
    // 2.实现点击谁就选中谁
    let oItems = document.querySelectorAll("ol>li");
    let currentItem = oItems[0];
    // 获取可视区域的高度
    let screenHeight = getScreen().height;

    let timerId = null;
    for(let i = 0; i < oItems.length; i++){
        let item = oItems[i];
        item.onclick = function () {
            currentItem.className = "";
            this.className = "selected";
            currentItem = this;
            // 实现滚动
            // window.scrollTo(0, i * screenHeight);
            // 注意点: 通过documentElement.scrollTop来实现网页滚动, 在设置值的时候不能添加单位
            // document.documentElement.scrollTop = i * screenHeight + "px";
            // document.documentElement.scrollTop = i * screenHeight;
            clearInterval(timerId);
            timerId = setInterval(function () {
                let begin = document.documentElement.scrollTop;
                let target = i * screenHeight;
                let step = (target - begin) * 0.2;
                begin += step;
                if(Math.abs(Math.floor(step)) <= 1){
                    clearInterval(timerId);
                    document.documentElement.scrollTop = i * screenHeight;
                    return;
                }
                document.documentElement.scrollTop = begin;
            }, 50);
        }
    }
</script>
</body>
</html>
```

### 27.滚动条

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>68-JavaScript-橱窗效果</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        .box{
            width: 800px;
            height: 190px;
            border: 1px solid #000;
            margin: 100px auto;
            overflow: hidden;
        }
        ul{
            list-style: none;
            display: flex;
            position: relative;
        }
        ul img{
            vertical-align: top;
        }
        .progress{
            width: 100%;
            height: 30px;
            background: #ccc;
            position: relative;
        }
        .progress>.line{
            width: 100px;
            height: 100%;
            background: deeppink;
            border-radius: 15px;
            position: absolute;
            left: 0;
            top: 0;
        }
    </style>
</head>
<body>
<div class="box">
    <ul>
        <li><img src="images/img1.jpg" alt=""></li>
        <li><img src="images/img2.jpg" alt=""></li>
        <li><img src="images/img3.jpg" alt=""></li>
        <li><img src="images/img4.jpg" alt=""></li>
        <li><img src="images/img5.jpg" alt=""></li>
        <li><img src="images/img6.jpg" alt=""></li>
        <li><img src="images/img7.jpg" alt=""></li>
        <li><img src="images/img8.jpg" alt=""></li>
        <li><img src="images/img9.jpg" alt=""></li>
        <li><img src="images/img10.jpg" alt=""></li>
    </ul>
    <div class="progress">
        <div class="line"></div>
    </div>
</div>
<script>
    // 1.拿到需要操作的元素
    let oUl = document.querySelector("ul");
    let oItems = document.querySelectorAll("ul>li");
    let oProgress = document.querySelector(".progress");
    let oBox = document.querySelector(".box");
    let oLine = document.querySelector(".line");
    // 2.计算UL的宽度
    let ulWidth = oItems[0].offsetWidth * oItems.length;
    // 3.设置UL的宽度
    oUl.style.width = ulWidth + "px";
    // 4.计算滚动条的宽度
    // 滚动条的宽度 / 滚动条滚动范围 = 容器的宽度 / 内容的范围
    // 滚动条的宽度  = 容器的宽度 / 内容的范围 * 滚动条滚动范围
    let progressWidth = oProgress.offsetWidth;
    let boxWidth = oBox.offsetWidth;
    let lineWidth = boxWidth / ulWidth * progressWidth;
    // 5.设置滚动条的宽度
    oLine.style.width = lineWidth + "px";
    // 计算滚动条最大能够滚动的范围
    let maxLineX = progressWidth - lineWidth;
    // 计算图片最大能够滚动的范围
    let maxImgX = boxWidth - ulWidth;
    // 6.监听鼠标按下的事件
    oLine.onmousedown = function (event) {
        event = event || window.event;
        // 0.拿到滚动条当前的位置
        let begin = parseFloat(oLine.style.left) || 0;
        // 1.拿到鼠标在滚动条中按下的位置
        let mouseX = event.pageX - oBox.offsetLeft;
        // 7.监听鼠标移动的事件
        oLine.onmousemove = function (event) {
            event = event || window.event;
            // 2.拿到鼠标在滚动条中移动之后的位置
            let moveMouseX = event.pageX - oBox.offsetLeft;
            // 3.计算偏移位
            let offsetX = moveMouseX - mouseX + begin;
            // 4.安全校验
            offsetX = offsetX < 0 ? 0 : offsetX;
            offsetX = offsetX > maxLineX ? maxLineX : offsetX;
            // 5.重新设置滚动条的位置
            oLine.style.left = offsetX + "px";
            // 6.计算图片的滚动距离
            // 滚动条滚动的距离 / 滚动条最大能够滚动的范围 = 图片滚动的距离 / 图片最大能够滚动的范围
            // 滚动条滚动的距离 / 滚动条最大能够滚动的范围 * 图片最大能够滚动的范围 = 图片滚动的距离
            let imgOffsetX = offsetX / maxLineX * maxImgX;
            // 7.重新设置图片的位置
            oUl.style.left = imgOffsetX + "px";
        }
    }
    document.onmouseup = function () {
        oLine.onmousemove = null;
    }
</script>
</body>
</html>
```
**Object.prototype.toString.call()**

> `toString()`  是  `Object`  的原型方法，调用该方法，可以统一返回格式为  `“[object Xxx]”`  的字符串，其中  `Xxx`  就是对象的类型。对于  `Object`  对象，直接调用  `toString()`  就能返回  `[object Object]`；而对于其他对象，则需要通过  `call`  来调用，才能返回正确的类型信息。我们来看一下代码。

```
Object.prototype.toString({})       // "[object Object]"
Object.prototype.toString.call({})  // 同上结果，加上call也ok
Object.prototype.toString.call(1)    // "[object Number]"
Object.prototype.toString.call('1')  // "[object String]"
Object.prototype.toString.call(true)  // "[object Boolean]"
Object.prototype.toString.call(function(){})  // "[object Function]"
Object.prototype.toString.call(null)   //"[object Null]"
Object.prototype.toString.call(undefined) //"[object Undefined]"
Object.prototype.toString.call(/123/g)    //"[object RegExp]"
Object.prototype.toString.call(new Date()) //"[object Date]"
Object.prototype.toString.call([])       //"[object Array]"
Object.prototype.toString.call(document)  //"[object HTMLDocument]"
Object.prototype.toString.call(window)   //"[object Window]"
```

### **typeof**

> typeof 对于原始类型来说，除了 null 都可以显示正确的类型

```
console.log(typeof 2);               // number
console.log(typeof true);            // boolean
console.log(typeof 'str');           // string
console.log(typeof []);              // object     []数组的数据类型在 typeof 中被解释为 object
console.log(typeof function(){});    // function
console.log(typeof {});              // object
console.log(typeof undefined);       // undefined
console.log(typeof null);            // object     null 的数据类型被 typeof 解释为 object
```

> `typeof`  对于对象来说，除了函数都会显示  `object`，所以说  `typeof`  并不能准确判断变量到底是什么类型,所以想判断一个对象的正确类型，这时候可以考虑使用  `instanceof`

### 28.offset、scroll、client的区别

**client**:

-   `oEvent.clientX`是指鼠标到可视区左边框的距离。
-   `oEvent.clientY`是指鼠标到可视区上边框的距离。
-   `clientWidth`是指可视区的宽度。
-   `clientHeight`是指可视区的高度。
-   `clientLeft`获取左边框的宽度。
-   `clientTop`获取上边框的宽度。

**offset**:

-   `offsetWidth`是指div的宽度（包括div的边框）
-   `offsetHeight`是指div的高度（包括div的边框）
-   `offsetLeft`是指div到整个页面左边框的距离（不包括div的边框）
-   `offsetTop`是指div到整个页面上边框的距离（不包括div的边框）

**scroll**:

-   `scrollTop`是指可视区顶部边框与整个页面上部边框的看不到的区域。
-   `scrollLeft`是指可视区左边边框与整个页面左边边框的看不到的区域。
-   `scrollWidth`是指左边看不到的区域加可视区加右边看不到的区域即整个页面的宽度（包括边框）
-   `scrollHeight`是指上边看不到的区域加可视区加右边看不到的区域即整个页面的高度（包括边框）

### 29.正则表达式

```javascript
    stringObject.replace(regexp/substr,replacement)
    参数	描述
    regexp/substr	
    必需。规定子字符串或要替换的模式的 RegExp 对象。

    请注意，如果该值是一个字符串，则将它作为要检索的直接量文本模式，而不是首先被转换为 RegExp 对象。

    replacement	必需。一个字符串值。规定了替换文本或生成替换文本的函数。
    
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>47-JavaScript-正则表达式</title>
</head>
<body>
<script>
    /*
    1.什么是正则表达式?
    正则表达式就是对字符串操作的一种逻辑公式

    2.正则表达式的作用?
    1.在字符串"查找"是否包含指定子串
    2.从字符串中"提取"指定子串
    3.对字符串中指定的内容进行"替换"
     */
    // 1.字符串查找
    /*
    let str = "123abc456";
    let index = str.indexOf("abc");
    let index = str.lastIndexOf("abc");
    let flag = str.includes("abc");
     */
    // 2.字符串提取
    /*
    let str = "123abc456";
    let startIndex = str.indexOf("a");
    console.log(str.substr(startIndex, "abc".length));
     */
    // 3.字符串替换
    /*
    let str = "123abc456";
    str.replace("abc", "it666");
     */

    // 1.利用正则表达式匹配(查找)
    /*
    let str = "123abc456";
    // 1.创建一个正则表达式对象
    // 2.指定匹配的规则
    // 注意点: 默认情况下在正则表达式中是区分大小写的
    let reg = new RegExp("A", "i");
    let res = reg.test(str);
    console.log(res);
     */
    /*
    let str = "abc2020-1-11def";
    // 通过构造函数创建正则表达式对象
    // let reg = new RegExp("\\d{4}-\\d{1,2}-\\d{1,2}");
    // 通过字面量来创建正则表达式对象
    let reg = /\d{4}-\d{1,2}-\d{1,2}/;
    let res = reg.test(str);
    console.log(res);
     */

    // 2.通过正则表达式提取符合规则的字符串
    /*
    let str = "abc2020-1-11def2019-11-11fdjsklf";
    // 注意点: 默认情况下在正则表达式中一旦匹配就会停止查找
    let reg = /\d{4}-\d{1,2}-\d{1,2}/g;
    let res = str.match(reg);
    console.log(res);
    console.log(res[0]);
    console.log(res[1]);
     */

    // 3.通过正则表达式替换符合规则的字符串
    let str = "abc2020-1-11def2019-11-11fdjsklf";
    let reg = /\d{4}-\d{1,2}-\d{1,2}/g;
    let newStr = str.replace(reg, "it666");
    console.log(str);
    console.log(newStr);
    
    
    
</script>
</body>
</html>
<!--
常用正则表达式合集:
验证数字：^[0-9]*$
验证n位的数字：^\d{n}$
验证至少n位数字：^\d{n,}$
验证m-n位的数字：^\d{m,n}$
验证零和非零开头的数字：^(0|[1-9][0-9]*)$
验证有两位小数的正实数：^[0-9]+(.[0-9]{2})?$
验证有1-3位小数的正实数：^[0-9]+(.[0-9]{1,3})?$
验证非零的正整数：^\+?[1-9][0-9]*$
验证非零的负整数：^\-[1-9][0-9]*$
验证非负整数（正整数 + 0）  ^\d+$
验证非正整数（负整数 + 0）  ^((-\d+)|(0+))$
验证长度为3的字符：^.{3}$
验证由26个英文字母组成的字符串：^[A-Za-z]+$
验证由26个大写英文字母组成的字符串：^[A-Z]+$
验证由26个小写英文字母组成的字符串：^[a-z]+$
验证由数字和26个英文字母组成的字符串：^[A-Za-z0-9]+$
验证由数字、26个英文字母或者下划线组成的字符串：^\w+$

验证用户密码:^[a-zA-Z]\w{5,17}$ 正确格式为：以字母开头，长度在6-18之间，只能包含字符、数字和下划线。
验证是否含有 ^%&',;=?$\" 等字符：[^%&',;=?$\x22]+
验证汉字：^[\u4e00-\u9fa5],{0,}$
验证Email地址：^\w+[-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$
验证InternetURL：^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$ ；^[a-zA-z]+://(w+(-w+)*)(.(w+(-w+)*))*(?S*)?$
验证电话号码：^(\d3,4|\d{3,4}-)?\d{7,8}$：--正确格式为：XXXX-XXXXXXX，XXXX-XXXXXXXX，XXX-XXXXXXX，XXX-XXXXXXXX，XXXXXXX，XXXXXXXX。
验证身份证号（15位或18位数字）：^\d{15}|\d{}18$
验证一年的12个月：^(0?[1-9]|1[0-2])$ 正确格式为：“01”-“09”和“1”“12”
验证一个月的31天：^((0?[1-9])|((1|2)[0-9])|30|31)$    正确格式为：01、09和1、31。
整数：^-?\d+$
非负浮点数（正浮点数 + 0）：^\d+(\.\d+)?$
正浮点数   ^(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*))$
非正浮点数（负浮点数 + 0） ^((-\d+(\.\d+)?)|(0+(\.0+)?))$
负浮点数  ^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$
浮点数  ^(-?\d+)(\.\d+)?$
-->
```

### 30.reduce

```javascript
var arr = [1, 2, 3, 4];
var sum = arr.reduce(function(prev, cur, index, arr) {
    console.log(prev, cur, index);
    return prev + cur;
})
console.log(arr, sum);


打印结果：
1 2 1
3 3 2
6 4 3
[1, 2, 3, 4] 10


reduce的简单用法
当然最简单的就是我们常用的数组求和，求乘积了。


var  arr = [1, 2, 3, 4];
var sum = arr.reduce((x,y)=>x+y)
var mul = arr.reduce((x,y)=>x*y)
console.log( sum ); //求和，10
console.log( mul ); //求乘积，24





reduce的高级用法
（1）计算数组中每个元素出现的次数

let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

let nameNum = names.reduce((pre,cur)=>{
  if(cur in pre){
    pre[cur]+	+
  }else{
    pre[cur] = 1 
  }
  return pre
},{})
console.log(nameNum); //{Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}
（2）数组去重

let arr = [1,2,3,4,4,1]
let newArr = arr.reduce((pre,cur)=>{
    if(!pre.includes(cur)){
      return pre.concat(cur)
    }else{
      return pre
    }
},[])
console.log(newArr);// [1, 2, 3, 4]
（3）将二维数组转化为一维

  let arr = [[0, 1], [2, 3], [4,[5,6,7]]]
    const newArr = function(arr){
    return arr.reduce((pre,cur)=>{
      return pre.concat(Array.isArray(cur)?newArr(cur):cur)
    },[])
    }
console.log(newArr); // [0, 1, 2, 3, 4, 5]
（3）将多维数组转化为一维


console.log(newArr(arr)); //[0, 1, 2, 3, 4, 5, 6, 7]
（4）对象里的属性求和


var result = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];

var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, 0);
console.log(sum) //60

```

