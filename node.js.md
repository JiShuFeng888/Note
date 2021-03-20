### 1.NodeJS基础

```javascript
1.Node环境和浏览器环境区别
NodeJS环境和浏览器环境一样都是一个JS的运行环境, 都可以执行JS代码.
但是由于宿主不同所以特点也有所不同

1.1内置对象不同
- 浏览器环境中提供了window全局对象
- NodeJS环境中的全局对象不叫window, 叫global

1.2this默认指向不同
- 浏览器环境中全局this默认指向window
- NodeJS环境中全局this默认指向空对象{}

1.3API不同
- 浏览器环境中提供了操作节点的DOM相关API和操作浏览器的BOM相关API
- NodeJS环境中没有HTML节点也没有浏览器, 所以NodeJS环境中没有DOM/BOM


```

### 2.NodeJS全局属性和方法

```javascript
1.和浏览器一样Node环境中的全局对象也提供了很多方法属性供我们使用
中文文档地址: http://nodejs.cn/api/

__dirname: 当前文件所在文件夹的绝对路径
__filename: 当前文件的绝对路径
setInterval / clearInterval : 和浏览器中window对象上的定时器一样
setTimeout /  clearTimeout : 和浏览器中window对象上的定时器一样
console :  和浏览器中window对象上的打印函数一样
```

### 3.NodeJS模块

```javascript
1.什么是模块?
1.1浏览器开发中的模块
   在浏览器开发中为了避免命名冲突, 方便维护等等
   我们采用类或者立即执行函数的方式来封装JS代码, 来避免命名冲突和提升代码的维护性
   其实这里的一个类或者一个立即执行函数就是浏览器开发中一个模块
   let obj = {
       模块中的业务逻辑代码
   };
   ;(function(){
      模块中的业务逻辑代码
      window.xxx = xxx;
   })();
存在的问题:
没有标准没有规范

1.2NodeJS开发中的模块
   NodeJS采用CommonJS规范实现了模块系统

1.3CommonJS规范
CommonJS规范规定了如何定义一个模块, 如何暴露(导出)模块中的变量函数, 以及如何使用定义好的模块

- 在CommonJS规范中一个文件就是一个模块
- 在CommonJS规范中每个文件中的变量函数都是私有的，对其他文件不可见的
- 在CommonJS规范中每个文件中的变量函数必须通过exports暴露(导出)之后其它文件才可以使用
- 在CommonJS规范中想要使用其它文件暴露的变量函数必须通过require()导入模块才可以使用



let name = "it666.com";

function sum(a, b) {
    return a + b;
}

// exports.str = name;
// exports.fn = sum;

// module.exports.str = name;
// module.exports.fn = sum;

global.str = name;
global.fn = sum;








let aModule = require("./07-a");

// console.log(aModule);
// console.log(aModule.str);

// let res = aModule.fn(10, 20);
// console.log(res);

console.log(str);
let res = fn(10, 20);
console.log(res);





1.exports和module.exports区别
exports只能通过 exports.xxx方式导出数据, 不能直接赋值
module.exports既可以通过module.exports.xxx方式导出数据, 也可以直接赋值

注意点:
在企业开发中无论哪种方式都不要直接赋值, 这个问题只会在面试中出现
```

### 4.require注意点

```javascript
1.1require导入模块时可以不添加导入模块的类型
如果没有指定导入模块的类型, 那么会依次查找.js .json .node文件
无论是三种类型中的哪一种, 导入之后都会转换成JS对象返回给我们

1.2导入自定义模块时必须指定路径
require可以导入"自定义模块(文件模块)"、"系统模块(核心模块)"、"第三方模块"
导入"自定义模块"模块时前面必须加上路径//!!!
 let aModule = require("./09-a.js");
//let aModule = require("09-a.js");错
导入"系统模块"和"第三方模块"是不用添加路径

1.3导入"系统模块"和"第三方模块"是不用添加路径的原因
如果是"系统模块"直接到环境变量配置的路径中查找
如果是"第三方模块"会按照module.paths数组中的路径依次查找
```

### 5.NPM

```javascript
1.什么是包?
前面说过在编写代码的时候尽量遵守单一原则,
也就是一个函数尽量只做一件事情
例如: 读取数据函数/写入数据函数/生成随机数函数等等,
不要一个函数既读取数据又写入数据又生成随机数,
这样代码非常容易出错, 也非常难以维护

在模块化开发中也一样, 在一个模块(一个文件中)尽量只完成一个特定的功能
但是有些比较复杂的功能可能需要由多个模块组成,
例如: jQuery选择器相关的代码在A模块, CSS相关的代码在B模块, ...
      我们需要把这些模块组合在一起才是完成的jQuery
那么这个时候我们就需要一个东西来维护多个模块之间的关系
这个维护多个模块之间关系的东西就是"包"

简而言之: 一个模块是一个单独的文件, 一个包中可以有一个或多个模块

2.NodeJS包的管理
在NodeJS中为了方便开发人员发布、安装和管理包, NodeJS推出了一个包管理工具
NPM(Node Package Manager)
NPM不需要我们单独安装, 只要搭建好NodeJS环境就已经自动安装好了
NPM就相当于电脑上的"QQ管家软件助手", 通过NPM我们可以快速找到我们需要的包,
可以快速安装我们需要的包, 可以快速删除我们不想要的包等等


npm config list  npm配置


 1.NPM包安装方式
    - 全局安装  (一般用于安装全局使用的工具, 存储在全局node_modules中)
    npm install -g 包名   (默认安装最新版本)
    npm uninstall -g 包名 
    npm update -g 包名   (更新失败可以直接使用install)

    - 本地安装 (一般用于安装当前项目使用的包, 存储在当前项目node_modules中)
    npm install 包名
    npm uninstall 包名
    npm update 包名

    2.初始化本地包
	在项目文件夹内打开终端输入
    npm init   ->  初始化package.json文件
    npm init -y -> 初始化package.json文件

	npm install 安装
    npm install 包名 --save 
    npm install 包名 --save-dev 

    包描述文件 package.json, 定义了当前项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。
    npm install 命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境
    注意点:package.json文件中, 不能加入任何注释

    - dependencies：生产环境包的依赖，一个关联数组，由包的名称和版本号组成
    - devDependencies：开发环境包的依赖，一个关联数组，由包的名称和版本号组成

    1.将项目拷贝给其它人, 或者发布的时候, 我们不会将node_modules也给别人, 因为太大
    2.因为有的包可能只在开发阶段需要, 但是在上线阶段不需要, 所以需要分开指定

    npm i               所有的包都会被安装
    npm i --production  只会安装dependencies中的包
    npm i --development  只会安装devDependencies中的包
```

### 6.NRM

```javascript
1.什么是nrm?
由于npm默认回去国外下载资源, 所以对于国内开发者来说下载会比较慢
所以就有人写了一个nrm工具, 允许你将资源下载地址从国外切换到国内

npm install -g nrm   安装NRM
nrm --version 查看是否安装成功
npm ls    查看允许切换的资源地址
npm use taobao  将下载地址切换到淘宝

PS:淘宝资源地址和国外的地址内容完全同步,。淘宝镜像与官方同步频率目前为 10分钟 一次以保证尽量与官方服务同步

2.什么是cnpm?
由于npm默认回去国外下载资源, 所以对于国内开发者来说下载会比较慢
cnpm 就是将下载源从国外切换到国内下载, 只不过是将所有的指令从npm变为cnpm而已

npm install cnpm -g –registry=https://registry.npm.taobao.org  安装CNPM
cnpm -v  查看是否安装成功
使用方式同npm, 例如: npm install jquery 变成cnpm install jquery 即可
```

### 7.YARN

```javascript
Yarn是由Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具
Yarn 是为了弥补 npm5.0之前 的一些缺陷而出现的

注意点:
在npm5.0之前，yarn的优势特别明显.但是现在NPM已经更新到6.9.x甚至7.x了,
随着NPM的升级NPM优化甚至超越Yarn,所以个人还是建议使用NPM

2.NPM的缺陷:
2.1npm install的时候巨慢
   npm 是按照队列执行每个 package，也就是说必须要等到当前 package 安装完成之后，才能继续后面的安装
2.2同一个项目，npm install的时候无法保持一致性
  “5.0.3”表示安装指定的5.0.3版本，
  “~5.0.3”表示安装5.0.X中最新的版本，
  “^5.0.3”表示安装5.X.X中最新的版本
2.3... ...

3.YARN优点:
3.1速度快:
    - 并行安装: 而 Yarn 是同步执行所有任务，提高了性能
    - 离线模式：如果之前已经安装过一个软件包，用Yarn再次安装时之间从缓存中获取，就不用像npm那样再从网络下载了
3.2安装版本统一：
    - 为了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号
3.3... ...

4.YARN的安装
npm install -g yarn
yarn --version

5.YARN使用
5.1初始化包
npm init -y
yarn init -y

5.2安装包
npm install xxx --save
yarn add xxx
npm install xxx --save-dev
yarn add xxx --dev

5.3移除包
npm uninstall xxx
yarn remove xxx

5.4更新包
npm update xxx
yarn upgrade xxx --latest

5.5全局安装
npm install -g xxx
npm uninstall -g xxx
npm update -g xxx

yarn global add xxx
yarn global upgrade xxx
yarn global remove xxx
```

### 8.NodeJS核心API

