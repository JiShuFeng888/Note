### 0.Web出征

```javascript
prompt
prompt 函数接收两个参数：

result = prompt(title, [default]);
浏览器会显示一个带有文本消息的模态窗口，还有 input 框和确定/取消按钮。

title
显示给用户的文本
default
可选的第二个参数，指定 input 框的初始值。
语法中的方括号 [...]
上述语法中 default 周围的方括号表示该参数是可选的，不是必需的。

访问者可以在提示输入栏中输入一些内容，然后按“确定”键。然后我们在 result 中获取该文本。或者他们可以按取消键或按 Esc 键取消输入，然后我们得到 null 作为 result。

prompt 将返回用户在 input 框内输入的文本，如果用户取消了输入，则返回 null。

举个例子：

let age = prompt('How old are you?', 100);

alert(`You are ${age} years old!`); // You are 100 years old!
IE 浏览器会提供默认值
第二个参数是可选的。但是如果我们不提供的话，Internet Explorer 会把 "undefined" 插入到 prompt。

我们可以在 Internet Explorer 中运行下面这行代码来看看效果：

let test = prompt("Test");
所以，为了 prompt 在 IE 中有好的效果，我们建议始终提供第二个参数：

let test = prompt("Test", ''); // <-- 用于 IE 浏览器
confirm
语法：

result = confirm(question);
confirm 函数显示一个带有 question 以及确定和取消两个按钮的模态窗口。

点击确定返回 true，点击取消返回 false。

例如：

let isBoss = confirm("Are you the boss?");

alert( isBoss ); // 如果“确定”按钮被按下，则显示 true
总结
我们学习了与用户交互的 3 个浏览器的特定函数：

alert
显示信息。
prompt
显示信息要求用户输入文本。点击确定返回文本，点击取消或按下 Esc 键返回 null。
confirm
显示信息等待用户点击确定或取消。点击确定返回 true，点击取消或按下 Esc 键返回 false。
这些方法都是模态的：它们暂停脚本的执行，并且不允许用户与该页面的其余部分进行交互，直到窗口被解除。

上述所有方法共有两个限制：

模态窗口的确切位置由浏览器决定。通常在页面中心。
窗口的确切外观也取决于浏览器。我们不能修改它。
这就是简单的代价。还有其他一些方法可以显示更漂亮的窗口，并与用户进行更丰富的交互，但如果“花里胡哨”不是非常重要，那使用本节讲的这些方法也挺好。







或运算符 || 做了如下的事情：

从左到右依次计算操作数。
处理每一个操作数时，都将其转化为布尔值。如果结果是 true，就停止计算，返回这个操作数的初始值。
如果所有的操作数都被计算过（也就是，转换结果都是 false），则返回最后一个操作数。
返回的值是操作数的初始形式，不会做布尔转换。

换句话说，一个或运算 || 的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。

例如：

alert( 1 || 0 ); // 1（1 是真值）

alert( null || 1 ); // 1（1 是第一个真值）
alert( null || 0 || 1 ); // 1（第一个真值）

alert( undefined || null || 0 ); // 0（都是假值，返回最后一个值）






与运算 && 做了如下的事：

从左到右依次计算操作数。
在处理每一个操作数时，都将其转化为布尔值。如果结果是 false，就停止计算，并返回这个操作数的初始值。
如果所有的操作数都被计算过（例如都是真值），则返回最后一个操作数。
换句话说，与运算返回第一个假值，如果没有假值就返回最后一个值。
```



###  1.工厂函数

```javascript
1.什么是工厂函数?
     工厂函数就是专门用于创建对象的函数, 我们就称之为工厂函数

     function createPerson(myName, myAge) {
            let obj = new Object();
            obj.name = myName;
            obj.age = myAge;
            obj.say = function () {
                console.log("hello world");
            }
            return obj;
        }
        let obj1 = createPerson("lnj", 34);
        let obj2 = createPerson("zs", 44);
        console.log(obj1);
        console.log(obj2);
```

### 2.构造函数1.0

```javascript
   	 /*
        1.什么是构造函数
        构造函数和工厂函数一样, 都是专门用于创建对象的
        构造函数本质上是工厂函数的简写

        2.构造函数和工厂函数的区别
        2.1构造函数的函数名称首字母必须大写
        2.2构造函数只能够通过new来调用
     */

        function Person(myName, myAge) {
            // let obj = new Object();  // 系统自动添加的
            // let this = obj; // 系统自动添加的
            this.name = myName;
            this.age = myAge;
			//注意say不用加（）
            this.say = function () {
            // 方法中的this谁调用就是谁, 所以当前是obj1调用, 所以当前的this就是obj1
                console.log("hello world");
            }
            // return this; // 系统自动添加的
        }

      	let obj1 = new Person("lnj", 34);
        let obj2 = new Person("zs", 44);

        console.log(obj1.say === obj2.say); // false
        // 通过三个等号来判断两个函数名称, 表示判断两个函数是否都存储在同一块内存中

		// 由于两个对象中的say方法的实现都是一样的, 但是保存到了不同的存储空间中
        // 所以有性能问题
```

<img src="Javascript.assets/%E6%89%B9%E6%B3%A8%202020-11-22%20101846.png" alt="批注 2020-11-22 101846" style="zoom:50%;" />

### 3.构造函数2.0

```javascript
      function mySay() {
            console.log("hello world");
        }
        function Person(myName, myAge) {
            // let obj = new Object();  // 系统自动添加的
            // let this = obj; // 系统自动添加的
            this.name = myName;
            this.age = myAge;
            this.say = mySay;
            // return this; // 系统自动添加的
        }
        let obj1 = new Person("lnj", 34);
        let obj2 = new Person("zs", 44);
        console.log(obj1.say === obj2.say); // true

        /*
        1.当前这种方式解决之后存在的弊端
        1.1阅读性降低了
        1.2污染了全局的命名空间
        */
```

<img src="Javascript.assets/%E6%89%B9%E6%B3%A8%202020-11-22%20103658.png" alt="批注 2020-11-22 103658" style="zoom:50%;" />

### 4.构造函数3.0

```javascript
let fns = {
            mySay: function () {
                console.log("hello world");
            }
        }
        function Person(myName, myAge) {
            // let obj = new Object();  // 系统自动添加的
            // let this = obj; // 系统自动添加的
            this.name = myName;
            this.age = myAge;
            this.say = fns.mySay;
            // return this; // 系统自动添加的
        }
        let obj1 = new Person("lnj", 34);
        let obj2 = new Person("zs", 44);
        console.log(obj1.say === obj2.say); // true
```

### 5.构造函数专业写法

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

### 6.Prototype特点

