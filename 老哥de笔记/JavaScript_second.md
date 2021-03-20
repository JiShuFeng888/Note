# JavaScript_second

## 函数

### 简介

#### 什么是函数

1. 什么是函数?
   函数是专门用于封装代码的, 函数是一段可以随时被反复执行的代码块

2. 函数格式

   ```js
   function /*函数名称*/(/*形参列表*/){
         /*被封装的代码*/;
   }
   ```

3. 不使用函数的弊端

   1. 冗余代码太多
   2. 需求变更, 需要修改很多的代码

4. 使用函数的好处

   1. 冗余代码变少了
   2. 需求变更, 需要修改的代码变少了

#### 函数的定义步骤

1. 书写函数的固定格式
2. 给函数起一个有意义的名称
   1. 为了提升代码的阅读性
   2. 函数名称也是标识符的一种, 所以也需要遵守标识符的命名规则和规范
3. 确定函数的形参列表, 看看使用函数的时候是否需要传入一些辅助的数据
4. 将需要封装的代码拷贝到{}中
5. 确定函数的返回值
   可以通过return 数据; 的格式, 将函数中的计算结果返回给函数的调用者

#### 函数的注意点

1. 一个函数可以有形参也可以没有形参(零个或多个)
   定义函数时函数()中的变量我们就称之为形参

   ```js
   // 没有形参的函数
   function say() {
       console.log("hello world");
   }
   say(); // hello world
   ```

   ```js
   // 有形参的函数
   function say(name) {
       console.log("hello " + name);
   }
   say("fhs"); // hello fhs
   ```

2. 一个函数可以有返回值也可以没有返回值

   ```js
   // 没有返回值的函数
   function say() {
       console.log("hello  world");
   }
   say();
   ```

   ```js
   // 有返回值的函数
   function getSum(a, b) {
       return a + b;
   }
   let res = getSum(10 , 20);
   console.log(res); // 30
   ```

3. 函数没有通过 return 明确返回值, 默认返回 undefined

   ```js
   function say() {
       console.log("hello world");
       return;
   }
   let res = say();
   console.log(res); // undefined
   ```

4. return的作用和break相似, 所以return后面不能编写任何语句 (永远执行不到)
   break作用立即结束switch语句或者循环语句
   return作用立即结束当前所在函数

   ```js
   function say() {
       console.log("hello world");
       return;
       console.log("return后面的代码");
   }
   say(); // hello world
   ```

5. 调用函数时实参的个数和形参的个数可以不相同
   调用函数时传入的数据我们就称之为实参

6. JavaScript中的函数和数组一样, 都是引用数据类型 (对象类型)
   既然函数是一种数据类型, 所以也可以保存到一个变量中
   将来可以通过变量名称找到函数并执行函数

   ```js
   let say = function () {
       console.log("hello world");
   }
   say(); // hello world
   ```

### 函数与参数

#### 参数 arguments

1. 因为 console.log(); 也是通过 () 来调用的, 所以 **log 也是一个函数**

2. log 函数的特点
   可以接收 1 个**或多个**参数

3. 为什么 log 函数可以接收 1 个或多个参数
   内部的实现原理就用到了 <font color="red">arguments</font>

4. arguments 的**作用**
   保存所有传递给函数的<font color="red">**实参**</font>

5. 每个函数中都有一个叫做arguments的东西, **arguments其实是一个<font color="red">伪数组</font>**

   ```js
   function getSum() {
       let sum = 0;
       for (let i = 0; i < arguments.length; i++){
           let num = arguments[i];
           sum += num;
   	}
   	return sum;
   }
   let res = getSum(10, 20, 30, 40);
   console.log(res); // 100
   ```
   
   函数括号内每个参数都被放进了 arguments 对象(伪数组)里					
   
   ```js
   // 补充
   function test(a) {
   	console.log(arguments);
   }
   test(0, 1, 2, 3, 4, 5);
   // [Arguments] { '0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5 }
   ```
   
   

#### 扩展运算符

1. 扩展运算符在等号左边, 将剩余的数据**打包**到一个新的数组中
   注意点: **只能写在最后**
   let [a, ...b] = [1, 3, 5]; a = 1; b = [3, 5];

2. 扩展运算符在等号右边, 将数组中的数据**解开**

   ```js
   let arr1 = [1, 3, 5];
   let arr2 = [2, 4, 6];
   let arr = [...arr1, ...arr2];
   let arr = [1, 3, 5, 2, 4, 6];
   ```

3. 扩展运算符在函数的形参列表中的作用
   将传递给函数的多出来的所有实参打包到一个数组中
   注意点: 和在等号左边一样, 也**只能写在形参列表的最后**

   ```js
   function getSum (a, ...values) {
       console.log(a);
       console.log(values);
   }
   getSum(10, 20 , 30);
   // 10
   // 20, 30
   ```

#### 函数形参默认值

在 **ES6 之前**可以通过逻辑运算符来给形参指定默认值
格式:
条件A || 条件B

- 如果条件 A 成立, 那么就返回条件 A
- 如果条件 A 不成立, 无论条件 B 是否成立, 都会返回条件B

```js
 function getSum(a, b) {
     a = a || "211";
     b = b || "996";
     console.log(a, b);
 }
getSum(123, "abc"); // 123, "abc" (妈欸这里控制台又有引号, 纯字符串又没引号, 薛定谔的引号, 非常淦)
```



**从 ES6 开始**, 可以直接在形参后面通过 = 指定默认值 (和解构赋值的指定默认值呼应上了)
注意点:
ES6 开始的默认值还可以**从其它的函数中获取**

```js
function getSum(a = "211", b = getDefault()) {
    console.log(a, b);
}
getSum();
function getDefault() {
    return "996"
}
```

#### 函数作为返回值

- 将函数赋给其他变量

```js
let say = function () {
    console.log("hello world");
}
let fn = say;
fn();
```

- 将函数作为其他函数的参数

```js
let say = function () {
    console.log("hello world");
}
function test(fn) { // 相当于 let fn = say;
    fn();
}
test(say);
```

- 将函数作为其他函数的返回值

```js
function test() {
    // 注意点: 在其它编程语言中函数是不可以嵌套定义的, 但是在JavaScript中函数是可以嵌套定义的
    let say = function () {
        console.log("hello world");
    }
    return say;
}
let fn = test(); // 相当于 let fn = say;
fn();
```

**注意点**:
在其它编程语言中函数是不可以嵌套定义的, 但是在JavaScript中函数是可以嵌套定义的

### 花哨的函数

#### 匿名函数

1. 什么是匿名函数?
   匿名函数就是没有名称的函数
2. 匿名函数的注意点
   **匿名函数不能够只定义不使用**
3. 匿名函数的应用场景
   1. 作为其他函数的参数
   2. 作为其他函数的返回值
   3. 作为一个立即执行的函数

- 有名称的函数

```js
function say() {
    console.log("hello fhs");
}
let say = function() {
    console.log("hello fhs");
}
```

- 匿名函数

```js
function() {
    console.log("hello fhs");
}
```

- 匿名函数作为其他函数的参数

```js
function test(fn) { // let fn = say;
    fn();
}
test(function () {
    console.log("hello world");
});
```

- 匿名函数作为其他函数的返回值

```js
function test() {
    return function () {
        console.log("hello fhs");
    };
}
let fn = test(); // let fn = say;
fn();
```

- 匿名函数作为一个立即执行的函数
  注意点:
  **如果想让匿名函数立即执行, 那么必须使用()将函数的<font color="red">定义</font>包裹起来才可以**

```js
(function () {
    console.log("hello it666");
})();
```