```javascript
0.准备知识
0.1计算机只能识别0和1(因为计算机只认识通电和断电两种状态),
0.2所有存储在计算机上的数据都是0和1组成的(数据越大0和1就越多)
0.3计算机中的度量单位
1 B(Byte字节) = 8 bit(位)
// 00000000  就是一个字节
// 111111111 也是一个字节
// 10101010  也是一个字节
// 任意8个 0或1的组合都是一个字节
1 KB = 1024 B
1 MB = 1024KB
1 GB = 1024MB

1.什么是Buffer?
Buffer是NodeJS全局对象上的一个类, 是一个专门用于存储字节数据的类
NodeJS提供了操作计算机底层API, 而计算机底层只能识别0和1,
所以就提供了一个专门用于存储字节数据的类

2.如何创建一个Buffer对象
2.1创建一个指定大小的Buffer
Buffer.alloc(size[, fill[, encoding]])

2.2根据数组/字符串创建一个Buffer对象
Buffer.from(string[, encoding])

3.Buffer对象本质
本质就是一个数组
```

### 9.Buffer实例方法

```javascript
1.将二进制数据转换成字符串
返回: <string> 转换后的字符串数据。
buf.toString();

2.往Buffer中写入数据
string <string> 要写入 buf 的字符串。
offset <integer> 开始写入 string 之前要跳过的字节数。默认值: 0。
length <integer> 要写入的字节数。默认值: buf.length - offset。
encoding <string> string 的字符编码。默认值: 'utf8'。
返回: <integer> 已写入的字节数。
buf.write(string[, offset[, length]][, encoding])

3.从指定位置截取新Buffer
start <integer> 新 Buffer 开始的位置。默认值: 0。
end <integer> 新 Buffer 结束的位置（不包含）
buf.slice([start[, end]])
```

### 10.Buffer静态方法

```a
1.检查是否支持某种编码格式
Buffer.isEncoding(encoding)

2.检查是否是Buffer类型对象
Buffer.isBuffer(obj)

3.获取Buffer实际字节长度
Buffer.byteLength(string[, encoding])
注意点: 一个汉字占用三个字节

4.合并Buffer中的数据
Buffer.concat(list[, totalLength])
```

### 11.Path

```javascript
1.路径模块(path)
封装了各种路径相关的操作
和Buffer一样,NodeJS中的路径也是一个特殊的模块
不同的是Buffer模块已经添加到Global上了, 所以不需要手动导入
而Path模块没有添加到Global上, 所以使用时需要手动导入

2.获取路径的最后一部分
path.basename(path[, ext])

3.获取路径
path.dirname(path)

4.获取扩展名称
path.extname(path)

5.判断是否是绝对路径
path.isAbsolute(path)

6.获取当前操作系统路径分隔符
path.delimiter  （windows是\ Linux是/）

7.获取当前路径环境变量分隔符
path.sep  (windows中使用; linux中使用:)
-->
<!--
1.路径的格式化处理
// path.parse()  string->obj
// path.format() obj->string

2.拼接路径
path.join([...paths])

3.规范化路径
path.normalize(path)

4.计算相对路径
path.relative(from, to)

5.解析路径
path.resolve([...paths])


// basename用于获取路径的最后一个组成部分
// let res = path.basename('/a/b/c/d/index.html');
// let res = path.basename('/a/b/c/d');
// let res = path.basename('/a/b/c/d/index.html', ".html");
// console.log(res);

// dirname用于获取路径中的目录, 也就是除了最后一个部分以外的内容
// let res = path.dirname('/a/b/c/d/index.html');
// let res = path.dirname('/a/b/c/d');
// console.log(res);

// extname用于获取路径中最后一个组成部分的扩展名
// let res = path.extname('/a/b/c/d/index.html');
// let res = path.extname('/a/b/c/d');
// console.log(res);
*/
/*
isAbsolute用于判断路径是否是一个绝对路径
注意点:
区分操作系统
在Linux操作系统中/开头就是绝对路径
在Windows操作系统中盘符开头就是绝对路径

在Linux操作系统中路径的分隔符是左斜杠 /
在Windows操作系统中路径的分隔符是右斜杠 \
* */
/*
// let res = path.isAbsolute('/a/b/c/d/index.html'); // true
// let res = path.isAbsolute('./a/b/c/d/index.html'); // false
// let res = path.isAbsolute('c:\\a\\b\\c\\d\\index.html'); // true
// let res = path.isAbsolute('a\\b\\c\\d\\index.html'); // false
// console.log(res);

// path.sep用于获取当前操作系统中路径的分隔符的
// 如果是在Linux操作系统中运行那么获取到的是 左斜杠 /
// 如果是在Windows操作系统中运行那么获取到的是 右斜杠 \
// console.log(path.sep);

// path.delimiter用于获取当前操作系统环境变量的分隔符的
// 如果是在Linux操作系统中运行那么获取到的是 :
// 如果是在Windows操作系统中运行那么获取到的是 ;
// console.log(path.delimiter);
*/

/*
path.parse(path): 用于将路径转换成对象
{
  root: '/',
  dir: '/a/b/c/d',
  base: 'index.html',
  ext: '.html',
  name: 'index'
}
path.format(pathObject): 用于将对象转换成路径
* */
/*
// let obj = path.parse("/a/b/c/d/index.html");
// console.log(obj);

let obj = {
    root: '/',
    dir: '/a/b/c/d',
    base: 'index.html',
    ext: '.html',
    name: 'index'
};
let str = path.format(obj);
console.log(str);
 */

/*
path.join([...paths]): 用于拼接路径
注意点:
如果参数中没有添加/, 那么该方法会自动添加
如果参数中有.., 那么会自动根据前面的参数生成的路径, 去到上一级路径
* */
/*
// let str = path.join("/a/b", "c"); // /a/b/c
// let str = path.join("/a/b", "/c"); // /a/b/c
// let str = path.join("/a/b", "/c", "../"); // /a/b/c --> /a/b
// let str = path.join("/a/b", "/c", "../../"); // /a/b/c --> /a
// console.log(str);
 */

/*
path.normalize(path): 用于规范化路径
* */
/*
let res = path.normalize("/a//b///c////d/////index.html");
console.log(res);
*/

/*
path.relative(from, to): 用于计算相对路径
第一个参数: /data/orandea/test/aaa
第二个参数: /data/orandea/impl/bbb

/data/orandea/test/aaa --> ../  --> /data/orandea/test
/data/orandea/test --> ../ --> /data/orandea
..\..\impl\bbb
* */
/*
let res = path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
console.log(res);
 */

/*
path.resolve([...paths]): 用于解析路径
注意点: 如果后面的参数是绝对路径, 那么前面的参数就会被忽略
* */
// let res = path.resolve('/foo/bar', './baz'); // /foo/bar/baz
// let res = path.resolve('/foo/bar', '../baz'); // /foo/baz
let res = path.resolve('/foo/bar', '/baz'); // /baz
console.log(res);

```

### 12.查看文件状态

```javascript
1.文件模块(fs)
封装了各种文件相关的操作

2.查看文件状态
fs.stat(path[, options], callback)
fs.statSync(path[, options])


let fs = require("fs");
/*
console.log("1");
fs.stat(__dirname, function (err, stats) {
    // console.log("3");
    // console.log(err);
    // birthtime: 文件的创建时间
    // mtime: 文件中内容发生变化, 文件的修改时间
    // console.log(stats);

    if(stats.isFile()){
        console.log("当前路径对应的是一个文件");
    }else if(stats.isDirectory()){
        console.log("当前路径对应的是一个文件夹");
    }
});
console.log("2");
 */

let stats = fs.statSync(__filename);
console.log(stats);
```

### 13.文件读取

```javascript
fs.readFile(path[, options], callback)
fs.readFileSync(path[, options])

注意点:
没有指定第二个参数, 默认会将读取到的数据放到Buffer中
第二个参数指定为utf8, 返回的数据就是字符串


let fs = require("fs");
let path = require("path");

// 1.拿到需要读取的文件路径
let str = path.join(__dirname, "data.txt");
console.log(str);
// 2.读取文件
/*
fs.readFile(str,"utf8", function (err, data) {
    if(err){
        throw new Error("读取文件失败");
    }
    console.log(data);
    // console.log(data.toString());
});
 */
let data = fs.readFileSync(str, "utf8");
console.log(data);
```

### 14.文件写入

```javascript
fs.writeFile(file, data[, options], callback)
fs.writeFileSync(file, data[, options])

let fs = require("fs");
let path = require("path");

// 1.拼接写入的路径
let str = path.join(__dirname, "lnj.txt");

// 2.写入数据
/*
// fs.writeFile(str, "知播渔 www.it666.com", "utf-8", function (err) {
 */
let buf = Buffer.from("www.itzb.com");
fs.writeFile(str, buf, "utf-8", function (err) {
    if(err){
        throw new Error("写入数据失败");
    }else{
        console.log("写入数据成功");
    }
});

// let res = fs.writeFileSync(str, "知播渔 www.it666.com", "utf-8");
// console.log(res);
```

### 15.追加写入

```javascript
fs.appendFile(path, data[, options], callback)
fs.appendFileSync(path, data[, options])

let fs = require("fs");
let path = require("path");

// 1.拼接写入的路径
let str = path.join(__dirname, "lnj.txt");

// 2.开始追加数据
fs.appendFile(str, "知播渔", "utf8", function (err) {
    if(err){
        throw new Error("追加数据失败");
    }else{
        console.log("追加数据成功");
    }
});

```

### 16.大文件操作-读取流和写入流

