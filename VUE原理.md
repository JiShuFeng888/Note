### 1.vue双向数据绑定原理上

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>01-Vue基本模板</title>
    <!--1.下载导入Vue.js-->
    <script src="js/vue.js"></script>
</head>
<body>
<div id="app">
    <input type="text" v-model="name">
    <p>{{ name }}</p>
</div>
<script>
    // 2.创建一个Vue的实例对象
    let vue = new Vue({
        // 3.告诉Vue的实例对象, 将来需要控制界面上的哪个区域
        el: '#app',
        // 4.告诉Vue的实例对象, 被控制区域的数据是什么
        data: {
            name: "李南江"
        }
    });
    
    1.Vue响应式的原理(数据改变界面就会改变)是什么?
      时时监听数据变化, 一旦数据发生变化就更新界面
    2.Vue是如何实现时时监听数据变化的?
      通过原生JS的defineProperty方法
    3.defineProperty方法的特点
      可以直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象!!!
    4.defineProperty用法
    obj: 需要操作的对象
    prop: 需要操作的属性
    descriptor: 属性描述符
    Object.defineProperty(obj, prop, descriptor)
   
    let obj = {name: '李南江'};
    // 需求: 给obj对象动态新增一个name属性, 并且name属性的取值必须是lnj
    Object.defineProperty(obj, 'name', {
        // 可以通过value来告诉defineProperty方法新增的属性的取值是什么
        value: 'lnj',
        默认情况下通过defineProperty新增的属性的取值是不能修改的
        如果想修改, 那么就必须显示的告诉defineProperty方法  
        writable: true,
        /默认情况下通过defineProperty新增的属性是不能删除的
         如果想删除, 那么就必须显示的告诉defineProperty方法
        configurable: true,
        默认情况下通过defineProperty新增的属性是不能迭代的
        如果想迭代, 那么就必须显示的告诉defineProperty方法
        enumerable: true
		//注意是Object对象,是新增的属性!!!
    });
    console.log(obj);
    注意点: 默认情况下通过defineProperty新增的属性的取值是不能修改的
    // obj.name = 'it666';
    // console.log(obj);
    注意点: 默认情况下通过defineProperty新增的属性是不能删除的
    // delete obj.name
    // console.log(obj);
    注意点: 默认情况下通过defineProperty新增的属性是不能遍历(迭代的)
    // for(let key in obj){
    //     console.log(key, obj[key]);
    // }
</script>
</body>
</html>
```

### 2.vue双向数据绑定原理中

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>01-Vue基本模板</title>
    <!--1.下载导入Vue.js-->
    <script src="js/vue.js"></script>
</head>
<body>
<div id="app">
    <input type="text" v-model="name">
    <p>{{ name }}</p>
</div>
<script>
    // 2.创建一个Vue的实例对象
    let vue = new Vue({
        // 3.告诉Vue的实例对象, 将来需要控制界面上的哪个区域
        el: '#app',
        // 4.告诉Vue的实例对象, 被控制区域的数据是什么
        data: {
            name: "李南江"
        }
    });
    /*
    1.defineProperty方法
    defineProperty除了可以动态修改/新增对象的属性以外
    还可以在修改/新增的时候给该属性添加get/set方法
    2.defineProperty get/set方法特点
    只要通过defineProperty给某个属性添加了get/set方法
    那么以后只要获取这个属性的值就会自动调用get, 设置这个属性的值就会自动调用set
    3.注意点:
    如果设置了get/set方法, 那么就不能通过value直接赋值, 也不能编写writable:true
    * */
    let obj = {};
    let oldValue = '李南江';
    Object.defineProperty(obj, 'name', {
        // value: oldValue,
        // writable: true,
        configurable: true,
        enumerable: true,
        get(){
            console.log("get方法被执行了");
            return oldValue;
        },
        set(newValue){
            if(oldValue !== newValue){
                console.log("set方法被执行了");
                oldValue = newValue;
            }
        }
    });
    console.log(obj.name);
    obj.name = 'lnj';
</script>
</body>
</html>
```

### 3.vue双向数据绑定原理下

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>01-Vue基本模板</title>
    <!--1.下载导入Vue.js-->
    <script src="js/vue.js"></script>