#### 箭头函数

1. 什么是箭头函数?

   - 箭头函数是ES6中新增的一种定义函数的格式

   - 目的: 就是为了简化定义函数的代码, 给一套花里胡哨的关于 this 的用法

   - ```js
     let arr = new Array();
     let arr = [];
     ```

2. 在 ES6 之前如何定义函数

   ```js
   function 函数名称(形参列表){
       /*需要封装的代码*/;
   }
   let 函数名称 = function(形参列表){
       /*需要封装的代码*/;
   }
   ```

3. ES6 新增的函数定义方式

   ```js
   let 函数名称 = (形参列表) =>{
       /*需要封装的代码*/;
   }
   ```

4. 箭头函数的**注意点**:

   1. 在箭头函数中如果只有一个形参, 那么 () 可以省略

      ```js
      // function say() {
      //     console.log("hello lnj");
      // }
      let say = () => {
          console.log("hello lnj");
      }
      say();
      ```

   2. 在箭头函数中如果 {} 中只有一句代码, 那么{}也可以省略

      ```js
      // function say(name) {
      //     console.log("hello  " + name);
      // }
      // let say = (name) => {
      //     console.log("hello  " + name);
      // }
      // let say = name => {
      //     console.log("hello  " + name);
      // }
      let say = name => console.log("hello  " + name); // 花里胡哨
      say("ccc");
      ```
      
   3. 当箭头函数的函数体只有一个 `return` 语句时，可以省略 `return` 关键字和方法体的花括号

      ```js
      var elements = [
       'Hydrogen',
        'Helium',
       'Lithium',
        'Beryllium'
      ];
      elements.map(element => element.length); // [8, 6, 7, 9]
      ```
   
   4. 如果箭头函数的函数体只有一句代码，就是返回一个对象，可以像下面这样写：
   
      ```js
      // 用小括号包裹要返回的对象，不报错
      let getTempItem = id => ({ id: id, name: "Temp" });
      
      // 但绝不能这样写，会报错。
      // 因为对象的大括号会被解释为函数体的大括号
      let getTempItem = id => { id: id, name: "Temp" };
      ```
   
   5. **箭头函数和正统函数的 this 不同**
   
      - 箭头函数中的 this, **是父作用域的 this**, 而非调用者
      - 箭头函数的 this **无法变更**
   
      - 对象**不会**成为箭头函数的 this
   
      ```js
      let p = {
          name: "fhs",
          say: function () {
           console.log(this);
          },
       // 因为没有将箭头函数放到其它的函数中, 所以箭头函数属于全局作用域
          // 在 JS 中只有定义一个新的函数才会开启一个新的作用域 (害, 块呢???)
          hi: () => {
              console.log(this);
          }
      }
      p.say(); // {name: "fhs", say: ƒ}
      p.hi(); // Window 
      console.log(this); // Window
      ```
   
      - 函数**会**成为箭头函数的 this
   
      ```js
      function Person() {
          this.name = "fhs";
          this.say = function () {
           console.log(this);
          }
       // 因为将箭头函数放到其它的函数中, 所以箭头函数属于其它函数(当前的其它函数就是构造函数)
          // 既然箭头函数属于构造函数, 所以箭头函数中的 this 就是构造函数的 this
          this.hi = () =>{
              console.log(this);
          }
      }
      let p = new Person();
      p.say(); // Person
      p.hi(); // Person
      ```
   
      - 箭头函数的 this **无法变更**
   
      ```js
      function Person() {
          this.name = "fhs";
          this.say = function () {
              console.log(this);
          }
          this.hi = () =>{
           console.log(this);
          }
      }
      let p = new Person();
      p.say.call({name: "zs"}); // {name: "zs"}
      /*
      注意点:
      箭头函数中的 this 永远都只看它所属的作用域的 this
      无法通过 bind/call/apply 来修改
      */
      p.hi.call({name: "zs"}); // Person
      ```
   
      - 类又不同了, 暴躁
   
      ```js
      class Person{
          constructor(name){
              this.name = name;
          }   
       say = function () {
              console.log(this);
       }
      hi = () =>{
          console.log(this);
      } 
      }
      
      let a = new Person("fhs");
      console.log(a.say()); // undefined
      console.log(a.hi()); // undefined
      ```
   
      - 这儿么写 this 也还是 undefined
   
      ```js
      class Person{
          constructor(name){
              this.name = name;
              this.say = function(){
                  console.log(this);
              }
              this.hi = () =>{
                  console.log(this);
              } 
          }   
      }
      
      let a = new Person("fhs");
      console.log(a.say()); // undefined
      console.log(a.hi()); // undefined
      ```

这里有个挺重要的知识点: this 是 this, 作用域链是作用域链, 俩有关系但不是一回事儿

#### 递归函数

1. 什么是递归函数? recursion
   - 递归函数就是在函数中自己调用自己, 我们就称之为递归函数
   - **递归函数在一定程度上可以实现循环的功能**
2. 递归函数的**注意点**:
   - 每次调用递归函数都会开辟一块新的存储空间, 所以**性能不是很好**
   - <font color="gold">函数执行完毕后会回到函数调用的地方</font>

```js
// let pwd = -1;
// do{
//     pwd = prompt("请输入密码");
// }while (pwd !== "123456");
// alert("欢迎回来");

function login() {
    // 1.接收用户输入的密码
    let pwd = prompt("请输入密码");
    // 2.判断密码是否正确
    if(pwd !== "123456"){
        login();
    }
    // 3.输出欢迎回来
    alert("欢迎回来"); // 输错几次, 在输入正确密码后就会多弹相同次的 欢迎回来	
}
login();
```

### 作用域与作用域链

#### 背景介绍

在JavaScript中定义变量有两种方式

- ES6 之前: **var** 变量名称;
- ES6 新增: **let** 变量名称;

#### var 与 let 区别

- 是否能重复定义
  - 通过 var 定义变量,**可以**重复定义同名的变量,并且后定义的会**覆盖**先定义的
  - 如果通过 let 定义变量, **"相同作用域内"不可以**重复定义同名的变量
- 是否能先使用后定义
  - 通过 var 定义变量, **可以**先使用后定义(预解析)
  - 通过 let 定义变量, **不可以**先使用再定义(不会预解析)
- 是否能被 {} 限制作用域
  - 无论是 var 还是 let 定义在 {} 外面都是全局变量
  - 将 var 定义的变量放到一个单独的 {} 里面, 还是一个全局变量
  - 将 let 定义的变量放到一个单独的 {} 里面, 是一个**局部**变量

#### 全局, 局部(函数), 块级作用域

1. 在 JavaScript 中 **{} 外面**的作用域, 我们称之为全局作用域
2. 在 JavaScript 中**函数后面 {} 中**的的作用域, 我们称之为"局部作用域", 或“函数作用域”
3. 在 ES6 中只要 **{} 没有和函数结合**在一起, 就是"块级作用域"
   块级作用域只能约束 let
4. **块级作用域和局部作用域区别** (气死人的绕)
   1. 在块级作用域中通过 var 定义的变量是全局变量
   2. 在局部作用域中通过 var 定义的变量是局部变量
5. 无论是在块级作用域还是在局部作用域, 省略变量前面的 let 或者 var 就会变成一个全局变量 (严格模式不给省略)

- 块级作用域 (**选择结构和循环结构都不是函数**)

```js
 {
     // 块级作用域
 }

if(false){
    // 块级作用域
}

switch () {
        // 块级作用域
}

while (false){
    // 块级作用域
}

for(;;){
    // 块级作用域
}

do{
    // 块级作用域
}while (false);
```