```javascript
前面讲解的关于文件写入和读取操作都是一次性将数据读入内存或者一次性写入到文件中
但是如果数据比较大, 直接将所有数据都读到内存中会导致计算机内存爆炸,卡顿,死机等
所以对于比较大的文件我们需要分批读取和写入

fs.createReadStream(path[, options])
fs.createWriteStream(path[, options])


let fs = require("fs");
let path = require("path");

/*
// 1.拼接读取的路径
let str = path.join(__dirname, "lnj.txt");
// 2.创建一个读取流
let readStream = fs.createReadStream(str, {encoding : "utf8", highWaterMark : 1});
// 3.添加事件监听
readStream.on("open", function () {
    console.log("表示数据流和文件建立关系成功");
});
readStream.on("error", function () {
    console.log("表示数据流和文件建立关系失败");
});
readStream.on("data", function (data) {
    console.log("表示通过读取流从文件中读取到了数据", data);
});
readStream.on("close", function () {
    console.log("表示数据流断开了和文件的关系, 并且数据已经读取完毕了");
});
 */

/*
// 1.拼接写入的路径
let str = path.join(__dirname, "it666.txt");
// 2.创建一个写入流
let writeStream = fs.createWriteStream(str, {encoding : "utf8"});
// 3.监听写入流的事件
writeStream.on("open", function () {
    console.log("表示数据流和文件建立关系成功");
});
writeStream.on("error", function () {
    console.log("表示数据流和文件建立关系失败");
});
writeStream.on("close", function () {
    console.log("表示数据流断开了和文件的关系");
});
let data = "www.it666.com";
let index = 0;
let timerId = setInterval(function () {
    let ch = data[index];
    index++;
    writeStream.write(ch);
    console.log("本次写入了", ch);
    if(index === data.length){
        clearInterval(timerId);
        writeStream.end();
    }
}, 1000);
*/

/*
// 1.生成读取和写入的路径
let readPath = path.join(__dirname, "test.mp4");
let writePath = path.join(__dirname, "abc.mp4");
// 2.创建一个读取流
let readStream = fs.createReadStream(readPath);
// 3.创建一个写入流
let writeStream = fs.createWriteStream(writePath);
// 4.监听读取流事件
readStream.on("open", function () {
    console.log("表示数据流和文件建立关系成功");
});
readStream.on("error", function () {
    console.log("表示数据流和文件建立关系失败");
});
readStream.on("data", function (data) {
    // console.log("表示通过读取流从文件中读取到了数据", data);
    writeStream.write(data);
});
readStream.on("close", function () {
    console.log("表示数据流断开了和文件的关系, 并且数据已经读取完毕了");
    writeStream.end();
});
// 5.监听写入流的事件
writeStream.on("open", function () {
    console.log("表示数据流和文件建立关系成功");
});
writeStream.on("error", function () {
    console.log("表示数据流和文件建立关系失败");
});
writeStream.on("close", function () {
    console.log("表示数据流断开了和文件的关系");
});
 */

// 1.生成读取和写入的路径
let readPath = path.join(__dirname, "test.mp4");
let writePath = path.join(__dirname, "abc.mp4");
// 2.创建一个读取流
let readStream = fs.createReadStream(readPath);
// 3.创建一个写入流
let writeStream = fs.createWriteStream(writePath);
// 利用读取流的管道方法来快速的实现文件拷贝
readStream.pipe(writeStream);


```

### 17.利用NodeJS生成项目模板

```javascript
利用NodeJS生成项目模板
projectName
   |---images
   |---css
   |---js
   |---index.html


let fs=require("fs");
let path=require("path");

class CreateProject{
    constructor(rootPath,projectName){
            this.rootPath=rootPath;
            this.projectName=projectName;
            this.subFiles=["images","css","js","index.html"];
    }
    initProject(){
        let projectPath=path.join(this.rootPath,this.projectName);
        fs.mkdirSync(projectPath);
        this.subFiles.forEach(function(fileName){
            if(path.extname(fileName)===""){
                let dirName=path.join(projectPath,fileName);
                fs.mkdirSync(dirName);
            }else{
                let file=path.join(projectPath,fileName);
                fs.writeFileSync(file,"");
            }
        });
    }
}

let cp=new CreateProject(__dirname,"taobao");
cp.initProject();
```

### 18.HTTP模块

```javascript
通过Nodejs提供的http模块，我们可以快速的构建一个web服务器,
也就是快速实现过去PHP服务器的功能(接收浏览器请求、响应浏览器请求等)

2.通过HTTP模块实现服务器功能步骤
2.1导入HTTP模块
2.2创建服务器实例对象
2.3绑定请求事件
2.4监听指定端口请求


let http = require("http");

/*
// 1.创建一个服务器实例对象
let server = http.createServer();
// 2.注册请求监听
server.on("request", function (req, res) {
    // end方法的作用: 结束本次请求并且返回数据
    // res.end("www.it666.com");
    // writeHead方法的作用: 告诉浏览器返回的数据是什么类型的, 返回的数据需要用什么字符集来解析
    res.writeHead(200, {
        "Content-Type": "text/plain; charset=utf-8"
    });
    res.end("知播渔");
});
// 3.指定监听的端口
server.listen(3000);
 */
http.createServer(function (req, res) {
    res.writeHead(200, {
        "Content-Type": "text/plain; charset=utf-8"
    });
    res.end("知播渔666");
}).listen(3000);
```

### 19.路径分发

```javascript
路径分发也称之为路由, 就是根据不同的请求路径返回不同的数据

如何根据不同的请求路径返回不同的数据?
通过请求监听方法中的request对象, 我们可以获取到当前请求的路径
通过判断请求路径的地址就可以实现不同的请求路径返回不同的数据

let http = require("http");

// 1.创建一个服务器实例对象
let server = http.createServer();
// 2.注册请求监听
/*
request对象其实是http.IncomingMessage 类的实例
response对象其实是http.ServerResponse 类的实例
* */
server.on("request", function (req, res) {
    res.writeHead(200, {
        "Content-Type": "text/plain; charset=utf-8"
    });
    // console.log(req.url);
    if(req.url.startsWith("/index")){
        // 注意点: 如果通过end方法来返回数据, 那么只会返回一次
        // res.end("首页1");
        // res.end("首页2");
        // 注意点: 如果通过write方法来返回数据, 那么可以返回多次
        //         write方法不具备结束本次请求的功能, 所以还需要手动的调用end方法来结束本次请求
        res.write("首页1");
        res.write("首页2");
        res.end();
    }else if(req.url.startsWith("/login")){
        res.end("登录");
    }else{
        res.end("没有数据");
    }
});
// 3.指定监听的端口
server.listen(3000);
```

### 20.响应完整页面

```javascript
拿到用户请求路径之后, 只需要利用fs模块将对应的网页返回即可


let http = require("http");
let path = require("path");
let fs = require("fs");

// 1.创建一个服务器实例对象
let server = http.createServer();
// 2.注册请求监听
server.on("request", function (req, res) {
    /*
    if(req.url.startsWith("/index")){
        // let filePath = path.join(__dirname, "www", "index.html");
        // let filePath = path.join(__dirname, "www", req.url);
        // fs.readFile(filePath, "utf8", function (err, content) {
        //     if(err){
        //         res.end("Server Error");
        //     }
        //     res.end(content);
        // });
        readFile(req, res);
    }else if(req.url.startsWith("/login")){
        // let filePath = path.join(__dirname, "www", req.url);
        // fs.readFile(filePath, "utf8", function (err, content) {
        //     if(err){
        //         res.end("Server Error");
        //     }
        //     res.end(content);
        // });
        readFile(req, res);
    }else{
        res.writeHead(200, {
            "Content-Type": "text/plain; charset=utf-8"
        });
        res.end("没有数据");
    }
    */
    readFile(req, res);
});
// 3.指定监听的端口
server.listen(3000);

function readFile(req, res) {
    let filePath = path.join(__dirname, "www", req.url);
    fs.readFile(filePath, "utf8", function (err, content) {
        if(err){
            res.end("Server Error");
        }
        res.end(content);
    });
}
```

### 21.响应静态资源

```javascript
在给浏览器返回数据的时候,
如果没有指定响应头的信息,
如果没有设置返回数据的类型,
那么浏览器不一定能正确的解析

所以无论返回什么类型的静态资源都需要添加对应的响应头信息






// let path = require("path");
let fs = require("fs");
let mime = require("./mime.json");

function readFile(req, res, rootPath) {
    let filePath = path.join(rootPath, req.url);
    // console.log(filePath);
    /*
    注意点:
    1.加载其它的资源不能写utf8
    2.如果服务器在响应数据的时候没有指定响应头, 那么在有的浏览器上, 响应的数据有可能无法显示
    * */
    let extName = path.extname(filePath);
    let type = mime[extName];
    if(type.startsWith("text")){
        type += "; charset=utf-8;";
    }
    res.writeHead(200, {
        "Content-Type": type
    });
    fs.readFile(filePath, function (err, content) {
        if(err){
            res.end("Server Error");
        }
        res.end(content);
    });
}

exports.StaticServer = readFile;














let http = require("http");
let path = require("path");
// let fs = require("fs");
// let mime = require("./mime.json");
let ss = require("./15-StaticServer.js");

// 1.创建一个服务器实例对象
let server = http.createServer();
// 2.注册请求监听
server.on("request", function (req, res) {
    // readFile(req, res);
    // let rootPath = path.join(__dirname, "www");
    let rootPath = "C:\\Users\\Jonathan_Lee\\Desktop\\abc";
    ss.StaticServer(req, res, rootPath);
});
// 3.指定监听的端口
server.listen(3000);
```