</head>
<body>
<div id="app">
    <input type="text" v-model="name">
    <p>{{ name }}</p>
</div>
<script>
    // 2.创建一个Vue的实例对象
    let vue = new Vue({
        // 3.告诉Vue的实例对象, 将来需要控制界面上的哪个区域
        el: '#app',
        // 4.告诉Vue的实例对象, 被控制区域的数据是什么
        data: {
            name: "李南江"
        }
    });
    /*
    需求: 快速监听对象中所有属性的变化
    * */
    let obj = {
        name: 'lnj',
        // name: {a: 'abc'},
        age: 33
    };
    class Observer{
        // 只要将需要监听的那个对象传递给Observer这个类
        // 这个类就可以快速的给传入的对象的所有属性都添加get/set方法
        constructor(data){
            this.observer(data);
        }
        observer(obj){
            if(obj && typeof obj === 'object'){
                // 遍历取出传入对象的所有属性, 给遍历到的属性都增加get/set方法
                for(let key in obj){
                    this.defineRecative(obj, key, obj[key])
                }
            }
        }
        // obj: 需要操作的对象
        // attr: 需要新增get/set方法的属性
        // value: 需要新增get/set方法属性的取值
        defineRecative(obj, attr, value){
            // 如果属性的取值又是一个对象, 那么也需要给这个对象的所有属性添加get/set方法
			if(value && typeof value === 'object'){
             		this.observer(value);   
            }
            Object.defineProperty(obj, attr, {
                get(){
                    return value;
                },
                set:(newValue)=>{
                    if(value !== newValue){
                        // 如果给属性赋值的新值又是一个对象, 那么也需要给这个对象的所有属性添加get/set方法
				if(newValue && typeof newValue === 'object'){
                        this.observer(newValue);
                }
                        value = newValue;
                        console.log('监听到数据的变化, 需要去更新UI');
                    }
                }
            })
        }
    }
    new Observer(obj);
    // obj.name = 'it666';
    // obj.age = 666;
    // obj.name.a = 'it666';
    obj.name = {a: 'abc'};
    obj.name.a = 'it666';
