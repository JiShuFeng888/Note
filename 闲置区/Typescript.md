### 1.Typescript开篇

```javascript
npm install typescript -g
 tsc .\01.ts  编译

 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>TypeScript核心</title>
</head>
<body>
<!--
1.初始化一个自动打包的webpack项目
2.通过tsc --init初始化TypeScript配置文件
3.通过npm install typescript ts-loader安装对应loader
4.修改webpack配置文件
entry: "./src/js/index.ts",
resolve: {
    extensions: [ '.tsx', '.ts', '.js' ]
},
rules: [
    // ts编译配置
    {
        test: /\.tsx?$/,
        use: 'ts-loader',
        exclude: /node_modules/
    }
]
-->
</body>
</html>
```

### 2.Typescript基础类型

```javascript
let a:boolean
let b:string
```

### 3.Typescript数组和元组类型

```javascript
let arr:Array<number> 定义一个存储number类型数据的数组

let arr:string[] 定义一个存储string类型数据的数组

let arr:(number|string)[]; 联合类型

let arr:any[] 任意类型

元组就是数组类型的扩展,用来存储长度一定的数据
let arr:[number,boolean] 定义一个长度为2的数组,类型必须一一对应
```

### 4.枚举类型

```javascript
/*
枚举类型是TS为JS扩展的一种类型, 在原生的JS中是没有枚举类型的
枚举用于表示固定的几个取值
例如: 一年只有四季、人的性别只能是男或者女
*/
enum Gender{ // 定义了一个名称叫做Gender的枚举类型, 这个枚举类型的取值有两个, 分别是Male和Femal
    Male,
    Femal
}
let val:Gender; // 定义了一个名称叫做val的变量, 这个变量中只能保存Male或者Femal
val = Gender.Male;
val = Gender.Femal;
// val = 'nan'; // 报错
// val  = false;// 报错
// 注意点: TS中的枚举底层实现的本质其实就是数值类型, 所以赋值一个数值不会报错
// val = 666; // 不会报错
// console.log(Gender.Male); // 0
// console.log(Gender.Femal);// 1

// 注意点: TS中的枚举类型的取值, 默认是从上至下从0开始递增的
//         虽然默认是从0开始递增的, 但是我们也可以手动的指定枚举的取值的值
// 注意点: 如果手动指定了前面枚举值的取值, 那么后面枚举值的取值会根据前面的值来递增
// console.log(Gender.Male); // 6
// console.log(Gender.Femal);// 7

// 注意点: 如果手动指定了后面枚举值的取值, 那么前面枚举值的取值不会受到影响
// console.log(Gender.Male); // 0
// console.log(Gender.Femal);// 6

// 注意点: 我们还可以同时修改多个枚举值的取值, 如果同时修改了多个, 那么修改的是什么最后就是什么
// console.log(Gender.Male); // 8
// console.log(Gender.Femal);// 6

// 我们可以通过枚举值拿到它对应的数字
console.log(Gender.Male); // 0
// 我们还可以通过它对应的数据拿到它的枚举值
console.log(Gender[0]); // Male


// 探究底层实现原理
/*
var Gender;
(function (Gender) {
 // Gender[key] = value;
    Gender[Gender["Male"] = 0] = "Male";
    Gender[Gender["Femal"] = 1] = "Femal";
})(Gender || (Gender = {}));

let Gender = {};
Gender["Male"] = 0;
Gender[0] = "Male";
Gender["Femal"] = 1;
Gender[1] = "Femal";
* */

```

### 5.any类型和void型

```javascript
let a:any
let a:void
 
// any类型
// any表示任意类型, 当我们不清楚某个值的具体类型的时候我们就可以使用any
// 一般用于定义一些通用性比较强的变量, 或者用于保存从其它框架中获取的不确定类型的值
// 在TS中任何数据类型的值都可以负责给any类型
// let value:any; // 定义了一个可以保存任意类型数据的变量
// value = 123;
// value = "abc";
// value = true;
// value = [1, 3, 5];


// void类型
// void与any正好相反, 表示没有任何类型, 一般用于函数返回值
// 在TS中只有null和undefined可以赋值给void类型
function test():void {
    console.log("hello world");
}
test();

let value:void; // 定义了一个不可以保存任意类型数据的变量, 只能保存null和undefined
// value = 123; // 报错
// value = "abc";// 报错
// value = true;// 报错
// 注意点: null和undefined是所有类型的子类型, 所以我们可以将null和undefined赋值给任意类型
// value = null; // 不会报错
value = undefined;// 不会报错

严格模式这东西
```

### 6.Never类型和Object类型