```javascript
		/*
        1.prototype特点
        1.1存储在prototype中的方法可以被对应构造函数创建出来的所有对象共享
        1.2prototype中除了可以存储方法以外, 还可以存储属性
        1.3prototype如果出现了和构造函数中同名的属性或者方法, 对象在访问的时候, 访问到的是构造函中的数据

        2.prototype应用场景
        prototype中一般情况下用于存储所有对象都相同的一些属性以及方法
        如果是对象特有的属性或者方法, 我们会存储到构造函数中
        */

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
        let obj1 = new Person("lnj", 34);
        obj1.say();
        console.log(obj1.currentType);
        let obj2 = new Person("zs", 44);
        obj2.say();
        console.log(obj2.currentType);
```

### 7.对象三角恋关系

```javascript
        /*
        1.每个"构造函数"中都有一个默认的属性, 叫做prototype
          prototype属性保存着一个对象, 这个对象我们称之为"原型对象"
        2.每个"原型对象"中都有一个默认的属性, 叫做constructor
          constructor指向当前原型对象对应的那个"构造函数"
        3.通过构造函数创建出来的对象我们称之为"实例对象"
          每个"实例对象"中都有一个默认的属性, 叫做__proto__
          __proto__指向创建它的那个构造函数的"原型对象"
        */
        function Person(myName, myAge) {
            this.name = myName;
            this.age = myAge;
        }
        let obj1 = new Person("lnj", 34);

        console.log(Person.prototype);
        console.log(Person.prototype.constructor);
        console.log(obj1.__proto__);
```

### 8.Function函数

```javascript
     /*
        1.JavaScript中函数是引用类型(对象类型), 既然是对象,
          所以也是通过构造函数创建出来的,"所有函数"都是通过Function构造函数创建出来的对象
        2.JavaScript中只要是"函数"就有prototype属性!!!
         "Function函数"的prototype属性指向"Function原型对象"
        3.JavaScript中只要"原型对象"就有constructor属性
          "Function原型对象"的constructor指向它对应的构造函数
        4.Person构造函数是Function构造函数的实例对象, 所以也有__proto__属性
          Person构造函数的__proto__属性指向"Function原型对象"
       */

        function Person(myName, myAge) {
            this.name = myName;
            this.age = myAge;
        }
        let obj1 = new Person("lnj", 34);

        // console.log(Function);
        // console.log(Function.prototype);
        // console.log(Function.prototype.constructor);
        // console.log(Function === Function.prototype.constructor); // true

        // console.log(Person.__proto__);
        console.log(Person.__proto__ === Function.prototype); // true
```

![批注 2020-11-22 111528](Javascript.assets/%E6%89%B9%E6%B3%A8%202020-11-22%20111528.png)

### 9.Object函数

```javascript
       /*
        1. JavaScript函数是引用类型(对象类型), 所以Function函数也是对象
        2."Function构造函数"也是一个对象, 所以也有__proto__属性
          "Function构造函数"__proto__属性指向"Function原型对象"
        3. JavaScript中还有一个系统提供的构造函数叫做Object
           只要是函数都是"Function构造函数"的实例对象
        4.只要是对象就有__proto__属性, 所以"Object构造函数"也有__proto__属性
          "Object构造函数"的__proto__属性指向创建它那个构造函数的"原型对象"
        5.只要是构造函数都有一个默认的属性, 叫做prototype
          prototype属性保存着一个对象, 这个对象我们称之为"原型对象"
        6.只要是原型对象都有一个默认的属性, 叫做constructor
          constructor指向当前原型对象对应的那个"构造函数"
         */
        function Person(myName, myAge) {
            this.name = myName;
            this.age = myAge;
        }
        let obj1 = new Person("lnj", 34);
        // console.log(Function.__proto__);
        // console.log(Function.__proto__ === Function.prototype); // true

        // console.log(Object);
        // console.log(Object.__proto__);
        // console.log(Object.__proto__ === Function.prototype); // true
        // console.log(Object.prototype);
        // console.log(Object.prototype.constructor);

        // console.log(Object.prototype.constructor === Object); // true
        // console.log(Object.prototype.__proto__); // null
```

![批注 2020-11-22 113047](Javascript.assets/%E6%89%B9%E6%B3%A8%202020-11-22%20113047.png)

### 10.函数对象关系

```javascript
        /*
        1.所有的构造函数都有一个prototype属性, 所有prototype属性都指向自己的原型对象
        2,所有的原型对象都有一个constructor属性, 所有constructor属性都指向自己的构造函数
        3.所有函数都是Function构造函数的实例对象
        4.所有函数都是对象, 包括Function构造函数
        5.所有对象都有__proto__属性
        6.普通对象的__proto__属性指向创建它的那个构造函数对应的"原型对象"
        7.所有对象的__proto__属性最终都会指向"Object原型对象"
        8."Object原型对象"的__proto__属性指向NULL
        */
        function Person(myName, myAge) {
            this.name = myName;
            this.age = myAge;
        }
        let obj1 = new Person("lnj", 34);

        console.log(Function.prototype.__proto__);
        console.log(Person.prototype.__proto__);
        console.log(Function.prototype.__proto__ === Person.prototype.__proto__);
        console.log(Function.prototype.__proto__ === Object.prototype);
        console.log(Person.prototype.__proto__ === Object.prototype);
```

![批注 2020-11-22 114108](Javascript.assets/%E6%89%B9%E6%B3%A8%202020-11-22%20114108.png)

### 11.原型链

```javascript
/*
        1.对象中__proto__组成的链条我们称之为原型链
		//注意！！！原型链
        2.对象在查找属性和方法的时候, 会先在当前对象查找
          如果当前对象中找不到想要的, 会依次去上一级原型对象中查找
          如果找到Object原型对象都没有找到, 就会报错
         */
        function Person(myName, myAge) {
            this.name = myName;
            this.age = myAge;
            // this.currentType = "构造函数中的type";
            // this.say = function () {
            //     console.log("构造函数中的say");
            // }
        }

        Person.prototype = {
            // 注意点: 为了不破坏原有的关系, 在给prototype赋值的时候, 需要在自定义的对象中手动的添加constructor属性, 手动的指定需要指向谁
            constructor: Person,
            // currentType: "人",
            // say: function () {
            //     console.log("hello world");
            // }
        }
        let obj1 = new Person("lnj", 34);
        // obj1.say();
        console.log(obj1.currentType);
        // console.log(Person.prototype.constructor);
```

### 12.原型链属性注意点

```javascript
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
        let obj = new Person("lnj", 34);
        // console.log(obj.currentType); // "人"
        // console.log(obj.__proto__.currentType); // "人"

        // 注意点: 在给一个对象不存在的属性设置值的时候, 不会去原型对象中查找, 如果当前对象没有就会给当前对象新增一个不存在的属性
        //原型仅用于读取属性。对于写入/删除操作可以直接在对象上进行。
        obj.currentType = "新设置的值";
        console.log(obj.currentType); // 新设置的值
        console.log(obj.__proto__.currentType); // "人"
```

		//let animal =  { eats:  true  }; 
		 let rabbit =  { jumps:  true, __proto__: animal }; 
		 _// Object.keys 只返回自己的 key alert(Object.keys(rabbit)); 								// jumps_  _
		 // for..in 会遍历自己以及继承的键 for(let prop in rabbit) alert(prop); // jumps，然后是 eats_