- 函数作用域 (局部作用域)

```js
function say() {
    // 局部作用域
}
```

- var 的辨析

```js
{
     // 块级作用域
     var num = 123; // 全局变量
}
console.log(num); // 123

function test() {
    var value = 666; // 局部变量
}
test();
console.log(value); // 报错
```

- 块级作用域中的 var 与 let

```js
{
    // var num = 678; // 全局变量
    // let num = 678; // 局部变量
    num = 678; // 全局变量, 严格模式下这个会报错, 引起舒适
}
console.log(num);
```

- 局部(函数)作用域中的 var 与 let

```js
function test() {
    // var num = 123; // 局部变量
    // let num = 123; // 局部变量
    num = 123; // 全局变量, 严格模式下这个会报错, 引起舒适
}
test();
console.log(num);
```

**思考**:
let 相比 var 灵活度被大大削弱, 好用程度却大幅上升, 这就是规矩的好处

**注意点**:

1. 在不同作用域范围内**可以**出现同名变量 (可以但极不推荐)
2. **只要**出现 let, 相同作用域内**就**不能出现同名的变量, 即使另一个是 var 也不行

#### 作用域链

全局作用域也称 0 级作用域

**<font color="red">注意点</font>**: 初学者在研究"作用域链"的时候最好将 ES6 之前和 ES6 分开研究

##### ES6 之前的作用域链

1. 需要明确:
   1. ES6 之前定义变量通过 var
   2. ES6 之前没有块级作用域, 只有全局作用域和局部作用域
   3. ES6 之前**函数大括号**外的都是全局作用域
   4. ES6 之前函数大括号中的都是局部作用域
2. ES6之前作用域链
   1. 全局作用域我们又称之为 0 级作用域
   2. **定义函数开启的作用域**就是 1级/ 2级/ 3级/...作用域
   3. JavaScript会将这些作用域链接在一起形成一个链条, 这个链条就是作用域链
      0 ---> 1 ----> 2 ----> 3 ----> 4
   4. 除0级作用域以外, 当前作用域级别等于**上一级 +1**
3. 变量在作用域链查找规则
   1. 先在当前找, 找到就使用当前作用域找到的
   2. 如果当前作用域中没有找到, 就去上一级作用域中查找
   3. 以此类推直到0级为止, 如果 0 级作用域还没找到, 就报错

```js
// 全局作用域 / 0级作用域
var num = 123;
function demo() {
    // 1级作用域
	var num = 456;
    function test() {
        // 2级作用域
		var num = 789;
        console.log(num);
    }
    test();
}
demo(); // 789
```

##### ES6 往后的作用域链

1. 需要明确:
   1. ES6 定义变量通过 let
   2. ES6 除了全局作用域、局部作用域以外, 还**新增了块级作用域**
   3. ES6 虽然新增了块级作用域, 但是**在块级作用域中通过 let 定义变量与函数作用域并无差异** (都是局部变量)
2. ES6 作用域链
   1. 全局作用域我们又称之为 0 级作用域
   2. **定义函数或者代码块**都会开启的作用域就是 1级/ 2级/ 3级/...作用域 (<font color="red">这里就是 ES6 之后的关键不同</font>)
   3. JavaScript 会将这些作用域链接在一起形成一个链条, 这个链条就是作用域链
      0 ---> 1 ----> 2 ----> 3 ----> 4
   4. 除 0 级作用域以外, 当前作用域级别等于**上一级 +1**
3. 变量在作用域链查找规则
   1. 先在当前找, 找到就使用当前作用域找到的
   2. 如果当前作用域中没有找到, 就去上一级作用域中查找
   3. 以此类推直到0级为止, 如果0级作用域还没找到, 就报错

```js
// 全局作用域 / 0级作用域
let num = 123;
{
    // 1级作用域
	let num = 456;
    function test() {
        // 2级作用域
		// let num = 789;
        console.log(num);
    }
    test(); // 456
}
```

### 预解析, 方法

#### 预解析

1. 什么是预解析?
   - 浏览器在执行JS代码的时候会分成两部分操作：预解析以及逐行执行代码
   - 也就是说浏览器不会直接执行代码, 而是**加工处理之后再执行**,
   - 这个加工处理的过程, 我们就称之为预解析
2. 预解析规则
   1. 将变量声明和函数声明**提升**到当前作用域最前面
   2. 将剩余代码按照书写顺序依次放到后面
3. **注意点**:
   - 通过 let 定义的变量不会被提升(不会被预解析)

##### 变量的预解析

- var 声明的变量的预解析

```js
 // 预解析之前
console.log(num); //undefined
var num = 123;

// 预解析之后
var num;
console.log(num); //undefined
num = 123;
```

- 通过 let 定义的变量**不会被提升**(不会被预解析)

##### 函数的预解析

- 正统函数的预解析

```js
 // ES6之前定义函数的格式
say(); 
// ES6之前的这种定义函数的格式, 是会被预解析的, 所以可以提前调用
function say() {
    console.log("hello 996");
}

// 预解析之后的代码
function say() {
    console.log("hello 996");
}
say();

/*
在其它语言中, 函数的声明是:
function say()

在 Javascript 中, 函数的声明是
function say() {
    console.log("hello 996");
}
*/
```

- 将函数赋给 var 变量的方式不预解析 (let 更不会啦)

```js
console.log(say); // undefined
say(); // say is not a function
var say = function() {
    console.log("hello itzb");
}

// 预解析之后的代码
console.log(say); // undefined
var say;
say(); // say is not a function
say = function() {
    console.log("hello itzb");
}
```

- 箭头函数也不预解析 (都是报错, 这个和 var 报的还不一样, 魔鬼在细节中)

```js
say(); // say is not defined
let say = () => {
    console.log("hello itzb");
}
```

##### 狗题目

**注意点**: 浏览器执行的是预解析之后的代码

- 预解析规则很简单, 搞顺顺

```js
var num = 123;
fun(); // undefined
function fun() {
    console.log(num);
    var num = 666;
}

/*
预解析之后:
var num;
function fun() {
var num;
console.log(num);
num = 666;
}
num = 123;
fun(); // undefined
*/
```

```js
var a = 666;
test();
function test() {
    var b = 777;
    console.log(a); // 作用域链的就近原则
    console.log(b);
    console.log(c); // 虽然这里会报错, 但前面该输出的也会输出	
    var a = 888;
    let c = 999;
}
/*
预解析之后:
var a;
function test() {
var b;
var a;
b = 777;
console.log(a); // undefined
console.log(b); // 777
console.log(c); // 报错
a = 888;
let c = 999;
}
a = 666;
test();
*/
```

- 高级浏览器不会对 {} 中定义的函数进行提升

```js
 if(true){
     function demo() {
         console.log("1");
     }
 }else{
     function demo() {
         console.log("2");
     }
 }
demo(); // 1

/*
纯逻辑: 预解析, 函数提升, 后写覆盖先写, 于是输出 2

实际中:
高级浏览器不会对 {} 中定义的函数进行提升,
于是顺序执行, 输出 1
*/
```

- 如果同级作用域 var 变量名与函数名同名, 函数的**优先级**高于变量 (<font color="red">淦!</font> 居然没一以贯之用‘覆盖’的逻辑)
- 一定要记住, 在企业开发中千万不要让变量名称和函数名称重名

```js
console.log(value); // 输出函数的定义
var value = 123;
function value() {
    console.log("fn value");
}
console.log(value); // 123

/*
预解析之后
function value() {
    console.log("fn value");
}
console.log(value);
var value;
value = 123;
console.log(value);
*/
```

#### 方法