```javascript
// Never类型
// 表示的是那些永不存在的值的类型
// 一般用于抛出异常或根本不可能有返回值的函数
// function demo():never {
//     throw new Error('报错了');
// }
// demo();

// function demo2():never {
//     while (true){}
// }
// demo2();

// Object类型
// 表示一个对象
let obj:object; // 定义了一个只能保存对象的变量
// obj = 1;
// obj = "123";
// obj = true;
obj = {name:'lnj', age:33};
console.log(obj);
```

### 7.类型断言

```javascript
/*
1.什么是类型断言?
TS中的类型断言和其它编程语言的类型转换很像, 可以将一种类型强制转换成另外一种类型
类型断言就是告诉编译器, 你不要帮我们检查了, 相信我，我知道自己在干什么。

例如: 我们拿到了一个any类型的变量, 但是我们明确的知道这个变量中保存的是字符串类型
      此时我们就可以通过类型断言告诉编译器, 这个变量是一个字符串类型
      此时我们就可以通过类型断言将any类型转换成string类型, 使用字符串类型中相关的方法了
* */
let str:any = 'it666';
// 方式一
// let len = (<string>str).length;
// 方式二
// 注意点: 在企业开发中推荐使用as来进行类型转换(类型断言)
//         因为第一种方式有兼容性问题, 在使用到了JSX的时候兼容性不是很好
let len = (str as string).length;
console.log(len);

```

### 8.接口类型

```javascript
/*
1.什么是接口类型?
和number,string,boolean,enum这些数据类型一样,
接口也是一种类型, 也是用来约束使用者的
* */
// 定义一个接口类型
interface FullName{
    firstName:string
    lastName:string
}
let obj = {
    firstName:'Jonathan',
    lastName:'Lee'
    // lastName:18
};
// 需求: 要求定义一个函数输出一个人完整的姓名, 这个人的姓必须是字符串, 这个人的名也必须是一个字符
function say({firstName, lastName}:FullName):void {
    console.log(`我的姓名是:${firstName}_${lastName}`);
}
say(obj);

```

### 9.可选属性和索引签名

```javascript
// 定义一个接口
interface FullName{
    firstName:string
    lastName:string
    middleName?:string
    [propName:string]:any
}
// 需求: 如果传递了middleName就输出完整名称, 如果没有传递middleName, 那么就输出firstName和lastName
function say({firstName, lastName, middleName}:FullName):void {
    // console.log(`我的姓名是:${firstName}_${lastName}`);
    if(middleName){
        console.log(`我的姓名是:${firstName}_${middleName}_${lastName}`);
    }else{
        console.log(`我的姓名是:${firstName}_${lastName}`);
    }
}
// 注意点: 如果使用接口来限定了变量或者形参, 那么在给变量或者形参赋值的时候,
// 赋予的值就必须和接口限定的一模一样才可以, 多一个或者少一个都不行

// say({firstName:'Jonathan'});
// say({firstName:'Jonathan', lastName:'Lee', middleName:"666"});

// 注意点: 但是在企业开发中可以多一个也可能少一个
// 少一个或多个怎么做? 可选属性
// say({firstName:'Jonathan', lastName:'Lee', middleName:"666"});
// say({firstName:'Jonathan', lastName:'Lee'});
// 多一个或者多多个怎么做? 如果绕开TS检查
// 方式一: 使用类型断言
// say({firstName:'Jonathan', lastName:'Lee', middleName:"666", abc:'abc'} as FullName);
// 方式二: 使用变量
// let obj = {firstName:'Jonathan', lastName:'Lee', middleName:"666", abc:'abc'};
// say(obj);
// 方式三: 使用索引签名
say({firstName:'Jonathan', lastName:'Lee', middleName:"666", abc:'abc', 123:123, def:"def"});


```

### 10.索引签名和只读属性

```javascript
// 1.什么是索引签名?
// 索引签名用于描述那些“通过索引得到”的类型，比如arr[10]或obj["key"]
/*
interface FullName {
    [propName:string]:string
}
let obj:FullName = {
    // 注意点: 只要key和value满足索引签名的限定即可, 无论有多少个都无所谓
    firstName:'Jonathan',
    lastName:'Lee',
    // middleName:false // 报错
    // false: '666' // 无论key是什么类型最终都会自动转换成字符串类型, 所以没有报错
}
 */
// interface stringArray {
//     [propName:number]:string
// }
/*
let arr:stringArray = {
    0:'a',
    1:'b',
    2:'c'
};
 */
// let arr:stringArray = ['a', 'b', 'c'];
// console.log(arr[0]);
// console.log(arr[1]);
// console.log(arr[2]);

// 2.什么是只读属性?
// 让对象属性只能在对象刚刚创建的时候修改其值
/*
interface FullName {
    firstName:string
    readonly lastName:string
}
let myName:FullName = {
    firstName: 'Jonathan',
    lastName: 'Lee'
};
myName.lastName = 'Wang';
console.log(myName);
 */
/*
// TS内部对只对属性进行了扩展, 扩展出来了一个只读数组
// let arr2:Array<string> = ['a', 'b', 'c'];
let arr2:ReadonlyArray<string> = ['a', 'b', 'c'];
console.log(arr2[0]); // a
arr2[0] = '666';
console.log(arr2[0]); // 666
 */
```