</script>
</body>
</html>
```

### 4.构建自定义Vue实例

```javascript
class Nue {
    constructor(options){
        // 1.保存创建时候传递过来的数据
        if(this.isElement(options.el)){
            this.$el = options.el;
        }else{
            this.$el = document.querySelector(options.el);
        }
        this.$data = options.data;
        // 2.根据指定的区域和数据去编译渲染界面
        if(this.$el){
            new Compiler(this)
        }
    }
    // 判断是否是一个元素
    isElement(node){
        return node.nodeType === 1;
    }
}
class Compiler {
    constructor(vm){
        this.vm = vm;
    }
}
```

### 5.提取元素到内存中

```javascript
class Nue {
    constructor(options){
        // 1.保存创建时候传递过来的数据
        if(this.isElement(options.el)){
            this.$el = options.el;
        }else{
            this.$el = document.querySelector(options.el);
        }
        this.$data = options.data;
        // 2.根据指定的区域和数据去编译渲染界面
        if(this.$el){
            new Compiler(this);
        }
    }
    // 判断是否是一个元素
    isElement(node){
        return node.nodeType === 1;
    }
}
class Compiler {
    constructor(vm){
        this.vm = vm;
        // 1.将网页上的元素放到内存中
        let fragment = this.node2fragment(this.vm.$el);
        console.log(fragment);
        // 2.利用指定的数据编译内存中的元素
        // 3.将编译好的内容重新渲染会网页上
    }
    node2fragment(app){
        // 1.创建一个空的文档碎片对象
        let fragment = document.createDocumentFragment();
        // 2.编译循环取到每一个元素
        let node = app.firstChild;
        while (node){
            // 注意点: 只要将元素添加到了文档碎片对象中, 那么这个元素就会自动从网页上消失
            fragment.appendChild(node);
            node = app.firstChild;
        }
        // 3.返回存储了所有元素的文档碎片对象
        return fragment;
    }
}
```

### 6.查找指令和模板

```javascript
class Nue {
    constructor(options){
        // 1.保存创建时候传递过来的数据
        if(this.isElement(options.el)){
            this.$el = options.el;
        }else{
            this.$el = document.querySelector(options.el);
        }
        this.$data = options.data;
        // 2.根据指定的区域和数据去编译渲染界面
        if(this.$el){
            new Compiler(this);
        }
    }
    // 判断是否是一个元素
    isElement(node){
        return node.nodeType === 1;
    }
}
class Compiler {
    constructor(vm){
        this.vm = vm;
        // 1.将网页上的元素放到内存中
        let fragment = this.node2fragment(this.vm.$el);
        // 2.利用指定的数据编译内存中的元素
        this.buildTemplate(fragment);
        // 3.将编译好的内容重新渲染会网页上
    }
    node2fragment(app){
        // 1.创建一个空的文档碎片对象
        let fragment = document.createDocumentFragment();
        // 2.编译循环取到每一个元素
        let node = app.firstChild;
        while (node){
            // 注意点: 只要将元素添加到了文档碎片对象中, 那么这个元素就会自动从网页上消失
            fragment.appendChild(node);
            node = app.firstChild;
        }
        // 3.返回存储了所有元素的文档碎片对象
        return fragment;
    }
    buildTemplate(fragment){
        let nodeList = [...fragment.childNodes];
        nodeList.forEach(node=>{
            // 需要判断当前遍历到的节点是一个元素还是一个文本
            // 如果是一个元素, 我们需要判断有没有v-model属性
            // 如果是一个文本, 我们需要判断有没有{{}}的内容
            if(this.vm.isElement(node)){
                // 是一个元素
                this.buildElement(node);
                // 处理子元素(处理后代)
                this.buildTemplate(node);
            }else{
                // 不是一个元素
                this.buildText(node);
            }
        })
    }
    buildElement(node){
        let attrs = [...node.attributes];
        attrs.forEach(attr => {
            let {name, value} = attr;
            if(name.startsWith('v-')){
                console.log('是Vue的指令, 需要我们处理', name);
            }
        })
    }
    buildText(node){
        let content = node.textContent;
        let reg = /\{\{.+?\}\}/gi;
        if(reg.test(content)){
            console.log('是{{}}的文本, 需要我们处理', content);
        }
    }
}
```

### 7.编译指令数据

```javascript
let CompilerUtil = {
    getValue(vm, value){
        // time.h --> [time, h]
       return value.split('.').reduce((data, currentKey) => {
            // 第一次执行: data=$data, currentKey=time
            // 第二次执行: data=time, currentKey=h
            return data[currentKey];
        }, vm.$data);
    },
    model: function (node, value, vm) { // value=time.h
        /*node.value = vm.$data[value]; // vm.$data[time.h] --> vm.$data[time] --> time[h]*/
        let val = this.getValue(vm, value);
        node.value = val;
    },
    html: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.innerHTML = val;
    },
    text: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.innerText = val;
    }
}
class Nue {
    constructor(options){
        // 1.保存创建时候传递过来的数据
        if(this.isElement(options.el)){
            this.$el = options.el;
        }else{
            this.$el = document.querySelector(options.el);
        }
        this.$data = options.data;
        // 2.根据指定的区域和数据去编译渲染界面
        if(this.$el){
            new Compiler(this);
        }
    }
    // 判断是否是一个元素
    isElement(node){
        return node.nodeType === 1;
    }
}
class Compiler {
    constructor(vm){
        this.vm = vm;
        // 1.将网页上的元素放到内存中
        let fragment = this.node2fragment(this.vm.$el);
        // 2.利用指定的数据编译内存中的元素
        this.buildTemplate(fragment);
        // 3.将编译好的内容重新渲染会网页上
        this.vm.$el.appendChild(fragment);
    }
    node2fragment(app){
        // 1.创建一个空的文档碎片对象
        let fragment = document.createDocumentFragment();
        // 2.编译循环取到每一个元素
        let node = app.firstChild;
        while (node){
            // 注意点: 只要将元素添加到了文档碎片对象中, 那么这个元素就会自动从网页上消失
            fragment.appendChild(node);
            node = app.firstChild;
        }
        // 3.返回存储了所有元素的文档碎片对象
        return fragment;
    }
    buildTemplate(fragment){
        let nodeList = [...fragment.childNodes];
        nodeList.forEach(node=>{
            // 需要判断当前遍历到的节点是一个元素还是一个文本
            // 如果是一个元素, 我们需要判断有没有v-model属性
            // 如果是一个文本, 我们需要判断有没有{{}}的内容
            if(this.vm.isElement(node)){
                // 是一个元素
                this.buildElement(node);
                // 处理子元素(处理后代)
                this.buildTemplate(node);
            }else{
                // 不是一个元素
                this.buildText(node);
            }
        })
    }
    buildElement(node){
        let attrs = [...node.attributes];
        attrs.forEach(attr => {
            let {name, value} = attr; // v-model="name" / name:v-model / value:name
            if(name.startsWith('v-')){ // v-model / v-html / v-text / v-xxx
                let [_, directive] = name.split('-'); // v-model -> [v, model]
                CompilerUtil[directive](node, value, this.vm);
            }
        })
    }
    buildText(node){
        let content = node.textContent;
        let reg = /\{\{.+?\}\}/gi;
        if(reg.test(content)){
            console.log('是{{}}的文本, 需要我们处理', content);
        }
    }
}
```

### 8.编译模板数据

```javascript
let CompilerUtil = {
    getValue(vm, value){
        // time.h --> [time, h]
       return value.split('.').reduce((data, currentKey) => {
            // 第一次执行: data=$data, currentKey=time
            // 第二次执行: data=time, currentKey=h
            return data[currentKey.trim()];
        }, vm.$data);
    },
    getContent(vm, value){
        // console.log(value); //  {{name}}-{{age}} -> 李南江-{{age}}  -> 李南江-33
        let reg = /\{\{(.+?)\}\}/gi;
        let val = value.replace(reg, (...args) => {
            // 第一次执行 args[1] = name
            // 第二次执行 args[1] = age
            // console.log(args);
            return this.getValue(vm, args[1]); // 李南江, 33
        });
        // console.log(val);
        return val;
    },
    model: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.value = val;
    },
    html: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.innerHTML = val;
    },
    text: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.innerText = val;
    },
    content: function (node, value, vm) {
        // console.log(value); // {{ name }} -> name -> $data[name]
        let val = this.getContent(vm, value);
        node.textContent = val;
    }
}
class Nue {
    constructor(options){
        // 1.保存创建时候传递过来的数据
        if(this.isElement(options.el)){
            this.$el = options.el;
        }else{
            this.$el = document.querySelector(options.el);
        }
        this.$data = options.data;
        // 2.根据指定的区域和数据去编译渲染界面
        if(this.$el){
            new Compiler(this);
        }
    }
    // 判断是否是一个元素
    isElement(node){
        return node.nodeType === 1;
    }
}
class Compiler {
    constructor(vm){
        this.vm = vm;
        // 1.将网页上的元素放到内存中
        let fragment = this.node2fragment(this.vm.$el);
        // 2.利用指定的数据编译内存中的元素
        this.buildTemplate(fragment);
        // 3.将编译好的内容重新渲染会网页上
        this.vm.$el.appendChild(fragment);
    }
    node2fragment(app){
        // 1.创建一个空的文档碎片对象
        let fragment = document.createDocumentFragment();
        // 2.编译循环取到每一个元素
        let node = app.firstChild;
        while (node){
            // 注意点: 只要将元素添加到了文档碎片对象中, 那么这个元素就会自动从网页上消失
            fragment.appendChild(node);
            node = app.firstChild;
        }
        // 3.返回存储了所有元素的文档碎片对象
        return fragment;
    }
    buildTemplate(fragment){
        let nodeList = [...fragment.childNodes];
        nodeList.forEach(node=>{
            // 需要判断当前遍历到的节点是一个元素还是一个文本
            if(this.vm.isElement(node)){
                // 是一个元素
                this.buildElement(node);
                // 处理子元素(处理后代)
                this.buildTemplate(node);
            }else{
                // 不是一个元素
                this.buildText(node);
            }
        })
    }
    buildElement(node){
        let attrs = [...node.attributes];
        attrs.forEach(attr => {
            let {name, value} = attr; // v-model="name" / name:v-model / value:name
            if(name.startsWith('v-')){ // v-model / v-html / v-text / v-xxx
                let [_, directive] = name.split('-'); // v-model -> [v, model]
                CompilerUtil[directive](node, value, this.vm);
            }
        })
    }
    buildText(node){
        let content = node.textContent;
        let reg = /\{\{.+?\}\}/gi;
        if(reg.test(content)){
            CompilerUtil['content'](node, content, this.vm);
        }
    }
}
```

### 9.监听数据发生变化

```javascript
let CompilerUtil = {
    getValue(vm, value){
        // time.h --> [time, h]
       return value.split('.').reduce((data, currentKey) => {
            // 第一次执行: data=$data, currentKey=time
            // 第二次执行: data=time, currentKey=h
            return data[currentKey.trim()];
        }, vm.$data);
    },
    getContent(vm, value){
        // console.log(value); //  {{name}}-{{age}} -> 李南江-{{age}}  -> 李南江-33
        let reg = /\{\{(.+?)\}\}/gi;
        let val = value.replace(reg, (...args) => {
            // 第一次执行 args[1] = name
            // 第二次执行 args[1] = age
            // console.log(args);
            return this.getValue(vm, args[1]); // 李南江, 33
        });
        // console.log(val);
        return val;
    },
    model: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.value = val;
    },
    html: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.innerHTML = val;
    },
    text: function (node, value, vm) {
        let val = this.getValue(vm, value);
        node.innerText = val;
    },
    content: function (node, value, vm) {
        // console.log(value); // {{ name }} -> name -> $data[name]
        let val = this.getContent(vm, value);
        node.textContent = val;
    }
}
class Nue {
    constructor(options){
        // 1.保存创建时候传递过来的数据
        if(this.isElement(options.el)){
            this.$el = options.el;
        }else{
            this.$el = document.querySelector(options.el);
        }
        this.$data = options.data;
        // 2.根据指定的区域和数据去编译渲染界面
        if(this.$el){
            // 第一步: 给外界传入的所有数据都添加get/set方法
            //         这样就可以监听数据的变化了
            new Observer(this.$data);
            new Compiler(this);
        }
    }
    // 判断是否是一个元素
    isElement(node){
        return node.nodeType === 1;
    }
}
class Compiler {
    constructor(vm){
        this.vm = vm;
        // 1.将网页上的元素放到内存中
        let fragment = this.node2fragment(this.vm.$el);
        // 2.利用指定的数据编译内存中的元素
        this.buildTemplate(fragment);
        // 3.将编译好的内容重新渲染会网页上
        this.vm.$el.appendChild(fragment);
    }
    node2fragment(app){
        // 1.创建一个空的文档碎片对象
        let fragment = document.createDocumentFragment();
        // 2.编译循环取到每一个元素
        let node = app.firstChild;
        while (node){
            // 注意点: 只要将元素添加到了文档碎片对象中, 那么这个元素就会自动从网页上消失
            fragment.appendChild(node);
            node = app.firstChild;
        }
        // 3.返回存储了所有元素的文档碎片对象
        return fragment;
    }
    buildTemplate(fragment){
        let nodeList = [...fragment.childNodes];
        nodeList.forEach(node=>{
            // 需要判断当前遍历到的节点是一个元素还是一个文本
            if(this.vm.isElement(node)){
                // 是一个元素
                this.buildElement(node);
                // 处理子元素(处理后代)
                this.buildTemplate(node);
            }else{
                // 不是一个元素
                this.buildText(node);
            }
        })
    }
    buildElement(node){
        let attrs = [...node.attributes];
        attrs.forEach(attr => {
            let {name, value} = attr; // v-model="name" / name:v-model / value:name
            if(name.startsWith('v-')){ // v-model / v-html / v-text / v-xxx
                let [_, directive] = name.split('-'); // v-model -> [v, model]
                CompilerUtil[directive](node, value, this.vm);
            }
        })
    }
    buildText(node){
        let content = node.textContent;
        let reg = /\{\{.+?\}\}/gi;
        if(reg.test(content)){
            CompilerUtil['content'](node, content, this.vm);
        }
    }
}
class Observer{
    // 只要将需要监听的那个对象传递给Observer这个类
    // 这个类就可以快速的给传入的对象的所有属性都添加get/set方法
    constructor(data){
        this.observer(data);
    }
    observer(obj){
        if(obj && typeof obj === 'object'){
            // 遍历取出传入对象的所有属性, 给遍历到的属性都增加get/set方法
            for(let key in obj){
                this.defineRecative(obj, key, obj[key])
            }
        }
    }
    // obj: 需要操作的对象
    // attr: 需要新增get/set方法的属性
    // value: 需要新增get/set方法属性的取值
    defineRecative(obj, attr, value){
        // 如果属性的取值又是一个对象, 那么也需要给这个对象的所有属性添加get/set方法
        this.observer(value);
        Object.defineProperty(obj, attr, {
            get(){
                return value;
            },
            set:(newValue)=>{
                if(value !== newValue){
                    // 如果给属性赋值的新值又是一个对象, 那么也需要给这个对象的所有属性添加get/set方法
                    this.observer(newValue);
                    value = newValue;
                    console.log('监听到数据的变化, 需要去更新UI');
                }
            }
        })
    }
}
```

### 10.数据驱动界面更新

```javascript
let Util={
    getValue(vm,value){
        return value.split('.').reduce((data,currentKey)=>{
            return data[currentKey.trim()]
        },vm.$data)
    },
    getContent(vm,value){
        let reg=/\{\{(.+?)\}\}/gi
        let val=value.replace(reg,(...args)=>{
            console.log(args);
            return this.getValue(vm,args[1])    
        })
        return val
    },
    setValue(vm,attr,newValue){
        attr.split('.').reduce((data,currentKey)=>{
            if(index===arr.length-1){
                data[currentAttr]=newValue
            }
            return data[currentKey]
        },vm.$data)
    },
    model:function(node,value,vm){
        //在第一次渲染的时候，就给所有属性添加观察者
        new Watcher(vm,value,(newValue,oldValue)=>{
            node.value=newValue
        })
        // node.value=vm.$data[value]
        let val=this.getValue(vm,value);
        node.value=val;
        
        //界面驱动数据更新
        node.addEventListener('input',(e)=>{
            let newValue=e.target.value
            this.setValue(vm,value,newValue)
        })


    },
    html:function(node,value,vm){
        // node.value=vm.$data[value]
        new Watcher(vm,value,(newValue,oldValue)=>{
            node.innerHTML=newValue
        })
        let val=this.getValue(vm,value);
        node.innerHTML=val;

    },
    text:function(node,value,vm){
        // node.value=vm.$data[value]
        new Watcher(vm,value,(newValue,oldValue)=>{
            node.innerText=newValue
        })
        let val=this.getValue(vm,value);
        node.innerText=val;

    },
    content:function(node,value,vm){
        let val=this.getContent(vm,value);
        let reg=/\{\{(.+?)\}\}/gi
        let val=value.replace(reg,(...args)=>{
            new Watcher(vm,args[1],(newValue,oldValue)=>{
                node.innerText=this.getContent(vm,value)
            })
            return this.getValue(vm,args[1])    
        })
        node.textContent=val;
    },
    on:function(node,value,vm,type){
        node.addEventListener(type,(e)=>{
            console.log("事件注册成功了");
            vm.$methods[value],call(vm,e)
        })
    }
}
class Nue{
    constructor(options){
        //1.保存传递过来的数据
        if(this.isElement(options.el)){
            this.$el=options.el
        }else{
            this.$el=document.querySelector(options.el)
        }
        this.$data=options.data
        this.proxyData(this.$data)
        this.$methods=options.methods
        this.$computed=options.computed
        this.computed2data()
        //2.根据指定的区域和数据渲染界面
        if(this.$el){
            //1.给外界传入的所有数据都添加get/set方法,这样就可以监听数据变化了
            new Observer(this)
            new Renderer(this)
        }
    }
    computed2data(){
        for(let key in this.$computed){
            Object.defineProperty(this.$data,key,{
                get(){
                    return this.$computed[key].call(this)
                }
            })
           }
    }
    proxyData(){
        for(let key in this.$data){
         Object.defineProperty(this,key,{
             get(){
                 return this.$data[key]
             }
         })
            
        }
    }
    isElement(node){
        return node.nodeType===1
    }

}

