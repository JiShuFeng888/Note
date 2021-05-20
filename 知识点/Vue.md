### 1.响应式原理

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

```
响应式原理：总体上来说，就是Object.defineProperty结合观察者-发布订阅模式来实现，细节上的话，就是先创建一个观察者和发布订阅的类，在观察者中能定义更新方法，在发布订阅中添加将观察者对象存在数组的方法，再添加遍历执行观察者们里更新方法，数据驱动界面更新就是把网页内容放在内存中编译的时候，递归遍历属性或文字，给属性或者模板添加观察者对象，然后就在Object.defineProperty里的get方法会添加观察者对象到发布订阅类上，set方法遍历发布订阅类里观察者对象数组里的更新内容的方法。
```

```javascript
## Proxy 相比于 defineProperty 的优势

> Object.defineProperty() 的问题主要有三个：

-   不能监听数组的变化
-   必须遍历对象的每个属性
-   必须深层遍历嵌套的对象

> Proxy 在 ES2015 规范中被正式加入，它有以下几个特点

-   针对对象：针对整个对象，而不是对象的某个属性，所以也就不需要对 keys 进行遍历。这解决了上述 Object.defineProperty() 第二个问题
-   支持数组：Proxy 不需要对数组的方法进行重载，省去了众多 hack，减少代码量等于减少了维护成本，而且标准的就是最好的。

> 除了上述两点之外，Proxy 还拥有以下优势：

-   Proxy 的第二个参数可以有 13 种拦截方法，这比起 Object.defineProperty() 要更加丰富
-   Proxy 作为新标准受到浏览器厂商的重点关注和性能优化，相比之下 Object.defineProperty() 是一个已有的老方法。

##
```

### 2.Vue-Router原理

```javascript

```

### 3.零食知识点

```javascript
爷孙组件传值：
	包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 (class 和 style 除外)。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 (class 和 style 除外)，并且可以通过 v-bind="$attrs" 传入内部组件——在创建高级别的组件时非常有用。
	孙子组件可以通过this.$attrs.属性名或者prop来接收
```