### 11.函数接口和混合接口**

```javascript
// 函数接口
// 我们除了可以通过接口来限定对象以外, 我们还可以使用接口来限定函数
/*
interface SumInterface {
    (a:number, b:number):number
}
let sum:SumInterface = function (x:number, y:number):number {
    return x + y;
}
let res = sum(10, 20);
console.log(res);
 */

// 混合类型接口
// 约定的内容中既有对象属性, 又有函数
// 要求定义一个函数实现变量累加
/*
let count = 0; // 会污染全局空间
function demo() {
    count++;
    console.log(count);
}
demo();
demo();
demo();
 */
/*
let demo = (()=>{ // 使用闭包确实可以解决污染全局空间的问题, 但是对于初学者来说不太友好
    let count = 0;
    return ()=>{
        count++;
        console.log(count);
    }
})();
demo();
demo();
demo();
 */
// 在JS中函数的本质是什么? 就是一个对象
// let demo = function () {
//     demo.count++;
// }
// demo.count = 0;
// demo();
// demo();
// demo();
interface CountInterface {
    ():void
    count:number
}
let getCounter = (function ():CountInterface {
    /*
    CountInterface接口要求数据既要是一个没有参数没有返回值的函数
                              又要是一个拥有count属性的对象
    fn作为函数的时候符合接口中函数接口的限定 ():void
    fn作为对象的时候符合接口中对象属性的限定  count:number
    * */
    let fn = <CountInterface>function () {
        fn.count++;
        console.log(fn.count);
    }
    fn.count = 0;
    return fn;
})();
getCounter();
getCounter();
getCounter();


```

### 12.接口的继承

```s
// 接口的继承
// TS中的接口和JS中的类一样是可以继承的
interface LengthInterface {
    length:number
}
interface WidthInterface {
    width:number
}
interface HeightInterface {
    height:number
}
interface RectInterface extends LengthInterface,WidthInterface,HeightInterface {
    // length:number
    // width:number
    // height:number
    color:string
}
let rect:RectInterface = {
    length:10,
    width:20,
    height:30,
    color:'red'
}


```

### 13.TS中的函数

```javascript
// TS中的函数
// TS中的函数大部分和JS相同
/*
// 命名函数
function say1(name) {
    console.log(name);
}
// 匿名函数
let say2 = function (name) {
    console.log(name);
}
// 箭头函数
let say3 = (name) => {
    console.log(name);
}
 */
// 命名函数
function say1(name:string):void {
    console.log(name);
}
// 匿名函数
let say2 = function (name:string):void {
    console.log(name);
}
// 箭头函数
let say3 = (name:string):void =>{
    console.log(name);
}

```

### 14.TS函数完整格式

```javascript
// TS函数完整格式
// 在TS中函数的完整格式应该是由函数的定义和实现两个部分组成的
/*
// 定义一个函数
let AddFun:(a:number, b:number)=>number;
// 根据定义实现函数
AddFun = function (x:number, y:number):number {
    return x + y;
};
let res = AddFun(10, 20);
console.log(res);
*/
/*
// 一步到位写法
let AddFun:(a:number, b:number)=>number =
function (x:number, y:number):number {
    return x + y;
};
let res = AddFun(20, 20);
console.log(res);
*/
/*
// 根据函数的定义自动推导对应的数据类型
let AddFun:(a:number, b:number)=>number =
    function (x, y) {
        return x + y;
    };
let res = AddFun(20, 20);
console.log(res);
*/

// TS函数声明
/*
// 先声明一个函数
type AddFun = (a:number, b:number)=>number;
// 再根据声明去实现这个函数
// let add:AddFun = function (x:number, y:number):number {
//     return x + y;
// };
let add:AddFun = function (x, y) {
    return x + y;
};
let res = add(30, 20);
console.log(res);
*/

// TS函数重载
// 函数的重载就是同名的函数可以根据不同的参数实现不同的功能
/*
function getArray(x:number):number[] {
    let arr = [];
    for(let i = 0; i <= x; i++){
        arr.push(i);
    }
    return arr;
}
function getArray(str:string):string[] {
    return str.split('');
}
 */
// 定义函数的重载
function getArray(x:number):number[];
function getArray(str:string):string[];
// 实现函数的重载
function getArray(value:any):any[] {
    if(typeof value === 'string'){
        return value.split('');
    }else{
        let arr = [];
        for(let i = 0; i <= value; i++){
            arr.push(i);
        }
        return arr;
    }
}
// let res = getArray(10);
let res = getArray('www.it666.com');
console.log(res);

```