### 22.mine.json

```
{
  ".323": "text/h323",
  ".3gp": "video/3gpp",
  ".aab": "application/x-authoware-bin",
  ".aam": "application/x-authoware-map",
  ".aas": "application/x-authoware-seg",
  ".acx": "application/internet-property-stream",
  ".ai": "application/postscript",
  ".aif": "audio/x-aiff",
  ".aifc": "audio/x-aiff",
  ".aiff": "audio/x-aiff",
  ".als": "audio/X-Alpha5",
  ".amc": "application/x-mpeg",
  ".ani": "application/octet-stream",
  ".apk": "application/vnd.android.package-archive",
  ".asc": "text/plain",
  ".asd": "application/astound",
  ".asf": "video/x-ms-asf",
  ".asn": "application/astound",
  ".asp": "application/x-asap",
  ".asr": "video/x-ms-asf",
  ".asx": "video/x-ms-asf",
  ".au": "audio/basic",
  ".avb": "application/octet-stream",
  ".avi": "video/x-msvideo",
  ".awb": "audio/amr-wb",
  ".axs": "application/olescript",
  ".bas": "text/plain",
  ".bcpio": "application/x-bcpio",
  ".bin ": "application/octet-stream",
  ".bld": "application/bld",
  ".bld2": "application/bld2",
  ".bmp": "image/bmp",
  ".bpk": "application/octet-stream",
  ".bz2": "application/x-bzip2",
  ".c": "text/plain",
  ".cal": "image/x-cals",
  ".cat": "application/vnd.ms-pkiseccat",
  ".ccn": "application/x-cnc",
  ".cco": "application/x-cocoa",
  ".cdf": "application/x-cdf",
  ".cer": "application/x-x509-ca-cert",
  ".cgi": "magnus-internal/cgi",
  ".chat": "application/x-chat",
  ".class": "application/octet-stream",
  ".clp": "application/x-msclip",
  ".cmx": "image/x-cmx",
  ".co": "application/x-cult3d-object",
  ".cod": "image/cis-cod",
  ".conf": "text/plain",
  ".cpio": "application/x-cpio",
  ".cpp": "text/plain",
  ".cpt": "application/mac-compactpro",
  ".crd": "application/x-mscardfile",
  ".crl": "application/pkix-crl",
  ".crt": "application/x-x509-ca-cert",
  ".csh": "application/x-csh",
  ".csm": "chemical/x-csml",
  ".csml": "chemical/x-csml",
  ".css": "text/css",
  ".cur": "application/octet-stream",
  ".dcm": "x-lml/x-evm",
  ".dcr": "application/x-director",
  ".dcx": "image/x-dcx",
  ".der": "application/x-x509-ca-cert",
  ".dhtml": "text/html",
  ".dir": "application/x-director",
  ".dll": "application/x-msdownload",
  ".dmg": "application/octet-stream",
  ".dms": "application/octet-stream",
  ".doc": "application/msword",
  ".docx": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
  ".dot": "application/msword",
  ".dvi": "application/x-dvi",
  ".dwf": "drawing/x-dwf",
  ".dwg": "application/x-autocad",
  ".dxf": "application/x-autocad",
  ".dxr": "application/x-director",
  ".ebk": "application/x-expandedbook",
  ".emb": "chemical/x-embl-dl-nucleotide",
  ".embl": "chemical/x-embl-dl-nucleotide",
  ".eps": "application/postscript",
  ".epub": "application/epub+zip",
  ".eri": "image/x-eri",
  ".es": "audio/echospeech",
  ".esl": "audio/echospeech",
  ".etc": "application/x-earthtime",
  ".etx": "text/x-setext",
  ".evm": "x-lml/x-evm",
  ".evy": "application/envoy",
  ".exe": "application/octet-stream",
  ".fh4": "image/x-freehand",
  ".fh5": "image/x-freehand",
  ".fhc": "image/x-freehand",
  ".fif": "application/fractals",
  ".flr": "x-world/x-vrml",
  ".flv": "flv-application/octet-stream",
  ".fm": "application/x-maker",
  ".fpx": "image/x-fpx",
  ".fvi": "video/isivideo",
  ".gau": "chemical/x-gaussian-input",
  ".gca": "application/x-gca-compressed",
  ".gdb": "x-lml/x-gdb",
  ".gif": "image/gif",
  ".gps": "application/x-gps",
  ".gtar": "application/x-gtar",
  ".gz": "application/x-gzip",
  ".h": "text/plain",
  ".hdf": "application/x-hdf",
  ".hdm": "text/x-hdml",
  ".hdml": "text/x-hdml",
  ".hlp": "application/winhlp",
  ".hqx": "application/mac-binhex40",
  ".hta": "application/hta",
  ".htc": "text/x-component",
  ".htm": "text/html",
  ".html": "text/html",
  ".hts": "text/html",
  ".htt": "text/webviewhtml",
  ".ice": "x-conference/x-cooltalk",
  ".ico": "image/x-icon",
  ".ief": "image/ief",
  ".ifm": "image/gif",
  ".ifs": "image/ifs",
  ".iii": "application/x-iphone",
  ".imy": "audio/melody",
  ".ins": "application/x-internet-signup",
  ".ips": "application/x-ipscript",
  ".ipx": "application/x-ipix",
  ".isp": "application/x-internet-signup",
  ".it": "audio/x-mod",
  ".itz": "audio/x-mod",
  ".ivr": "i-world/i-vrml",
  ".j2k": "image/j2k",
  ".jad": "text/vnd.sun.j2me.app-descriptor",
  ".jam": "application/x-jam",
  ".jar": "application/java-archive",
  ".java": "text/plain",
  ".jfif": "image/pipeg",
  ".jnlp": "application/x-java-jnlp-file",
  ".jpe": "image/jpeg",
  ".jpeg": "image/jpeg",
  ".jpg": "image/jpeg",
  ".jpz": "image/jpeg",
  ".js": "application/x-javascript",
  ".jwc": "application/jwc",
  ".kjx": "application/x-kjx",
  ".lak": "x-lml/x-lak",
  ".latex": "application/x-latex",
  ".lcc": "application/fastman",
  ".lcl": "application/x-digitalloca",
  ".lcr": "application/x-digitalloca",
  ".lgh": "application/lgh",
  ".lha": "application/octet-stream",
  ".lml": "x-lml/x-lml",
  ".lmlpack": "x-lml/x-lmlpack",
  ".log": "text/plain",
  ".lsf": "video/x-la-asf",
  ".lsx": "video/x-la-asf",
  ".lzh": "application/octet-stream",
  ".m13": "application/x-msmediaview",
  ".m14": "application/x-msmediaview",
  ".m15": "audio/x-mod",
  ".m3u": "audio/x-mpegurl",
  ".m3url": "audio/x-mpegurl",
  ".m4a": "audio/mp4a-latm",
  ".m4b": "audio/mp4a-latm",
  ".m4p": "audio/mp4a-latm",
  ".m4u": "video/vnd.mpegurl",
  ".m4v": "video/x-m4v",
  ".ma1": "audio/ma1",
  ".ma2": "audio/ma2",
  ".ma3": "audio/ma3",
  ".ma5": "audio/ma5",
  ".man": "application/x-troff-man",
  ".map": "magnus-internal/imagemap",
  ".mbd": "application/mbedlet",
  ".mct": "application/x-mascot",
  ".mdb": "application/x-msaccess",
  ".mdz": "audio/x-mod",
  ".me": "application/x-troff-me",
  ".mel": "text/x-vmel",
  ".mht": "message/rfc822",
  ".mhtml": "message/rfc822",
  ".mi": "application/x-mif",
  ".mid": "audio/mid",
  ".midi": "audio/midi",
  ".mif": "application/x-mif",
  ".mil": "image/x-cals",
  ".mio": "audio/x-mio",
  ".mmf": "application/x-skt-lbs",
  ".mng": "video/x-mng",
  ".mny": "application/x-msmoney",
  ".moc": "application/x-mocha",
  ".mocha": "application/x-mocha",
  ".mod": "audio/x-mod",
  ".mof": "application/x-yumekara",
  ".mol": "chemical/x-mdl-molfile",
  ".mop": "chemical/x-mopac-input",
  ".mov": "video/quicktime",
  ".movie": "video/x-sgi-movie",
  ".mp2": "video/mpeg",
  ".mp3": "audio/mpeg",
  ".mp4": "video/mp4",
  ".mpa": "video/mpeg",
  ".mpc": "application/vnd.mpohun.certificate",
  ".mpe": "video/mpeg",
  ".mpeg": "video/mpeg",
  ".mpg": "video/mpeg",
  ".mpg4": "video/mp4",
  ".mpga": "audio/mpeg",
  ".mpn": "application/vnd.mophun.application",
  ".mpp": "application/vnd.ms-project",
  ".mps": "application/x-mapserver",
  ".mpv2": "video/mpeg",
  ".mrl": "text/x-mrml",
  ".mrm": "application/x-mrm",
  ".ms": "application/x-troff-ms",
  ".msg": "application/vnd.ms-outlook",
  ".mts": "application/metastream",
  ".mtx": "application/metastream",
  ".mtz": "application/metastream",
  ".mvb": "application/x-msmediaview",
  ".mzv": "application/metastream",
  ".nar": "application/zip",
  ".nbmp": "image/nbmp",
  ".nc": "application/x-netcdf",
  ".ndb": "x-lml/x-ndb",
  ".ndwn": "application/ndwn",
  ".nif": "application/x-nif",
  ".nmz": "application/x-scream",
  ".nokia-op-logo": "image/vnd.nok-oplogo-color",
  ".npx": "application/x-netfpx",
  ".nsnd": "audio/nsnd",
  ".nva": "application/x-neva1",
  ".nws": "message/rfc822",
  ".oda": "application/oda",
  ".ogg": "audio/ogg",
  ".oom": "application/x-AtlasMate-Plugin",
  ".p10": "application/pkcs10",
  ".p12": "application/x-pkcs12",
  ".p7b": "application/x-pkcs7-certificates",
  ".p7c": "application/x-pkcs7-mime",
  ".p7m": "application/x-pkcs7-mime",
  ".p7r": "application/x-pkcs7-certreqresp",
  ".p7s": "application/x-pkcs7-signature",
  ".pac": "audio/x-pac",
  ".pae": "audio/x-epac",
  ".pan": "application/x-pan",
  ".pbm": "image/x-portable-bitmap",
  ".pcx": "image/x-pcx",
  ".pda": "image/x-pda",
  ".pdb": "chemical/x-pdb",
  ".pdf": "application/pdf",
  ".pfr": "application/font-tdpfr",
  ".pfx": "application/x-pkcs12",
  ".pgm": "image/x-portable-graymap",
  ".pict": "image/x-pict",
  ".pko": "application/ynd.ms-pkipko",
  ".pm": "application/x-perl",
  ".pma": "application/x-perfmon",
  ".pmc": "application/x-perfmon",
  ".pmd": "application/x-pmd",
  ".pml": "application/x-perfmon",
  ".pmr": "application/x-perfmon",
  ".pmw": "application/x-perfmon",
  ".png": "image/png",
  ".pnm": "image/x-portable-anymap",
  ".pnz": "image/png",
  ".pot,": "application/vnd.ms-powerpoint",
  ".ppm": "image/x-portable-pixmap",
  ".pps": "application/vnd.ms-powerpoint",
  ".ppt": "application/vnd.ms-powerpoint",
  ".pptx": "application/vnd.openxmlformats-officedocument.presentationml.presentation",
  ".pqf": "application/x-cprplayer",
  ".pqi": "application/cprplayer",
  ".prc": "application/x-prc",
  ".prf": "application/pics-rules",
  ".prop": "text/plain",
  ".proxy": "application/x-ns-proxy-autoconfig",
  ".ps": "application/postscript",
  ".ptlk": "application/listenup",
  ".pub": "application/x-mspublisher",
  ".pvx": "video/x-pv-pvx",
  ".qcp": "audio/vnd.qcelp",
  ".qt": "video/quicktime",
  ".qti": "image/x-quicktime",
  ".qtif": "image/x-quicktime",
  ".r3t": "text/vnd.rn-realtext3d",
  ".ra": "audio/x-pn-realaudio",
  ".ram": "audio/x-pn-realaudio",
  ".rar": "application/octet-stream",
  ".ras": "image/x-cmu-raster",
  ".rc": "text/plain",
  ".rdf": "application/rdf+xml",
  ".rf": "image/vnd.rn-realflash",
  ".rgb": "image/x-rgb",
  ".rlf": "application/x-richlink",
  ".rm": "audio/x-pn-realaudio",
  ".rmf": "audio/x-rmf",
  ".rmi": "audio/mid",
  ".rmm": "audio/x-pn-realaudio",
  ".rmvb": "audio/x-pn-realaudio",
  ".rnx": "application/vnd.rn-realplayer",
  ".roff": "application/x-troff",
  ".rp": "image/vnd.rn-realpix",
  ".rpm": "audio/x-pn-realaudio-plugin",
  ".rt": "text/vnd.rn-realtext",
  ".rte": "x-lml/x-gps",
  ".rtf": "application/rtf",
  ".rtg": "application/metastream",
  ".rtx": "text/richtext",
  ".rv": "video/vnd.rn-realvideo",
  ".rwc": "application/x-rogerwilco",
  ".s3m": "audio/x-mod",
  ".s3z": "audio/x-mod",
  ".sca": "application/x-supercard",
  ".scd": "application/x-msschedule",
  ".sct": "text/scriptlet",
  ".sdf": "application/e-score",
  ".sea": "application/x-stuffit",
  ".setpay": "application/set-payment-initiation",
  ".setreg": "application/set-registration-initiation",
  ".sgm": "text/x-sgml",
  ".sgml": "text/x-sgml",
  ".sh": "application/x-sh",
  ".shar": "application/x-shar",
  ".shtml": "magnus-internal/parsed-html",
  ".shw": "application/presentations",
  ".si6": "image/si6",
  ".si7": "image/vnd.stiwap.sis",
  ".si9": "image/vnd.lgtwap.sis",
  ".sis": "application/vnd.symbian.install",
  ".sit": "application/x-stuffit",
  ".skd": "application/x-Koan",
  ".skm": "application/x-Koan",
  ".skp": "application/x-Koan",
  ".skt": "application/x-Koan",
  ".slc": "application/x-salsa",
  ".smd": "audio/x-smd",
  ".smi": "application/smil",
  ".smil": "application/smil",
  ".smp": "application/studiom",
  ".smz": "audio/x-smd",
  ".snd": "audio/basic",
  ".spc": "application/x-pkcs7-certificates",
  ".spl": "application/futuresplash",
  ".spr": "application/x-sprite",
  ".sprite": "application/x-sprite",
  ".sdp": "application/sdp",
  ".spt": "application/x-spt",
  ".src": "application/x-wais-source",
  ".sst": "application/vnd.ms-pkicertstore",
  ".stk": "application/hyperstudio",
  ".stl": "application/vnd.ms-pkistl",
  ".stm": "text/html",
  ".svg": "image/svg+xml",
  ".sv4cpio": "application/x-sv4cpio",
  ".sv4crc": "application/x-sv4crc",
  ".svf": "image/vnd",
  ".svg": "image/svg+xml",
  ".svh": "image/svh",
  ".svr": "x-world/x-svr",
  ".swf": "application/x-shockwave-flash",
  ".swfl": "application/x-shockwave-flash",
  ".t": "application/x-troff",
  ".tad": "application/octet-stream",
  ".talk": "text/x-speech",
  ".tar": "application/x-tar",
  ".taz": "application/x-tar",
  ".tbp": "application/x-timbuktu",
  ".tbt": "application/x-timbuktu",
  ".tcl": "application/x-tcl",
  ".tex": "application/x-tex",
  ".texi": "application/x-texinfo",
  ".texinfo": "application/x-texinfo",
  ".tgz": "application/x-compressed",
  ".thm": "application/vnd.eri.thm",
  ".tif": "image/tiff",
  ".tiff": "image/tiff",
  ".tki": "application/x-tkined",
  ".tkined": "application/x-tkined",
  ".toc": "application/toc",
  ".toy": "image/toy",
  ".tr": "application/x-troff",
  ".trk": "x-lml/x-gps",
  ".trm": "application/x-msterminal",
  ".tsi": "audio/tsplayer",
  ".tsp": "application/dsptype",
  ".tsv": "text/tab-separated-values",
  ".ttf": "application/octet-stream",
  ".ttz": "application/t-time",
  ".txt": "text/plain",
  ".uls": "text/iuls",
  ".ult": "audio/x-mod",
  ".ustar": "application/x-ustar",
  ".uu": "application/x-uuencode",
  ".uue": "application/x-uuencode",
  ".vcd": "application/x-cdlink",
  ".vcf": "text/x-vcard",
  ".vdo": "video/vdo",
  ".vib": "audio/vib",
  ".viv": "video/vivo",
  ".vivo": "video/vivo",
  ".vmd": "application/vocaltec-media-desc",
  ".vmf": "application/vocaltec-media-file",
  ".vmi": "application/x-dreamcast-vms-info",
  ".vms": "application/x-dreamcast-vms",
  ".vox": "audio/voxware",
  ".vqe": "audio/x-twinvq-plugin",
  ".vqf": "audio/x-twinvq",
  ".vql": "audio/x-twinvq",
  ".vre": "x-world/x-vream",
  ".vrml": "x-world/x-vrml",
  ".vrt": "x-world/x-vrt",
  ".vrw": "x-world/x-vream",
  ".vts": "workbook/formulaone",
  ".wav": "audio/x-wav",
  ".wax": "audio/x-ms-wax",
  ".wbmp": "image/vnd.wap.wbmp",
  ".wcm": "application/vnd.ms-works",
  ".wdb": "application/vnd.ms-works",
  ".web": "application/vnd.xara",
  ".wi": "image/wavelet",
  ".wis": "application/x-InstallShield",
  ".wks": "application/vnd.ms-works",
  ".wm": "video/x-ms-wm",
  ".wma": "audio/x-ms-wma",
  ".wmd": "application/x-ms-wmd",
  ".wmf": "application/x-msmetafile",
  ".wml": "text/vnd.wap.wml",
  ".wmlc": "application/vnd.wap.wmlc",
  ".wmls": "text/vnd.wap.wmlscript",
  ".wmlsc": "application/vnd.wap.wmlscriptc",
  ".wmlscript": "text/vnd.wap.wmlscript",
  ".wmv": "audio/x-ms-wmv",
  ".wmx": "video/x-ms-wmx",
  ".wmz": "application/x-ms-wmz",
  ".wpng": "image/x-up-wpng",
  ".wps": "application/vnd.ms-works",
  ".wpt": "x-lml/x-gps",
  ".wri": "application/x-mswrite",
  ".wrl": "x-world/x-vrml",
  ".wrz": "x-world/x-vrml",
  ".ws": "text/vnd.wap.wmlscript",
  ".wsc": "application/vnd.wap.wmlscriptc",
  ".wv": "video/wavelet",
  ".wvx": "video/x-ms-wvx",
  ".wxl": "application/x-wxl",
  ".x-gzip": "application/x-gzip",
  ".xaf": "x-world/x-vrml",
  ".xar": "application/vnd.xara",
  ".xbm": "image/x-xbitmap",
  ".xdm": "application/x-xdma",
  ".xdma": "application/x-xdma",
  ".xdw": "application/vnd.fujixerox.docuworks",
  ".xht": "application/xhtml+xml",
  ".xhtm": "application/xhtml+xml",
  ".xhtml": "application/xhtml+xml",
  ".xla": "application/vnd.ms-excel",
  ".xlc": "application/vnd.ms-excel",
  ".xll": "application/x-excel",
  ".xlm": "application/vnd.ms-excel",
  ".xls": "application/vnd.ms-excel",
  ".xlsx": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
  ".xlt": "application/vnd.ms-excel",
  ".xlw": "application/vnd.ms-excel",
  ".xm": "audio/x-mod",
  ".xml": "text/plain",
  ".xml": "application/xml",
  ".xmz": "audio/x-mod",
  ".xof": "x-world/x-vrml",
  ".xpi": "application/x-xpinstall",
  ".xpm": "image/x-xpixmap",
  ".xsit": "text/xml",
  ".xsl": "text/xml",
  ".xul": "text/xul",
  ".xwd": "image/x-xwindowdump",
  ".xyz": "chemical/x-pdb",
  ".yz1": "application/x-yz1",
  ".z": "application/x-compress",
  ".zac": "application/x-zaurus-zac",
  ".zip": "application/zip",
  ".json": "application/json"
}
```