##### 创建默认对象

1. JavaScript 中提供了一个**默认的类 Object**, 我们可以通过这个类来创建对象
2. 由于我们是使用系统默认的类创建的对象, 所以系统不知道我们想要什么属性和行为,
   所以我们必须**手动的添加**我们想要的属性和行为
3. 如何给一个对象**添加属性**
   对象名称.属性名称 = 值;
4. 如何给一个对象**添加行为**
   对象名称.行为名称 = 函数;

创建对象的三种方式

1. new 一个, 往这个对象里加属性和方法

   ```js
   let obj = new Object();
   obj.name = "fhs";
   obj.age = 23;
   obj.say = function () {
       console.log("hello world");
   }
   console.log(obj.name);
   console.log(obj.age);
   obj.say();
   ```

2. 把个不完整的对象(甚至空对象也可)赋给变量

   ```js
   let obj = {}; // let obj = new Object(); 的简写
   obj.name = "fhs";
   obj.age = 23;
   obj.say = function () {
       console.log("hello world");
   }
   console.log(obj.name);
   console.log(obj.age);
   obj.say();
   ```

3. 直接把完整的对象赋给变量 (格式上有区别的哈, 这里是键值对的键和值以**冒号**隔开, 且键值对间以**逗号**隔开)

   ```js
   let obj = {
       name: "fhs",
       age: 23,
       say: function () {
           console.log("hello world");
       }
   };
   console.log(obj.name);
   console.log(obj.age);
   obj.say();
   ```

**注意点**: 

对象内方法**只应该**是函数赋给变量的形式, 以**正统函数形式存在于对象内的函数<font color="red">不是</font>对象的方法**

##### 函数与方法的区别

对象的行为称为方法而非函数

1. 什么是函数?
   函数就是没有和其它的类显示的绑定在一起的, 我们就称之为函数

2. 什么是方法?
   方法就是显示的和其它的类绑定在一起的, 我们就称之为方法

3. 函数和方法的区别

   1. 函数可以直接调用, 但是方法不能直接调用, 只能通过对象来调用
   2. 函数内部的 this 输出的是 window, 方法内部的this输出的是当前调用的那个对象

4. 无论是函数还是方法, 内部都有一个叫做 this 的东西

   this 是什么? 谁调用了当前的函数或者方法, 当前的 this 就是谁

### 工厂函数, 构造函数

我悟了, js 中构造函数的名字就是 js 的所谓类名

#### 工厂函数

什么是工厂函数?
工厂函数就是专门用于创建对象的函数, 我们就称之为工厂函数

**作用**:
降低代码冗余度

```javascript
/*
let obj = {
	name: "zs",
	age: 23,
    say: function () {
        console.log("hello world");
	}
};
let obj = {
	name: "xhx",
	age: 22,
    say: function () {
        console.log("hello world");
    }
};
*/
function createPerson(myName, myAge) {
    let obj = new Object();
    obj.name = myName;
    obj.age = myAge;
    obj.say = function () {
        console.log("hello world");
    }
    return obj;
}
let obj1 = createPerson("zs", 23);
let obj2 = createPerson("xhx", 22);
console.log(obj1);
console.log(obj2);
```

#### 构造函数

##### 朴素版构造函数

1. 什么是构造函数
   - 构造函数和工厂函数一样, 都专门用于创建对象
   - 构造函数本质上是工厂函数的简写 (还限制了创建方式, 更专业)
2. 构造函数和工厂函数的区别
   - 构造函数的函数名称**首字母必须大写**
   - **构造函数只能够通过 new 来调用**

```js
function Person(myName, myAge) {
    // let obj = new Object();  // 系统自动添加的
    // let this = obj; // 系统自动添加的
    this.name = myName;
    this.age = myAge;
    this.say = function () {
        console.log("hello world");
    }
    // return this; // 系统自动添加的
}
let obj1 = new Person("zs", 23);
let obj2 = new Person("xhx", 22);
console.log(obj1);
console.log(obj2);
```

当我们 new Person("zs", 23); 系统做了什么?
1. 会在构造函数中自动创建一个对象
2. 会自动将刚才创建的对象赋值给 this
3. 会在构造函数的最后自动添加 return this;
4. 注意到, 如果手动补齐构造函数中 js 自动为我们添加的部分, 那就成为了工厂函数

##### 优化构造函数

###### 为什么优化

- 朴素版构造函数两个对象中的 say 方法的实现都是一样的, 但是保存到了不同的存储空间中, 这样性能不好
- 要优化以提升性能

###### 第一版优化

当前这种方式存在的**弊端**

1. 阅读性降低了
2. 污染了全局的命名空间

```js
function mySay() {
    console.log("hello world");
}
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
    this.say = mySay;
}
let obj1 = new Person("zs", 23);
let obj2 = new Person("xhx", 22);
// 通过三等来判断两个函数名称, 表示判断两个函数是否都存储在同一块内存中
console.log(obj1.say === obj2.say); // true
```

###### 第二版优化

fns 是 function name space 的缩写, hhh 这个相比第一版并没有进步很多嘛

```js
// function mySay() {
//     console.log("hello world");
// }
let fns = {
    mySay: function () {
        console.log("hello world");
    }
}
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
    this.say = fns.mySay;
}
let obj1 = new Person("zs", 23);
let obj2 = new Person("xhx", 22);
console.log(obj1.say === obj2.say); // true
```

###### 三版优化 (原型入门)

prototype 是对象, 在这里 prototype 是构造函数这个对象的对象

用原型做到了真正不污染, 但可读性方面存在一定门槛

我在 chrome 尝试了一下, 构造函数本质和普通函数还真是一样的

```js
// let fns = {
//     mySay: function () {
//         console.log("hello world");
//     }
// }
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
}
Person.prototype = { // 用 Person.prototype.say = function (){} 也能行, 亲测能行
    say: function () {
        console.log("hello world");
    }
}
let obj1 = new Person("zs", 23);
let obj2 = new Person("xhx", 22);
console.log(obj1.say === obj2.say); // true
```

<font color="red">补充</font>:
第十行这种被称为自定义原型对象, 第十行注释部分称为给原型对象动态添加方法

### 原型与原型链

#### prototype

1. prototype **特点**
   1. 存储在 prototype 中的方法可以被对应构造函数创建出来的所有对象共享
   2. prototype 中除了可以存储方法以外, 还可以存储属性
   3. prototype 如果出现了和构造函数中同名的属性或者方法, 对象在访问的时候, **访问到的是构造函中的数据**
2. prototype **应用场景** (储存一类对象**共性**的部分)
   1. prototype 中一般情况下用于存储所有对象**都相同**的一些属性以及方法
   2. 如果是对象特有的属性或者方法, 我们会存储到构造函数中

```js
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
    this.currentType = "构造函数中的type";
    this.say = function () {
        console.log("构造函数中的say");
    }
}
Person.prototype = {
    currentType: "人",
    say: function () {
        console.log("hello world");
    }
}
```

#### \_\_proto\_\_ 与 prototype

1. **prototype**:
   每个"构造函数"中都有一个默认的属性 (打引号是因为:普通函数也有), 叫做 prototype
   prototype 属性保存着一个对象, 这个对象我们称之为"**原型对象**"

   正确但绕的说法: 
   prototype 是个默认的变量, 保存着对象, 该对象属性方法被同类对象共享

2. **constructor**:
   每个"原型对象"中都有一个默认的属性, 叫做 constructor
   constructor 指向当前原型对象对应的那个"构造函数"