let animal =  { eats:  true  }; 

 let rabbit =  { jumps:  true, __proto__: animal }; 

 for(let prop in rabbit)  {  let isOwn = rabbit.hasOwnProperty(prop);  

if  (isOwn)  {  alert(`Our: ${prop}`);  // Our: jumps  }  else  {  alert(`Inherited: ${prop}`);  // Inherited: eats


几乎所有其他键/值获取方法都忽略继承的属性

几乎所有其他键/值获取方法，例如  `Object.keys`  和  `Object.values`  等，都会忽略继承的属性。

它们只会对对象自身进行操作。**不考虑**  继承自原型的属性。 

```
let hamster = {
  stomach: [],

  eat(food) {
    // 分配给 this.stomach 而不是 this.stomach.push
    this.stomach = [food];
  }
};

let speedy = {
   __proto__: hamster
};

let lazy = {
  __proto__: hamster
};

// 仓鼠 Speedy 找到了食物
speedy.eat("apple");
alert( speedy.stomach ); // apple

// 仓鼠 Lazy 的胃是空的
alert( lazy.stomach ); // <nothing>



function  Rabbit(name)  { 
	this.name = name;  
	alert(name);
 }  
let rabbit =  new  Rabbit("White Rabbit"); 
_let rabbit2 = new rabbit.constructor("Black Rabbit");_





function Rabbit() {}
Rabbit.prototype = {eats: true};
let rabbit = new Rabbit();
Rabbit.prototype = {};
alert( rabbit.eats ); // ?


New 实现原理!!!!!
New 实现原理!!!!!
New 实现原理!!!!!

let New = function (P) {
        let o = {};
        let arg = Array.prototype.slice.call(arguments,1);
        
        o.__proto__ = P.prototype;
  
       
        P.apply(o,arg);
        //已经保存参数了
        
        return o;


```

 

### 13.封装性

```
​```javascript
    /*
        1.局部变量和局部函数
        无论是ES6之前还是ES6, 只要定义一个函数就会开启一个新的作用域
        只要在这个新的作用域中, 通过let/var定义的变量就是局部变量
        只要在这个新的作用域中, 定义的函数就是局部函数

        2.什么是对象的私有变量和函数
        默认情况下对象中的属性和方法都是公有的, 只要拿到对象就能操作对象的属性和方法
        外界不能直接访问的变量和函数就是私有变量和是有函数
        构造函数的本质也是一个函数, 所以也会开启一个新的作用域, 所以在构造函数中定义的变量和函数就是私有和函数
        */
        /*
        3.什么是封装?
        封装性就是隐藏实现细节，仅对外公开接口

        4.为什么要封装?
        4.1不封装的缺点：当一个类把自己的成员变量暴露给外部的时候,那么该类就失去对属性的管理权，别人可以任意的修改你的属性
        4.2封装就是将数据隐藏起来,只能用此类的方法才可以读取或者设置数据,不可被外部任意修改. 封装是面向对象设计本质(将变化隔离)。这样降低了数据被误用的可能 (提高安全性和灵活性)
        */

        /*
        function demo() {
            var num = 123;
            let value = 456;
            function test() {
                console.log("test");
            }

            // console.log(num);
            // console.log(value);
            // test();
        }
        demo();
        console.log(num);
        console.log(value);
        test();
        */

        function Person() {
            this.name = "lnj";
            // this.age = 34;
            let age = 34;
            this.setAge = function (myAge) {
                if(myAge >= 0){
                    age = myAge;
                }
            }
            this.getAge = function () {
                return age;
            }
            this.say = function () {
                console.log("hello world");
            }
            /*
            // 由于构造函数也是一个函数, 所以也会开启一个新的作用域
            // 所以在构造函数中通过var/let定义的变量也是局部变量
            // 所以在构造函数中定义的函数也是局部函数
            var num = 123;
            let value = 456;
            function test() {
                console.log("test");
            }
            */
        }
        let obj = new Person();
        // 结论: 默认情况下对象的属性和方法都是公开的, 只要拿到对象就可以操作对象的属性和方法
        // console.log(obj.name);
        // obj.age = -3;
        // console.log(obj.age);
        // obj.say();

        // console.log(age);
        obj.setAge(-3);
        console.log(obj.getAge());
```

### 14.私有属性注意点

```javascript
        function Person() {
            this.name = "lnj";
            let age = 34;
            this.setAge = function (myAge) {
                if (myAge >= 0) {
                    age = myAge;
                }
            }
            this.getAge = function () {
                return age;
            }
            this.say = function () {
                console.log("hello world");
            }
        }
        let obj = new Person();
        // 1.操作的是私有属性(局部变量)
        obj.setAge(-3);
        console.log(obj.getAge());

        /*
        // 注意点:
        // 在给一个对象不存在的属性设置值的时候, 不会去原型对象中查找, 如果当前对象没有就会给当前对象新增一个不存在的属性
        // 由于私有属性的本质就是一个局部变量, 并不是真正的属性, 所以如果通过 对象.xxx的方式是找不到私有属性的, 所以会给当前对象新增一个不存在的属性
        */
        // 2.操作的是公有属性
        obj.age = -3;
        console.log(obj.age);
```

### 15.静态属性/静态方法

```javascript
     /*
        1.在JavaScript中属性和方法分类两类
        1.1实例属性/实例方法
        在企业开发中通过实例对象访问的属性, 我们就称之为实例属性
        在企业开发中通过实例对象调用的方法, 我们就称之为实例方法
        1.2静态属性/静态方法
        在企业开发中通过构造函数访问的属性, 我们就称之为静态属性
        在企业开发中通过构造函数调用的方法, 我们就称之为静态方法
        */
        function Person() {
            this.name = "lnj";
            this.say = function () {
                console.log("hello world");
            }
        }
        /*
        // 通过构造函数创建的对象, 我们称之为"实例对象"
        let obj = new Person();
        console.log(obj.name);
        obj.say();

        obj.age = 34;
        console.log(obj.age);
        obj.eat = function () {
            console.log("eat");
        }
        obj.eat();
        */

        // 构造函数也是一个"对象", 所以我们也可以给构造函数动态添加属性和方法
        Person.num = 666;
        Person.run = function () {
            console.log("run");
        }
        console.log(Person.num);
        Person.run();
```

### 16.继承性1.0

```javascript
        function Person() {
            this.name = null;
            this.age = 0;
            this.say = function () {
                console.log(this.name, this.age);
            }
        }
        let per = new Person();
        per.name = "lnj";
        per.age = 34;
        per.say();

        // 在企业开发中如果构造函数和构造函数之间的关系是is a关系, 那么就可以使用继承来优化代码, 来减少代码的冗余度
        // 学生 is a 人 , 学生是一个人
        function Student() {
            // this.name = null;
            // this.age = 0;
            // this.say = function () {
            //     console.log(this.name, this.age);
            // }
            this.score = 0;
            this.study = function () {
                console.log("day day up");
            }
        }
        Student.prototype = new Person();
        Student.prototype.constructor = Student;

        let stu = new Student();
        stu.name = "zs";
        stu.age = 18;
        stu.score = 99;
        stu.say();
        stu.study();


//弊端
//破坏原有原型链关系
//子类实例化对象时没法为（存在于父类不存在于子类的属性赋值），只能等实例化对象完后通过原型链赋值
```

### 17.bind/call/apply方法

```javascript
     /*
        1.this是什么?
        谁调用当前函数或者方法, this就是谁
        */

        /*
        2.这三个方法的作用是什么?
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
        */
        let obj = {
            name: "zs"
        }
        /*
        // function test(a, b) {
        //     console.log(a, b);
        //     console.log(this);
        // }
        // test(10, 20);
        // window.test();
        // let fn = test.bind(obj, 10, 20);
        // fn();

        // test.call(obj, 10, 20);

        // test.apply(obj, [10, 20]);
        */

        function Person() {
            this.name = "lnj";
            this.say = function () {
                console.log(this);
            }
        }
        let p = new Person();
        // p.say();
        // let fn = p.say.bind(obj);
        // fn();
        // p.say.call(obj);
        p.say.apply(obj);
```

### 18.继承性2.0 

```javascript
      function Person(myName, myAge) {
            // let per = new Object();
            // let this = per;
            // this = stu;
            this.name = myName; // stu.name = myName;
            this.age = myAge; // stu.age = myAge;
            this.say = function () { // stu.say = function () {}
                console.log(this.name, this.age);
            }
            // return this;
        }
        function Student(myName, myAge, myScore) {
            // let stu = new Object();
            // let this = stu;
            Person.call(this, myName, myAge); //  Person.call(stu);
            this.score = myScore;
            this.study = function () {
                console.log("day day up");
            }
            // return this;
        }
        let stu = new Student("ww", 19, 99);
        // stu.name = "zs";
        // stu.age = 18;
        // stu.score = 99;
        console.log(stu.score);
        stu.say();
        stu.study();

//弊端
//假如say方法存在于Person的原型对象，不存在于Person，那么它就找不到say方法，得修改原型链
```

### 19.继承性3.0

```javascript
        function Person(myName, myAge) {
            // let per = new Object();
            // let this = per;
            // this = stu;
            this.name = myName; // stu.name = myName;
            this.age = myAge; // stu.age = myAge;
            // this.say = function () { // stu.say = function () {}
            //     console.log(this.name, this.age);
            // }
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
        // 注意点: 要想使用Person原型对象中的属性和方法, 那么就必须将Student的原型对象改为Person的原型对象才可以
        Student.prototype = Person.prototype;
        Student.prototype.constructor = Student;
		//重点

        let stu = new Student("ww", 19, 99);
        console.log(stu.score);
        stu.say();
        stu.study();

		//弊端
		//破坏了原有的原型链关系，严重破环了Person原型
```

### 20.继承性专业写法

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


        1.js中继承的终极方法！！！！！！！！！！！！1
        1.1在子类的构造函数中通过call借助父类的构造函数
        1.2将子类的原型对象修改为父类的实例对象
   
        // let stu = new Student("ww", 19, 99);
        // console.log(stu.score);
        // stu.say();
        // stu.study();
```

![批注 2020-11-22 154211](C:\Users\阔乐c\Desktop\批注 2020-11-22 154211.png)

### 21.ES6类和对象

```javascript
2.从ES6开始系统提供了一个名称叫做class的关键字, 这个关键字就是专门用于定义类的
        class Person{
            // 当我们通过new创建对象的时候, 系统会自动调用constructor
            // constructor我们称之为构造函数
			//ES6中定义实例属性必须写在constructor中
            constructor(myName, myAge){
                this.name = myName;
                this.age = myAge;
            }
            // 实例属性 错误写法
            // name = "lnj";
            // age = 34;

            // 实例方法 写在constructor外会被添加到原型中 不想的话就写在constructor里面
            say(){
                console.log(this.name, this.age);
            }
            // 静态属性 错误写法
            //static num = 666;
            
            // 静态方法
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

### 22.ES6继承

```javascript
		// ES6开始的继承
        class Person{
            constructor(myName, myAge){
                // this = stu;
                this.name = myName; // stu.name = myName;
                this.age = myAge; // stu.age = myAge;
            }
            say(){
                console.log(this.name, this.age);
            }
        }
        /*
        1.在ES6中如何继承
        1.1在子类后面添加extends并指定父类的名称
        1.2在子类的constructor构造函数中通过super方法借助父类的构造函数
        */
        // 以下代码的含义: 告诉浏览器将来Student这个类需要继承于Person这个类
        class Student extends Person{
            constructor(myName, myAge, myScore){
                // 1.在子类中通过call/apply方法借助父类的构造函数
                // Person.call(this, myName, myAge);
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

### 23.获取对象类型

```javascript
 /*
        let obj = new Object();  --> object
        let arr = new Array(); --> Array
        let p = new Person(); --> Person
        */
        let obj = new Object();
        console.log(typeof obj); // object

        let arr = new Array();
        // console.log(typeof arr); // object
        console.log(arr.constructor.name); // Array


        function Person() {
            // let obj = new Object();
            // let this = obj;
            this.name = "lnj";
            this.age = 34;
            this.say = function () {
                console.log(this.name, this.age);
            }
            // return this;
        }
        let p = new Person();
        // console.log(typeof p); // object
        console.log(p.constructor.name); // Person
```

### 24.instanceof关键字

```javascript
		/*
        1.什么是instanceof关键字?
        instanceof用于判断 "对象" 是否是指定构造函数的 "实例"
        */
        /*
        2.instanceof注意点
        只要 构造函数的原型对象出现在实例对象的原型链中都会返回true
        */

        /*
        class Person{
            name = "lnj";
        }
        let p = new Person();
        console.log(p instanceof Person); // true

        class Cat{
            name = "mm";
        }
        let c = new Cat();
        console.log(c instanceof Person); // false
        */

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
        console.log(stu instanceof Person); // true
```

### 25.isPrototype

```javascript
 /*
        1.什么是isPrototypeOf属性
        isPrototypeOf用于判断 一个对象是否是另一个对象的原型
        */
        /*
        2.isPrototypeOf注意点
        2.1只要调用者在传入对象的原型链上都会返回true
        */

        /*
        class Person{
            name = "lnj";
        }
        let  p = new Person();
        console.log(Person.prototype.isPrototypeOf(p)); // true

        class Cat{
            name = "mm";
        }
        console.log(Cat.prototype.isPrototypeOf(p)); // false
        */

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
		//只要实例对象在这个原型链中,都返回true
```

![批注 2020-11-22 173308](C:\Users\阔乐c\Desktop\批注 2020-11-22 173308.png)

### 26.判断对象属性

```javascript
      // 需求: 判断某一个对象是否拥有某一个属性
        class Person{
            name = null;
            age = 0;
        }
        Person.prototype.height = 0;
        /*
        let p = new Person();
        // in的特点: 只要类中或者原型对象中有, 就会返回true
        console.log("name" in p); // true
        console.log("width" in p); // false
        console.log("height" in p); // true
        */

        // 需求: 判断某一个对象自身是否拥有某一个属性
        let p = new Person();
        // 特点: 只会去类中查找有没有, 不会去原型对象中查找
        console.log(p.hasOwnProperty("name")); // true
        console.log(p.hasOwnProperty("height")); // false
```

### 27.对象增删改查

```javascript
 class Person{}
        let p = new Person();
        // 增加(C)
        // p.name = "lnj";
        p["name"] = "zs";
        // p.say = function(){
        //     console.log("hello world");
        // }
        p["say"] = function(){
            console.log("hello world");
        }
        // console.log(p);

        // 删除(R)
        // delete p.name;
        // delete p["name"];
        // delete p.say;
        // delete p["say"];
        // console.log(p);

        // 修改(U)
        // p.name = "lnj";
        // p["name"] = "ww";
        // console.log(p.name);
        // p.say = function(){
        //     console.log("hi");
        // }
        // p["say"] = function(){
        //     console.log("hi");
        // }
        // p.say();

        // 查询(D)
        // console.log(p.name);
        // console.log(p["name"]);
        p.say();
```

### 28.对象遍历

```javascript
如何遍历一个对象?
        在JS中可以通过高级for循环来遍历对象
        以下代码的含义: 将指定对象中所有的属性和方法的名称取出来了依次的赋值给key这个变量
        for(let key in obj){}

        class Person{
            constructor(myName, myAge){
                this.name = myName;
                this.age = myAge;
            }
            // 注意点: ES6定义类的格式, 会将方法默认放到原型对象中
            say(){
                console.log(this.name, this.age);
            }
        }

        function Person(myName, myAge){
            this.name = myName;
            this.age = myAge;
            this.say = function(){
                console.log(this.name, this.age);
            }
        }
        let p = new Person("LNJ", 34);
        console.log(p);
        for(let key in p){
            if(p[key] instanceof Function){
                continue;
            }
            // console.log(key); // name / age / say
            // 注意点: 以下代码的含义:取出p对象中名称叫做当前遍历到的名称的属性或者方法的取值
            console.log(p[key]); // p["name"] / p["age"] / p["say"]
            // 注意点: 以下代码的含义:取出p对象中名称叫做key的属性的取值
            // console.log(p.key); // undefined
        }
```

### 29.对象解构赋值

```javascript
 /*
        注意点:
        对象的解构赋值和数组的解构赋值 除了符号不一样, 其它的一模一样
        数组解构使用[]
        对象解构使用{}
        */
        /*
        // 1.在数组的解构赋值中, 等号左边的格式必须和等号右边的格式一模一样, 才能完全解构
        let [a, b, c] = [1, 3, 5];
        console.log(a, b, c); // 1 3 5

        // 2.在数组的解构赋值中, 两边的个数可以不一样
        let [a, b] = [1, 3, 5];
        console.log(a, b); // 1 3
        let [a, b, c] = [1, 3];
        console.log(a, b, c); // 1 3 undefined

        // 3.在数组的解构赋值中,如果右边少于左边, 我们可以给左边指定默认值
        let [a, b, c = 666] = [1, 3];
        console.log(a, b, c); // 1 3 666
        */

        // let obj = {
        //     name: "lnj",
        //     age: 34
        // }
        // let name = obj.name;
        // let age = obj.age;
        // let {name, age} = obj;
        // let {name, age} = {name: "lnj",age: 34};
        // console.log(name, age);

        // let {name} = {name: "lnj",age: 34};
        // console.log(name);

        // let {name, age, height} = {name: "lnj",age: 34};
        // console.log(name, age, height);

        // let {name, age, height = 1.80} = {name: "lnj",age: 34};
        // console.log(name, age, height);
		
        // 注意点: 在对象解构赋值中, 左边的变量名称必须和对象的属性名称一致, 才能解构出数据
        // let {a, b} = {name: "lnj",age: 34};
        // console.log(a, b); // undefined undefined

        let {age} = {name: "lnj",age: 34};
        console.log(age); // 34




		//应用场景
        let arr = [1, 3];
        // function sum(a, b) {
        function sum([a, b]) {
            return a + b;
        }
        // let res = sum(arr[0], arr[1]);
        let res = sum(arr);
        console.log(res);
        */
        let obj = {
            name: "lnj",
            age: 34
        }
        // function say(name, age) {
        function say({name, age}) {
            console.log(name, age);
        }
        // say(obj.name, obj.age);
        say(obj);
```

### 30.深拷贝和浅拷贝

```javascript
/*
        1.什么是深拷贝什么是浅拷贝?
        1.1深拷贝
        修改新变量的值不会影响原有变量的值
        默认情况下基本数据类型都是深拷贝

        1.1浅拷贝
        修改新变量的值会影响原有的变量的值
        默认情况下引用类型都是浅拷贝
        */
        // 深拷贝
        /*
        let num1 = 123;
        let num2 = num1;
        num2 = 666; // 修改形变量的值
        console.log(num1);
        console.log(num2);
        */

        // 浅拷贝
        class Person{
            name = "lnj";
            age = 34;
        }
        let p1 = new Person();
        let p2 = p1;
        p2.name = "zs"; // 修改变量的值
        console.log(p1.name);
        console.log(p2.name);
```

### 31.对象的深拷贝

```javascript
 		class Person{
            name = "lnj";
            age = 34;
        }
        let p1 = new Person();
        // 浅拷贝
        // let p2 = p1;
        // p2.name = "zs"; // 修改变量的值

        // 深拷贝
        let p2 = new Object();
        // p2.name = p1.name;
        // p2.age = p1.age;
        // p2.name = "zs";

        // for(let key in p1){
        //     p2[key] = p1[key];
        // }
        // console.log(p2);
        // p2.name = "zs";

        // assign方法可以将第二个参数的对象的属性和方法拷贝到第一个参数的对象中
        Object.assign(p2, p1);
        // console.log(p2);
        p2.name = "zs";
        console.log(p1.name);
        console.log(p2.name);
        // 注意点: 只有被拷贝对象中所有属性都是基本数据类型, 以上代码才是深拷贝
      	// 注意点: 只有被拷贝对象中所有属性都是基本数据类型, 以上代码才是深拷贝


		
```

### 32.自定义函数实现对象的深拷贝(难)

```javascript
 class Person{
            name = "lnj";
            cat = {
                age : 3
            };
            scores = [1, 3, 5];
        }
        let p1 = new Person();
        let p2 = new Object();
        /*

        // p2.name = p1.name;
        // p2.name = "zs";
        // console.log(p1.name);
        // console.log(p2.name);
        p2.cat = p1.cat;
        p2.cat.age = 666;
        console.log(p1.cat.age);
        console.log(p2.cat.age);
        */

        depCopy(p2, p1);
        // console.log(p2);

        p2.cat.age = 666;
        console.log(p1.cat.age);
        console.log(p2.cat.age);

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
```

### 33.数组高级API上

```javascript
		// 利用forin循环来遍历数组
        /*
        // 注意点: 在企业开发中不推荐使用forin循环来遍历数组
        // https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in
        // for(let key in arr){
        //     // console.log(key);
        //     console.log(arr[key]);
        // }

        function Person() {
            this.name = "lnj";
            this.age = 34;
            this.score = 99;
        }
        // 注意点: 对象中的属性是无序的
        // forin循环是专门用于遍历对象的, 但是对象的属性是无序的, 所以forin循环就是专门用于遍历无序的东西的, 所以不推荐使用forin循环来遍历数组
        let p = new Person();
        console.log(p);
        */

        // 3.利用ES6中推出的for of循环来遍历数组
        // for(let value of arr){
        //     console.log(value);
        // }

        // 4.还可以利用Array对象的forEach方法来遍历数组
        /*
        // forEach方法会自动调用传入的函数
        // 每次调用都会将当前遍历到的元素和当前遍历到的索引和当前被遍历的数组传递给这个函数
        arr.forEach(function (currentValue, currentIndex, currentArray) {
            // console.log(currentValue, currentIndex, currentArray);
            console.log(currentValue);
        });
        */
        Array.prototype.myForEach = function (fn) {
            // this === [1, 3, 5, 7, 9]
            for(let i = 0; i < this.length; i++){
                fn(this[i], i, this);
            }
        };
        arr.myForEach(function (currentValue, currentIndex, currentArray) {
            console.log(currentValue, currentIndex, currentArray);
        });




		//         0  1  2  3  4
        let arr = [3, 2, 6, 7, 6];
        /*
        // 从左往右查找, 找到返回索引, 找不到返回-1
        let index1 = arr.indexOf(6);
        console.log(index1); // 2
        // 从右至左查找, 找到返回索引, 找不到返回-1
        let index2 = arr.lastIndexOf(6);
        console.log(index2); // 4
        // 从左往右查找, 找到返回true, 找不到返回false
        let result = arr.includes(6);
        console.log(result); // true
        */
        // 1.数组的findIndex方法
        // findIndex方法: 定制版的indexOf, 找到返回索引, 找不到返回-1
        /*
        let index = arr.findIndex(function (currentValue, currentIndex, currentArray) {
            // console.log(currentValue, currentIndex, currentArray);
            // if(currentValue === 6){
            if(currentValue === 10){
                return true;
            }
        });
        console.log(index);
        */
        // 2.数组的find方法
        // findIndex方法返回索引, find方法返回找到的元素
        // find方法如果找到了就返回找到的元素, 如果找不到就返回undefined
        let value = arr.find(function (currentValue, currentIndex, currentArray) {
            // console.log(currentValue, currentIndex, currentArray);
            // if(currentValue === 6){
            if(currentValue === 10){
                return true;
            }
        });
        console.log(value);

        // findIndex实现
        Array.prototype.myFindIndex = function (fn) {
            for(let i = 0; i < this.length; i++){
                let result = fn(this[i], i, this);
                if(result){
                    return i;
                }
            }
            return -1;
        }

        // findIndex实现
        Array.prototype.myFind = function (fn) {
            for(let i = 0; i < this.length; i++){
                let result = fn(this[i], i, this);
                if(result !== undefined){
                    return result;
                }
            }
            return undefined;
        }
```

### 34.数组高级API下

```javascript
 		//      0  1  2  3  4
        let arr = [1, 2, 3, 4, 5];
        // 1.数组的filter方法:
        // 将满足条件的元素添加到一个新的数组中
     
        let newArray = arr.filter(function (currentValue, currentIndex, currentArray) {
            // console.log(currentValue, currentIndex, currentArray);
            if(currentValue % 2 === 0){
                return true;
            }
        });
        console.log(newArray); // [2, 4]
      

        // 2.数组的map方法:
        // 将满足条件的元素映射到一个新的数组中
        /*
        let newArray = arr.map(function (currentValue, currentIndex, currentArray) {
            // console.log(currentValue, currentIndex, currentArray);
            if(currentValue % 2 === 0){
                return currentValue;
            }
        });
        console.log(newArray); // [undefined, 2, undefined, 4, undefined]
        */

        // filter实现
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

        // map实现
        Array.prototype.myMap = function (fn) {
            let newArray = new Array(this.length);
            newArray.fill(undefined);
            for(let i = 0; i < this.length; i++){
                let result = fn(this[i], i, this);
                if(result !== undefined){
                    newArray[i] = result;
                }
            }
            return newArray;
        }
```

### 35.删除数组元素

```javascript
		let arr = [1, 2, 3, 4, 5];

        // 需求: 遍历的同时删除数组中所有元素
        // arr.splice(2, 1);
        // delete arr[2];
        console.log(arr);
        /*
        //       0     0 < 5
        //       1     1 < 4
        //       2     2 < 3
        //       3     3 < 2
        // for(let i = 0; i < arr.length; i++){
        let len = arr.length;
        // for(let i = 0; i < len; i++){
        for(let i = len - 1; i >= 0; i--){
            // console.log(arr.length); // 5, 4, 3
            // console.log(len);
            arr.splice(i, 1);
        }
        */
        for(let i = 0; i < arr.length; i++){
            console.log(arr.length);
            // 注意点: 通过delete来删除数组中的元素, 数组的length属性不会发生变化
            delete arr[i];
        }
        console.log(arr);
```

### 36.数组排序方法

```javascript
// let arr = ["c", "a", "b"];
        // arr.sort();
        /*
        如果 compareFunction(a, b) 小于 0 ，那么 a 会被排列到 b 之前；
        如果 compareFunction(a, b) 等于 0 ， a 和 b 的相对位置不变。
        如果 compareFunction(a, b) 大于 0 ， b 会被排列到 a 之前
        注意点: 如果元素是字符串类型, 那么比较的是字符串的Unicode编码
        */
        /*
        arr.sort(function (a, b) {
            if(a > b){
                return -1;
            }else if(a < b){
                return 1;
            }else{
                return 0;
            }
        });
        console.log(arr);
        */

        /*
        let arr = [3, 4, 2, 5, 1];
        // arr.sort();
        arr.sort(function (a, b) {
            // if(a > b){
            //     return -1;
            // }else if(a < b){
            //     return 1;
            // }else{
            //     return 0;
            // }
            // 规律: 如果数组中的元素是数值类型
            //       如果需要升序排序, 那么就返回a - b;
            //       如果需要降序排序, 那么就返回b - a;
            // return a - b;
            return b - a;
        });
        console.log(arr);
        */

        /*
        let arr = ["1234", "21", "54321", "123", "6"];
        arr.sort(function (str1, str2) {
            // return str1.length - str2.length;
            return str2.length - str1.length;
        });
        console.log(arr);
        */

        let students = [
            {name: "zs", age: 34},
            {name: "ls", age: 18},
            {name: "ww", age: 22},
            {name: "mm", age: 28},
        ];
        students.sort(function (o1, o2) {
            // return o1.age - o2.age;
            return o2.age - o1.age;
        });
        console.log(students);		
```

### 37.字符串常用方法上

```javascript
*
        在js中字符串可以看做一个特殊的数组, 所以大部分数组的属性/方法字符串都可以使用
        */
        // 1.获取字符串长度  .length
        // let str = "abcd";
        // console.log(str.length);

        // 2.获取某个字符 [索引] / charAt
        // let str = "abcd";
        // let ch = str[1];
        // let ch = str.charAt(1);
        // console.log(ch);

        // 3.字符串查找 indexOf / lastIndexOf / includes
        // let str = "vavcd";
        // let index = str.indexOf("v");
        // let index = str.lastIndexOf("v");
        // console.log(index);
        // let result = str.includes("p");
        // console.log(result);

        // 4.拼接字符串 concat / +
        // let str1 = "www";
        // let str2 = "it666";
        // let str = str1 + str2; // 推荐
        // let str = str1.concat(str2);
        // console.log(str);

        // 5.截取子串 slice / substring / substr
        let str = "abcdef";
        // let subStr = str.slice(1, 3);
        // let subStr = str.substring(1, 3);
        let subStr = str.substr(1, 3);
        console.log(subStr);
```

### 38.字符串常用方法-ES6

```javascript
 // 1.字符串切割
       // let arr = [1, 3, 5];
       // let str = arr.join("-");
       //  console.log(str);
       //  let str = "1-3-5";
       //  let arr = str.split("-");
       //  console.log(arr);

        // 2.判断是否以指定字符串开头 ES6
        // let str = "http://www.it666.com";
        // let result = str.startsWith("www");
        // console.log(result);


        // 3.判断是否以指定字符串结尾 ES6
        // let str = "lnj.jpg";
        // let result = str.endsWith("png");
        // console.log(result);


        // 4.字符串模板 ES6
        // let str = "";
        // let str = '';
        // let str = `www.it666.com`;
        // console.log(str);
        // console.log(typeof str);

        // let str =   "<ul>\n" +
        //             "    <li>我是第1个li</li>\n" +
        //             "    <li>我是第2个li</li>\n" +
        //             "    <li>我是第3个li</li>\n" +
        //             "</ul>";

        // let str = `<ul>
        //                 <li>我是第1个li</li>
        //                 <li>我是第2个li</li>
        //                 <li>我是第3个li</li>
        //             </ul>`;

        let name = "lnj";
        let age = 34;
        // let str = "我的名字是" + name + ",我的年龄是" + age;
        let str = `我的名字是${name},我的年龄是${age}`;
        console.log(str);
```

### 39.基本数据类型和包装类型

```javascript
  /*
        1.有哪些基本数据类型?
        字符串类型 / 数值类型 / 布尔类型 / 空类型 / 未定义类型

        2.通过字面量创建的基本数据类型的数据都是常量

        3.常量的特点和注意点
        常量是不能被修改的
        每次修改或者拼接都是生成一个新的
        */
        /*
        4.基本类型特点
        没有属性和方法

        5.对象类型的特点
        有属性和方法

        6.以前之所以能够访问基本数据类型的属性和方法, 是因为
        在运行的时候系统自动将基本数据类型包装成了对象类型
        String() / Number() / Boolean()
        */
        /*
        let str = "abc";
        // str[1] = "m";
        let newStr = str.replace("b", "m");
        console.log(str); // abc
        console.log(newStr); // amc
        */
        /*
        let str1 = "www";
        let str2 = "it666";
        let str3 = str1 + str2;
        console.log(str1);
        console.log(str2);
        console.log(str3);
        */

        /*
        let str = "lnj";
        str.age = 34;
        str.say = function () {
            console.log("hello");
        }
        console.log(str.age); // undefined
        str.say(); // str.say is not a function
        */
        let str = "www.it666.com";
        // let str = new String(str);
        console.log(str.length);
        str.split(".");
```

### 40.三大对象

```javascript

        JavaScript中提供三种自带的对象, 分别是"本地对象"/"内置对象"/"宿主对象"

        什么是宿主?
        宿主就是指JavaScript运行环境, js可以在浏览器中运行, 也可以在服务器上运行(nodejs)
        */
        /*
        1.本地对象
        与宿主无关，无论在浏览器还是服务器中都有的对象
        就是ECMAScript标准中定义的类(构造函数)。
        在使用过程中需要我们手动new创建
        例如：Boolean、Number、String、Array、Function、Object、Date、RegExp等。

        2.内置对象
        与宿主无关，无论在浏览器还是服务器中都有的对象
        ECMAScript已经帮我们创建好的对象。
        在使用过程中无需我们手动new创建
        例如：Global、Math、JSON

        3.宿主对象
        对于嵌入到网页中的JS来说，其宿主对象就是浏览器, 所以宿主对象就是浏览器提供的对象
        包含: Window和Document等。
        所有的DOM和BOM对象都属于宿主对象。

        ----------------------------------------------------------------------------------------
        4.自定义对象
        我们自己编写的类创建的对象
```

### 41.内置对象Math

```javascript
 /*
        Math.floor()    向下取整
        Math.ceil()     向上取整
        Math.round()    四舍五入
        Math.abs()      绝对值
        Math.random()   生成随机数
        */
        /*
        // Math.floor()    向下取整
        // 直接砍掉所有的小数位就是向下取整
        // let num = 3.9;
        // let value = Math.floor(num);
        // console.log(value);
        // Math.ceil()     向上取整
        // 只要有小数位就会给整数位+1, 然后砍掉所有小数位
        // let num = 3.9;
        // let value = Math.ceil(num);
        // console.log(value);
        // Math.round()    四舍五入
        // 和小学数学一样, 如果小数位满5就会进1
        // let num = 3.5;
        // let value = Math.round(num);
        // console.log(value);
        // Math.abs()      绝对值
        // 和小学数学一样, 统一变为正数
        // let num = -3;
        // let value = Math.abs(num);
        // console.log(value);
        */

        // 会生成一个0~1的随机数, 但是不包括1
        // let value = Math.random();
        // console.log(value);

        // 需求: 要求生成一个1~10的随机数
        function getRandomIntInclusive(min, max) {
            min = Math.ceil(min);
            max = Math.floor(max);
            return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值
        }
        let value = getRandomIntInclusive(1, 10);
        console.log(value);
```

### 42.函数节流和防抖

![批注 2021-03-14 094550](Javascript.assets/%E6%89%B9%E6%B3%A8%202021-03-14%20094550-1615686373559.png)

### 43.闭包 

```javascript
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
let counter2 = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1

alert( counter2() ); // ?
alert( counter2() ); // ?




function makeArmy() {
  ...
  let i = 0;
  while (i < 10) {
    let shooter = function() { // shooter 函数
      alert( i ); // 应该显示它自己的编号
    };
    shooters.push(shooter); // 将 shooter 函数添加到该数组中
      i++;
  }
  ...
}
```

### 44.基本类型按值传递，引用类型按共享传递

```javascript
var person = {name: "MJ"};
function foo(obj) {
  obj = new Object(); // 修改部分
  obj.name = "EP";
}
foo(person);
console.log(person.name); 

我们都知道对象保存在堆中，person持有堆中对象的引用，在调用foo函数时，函数接收的实际是person持有的对象（下面称之为原对象）引用的副本，这样obj和person都指向了同一个地方（也就是原对象在堆中存放的地址），而函数中的obj = new Object()操作其实是在堆中创建了一个新对象，并让obj持有该对象的引用，这样obj与原对象之间的关系就断开了，转而与新对象建立了关系，所以对obj的修改并不会影响到原对象。

调用函数传参时，函数接受对象实参引用的副本(既不是按值传递的对象副本，也不是按引用传递的隐式引用)

新开辟一块内存，把对象的引用赋值给它

function sum(a) {

  return function(b) {
    return a + b; // 从外部词法环境获得 "a"
  };

}

alert( sum(1)(2) ); // 3
alert( sum(5)(-1) ); // 4
```

![微信图片_20210322215918](Javascript.assets/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20210322215918.png)

### 45.预解析

```javascript
1.什么是预解析?
    浏览器在执行JS代码的时候会分成两部分操作：预解析以及逐行执行代码
也就是说浏览器不会直接执行代码, 而是加工处理之后再执行,
    这个加工处理的过程, 我们就称之为预解析

2.预解析规则
2.1将变量声明和函数声明提升到当前作用域最前面
2.2将剩余代码按照书写顺序依次放到后面

3.注意点
通过let定义的变量不会被提升(不会被预解析)

      // 下列程序的执行结果是什么?
        var a = 666;
        test();
        function test() {
            var b = 777;
            console.log(a);
            console.log(b);
            console.log(c);
            var a = 888;
            let c = 999;
        }
        /*
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




let x = 1;

function func() {
  console.log(x); // ReferenceError: Cannot access 'x' before initialization
  let x = 2;
}

func();
```

### 46.call/apply

```javascript
call 和 apply 的共同点
它们的共同点是，都能够改变函数执行时的上下文，将一个对象的方法交给另一个对象来执行，并且是立即执行的。

call 的写法	
    Function.call(obj,[param1[,param2[,…[,paramN]]]])
    需要注意以下几点：
    调用 call 的对象，必须是个函数 Function。
    call 的第一个参数，是一个对象。 Function 的调用者，将会指向这个对象。如果不传，则默认为全局对象 window。
    第二个参数开始，可以接收任意个参数。每个参数会映射到相应位置的 Function 的参数上。但是如果将所有的参数作为数组传入，它们会作为一个整体映射到 Function 对应的第一个参数上，之后参数都为空。
    function func (a,b,c) {}

    func.call(obj, 1,2,3)
    // func 接收到的参数实际上是 1,2,3

    func.call(obj, [1,2,3])
    // func 接收到的参数实际上是 [1,2,3],undefined,undefined




Function.apply(obj[,argArray])
    需要注意的是：
    它的调用者必须是函数 Function，并且只接收两个参数，第一个参数的规则与 call 一致。
    第二个参数，必须是数组或者类数组，它们会被转换成类数组，传入 Function 中，并且会被映射到 Function 对应的参数上。这也是 call 和 apply 之间，很重要的一个区别。
    func.apply(obj, [1,2,3])
    // func 接收到的参数实际上是 1,2,3

    func.apply(obj, {
        0: 1,
        1: 2,
        2: 3,
        length: 3
    })
    // func 接收到的参数实际上是 1,2,3


有两种情况需要注意，传null或undefined时，将是JS执行环境的全局变量。浏览器中是window，其它环境（如node）则是global
apply 的一些妙用
    1、Math.max。用它来获取数组中最大的一项。

    let max = Math.max.apply(null, array);
    同理，要获取数组中最小的一项，可以这样：

    let min = Math.msn.apply(null, array);
    2、实现两个数组合并。在 ES6 的扩展运算符出现之前，我们可以用 Array.prototype.push来实现。

    let arr1 = [1, 2, 3];
    let arr2 = [4, 5, 6];

    Array.prototype.push.apply(arr1, arr2);
    console.log(arr1); // [1, 2, 3, 4, 5, 6]
```

### 47.Promise

```
由 new Promise 构造器返回的 promise 对象具有以下内部属性：

state — 最初是 "pending"，然后在 resolve 被调用时变为 "fulfilled"，或者在 reject 被调用时变为 "rejected"。
result — 最初是 undefined，然后在 resolve(value) 被调用时变为 value，或者在 reject(error) 被调用时变为 error。
```

### 48.执行上下文

```
	全局执行上下文 — 这是默认或者说基础的上下文，任何不在函数内部的代码都在全局上下文中。它会执行两件事：创建一个全局的 window 对象（浏览器的情况下），并且设置 this 的值等于这个全局对象。一个程序中只会有一个全局执行上下文。
	函数执行上下文 — 每当一个函数被调用时, 都会为该函数创建一个新的上下文。每个函数都有它自己的执行上下文，不过是在函数被调用时创建的。函数上下文可以有任意多个。每当一个新的执行上下文被创建，它会按定义的顺序（将在后文讨论）执行一系列步骤。
	Eval 函数执行上下文 — 执行在 eval 函数内部的代码也会有它属于自己的执行上下文，但由于 JavaScript 开发者并不经常使用 eval，所以在这里我不会讨论它。
```

https://i0.hdslb.com/bfs/article/f6d3c8eca3baa4ca211efa8d3b77bdf13247e277.png@1320w_584h.webp
https://i0.hdslb.com/bfs/article/d9ec8706ee606831803506300ef4c0ebb042b783.png@1320w_640h.webp

### 49.

```javascript

```