### 23.拿到Get请求传递过来的参数

```javascript
使用URL模块

url.format(urlObject)  将路径转换为对象
url.parse(urlString[, parseQueryString[, slashesDenoteHost]])  将对象转换为路径


let url = require("url");
let http = require("http");

// let str = "http://root:123456@www.it666.com:80/index.html?name=lnj&age=68#banner";
// let obj = url.parse(str, true);
// console.log(obj);
// console.log(obj.query.name);
// console.log(obj.query.age);

// 1.创建一个服务器实例对象
let server = http.createServer();
server.on("request", function (req, res) {
    // console.log(req.url);
    let obj = url.parse(req.url, true);
    res.end(obj.query.name + "----" + obj.query.age);
});
// 3.指定监听的端口
server.listen(3000);
```

### 24.拿到POST请求传递过来的参数

```javascript
<form action="http://127.0.0.1:3000/index.html" method="post">
    <input type="text" name="userName">
    <input type="text" name="password">
    <input type="submit" value="提交">
</form>
<!--
1.如何拿到POST请求传递过来的参数
使用querystring模块

querystring.parse(str[, sep[, eq[, options]]])  将参数转换为对象
querystring.stringify(obj[, sep[, eq[, options]]]) 将对象转换为参数
-->


    

let http = require("http");
let queryString = require("querystring");

// 1.创建一个服务器实例对象
let server = http.createServer();
server.on("request", function (req, res) {
    // 1.定义变量保存传递过来的参数
    let params = "";
    // 注意点: 在NODEJS中 ,POST请求的参数我们不能一次性拿到, 必须分批获取
    req.on("data", function (chunk) {
        // 每次只能拿到一部分数据
        params += chunk;
    });
    req.on("end", function () {
        // 这里才能拿到完整的数据
        // console.log(params);
        let obj = queryString.parse(params);
        // console.log(obj.userName);
        // console.log(obj.password);
        res.end(obj.userName + "----" + obj.password);
    });
});
// 3.指定监听的端口
server.listen(3000);
```