3. **\_\_proto\_\_**:
   通过构造函数创建出来的对象我们称之为"**实例对象**"
   每个"实例对象"中都有一个默认的属性, 叫做 \_\_proto\_\_
   \_\_proto\_\_ 指向创建它的那个构造函数的"原型对象"

   正确但绕的说法:
   构造函数的 prototype 中的内容是构造函数生成的对象的内容

小发现: 隐式存在的东西容易让人懵逼, 我尤其懵逼

#### Function 与 Object

##### Function

1. JavaScript 中函数是引用类型(对象类型), 即对象,
   所以也是通过构造函数创建出来的,**所有函数都是**通过 Function 构造函数创建出来的对象
2. JavaScript 中只要是函数就有 prototype 属性
   Function 函数的 prototype 属性指向 Function 原型对象
   **Function 的特殊之处在于他的 \_\_proto\_\_ 也是指向 Function 原型对象**
3. JavaScript 中只要原型对象就有 constructor 属性
   Function 原型对象的 constructor 指向它对应的构造函数
4. Person 构造函数是 Function 构造函数的实例对象, 所以也有 \_\_proto\_\_ 属性
   Person 构造函数的 \_\_proto\_\_ 属性指向 Function 原型对象

##### Object

1. JavaScript 中函数是引用类型(对象类型), 所以 Function 函数也是对象
2. Function构造函数也是一个对象, 所以也有 \_\_proto\_\_ 属性
   Function构造函数的 \_\_proto\_\_属性指向"Function原型对象" (所有函数包括普通函数, Object 的\_\_proto\_\_也是)
3. JavaScript中还有一个系统提供的构造函数叫做 Object
   只要是函数都是"Function 构造函数"的实例对象
4. 只要是对象就有 \_\_proto\_\_ 属性, 所以"Object 构造函数"也有\_\_proto\_\_属性
   Object构造函数的 \_\_proto\_\_ 属性指向创建它那个构造函数(也就是 Function)的"原型对象"
5. 只要是构造函数都有一个默认的属性, 叫做 prototype (普通函数也有的)
   prototype属性保存着一个对象, 这个对象我们称之为"原型对象"
6. 只要是原型对象都有一个默认的属性, 叫做 constructor
   constructor 指向当前原型对象对应的那个"构造函数"

#### 原型链 - 构造函数终版优化

1. 对象中 \_\_proto\_\_ 组成的链条我们称之为原型链
2. 对象在查找属性和方法的时候, 会先在当前对象查找
   如果当前对象中找不到想要的, 会依次去**上一级原型对象**中查找
   如果找到 Object 原型对象都没有找到, 就会报错

**注意点**:
**为了不破坏原有的关系**, 在给 prototype 赋值的时候,
需要在自定义的对象中**手动的添加** constructor 属性, 
**手动的指定**需要指向谁

```js
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
}

Person.prototype = {
    constructor: Person,
    currentType: "人",
    say: function () {
        console.log("hello world");
    }
}
```

**补充**:
在给一个对象不存在的属性设置值的时候,
不会去原型对象中查找,
如果当前对象没有就会给当前对象新增一个不存在的属性

#### 小结

- 一般实例对象的 \_\_proto\_\_ 指向其构造函数的原型对象 
  (所以 Function 的特殊之处在于其自己构造了自己)
- **所有原型对象的 \_\_proto\_\_ 都指向 Object 的原型对象** 
  (Object.prototype.\_\_proto\_\_ 指向 null)
- constructor 指向其所属对象的所属对象
- 函数都有 prototype
- **prototype 的 constructor 要指回 prototype 的所属函数才完整**

### 面向对象

#### 封装, 继承, 多态

##### 属性和方法的分类

辨析:

1. 通过构造函数创建的对象, 我们称之为"实例对象"
2. 构造函数也是一个对象, 所以我们也可以给构造函数动态添加属性和方法



在 JavaScript 中属性和方法分类两类

1. 实例属性/实例方法
   - 在企业开发中通过实例对象访问的属性, 我们就称之为实例属性
   - 在企业开发中通过实例对象调用的方法, 我们就称之为实例方法
2. 静态属性/静态方法 (这倒是和 Java 有点像了)
   - 在企业开发中通过构造函数访问的属性, 我们就称之为静态属性
   - 在企业开发中通过构造函数调用的方法, 我们就称之为静态方法

##### 封装

1. 局部变量和局部函数
   - 无论是ES6之前还是ES6, 只要定义一个函数就会开启一个新的作用域
   - 只要在这个新的作用域中, 通过let/var定义的变量就是局部变量
   - 只要在这个新的作用域中, 定义的函数就是局部函数
2. 什么是对象的私有变量和函数
   - **默认**情况下对象中的属性和方法都是**公有**的, 只要拿到对象就能操作对象的属性和方法
   - 外界不能直接访问的变量和函数就是私有变量和是有函数
   - 构造函数的本质也是一个**函数**, 所以也会开启一个新的作用域, 所以**在构造函数中定义的变量和函数就是私有和函数**
     <font color="red">这里的怪异之处在于: this.xxx 居然不算是函数中定义的变量</font>
     哦哦哦,**私有属性的本质就是一个局部变量, 并不是真正的属性, 所以如果通过 对象.xxx的方式是找不到私有属性的, 所以会给当前对象新增一个不存在的属性**
3. 什么是封装? 
   - 封装性就是隐藏实现细节，仅对外公开接口
4. 为什么要封装?
   - 不封装的缺点：当一个类把自己的成员变量暴露给外部的时候,那么该类就失去对属性的管理权，别人可以任意的修改你的属性
   - 封装就是将数据隐藏起来,只能用此类的方法才可以读取或者设置数据,不可被外部任意修改. 封装是面向对象设计本质(将变化隔离)。这样降低了数据被误用的可能 (提高安全性和灵活性)

##### 继承 (本质只是复用, 伪继承!)

###### 方法一

- 修改子类构造函数原型对象的指向

```js
function Person() {
    this.name = null;
    this.age = 0;
    this.say = function () {
        console.log(this.name, this.age);
    }
}

function Student() {
    this.score = 0;
    this.study = function () {
        console.log("day day up");
    }
}
Student.prototype = new Person(); // 将 Person 的实例对象作为构造函数 Student 的原型对象
Student.prototype.constructor = Student; // 显式地将 Student 的原型对象的 constructor 指回 Student

let stu = new Student();
stu.name = "zs"; // 实例对象默认拥有原型对象的属性, 好鬼酷!
stu.age = 18;
stu.score = 99;
stu.say();
stu.study();
```

- 方法一的弊端:
  如果父类(妈的不先学 Java 知道个 p 的父类的概念)是个带参构造函数,
  子构造函数并不能用通过带参赋值给继承自父类的属性赋值

```js
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
    this.say = function () {
        console.log(this.name, this.age);
    }
}

// 学生 is a 人 , 学生是一个人
function Student(myName, myAge, myScore) { // 这样不报错但是不得行
    this.score = myScore;
    this.study = function () {
        console.log("day day up");
    }
}
```

###### 方法二

- 在子类构造函数中改变父类构造函数的 this 指向
  从而解决子类构造函数无法在创建时通过传参指定继承自父类的属性的属性值
  弊端:
  这样搞 Student 用不了 Person 的原型对象的属性和方法

  ```js
   function Person(myName, myAge) {
       // let per = new Object();   // 系统自动添加的
       // let this = per;  // 系统自动添加的
       // this = stu;  // 子类构造函数改了父类构造函数的 this
       this.name = myName; // stu.name = myName;
       this.age = myAge; // stu.age = myAge;
       this.say = function () { // stu.say = function () {}
           console.log(this.name, this.age);
       }
       // return this;  // 系统自动添加的
   }
  function Student(myName, myAge, myScore) { // 我他妈服
      // let stu = new Object();  // 系统自动添加的
      // let this = stu;  // 系统自动添加的
      Person.call(this, myName, myAge); //  Person.call(stu);
      this.score = myScore;
      this.study = function () {
          console.log("day day up");
      }
      // return this;  // 系统自动添加的
  }
  let stu = new Student("ww", 19, 99);
  // stu.name = "zs";
  // stu.age = 18;
  // stu.score = 99;
  console.log(stu.score);
  stu.say();
  stu.study();
  ```