class Renderer{
    constructor(vm){
        this.vm=vm
        //1.将网页上的与元素放到内存中
        let fragments=node2fragments(this.vm.$el)
        //2.利用指定的数据编译内存中的元素
        this.buildTemplate(fragments)
        //3.将编译好的内容重新渲染到网页上
        this.vm.$el.appendChild(fragment) 
    }
    node2fragments(app){
        //1.创建空的文档碎片对象
        let fragment=document.createDocumentFragment();
        //2.依次循环取出每一个元素
        let node=app.firstChild(node) 
        while(node){
            fragment.appendChild(node)
            node=app.firstChild
        }
        //3.返回储存所有元素的文档碎片对象
        return fragment
    }
    buildTemplate(fragment){
        let nodeList=[...fragment.childNodes]
        //需要判断当前遍历的节点是一个元素还是一个文本
        //如果是一个元素，我们需要判断有没有v-model属性
        //如果是一个文本，我们需要判断有没有{{}}的内容
        nodeList.forEach((node)=>{
            if(this.vm.isElement(node)){
                //是一个元素
                this.buildElement(node)
                // 递归处理子元素
                this.buildTemplate(node)
            }else{
                //不是一个元素
                this.buildText(node)
            }
        })
    }
    buildElement(node){
        let attrs=[...node.attributes]
        attrs.forEach((attr)=>{
            console.log(attr);
            let {name,value} = attr
            if(name.startsWith('v-')){
                //替换内容

                let [directiveName,directiveType]=name.split(':')
                let [,directive]=name.split('-')
                Util[directive](node,value,this.vm,directiveType) 
            }
        })

    }
    buildText(node){ 
        let content =node.textContent
        let reg=/\{\{.+?\}\}/gi
        if(reg.test(content)){
            console.log("{{}}的文本，需要处理");
        }
    } 
}