### 25.区分GET请求和POST请求

```javascript
1.在服务端如何区分用户发送的是GET请求和POST请求?
通过HTTP模块http.IncomingMessage 类的.method属性


let http = require("http");

// 1.创建一个服务器实例对象
let server = http.createServer();
server.on("request", function (req, res) {
    // console.log(req.method);
    res.writeHead(200, {
        "Content-Type": "text/plain; charset=utf-8"
    });
    if(req.method.toLowerCase() === "get"){
        res.end("利用GET请求的方式处理参数");
    }else if(req.method.toLowerCase() === "post"){
        res.end("利用POST请求的方式处理参数");
    }
});
// 3.指定监听的端口
server.listen(3000);
```

### 26.模板引擎

```javascript
<form action="./info.html" method="post">
    <input type="text" name="userName">
    <input type="submit" value="查询">
</form>
```

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<ul>
    <!--<li>姓名: !!!name!!!</li>
    <li>性别: !!!gender!!!</li>
    <li>年龄: !!!age!!!</li>-->

    <li>姓名: <%=name%></li>
    <li>性别: <%=gender%></li>
    <li>年龄: <%=age%></li>
</ul>
</body>
</html>
```

```javascript
let http = require("http");
let path = require("path");
let fs = require("fs");
let url = require("url");
let queryString = require("querystring");
let template = require("art-template");

let persons = {
    "lisi": {
        name: "lisi",
        gender: "male",
        age: "33"
    },
    "zhangsan": {
        name: "zhangsan",
        gender: "female",
        age: "18"
    }
};

// 1.创建一个服务器实例对象
let server = http.createServer();
// 2.注册请求监听
server.on("request", function (req, res) {
   if(req.url.startsWith("/index") && req.method.toLowerCase() === "get"){
       let obj = url.parse(req.url);
       let filePath = path.join(__dirname, obj.pathname);
       fs.readFile(filePath, "utf8", function (err, content) {
           if(err){
               res.writeHead(404, {
                   "Content-Type": "text/plain; charset=utf-8"
               });
               res.end("Page Not Found");
           }
           res.writeHead(200, {
               "Content-Type": "text/html; charset=utf-8"
           });
           res.end(content);
       });
   }
   else if(req.url.startsWith("/info") && req.method.toLowerCase() === "post"){
       let params = "";
       req.on("data", function (chunk) {
           params += chunk;
       });
       req.on("end", function () {
           let obj = queryString.parse(params);
           let per = persons[obj.userName];
           // console.log(per);
           let filePath = path.join(__dirname, req.url);
           /*
           fs.readFile(filePath, "utf8", function (err, content) {
               if(err){
                   res.writeHead(404, {
                       "Content-Type": "text/plain; charset=utf-8"
                   });
                   res.end("Page Not Found");
               }
               content = content.replace("!!!name!!!", per.name);
               content = content.replace("!!!gender!!!", per.gender);
               content = content.replace("!!!age!!!", per.age);
               res.end(content);
           });
            */
           let html = template(filePath, per);
           res.writeHead(200, {
               "Content-Type": "text/html; charset=utf-8"
           });
           res.end(html);
       });
   }
});
// 3.指定监听的端口
server.listen(3000);
```

### 27.Node模块原理分析

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>01-Node模块原理分析</title>
</head>
<body>
<!--
1.Node模块
1.1在CommonJS规范中一个文件就是一个模块
1.2在CommonJS规范中通过exports暴露数据
1.3在CommonJS规范中通过require()导入模块

2.Node模块原理分析
既然一个文件就是一个模块,
既然想要使用模块必须先通过require()导入模块
所以可以推断出require()的作用其实就是读取文件
所以要想了解Node是如何实现模块的, 必须先了解如何执行读取到的代码

3.执行从文件中读取代码
我们都知道通过fs模块可以读取文件,
但是读取到的数据要么是二进制, 要么是字符串
无论是二进制还是字符串都无法直接执行

但是我们知道如果是字符串, 在JS中是有办法让它执行的
eval  或者 new Function;

4.通过eval执行代码
缺点: 存在依赖关系, 字符串可以访问外界数据,不安全

5.通过new Function执行代码
缺点: 存在依赖关系, 依然可以访问全局数据,不安全
-->
<!--
6.通过NodeJS的vm虚拟机执行代码
runInThisContext: 无权访问外部变量, 但是可以访问global
runInNewContext:  无权访问外部变量, 也不能访问global
-->

<script>
    // let str = "console.log('www.it666.com');";
    // eval(str);

    // 存在依赖关系, 字符串可以访问外界数据,不安全
    // let name = "lnj";
    // let str = "console.log(name);";
    // eval(str);

    // let str = "console.log('www.it666.com');";
    // let fn = new Function(str);
    // console.log(fn);
    // fn();

    // 存在依赖关系, 字符串可以访问外界数据,不安全
    let name = "lnj";
    let str = "console.log(name);";
    let fn = new Function(str);
    fn();
</script>
</body>
</html>
```