- bind, call, apply (作用是<font color="red">复用!</font>)

1. this是什么?
   谁调用当前函数或者方法, this 就是谁
2. 这三个方法的作用是什么?
   这三个方法都是用于修改函数**或者方法**中的 this 的
   1. **bind 方法作用**
      let boundFunc = func.bind(thisArg[, arg1[, arg2[, ...argN]]])
      修改函数或者方法中的 this <font color="red">为指定的对象</font>, 并且会**返回一个修改之后的新函数**给我们
      注意点:
      bind 方法除了可以修改 this 以外, 还可以传递参数, 只不过参数必须写在 this 对象的后面
   2. **call 方法作用**
      func.call([thisArg[, arg1, arg2, ...argN]])
      修改函数或者方法中的 this 为指定的对象, 并且会**立即调用修改之后的函数**
      注意点:
      call 方法除了可以修改 this 以外, 还可以传递参数, 只不过参数必须写在 this 对象的后面
   3. **apply 方法作用**
      func.apply(thisArg, [ argsArray])
      修改函数或者方法中的 this 为指定的对象, 并且会**立即调用修改之后的函数**
      注意点:
      apply 方法除了可以修改 this 以外, 还可以传递参数, 只不过参数必须通过数组的方式传递

- 注意到:
  <font color="red">本质上 Student 和 Person 半毛钱关系都没有</font>,
  Student 只是借用了 Person 的属性和方法,
  这种约定俗成的继承和 Java 的规矩上的继承完全不是一回事儿

###### 方法三

- 在方法二的基础上通过更改 Student 原型对象的指向
  使得 Student 产的对象不仅能使用 Person 的属性和方法
  还能使用 Person 原型对象的属性和方法
  **弊端**:

  - 改变了 Person 的原型对象的 constructor 的指向, **破坏了 Person 的原型关系**
  - 用了这法子以后给 Student.prototype 添加属性方法的时候会**污染 Person 的原型对象**

  ```js
  function Person(myName, myAge) {
      this.name = myName;
      this.age = myAge;
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
  注意点:
  要想使用Person原型对象中的属性和方法,
  那么就必须将Student的原型对象改为Person的原型对象才可以
  */
  Student.prototype = Person.prototype; // 这个是败笔
  Student.prototype.constructor = Student;
  
  let stu = new Student("ww", 19, 99);
  console.log(stu.score);
  stu.say();
  stu.study();
  ```

###### 方法四 (只用这个就好)

**js 中继承的终极方法**

1. 在子类的构造函数中通过 call 借助父类的构造函数
2. 将子类的原型对象修改为父类的**实例对象**
   **优点**:
   使得 Student 产的对象不仅能使用 Person 的属性和方法
   还能使用 Person 原型对象的属性和方法
   最重要的是不会污染 Person 的原型

```js
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

Student.prototype = new Person(); // 小改动, 大不同
Student.prototype.constructor = Student;
Student.prototype.run = function(){
    console.log("run");
}

let per = new Person();
per.run();
```

##### 多态

###### 强类型语言与弱类型语言

1. 什么是强类型语言?
   一般编译型语言都是强类型语言,
   强类型语言，要求变量的使用要严格符合定义
   例如定义 int num; 那么 num 中将来就**只**能够存储整型数据
2. 什么是弱类型语言?
   一般解释型语言都是弱类型语言,
   弱类型语言, 不会要求变量的使用要严格符合定义
   例如定义 let num; num 中**既**可以存储整型, **也**可以存储布尔类型等
3. 由于js语言是弱类型的语言, 所以我们不用关注多态

###### 多态

多态是指事物的多种状态, js 天生是多态的	

例如:
按下 F1 键这个动作，
如果当前在 webstorm 界面下弹出的就是 webstorm 的帮助文档；
如果当前在 Word 下弹出的就是 Word 帮助；
同一个事件发生在不同的对象上会产生不同的结果 (不同类的对象调同名方法有不同的行为)。

多态在编程语言中的体现
父类型变量保存子类型对象, 父类型变量当前保存的对象不同, 产生的结果也不同

```js
function Dog() {
    this.eat = function () {
        console.log(" 狗吃东西");
    }
}

function Cat() {
    this.eat = function () {
        console.log(" 猫吃东西");
    }
}

function feed(animal){
    animal.eat();
}

let dog = new Dog();
feed(dog);

let cat = new Cat();
feed(cat);
```

##### 小结

私有属性本质不是属性, 继承本质只是借用, 多态是天生的, js 净整些花活儿

从法三到法四的进化来看, 发现做同一件事, 用到的权限和资源越少反而越好, 挺合理

#### ES6 的类

说真的, 不先学 Java 就来看这个能学明白的就应该去搞算法

##### class 关键字

- 在 ES6 之前通过构造函数来定义一个类

```js
function Person(myName, myAge) {
    // 实例属性
    this.name = myName;
    this.age = myAge;

    // 实例方法
    this.say = function () {
        console.log(this.name, this.age);
    }
    // 静态属性
    Person.num = 666;
    // 静态方法
    Person.run = function () {
        console.log("run");
    }
}

let p = new Person("zs", 18);
p.say();
console.log(Person.num);
Person.run();
```

- 从 ES6 开始系统提供了一个名称叫做class的关键字, 这个关键字就是专门用于定义类的
  class 不纯是构造函数套壳子, class 的 this 和 构造函数的 this 还有不同

```js
class Person{
    // 当我们通过 new 创建对象的时候, 系统会自动调用 constructor
    // constructor 我们称之为构造函数
    // ES6 标准规定通过 class 定义的实例属性都要在 constructor 中添加
    constructor(myName, myAge){
        this.name = myName;
        this.age = myAge;
        // 一般定义原型方法才恰当嗷
        this.hi = function () {
            console.log("hi");
        }
    }
    // 原型方法, 默认存到原型对象中
    say(){
        console.log(this.name, this.age);
    }
    // 静态属性
    static num = 666;
    // 静态方法
    static run() {
        console.log("run");
    }
}
// let p = new Person();
let p = new Person("zs", 18);
p.say();
console.log(Person.num);
Person.run();
```

**注意点**:

- 如果通过class定义类, 则**不能自定义这个类的原型对象**
- 如果想将属性和方法保存到原型中, 只能动态给原型对象添加属性和方法
  (优化构造函数三版优化里有说明什么叫动态添加)
- ES6 标准规定通过 class 定义的实例属性都只能在 constructor 中添加,
  直接在 class 里加的属性的方式只有 chrome 才认

##### extends 关键字

###### ES6 之前的继承

1. 在子类中通过 call/ apply 方法借助父类的构造函数
2. 将子类的原型对象设置为父类的实例对象

```js
function Person(myName, myAge) {
    this.name = myName;
    this.age = myAge;
}
Person.prototype.say =  function () {
    console.log(this.name, this.age);
}
function Student(myName, myAge, myScore) {
    // 1.在子类中通过 call/apply 方法借助父类的构造函数
    Person.call(this, myName, myAge);
    this.score = myScore;
    this.study = function () {
        console.log("day day up");
    }
}
// 2. 将子类的原型对象设置为父类的实例对象
Student.prototype = new Person();
Student.prototype.constructor = Student;

let stu = new Student("zs", 18, 99);
stu.say();
```

