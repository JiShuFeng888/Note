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

```