```
let vm = require("vm");

// let str = "console.log('www.it666.com');";
// vm.runInThisContext(str);

/*
runInThisContext: 提供了一个安全的环境给我们自行字符串中的代码
runInThisContext提供的环境不能访问本地的变量, 但是可以访问全局的变量(也就是global上的变量)
* */
// let name = "lnj";
// let str = "console.log(name);";
// vm.runInThisContext(str); // name is not defined

// global.name = "lnj";
// let str = "console.log(name);";
// vm.runInThisContext(str);
/*
runInNewContext: 提供了一个安全的环境给我们执行字符串中的代码
runInNewContext提供的环境不能访问本地的变量, 也不能访问全局的变量(也就是global上的变量)
* */
// let name = "lnj";
// let str = "console.log(name);";
// vm.runInNewContext(str); // name is not defined

global.name = "lnj";
let str = "console.log(name);";
vm.runInNewContext(str); // name is not defined
```

### 28.Node模块加载流程分析

```javascript
1.内部实现了一个require方法
function require(path) {
  return self.require(path);
}

2.通过Module对象的静态__load方法加载模块文件
Module.prototype.require = function(path) {
  return Module._load(path, this, /* isMain */ false);
};

3.通过Module对象的静态_resolveFilename方法, 得到绝对路径并添加后缀名
var filename = Module._resolveFilename(request, parent, isMain);

4.根据路径判断是否有缓存, 如果没有就创建一个新的Module模块对象并缓存起来
var cachedModule = Module._cache[filename];
if (cachedModule) {
   return cachedModule.exports;
}
var module = new Module(filename, parent);
Module._cache[filename] = module;

function Module(id, parent) {
  this.id = id;
  this.exports = {};
}
5.利用tryModuleLoad方法加载模块
tryModuleLoad(module, filename);
    - 6.1取出模块后缀
    var extension = path.extname(filename);

    - 6.2根据不同后缀查找不同方法并执行对应的方法, 加载模块
    Module._extensions[extension](this, filename);

    - 6.3如果是JSON就转换成对象
    module.exports = JSON.parse(internalModule.stripBOM(content));

    - 6.4如果是JS就包裹一个函数
    var wrapper = Module.wrap(content);
    NativeModule.wrap = function(script) {
        return NativeModule.wrapper[0] + script + NativeModule.wrapper[1];
    };
    NativeModule.wrapper = [
        '(function (exports, require, module, __filename, __dirname) { ',
        '\n});'
    ];
    - 6.5执行包裹函数之后的代码, 拿到执行结果(String -- Function)
    var compiledWrapper = vm.runInThisContext(wrapper);

    - 6.6利用call执行fn函数, 修改module.exports的值
    var args = [this.exports, require, module, filename, dirname];
    var result = compiledWrapper.call(this.exports, args);

    - 6.7返回module.exports
    return module.exports;
```

```javascript
let path=require("path");
let fs=require("fs");
let vm=require("vm");

//新建Module对象
class myModule{
    constructor(id){
        this.id=id;
        this.exports={};
    }
}
myModule._cache={};
myModule._extensions={
    ".js":function(module){
        //读取js代码
        let script=fs.readFileSync(module.id);
        //将js代码包裹到函数中
        let strScript=myModule.wrapper[0]+script+myModule.wrapper[1];
        module.exports=strScript;
        //将字符串转换成js代码
        let isScript=vm.runInNewContext(strScript);
        //执行转换后的js代码?call回立即执行
        isScript.call(module.exports,module.exports);

    },
    ".json":function(module){
        let json=fs.readFileSync(module.id);
        let obj=JSON.parse(json);
        module.exports=obj;   
    }
};
myModule.wrapper=[
    "(function(exports,require,module,_filename,_dirname){","\n});"
];
function myRequire(filePath){
    //1.将传入的相对路径转化为绝对路径
    let absPath=path.join(__dirname,filePath);
    // console.log(absPath);
    //2.尝试从缓存中获取当前模块
    let  cacheModule=myModule._cache[absPath];
    if(cacheModule){
        return cacheModule.exports; 
    }
    //3.如果没有缓存就自己创建myModule对象，并缓存起来
    let module=new myModule(absPath);
    myModule._cache[absPath]=module;
    //4.利用tryModuleLode方法加载模块
    tryModule(module);
    //5.返回模块的exports
    return module.exports;
}

function tryModule(module){
    //1.取出模块后缀
    let exName=path.extname(module.id);
    //如果后缀为json  
    myModule._extensions[exName](module);
    //如果后缀为js
    myModule._extensions[exName](module);
    
}



let aModule=myRequire("./01.js");
console.log(aModule);
```

### 29.NodeJS-面试题

```javascript
<!--
1.NodeJS中的this为什么是一个空对象?
-->
<!--
因为所有的NodeJS文件在执行的时候都会被包裹到一个函数中, this都被修改为了空的module.exports
(function (exports, require, module, __filename, __dirname) {
    // 我们编写的代码
    // 所以说在这里面拿到的this就是 空的module.exports
});
compiledWrapper.call(module.exports, args);
-->
<!--
2.NodeJS中为什么可以直接使用exports, require, module, __filename, __dirname
-->
<!--
因为所有的NodeJS文件在执行的时候都会被包裹到一个函数中, 这些属性都被通过参数的形式传递过来了
var args = [module.exports, require, module, filename, dirname];
compiledWrapper.call(this.exports, args);
-->
<!--
3.NodeJS中为什么不能直接exports赋值, 而可以给module.exports赋值
-->
<!--
(function (exports, require, module, __filename, __dirname) {
    exports = "lnj";
});
jsScript.call(module.exports, module.exports);
return module.exports;

相当于
let exports = module.exports;
exports = "lnj";
return module.exports;
-->
<!--
4.通过require导入包时候应该使用var/let还是const?
导入包的目的是使用包而不是修改包, 所以导入包时使用const接收
-->
```

```
对象是引用类型的，const定义的对象t中保存的是指向对象t的指针，这里的“不变”指的是指向对象的指针不变，而修改对象中的属性并不会让指向对象的指针发生变化，所以用const定义对象，对象的属性是可以改变的。
```

### 30.浏览器事件循环

```javascript
1.JS是单线程的
  JS中的代码都是串行的, 前面没有执行完毕后面不能执行
2.执行顺序
2.1程序运行会从上至下依次执行所有的同步代码
2.2在执行的过程中如果遇到异步代码会将异步代码放到事件循环中
2.3当所有同步代码都执行完毕后, JS会不断检测 事件循环中的异步代码是否满足条件
2.4一旦满足条件就执行满足条件的异步代码

3.宏任务和微任务
在JS的异步代码中又区分"宏任务(MacroTask)"和"微任务(MicroTask)"
宏任务: 宏/大的意思, 可以理解为比较费时比较慢的任务
微任务: 微/小的意思, 可以理解为相对没那么费时没那么慢的任务

4.常见的宏任务和微任务
MacroTask: setTimeout, setInterval, setImmediate（IE独有）...
MicroTask: Promise, MutationObserver ,process.nextTick（node独有) ...
注意点: 所有的宏任务和微任务都会放到自己的执行队列中, 也就是有一个宏任务队列和一个微任务队列
        所有放到队列中的任务都采用"先进先出原则", 也就是多个任务同时满足条件, 那么会先执行先放进去的

5.完整执行顺序
1.从上至下执行所有同步代码
2.在执行过程中遇到宏任务就放到宏任务队列中,遇到微任务就放到微任务队列中
3.当所有同步代码执行完毕之后, 就执行微任务队列中满足需求所有回调
4.当微任务队列所有满足需求回调执行完毕之后, 就执行宏任务队列中满足需求所有回调
... ...
注意点:
每执行完一个宏任务都会立刻检查微任务队列有没有被清空, 如果没有就立刻清空
```

```javascript
<div></div>
<button class="add">添加节点</button>
<button class="del">删除节点</button>
<script>
    /*
    // setImmediate和setTimeout, setInterval区别:
    // setImmediate不能设置延迟时间, 并且只能执行一次
    setImmediate(function () {
        console.log("setImmediate");
    });
    console.log("同步代码Start");
    console.log("同步代码End");
    */

    /*
    // MutationObserver是专门用于监听节点的变化
    let oDiv = document.querySelector("div");
    let oAddBtn = document.querySelector(".add");
    let oDelBtn = document.querySelector(".del");
    oAddBtn.onclick = function () {
        let op = document.createElement("p");
        op.innerText = "我是段落";
        oDiv.appendChild(op);
    }
    oDelBtn.onclick = function () {
        let op = document.querySelector("p");
        oDiv.removeChild(op);
    }
    let mb = new MutationObserver(function () {
        console.log("执行了");
    });
    mb.observe(oDiv, {
        "childList": true
    });
    console.log("同步代码Start");
    console.log("同步代码End");
     */

    /*
   // 1.定义一个宏任务
    setTimeout(function () {
        console.log("setTimeout1");
    }, 0);
    // 2.定义一个微任务
    Promise.resolve().then(function () {
        console.log("Promise1");
    });
    console.log("同步代码Start");
    Promise.resolve().then(function () {
        console.log("Promise2");
    });
    setTimeout(function () {
        console.log("setTimeout2");
    }, 0);
    console.log("同步代码End");
     */

    /*
    // 1.定义一个宏任务
    setTimeout(function () {
        console.log("setTimeout1");
        // 2.定义一个微任务 p1
        Promise.resolve().then(function () {
            console.log("Promise1");
        });
        // 2.定义一个微任务 p2
        Promise.resolve().then(function () {
            console.log("Promise2");
        });
    }, 0);
    // 1.定义一个宏任务
    setTimeout(function () {
        console.log("setTimeout2");
        // 2.定义一个微任务 p3
        Promise.resolve().then(function () {
            console.log("Promise3");
        });
        // 2.定义一个微任务 p4
        Promise.resolve().then(function () {
            console.log("Promise4");
        });
    }, 0);
     */

    /*
    // 1.定义一个宏任务
    setTimeout(function () {
        console.log("setTimeout1");
        // 2.定义一个微任务 p2
        Promise.resolve().then(function () {
            console.log("Promise2");
        });
        // 2.定义一个微任务 p3
        Promise.resolve().then(function () {
            console.log("Promise3");
        });
    }, 0);
    // 2.定义一个微任务 p3
    Promise.resolve().then(function () {
        console.log("Promise1");
        // s2
        setTimeout(function () {
            console.log("setTimeout2");
        });
        // s3
        setTimeout(function () {
            console.log("setTimeout3");
        });
    });
     */
</script>
```