###### ES6 之后的继承

1. 在子类后面添加extends并指定父类的名称
2. 在子类的constructor构造函数中通过super方法借助父类的构造函数

```js
 class Person{
     constructor(myName, myAge){
         this.name = myName;
         this.age = myAge;
     }
     say(){
         console.log(this.name, this.age);
     }
 }

// 1. 在子类后面添加extends并指定父类的名称
class Student extends Person{
    constructor(myName, myAge, myScore){
        // 2. 在子类的constructor构造函数中通过super方法借助父类的构造函数
        super(myName, myAge);
        this.score = myScore;
    }
    study(){
        console.log("day day up");
    }
}
let stu = new Student("zs", 18, 98);
stu.say();
```

##### 类, 属性, 原型

###### `obj.constructor.name`

每个实例对象的 \_\_proto\_\_ 都指向其构造函数的原型对象,
实例对象本身没有 constructor 属性但其构造函数的原型对象有,
于是 console.log(实例对象.constructor) 可以得到该实例对象的构造函数,
构造函数有个**默认属性** name, 其值即为该构造函数的名字, 也就是 JS 中的类名.
所以, 用`实例对象.constructor.name`可以拿到类名

```js
function Person() {
    this.name = "lnj";
    this.age = 34;
    this.say = function () {
        console.log(this.name, this.age);
    }
}

let p = new Person();
console.log(typeof p); // object
console.log(p.constructor.name); // Person
```

###### instanceof 关键字

instanceof 关键字的作用:
**instanceof 用于判断 "对象" 是否是指定构造函数的 "实例"**

```js
class Person{
    name = "fhs";
}
let p = new Person();
console.log(p instanceof Person); // true
```

**注意点**:
只要构造函数的原型对象出现在实例对象的**原型链**中都会返回 true

```js
function Person(myName) {
    this.name = myName;
}
function Student(myName, myScore) {
    Person.call(this, myName);
    this.score = myScore;
}
Student.prototype = new Person();
Student.prototype.constructor = Student;

let stu = new Student();
console.log(stu instanceof Student); // true
console.log(stu instanceof Person); // true
```

###### isPrototypeOf 方法

什么是isPrototypeOf属性?
isPrototypeOf 是原型对象的一个方法, 用于判断一个对象是否是另一个对象的原型

```js
class Person{
    name = "fhs";
}
let  p = new Person();
console.log(Person.prototype.isPrototypeOf(p)); // true

class Cat{
    name = "mm";
}
console.log(Cat.prototype.isPrototypeOf(p)); // false
```

**注意点**:
只要调用者在传入对象的**原型链**上都会返回 true

```js
function Person(myName) {
    this.name = myName;
}
function Student(myName, myScore) {
    Person.call(this, myName);
    this.score = myScore;
}
Student.prototype = new Person();
Student.prototype.constructor = Student;

let stu = new Student();
console.log(Person.prototype.isPrototypeOf(stu)); // true
```

###### in 关键字

in 关键字的作用:
判断某一个对象是否拥有某一个属性

**注意点**:
只要类中**或者原型对象**中有, 就会返回 true

```js
class Person{
    name = null;
	age = 0;
}
Person.prototype.height = 0;

let p = new Person();
console.log("name" in p); // true
console.log("width" in p); // false
console.log("height" in p); // true
```

###### hasOwnProperty 方法

hasOwnProperty 方法的作用:
判断某一个对象**自身**是否拥有某一个属性

**注意点**:
只会去类中查找有没有, **不会去原型对象中查找**

```js
class Person{
    name = null;
age = 0;
}
Person.prototype.height = 0;

let p = new Person();
console.log(p.hasOwnProperty("name")); // true
console.log(p.hasOwnProperty("height")); // false
```

#### 属性, 方法的增删改查

方括号引号的作用和 . 作用相同.
但方括号不带引号时能做 . 做不到的事, 详见遍历对象

##### 增

- 通过 .

```js
class Person{}

let p = new Person();        
p.name = "fhs";
p.say = function(){
    console.log("hello world");
}
```

- 通过方括号引号

```js
class Person{}

let p = new Person();        
p["name"] = "zs";
p["say"] = function(){
	console.log("hello world");
}
```

. 和方括号引号 效果是一样的, 以下 . 操作都可用<font color="red">**方括号引号**</font>代替

##### 删 (delete 关键字)

- 用 delete 关键字来删除

```js
class Person{
    name = 'fhs';
	age = 23;
    say(){
        console.log(this.name, this.age);
    }
}

let p = new Person();
delete p.name;
delete p.say;
console.log(p);
```

##### 改

- 直接给属性赋新值即可

```js
class Person{
    name = 'fhs';
	age = 23;
	say(){
        console.log("hello");
    }
}

let p = new Person();
p.name = "xhx";
p.say = function(){
	console.log("hi");
}
console.log(p);
```

##### 查

- 对象.属性 或 对象.方法 就能查了

```js
class Person{
    name = 'fhs';
	age = 23;
	say(){
        console.log("hello");
    }
}

let p = new Person();
console.log(p.name);
console.log(p.say);
```

#### 遍历对象

1. 在JavaScript中对象和数组一样是可以遍历的
2. 什么是对象的遍历?
   对象的遍历就是依次取出对象中所有的属性和方法
3. 如何遍历一个对象?
   在JS中可以通过高级for循环来遍历对象
4. 形式:
   for(let key in obj) {}
   **注意点**:
   只能历到对象本身的属性方法, **原型链上的不会被遍历到**

- 遍历不到原型链上的属性, 方法

```js
class Person{
    constructor(myName, myAge){
        this.name = myName;
        this.age = myAge;
    }
    // 注意点: ES6定义类的格式, 默认将方法放到原型对象中
    say(){
        console.log(this.name, this.age);
    }
}

let p = new Person("fhs", 34);
console.log(p);
for(let key in p){
    if(p[key] instanceof Function){
        continue;
    }
    console.log(p[key]); // name age
    // 注意到这里没有 say, 因为 say 在原型对象上
}
```

- 在类里面这点要注意

```js
function Person(myName, myAge){
    this.name = myName;
    this.age = myAge;
    this.say = function(){
        console.log(this.name, this.age);
    }
}

let p = new Person("fhs", 34);
console.log(p); // 这时 say 才在对象里
for(let key in p){
    console.log(key); // name / age / say
    // 以下代码的含义取出 p 对象中名称叫做当前遍历到的名称的属性或者方法的取值
    console.log(p[key]); // p["name"] / p["age"] / p["say"]
    // 以下代码的含义取出 p 对象中名称叫做 key 的属性的取值 (那当然是没有, 所以这样不行)
    console.log(p.key); // undefined
}
```

- 还可以通过判断使不遍历方法

```js
function Person(myName, myAge){
    this.name = myName;
    this.age = myAge;
    this.say = function(){
        console.log(this.name, this.age);
    }
}

let p = new Person("fhs", 34);
console.log(p); // 这时 say 才在对象里
    for(let key in p){
        if(p[key] instanceof Function){ // 加这个判断以去掉方法, 一般对象原型链上没有 Function 嗷
            continue;
    }
	console.log(key); // name / age
}
```

#### 对象解构赋值

##### 对象与数组解构赋值的异同

- 对象的解构赋值和数组的解构赋值**符号不一样**
  - 数组解构使用 [], 对象解构使用 **{}**