class Observer{
    constructor(data){
        this.observer(data)
    }
    observer(obj){
        if(obj && typeof obj ==="object"){
            for(let key in obj){
                this.defineReactive(obj,key, obj[key])
            }
        }
    }
    defineReactive(obj,key,value){
        if(typeof value === "object"){
            this.observer(value)
        }
        //将当前所有属性的观察者对象都放到当前属性的发布订阅对象中管理起来
        let dep=new Dep() 
        Object.defineProperty(obj,key,{
            get(){
                Dep.target&&dep.addSub(Dep.target)
                return value;
            },
            set:(newValue)=>{
                if(typeof newValue==="object"){
                     this.observer(newValue)
                }
                if(newValue!==oldValue){
                    value=newValue;
                    dep.notify()
                    console.log("监听到数据的变化");
                }
            }
        })
    }
}

//想要实现数据数据变化后更新ui界面，可以使用发布订阅模式
//先定义一个观察者的类，载定义一个发布订阅的类，然后再通过发布订阅的类来管理观察者的类

class Watcher{
    constructor(vm,attr,cb){
        this.vm = vm;
        this.attr = attr;
        this.cb = cb; 
        //在创建观察者对象的时候就去获取当前的旧值
        this.oldValue=this.getOldValue()
    }
    getOldValue(){
        Dep.target=this
        let oldValue=Util.getValue(this.vm,attr);
        Dep.target=null
        return oldValue
    }
    //定义一个更新的方法，用于判断新值和旧值是否相同
    update(){
         let newValue=Util.getValue(this.vm,attr)
         if(newValue!==this.oldValue){
             this.cb(newValue,this.oldValue)
         }
    }
}

class Dep{
    constructor(){
        //管理某个属性所有的观察者对象的
        this.subs=[]
    }
    //订阅观察
    addSub(water){
        this.subs.push(water)
    }
    //发布订阅
    notify(){
         this.subs.forEach(watcher=>{
             watcher.update()
         })
    }
}
```

```javascript
响应式原理：总体上来说，就是Object.defineProperty结合观察者-发布订阅模式来实现，细节上的话，就是先创建一个观察者和发布订阅的类，在观察者中能定义更新方法，在发布订阅中添加将观察者对象存在数组的方法，再添加遍历执行观察者们里更新方法，数据驱动界面更新就是把网页内容放在内存中编译的时候，递归遍历属性或文字，给属性或者模板添加观察者对象，然后就在Object.defineProperty里的get方法执行发布订阅里添加观察者对象那个方法，set方法遍历发布订阅类里观察者对象数组里的更新内容的方法。
```

### 11.vue-router

```javascript

```