### 31.NodeJS事件环

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>06-NodeJS事件环</title>
</head>
<body>
<!--
1.概述
和浏览器中一样NodeJS中也有事件环(Event Loop),
但是由于执行代码的宿主环境和应用场景不同,
所以两者的事件环也有所不同.

>扩展阅读: 在NodeJS中使用libuv实现了Event Loop.
>源码地址: https://github.com/libuv/libuv
>别看了C/C++语言写的, 你现在看不懂

2.NodeJS事件环和浏览器事件环区别
2.1任务队列个数不同
浏览器事件环有2个事件队列(宏任务队列和微任务队列)
NodeJS事件环有6个事件队列
2.2微任务队列不同
浏览器事件环中有专门存储微任务的队列
NodeJS事件环中没有专门存储微任务的队列
2.3微任务执行时机不同
浏览器事件环中每执行完一个宏任务都会去清空微任务队列
NodeJS事件环中只有同步代码执行完毕和其它队列之间切换(清空队列)的时候回去清空微任务队列
2.4微任务优先级不同
浏览器事件环中如果多个微任务同时满足执行条件, 采用先进先出
NodeJS事件环中如果多个微任务同时满足执行条件, 会按照优先级执行

2.NodeJS中的任务队列
    ┌───────────────────────┐
┌> │timers          │执行setTimeout() 和 setInterval()中到期的callback
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │pending callbacks│执行系统操作的回调, 如:tcp, udp通信的错误callback
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │idle, prepare   │只在内部使用
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │poll            │执行与I/O相关的回调
    │                  (除了close回调、定时器回调和setImmediate()之外，几乎所有回调都执行);
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │check           │执行setImmediate的callback
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└─┤close callbacks │执行close事件的callback，例如socket.on("close",func)
    └───────────────────────┘


    ┌───────────────────────┐
┌> │timers          │执行setTimeout() 和 setInterval()中到期的callback
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
│  │poll            │执行与I/O相关的回调
    │                  (除了close回调、定时器回调和setImmediate()之外，几乎所有回调都执行);
│  └──────────┬────────────┘
│  ┌──────────┴────────────┐
└─┤check           │执行setImmediate的callback
    └───────────────────────┘

1.注意点:
和浏览器不同的是没有宏任务队列和微任务队列的概念
宏任务被放到了不同的队列中, 但是没有队列是存放微任务的队列
微任务会在执行完同步代码和队列切换的时候执行

什么时候切换队列?
当队列为空(已经执行完毕或者没有满足条件回到)
或者执行的回调函数数量到达系统设定的阈值时任务队列就会切换

2.注意点:
在NodeJS中process.nextTick微任务的优先级高于Promise.resolve微任务
-->
<!--
            ┌───────────────────────┐
            │                同步代码
            └──────────┬────────────┘
                                  │
                                  │ <---- 满足条件微任务代码
                                  │
            ┌──────────┴────────────┐
        ┌> │timers          │执行setTimeout() 和 setInterval()中到期的callback
        │  └──────────┬────────────┘
        │                        │
        │                        │ <---- 满足条件微任务代码
        │                        │
        │  ┌──────────┴────────────┐
        │  │poll            │执行与I/O相关的回调
        │  │                  (除了close回调、定时器回调和setImmediate()之外，几乎所有回调都执行);
        │  └──────────┬────────────┘
        │                        │
        │                        │ <---- 满足条件微任务代码
        │                        │
        │  ┌──────────┴────────────┐
        └─┤check           │执行setImmediate的callback
            └───────────────────────┘

注意点:
执行完poll, 会查看check队列是否有内容, 有就切换到check
如果check队列没有内容, 就会查看timers是否有内容, 有就切换到timers
如果check队列和timers队列都没有内容, 为了避免资源浪费就会阻塞在poll
-->
</body>
</html>
```

```
/*
Promise.resolve().then(function () {
    console.log("Promise");
});
process.nextTick(function () {
    console.log("process.nextTick1");
});
process.nextTick(function () {
    console.log("process.nextTick2");
});
process.nextTick(function () {
    console.log("process.nextTick3");
});
 */
/*
setTimeout(function () {
    console.log("setTimeout");
});
Promise.resolve().then(function () {
    console.log("Promise");
});
console.log("同步代码 Start");
process.nextTick(function () {
    console.log("process.nextTick");
});
setImmediate(function () {
    console.log("setImmediate");
});
console.log("同步代码 End");
 */
/*
setTimeout(function () {
    console.log("setTimeout1");
    // p1
    Promise.resolve().then(function () {
        console.log("Promise1");
    });
    // n1
    process.nextTick(function () {
        console.log("process.nextTick1");
    });
});
console.log("同步代码 Start");
setTimeout(function () {
    console.log("setTimeout2");
    // p2
    Promise.resolve().then(function () {
        console.log("Promise2");
    });
    // n2
    process.nextTick(function () {
        console.log("process.nextTick2");
    });
});
console.log("同步代码 End");
 */

/*
注意点: 如下代码输出的结果是随机的
        在NodeJS中指定的延迟时间是有一定的误差的, 所以导致了输出结果随机的问题
* */
/*
setTimeout(function () {
    console.log("setTimeout");
}, 0);
setImmediate(function () {
    console.log("setImmediate");
});
 */

const path = require("path");
const fs = require("fs");

fs.readFile(path.join(__dirname, "04.js"), function () {
    setTimeout(function () {
        console.log("setTimeout");
    }, 0);
    setImmediate(function () {
        console.log("setImmediate");
    });
});

```

![批注 2020-12-26 111314](node.js.assets/%E6%89%B9%E6%B3%A8%202020-12-26%20111314.png)![批注 2020-12-26 132428](node.js.assets/%E6%89%B9%E6%B3%A8%202020-12-26%20132428.png)![批注 2020-12-26 111016](node.js.assets/%E6%89%B9%E6%B3%A8%202020-12-26%20111016.png)



![批注 2020-12-26 133859](node.js.assets/%E6%89%B9%E6%B3%A8%202020-12-26%20133859.png)

![浏览器和NodeJS事件环区别](node.js.assets/%E6%B5%8F%E8%A7%88%E5%99%A8%E5%92%8CNodeJS%E4%BA%8B%E4%BB%B6%E7%8E%AF%E5%8C%BA%E5%88%AB.png)

### 32.自定义本地包和全局包

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>07-自定义本地包和全局包</title>
</head>
<body>
<!--
1.包的规范(了解)
- package.json必须在包的顶层目录下
- 二进制文件应该在bin目录下
- JavaScript代码应该在lib目录下
- 文档应该在doc目录下
- 单元测试应该在test目录下

2.package.json字段分析(了解)
- name：包的名称，必须是唯一的，由小写英文字母、数字和下划线组成，不能包含空格
- description：包的简要说明
- version：符合语义化版本识别规范的版本字符串
    + 主版本号：当你做了不兼容的 API 修改
    + 子版本号：当你做了向下兼容的功能性新增
    + 修订号：当你做了向下兼容的问题修正
- keywords：关键字数组，通常用于搜索
- maintainers：维护者数组，每个元素要包含name、email（可选）、web（可选）字段
- contributors：贡献者数组，格式与maintainers相同。包的作者应该是贡献者数组的第一- 个元素
- bugs：提交bug的地址，可以是网站或者电子邮件地址
- licenses：许可证数组，每个元素要包含type（许可证名称）和url（链接到许可证文本的- 地址）字段
- repositories：仓库托管地址数组，每个元素要包含type（仓库类型，如git）、url（仓- 库的地址）和path（相对于仓库的路径，可选）字段
- dependencies：生产环境包的依赖，一个关联数组，由包的名称和版本号组成
- devDependencies：开发环境包的依赖，一个关联数组，由包的名称和版本号组成

3.自定义包实现步骤
1.创建一个包文件夹
2.初始化一个package.json文件
3.初始化一个包入口js文件
  注意点: 如果没有配置main, 默认会将index.js作为入口
          如果包中没有index.js, 那么就必须配置main
4.根据包信息配置package.json文件
  注意点: 通过scripts可以帮我们记住指令, 然后通过npm run xxx方式就可以执行该指令
          如果指令的名称叫做start或者test, 那么执行的时候可以不加run
5.给package.json添加bin属性, 告诉系统执行全局命令时需要执行哪一个JS文件
6.在全局命令执行的JS文件中添加 #! /usr/bin/env node
7.通过npm link 将本地包放到全局方便我们调试

4.将自定义包发布到官网
1.在https://www.npmjs.com/注册账号
2.在终端输入npm addUser
3.在终端输入npm publish
-->
</body>
</html>
```