- <font color="red">另外的不同</font>: 
  - 在对象解构赋值中, **左边的变量名称必须和对象的属性名称一致**, 才能解构出数据
  - 且值与名字对应, 而非与顺序对应

- 其它的一模一样

```js
let obj = {
    name: "lnj",
    age: 34
}

// 法一, 完全没用到解构赋值
// let name = obj.name;
// let age = obj.age;

// 法二
// let {name, age} = obj;

// 法三
let {name, age} = {name: "lnj",age: 34};
console.log(name, age);
```

##### 解构赋值应用场景

不管是数组解构赋值还是对象结构赋值, 都可以**用在函数传参中**
倒不是有什么用, 主要是够花哨

###### 数组解构赋值的应用

```js
let arr = [1, 3];

// function sum(a, b) {
function sum([a, b]) {
    return a + b;
}

// let res = sum(arr[0], arr[1]);
let res = sum(arr);
console.log(res);
```

###### 对象解构赋值的应用

```js
let obj = {
    name: "fhs",
    age: 23
}

// function say(name, age) {
function say({name, age}) {
    console.log(name, age);
}

// say(obj.name, obj.age);
say(obj);
```

###### 可以在解构赋值时给变量==换名字==

```js
let user = { 
    name: "John", 
    years: 30 
};

// let { name, years: age, isAdmin = false } = user;
let { name, years: age, isAdmin = false } = user;
console.log(name); // John
console.log(age); // 30
console.log(isAdmin); // false
```

#### 深拷贝, 浅拷贝

##### 深, 浅拷贝辨析

什么是深拷贝什么是浅拷贝?

1. 深拷贝

   - 修改新变量的值不会影响原有变量的值
   - 默认情况下基本数据类型都是深拷贝

   ```js
   let num1 = 123;
   let num2 = num1;
   num2 = 666; // 修改形变量的值
   console.log(num1); // 123
   console.log(num2); // 666
   ```

2. 浅拷贝

   - 修改新变量的值会影响原有的变量的值
   - **默认情况下引用类型都是浅拷贝**

   ```js
   class Person{
       name = "fhs";
   	age = 23;
   }
   let p1 = new Person();
   let p2 = p1;
   p2.name = "zs"; // 修改变量的值
   console.log(p1.name); // zs
   console.log(p2.name); // zs
   ```

##### 深拷贝狗题目

###### 浅拷贝确认

```js
class Person{
    name = "fhs";
	age = 23;
}
let p1 = new Person();
// 浅拷贝
let p2 = p1;
p2.name = "zs"; // 修改变量的值
```

###### 对象的属性值都是基本数据类型且不带方法时的深拷贝

以下三块代码都没法儿对对象套对象的对象做深拷贝

```js
class Person{
    name = "fhs";
	age = 23;
}

// 这个对象只有属性没有方法, 且属性值都是基本数据类型, 所以这样就可以了
let p1 = new Person();
// 拙劣的手法
p2.name = p1.name;
p2.age = p1.age;
p2.name = "zs";
console.log(p1.name); // fhs
```

- 高级 for 走一波
  要注意: 高级 for 也能遍历数组, in 前的是数组下标 (毕竟 js 里数组也是对象), 但**并不推荐**用 for in 遍历数组

```js
class Person{
    name = "fhs";
	age = 23;
}

// 这个对象只有属性没有方法, 且属性值都是基本数据类型, 所以这样就可以了
let p1 = new Person();
// 朴素的手法
for(let key in p1){
    p2[key] = p1[key];
}
console.log(p2);
p2.name = "zs";
console.log(p1.name); // fhs
```

- Object 的静态方法 assign
  **注意点**:
  只有被拷贝对象中所有属性都是基本数据类型, 以下代码才是深拷贝

```js
class Person{
    name = "fhs";
	age = 23;
}

// 这个对象只有属性没有方法, 且属性值都是基本数据类型, 所以这样就可以了
let p1 = new Person();
// js 给的工具
Object.assign(p2, p1);
// console.log(p2);
p2.name = "zs";
console.log(p1.name); // fhs
console.log(p2.name); // zs
```

###### 对象属性值不都是基本数据类型时的深拷贝

assign **并不能**在对象属性值不都是基本数据类型时实现深拷贝

要深拷贝就要借助类库, 或者自己**造一个不太圆的轮子**

```js
class Person{
    name = "fhs";
    cat = {
        age : 3
    };
    scores = [1, 3, 5];
}

let p1 = new Person();
let p2 = new Object();
depCopy(p2, p1);

// console.log(p2);
p2.cat.age = 666;
console.log(p1.cat.age);
console.log(p2.cat.age);

function depCopy(target, source) {
    // 1.通过遍历拿到source中所有的属性
    for(let key in source){
        // 2.取出当前遍历到的属性对应的取值, 这个酷
        let sourceValue = source[key];
        // console.log(sourceValue);
        // 3.判断当前的取值是否是引用数据类型 (所有对象都是 Object 的实例)
        if(sourceValue instanceof Object){
            // sourceValue.constructor 可以返回这个值的构造函数, 从而分辨对象是数组还是对象还是函数还是狭义对象
            // new 一个 sourceValue.constructor, 可以给到广义对象恰当的容器 (放括号或花括号)
            let subTarget = new sourceValue.constructor;
            // 这一步是将空容器赋给 target 的同名属性
            target[key] = subTarget;
            
            // 递归! 自己调自己! 遇到简单值就赋上去, 遇到引用值就再判断! 酷!
            // 要注意: 高级 for 也能遍历数组, in 前的是数组下标
            depCopy(subTarget, sourceValue);
        }else{
            target[key] = sourceValue; // 基本数据类型直接安心的把值赋给 target 同名属性即可
        }
    }
}
```

###### 小结

- 深和浅之间还有半深不浅
- 最浅就是一开始共用同一个对象
- 半深不浅时一开始不共用, 到了一定深度开始公用
- 完全的深拷贝做不到吧, 毕竟归根到底都属于 Object 类, 总有一些共性的东西是要共享的
- 断点调试中点上弯弯的箭头意思是“顺序执行”,
  箭头向下指向点点意思是“跳到下一个断点”,
  箭头向上指向点点意思是“复原到上一个断点”

## 提醒自己

1. 普通对象, 数组, 函数在 js 中都是对象
   但对象不是类, 而是类的产物, 是有其**特性**的
   所以不要总是纠结“都是对象, 怎么数组就这么特殊或者函数怎么就这么特殊的问题”
   因为就是特殊啊! Java 同一个类产的对象还能有不同属性值嘞
   数组(方括号包裹), 函数(形式特殊), 狭义对象(花括号包裹) 有些重大区别怎么了嘛!
   
2. 函数套函数就容易茫, 清醒一点!分清清!

3. 找到共性当然是很好的, 但个性多到让人晕眩的时候也不能烦躁, 丰富不是缺点. 这里我说的是 js 方法

4. java 不会说类是对象, 因为在 java 里类是对象的爸爸
   但 javascript 会说构造函数 (js 的类) 是对象
   因为 js 里类本质是个函数, js 里的函数是对象, 其原型链上有 Object
   
5. js 的 class 和 css 的 class 完全不是一回事嗷
   由于 class 是 js 的关键字, 所以 css 的 class 在 js 里改叫 className 了
   
6. js 的函数内变量和对象属性完全不同, 函数作为对象可以拥有属性, 但这个属性不是函数的变量

   > We can treat a function as an object, store properties in it, 
   > but that has no effect on its execution. 
   > Variables are not function properties and vice versa. 
   > These are just parallel worlds.
