###  0.初始化Node本地服务器

```
下载文件cmd启动
node app.js
npm install
```

```
vue create 项目名称
```

### 1.初始化index.html中的代码

```javascript
<meta charset="utf-8">
    <!--可以让部分国产浏览器默认采用高速模式渲染页面-->
    <meta name="renderer" content="webkit">
    <!--为了让 IE 浏览器运行最新的渲染模式下-->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <!--SEO三大标签-->
<!--    <title>知渔音乐</title>-->
<!--    <meta name="keywords" content="网易云音乐，音乐，播放器，网易，下载，播放，DJ，免费，明星，精选，歌单，识别音乐，收藏，分享音乐，音乐互动，高音质，320K，音乐社交，官网，移动站，music.163.com">-->
<!--    <meta name="description" content="网易云音乐是一款专注于发现与分享的音乐产品，依托专业音乐人、DJ、好友推荐及社交功能，为用户打造全新的音乐生活。">-->
    <!--
    apple-touch-icon: 是苹果私有的属性
    作用: 指定将网页保存到主屏幕上的时候的图标
    -->
    <link rel="apple-touch-icon"  href="./apple-touch-icon.png">
    <link rel="apple-touch-icon" sizes="114x114" href="./apple-touch-icon114.png">
    <link rel="apple-touch-icon" sizes="152x152" href="./apple-touch-icon152.png">
    <link rel="apple-touch-icon" sizes="180x180" href="./apple-touch-icon180.png">
    <!--网页快捷图标-->
    <link rel="icon" href="./favicon.ico">
```

### 2.利用rem+视口释放来适配移动端

```
      let scale = 1.0 / window.devicePixelRatio;
      let text = `<meta name="viewport" content="width=device-width, initial-scale=${scale}, maximum-scale=${scale}, minimum-scale=${scale}, user-scalable=no">`;
      document.write(text);
      document.documentElement.style.fontSize = window.innerWidth / 7.5 + "px";

注意点: 如果在HTML文件中用到了字符串模板, 字符串模板中用到了变量, 那么html-plugin是无法处理的, 所以会报错
！！！
如果想解决这个问题, 那么我们需要再借助一个loader, html-loader
npm -i -D html-loader
要在项目根目录下创建vue.config.js文件进行配置

vue.config.js就是webpack配置文件
```

### 3.借助postcss-pxtorem实现自动将px转换成rem

```
npm i -D postcss-pxtorem （安装到开发环境）
npm i -d postcss-pxtorem （安装到生产环境）
！！！
包名不会进入package.json里面，因此别人不知道你安装了这个包
npm install -D 就是 npm install --save-dev 安装到开发环境 例如 gulp ，babel，webpack 一般都是辅助工具
npm insatll -s 就是npm install --save 安装到生产环境 如 vue ,react 等de
！！！

新建postcss.config.js配置文件
module.exports={
    configureWebpack:{
        module: {
            rules: [
              {
                test: /\.html$/i,
                loader: 'html-loader',
                options:{
                    minimize:true,//进行压缩
                }
              },
            ],
          }, 
        
    }
}

这个才是
module.exports = {
    plugins: {
      autoprefixer: {},
      'postcss-pxtorem': {
        rootValue: 100, // 根元素字体大小
        // propList: ['width', 'height']
        propList: ['*']
      }
    }
  }
  
```

### 4.借助webpack实现CSS3/ES678语法的兼容*

```
修改.browserslistrc文件

ie >= 8
Firefox >= 3.5
chrome  >= 35
opera >= 11.5
```

### 5.借助fastclick解决移动端100~300ms的点击事件延迟问题

```
npm install fastvlick
import fastclick from 'fastclick'

fastclick.attach(document.body)


npm i 和 npm install 的区别
实际使用的区别点主要如下(windows下)： 
1. 用npm i安装的模块无法用npm uninstall删除，用npm uninstall i才卸载掉 
2. npm i会帮助检测与当前node版本最匹配的npm包版本号，并匹配出来相互依赖的npm包应该提升的版本号 
3. 部分npm包在当前node版本下无法使用，必须使用建议版本 
4. 安装报错时intall肯定会出现npm-debug.log 文件，npm i不一定
```

### 6.初始化默认的全局样式

```
*注意点: 在移动端开发中, 一般情况下我们不需要让字体大小随着屏幕尺寸的变化而变化*
 *由于我们是通过视口缩放来适配移动端的, 所以我们不能直接设置字体大小, 否则字体大小就会随着屏幕尺寸的变化而变化*
```

```
/*
YUI 3.18.1 (build f7e7bcb)
Copyright 2014 Yahoo! Inc. All rights reserved.
Licensed under the BSD License.
http://yuilibrary.com/license/
*/

html{color:#000;background:#FFF}
body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,form,fieldset,legend,input,textarea,p,blockquote,th,td{margin:0;padding:0}
table{border-collapse:collapse;border-spacing:0}
fieldset,img{border:0}
address,caption,cite,code,dfn,em,strong,th,var{font-style:normal;font-weight:normal}
ol,ul{list-style:none}
caption,th{text-align:left}
h1,h2,h3,h4,h5,h6{font-size:100%;font-weight:normal}
q:before,q:after{content:''}
abbr,acronym{border:0;font-variant:normal}
sup{vertical-align:text-top}
sub{vertical-align:text-bottom}
input,textarea,select{font-family:inherit;font-size:inherit;font-weight:inherit;*font-size:100%}
legend{color:#000}
a{text-decoration: none}
#yui3-css-stamp.cssreset{display:none}
```

```html
@import "./variable.scss";
/*根据dpr计算font-size*/
@mixin font_dpr($font-size){
  font-size: $font-size;
  [data-dpr="2"] & { font-size: $font-size * 2;}
  [data-dpr="3"] & { font-size: $font-size * 3;}
}
/*通过该函数设置字体大小，后期方便统一管理；*/
@mixin font_size($size){
  @include font_dpr($size);
}
// 不换行
@mixin no-wrap(){
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}
// 限制行数
@mixin clamp($row){
  overflow:hidden;
  text-overflow:ellipsis;
  display:-webkit-box;
  -webkit-box-orient:vertical;
  -webkit-line-clamp:$row;
}

// 根据属性选择器来设置背景颜色
@mixin bg_color(){
  background: $background-color-theme;
  [data-theme=theme1] & {
    background: $background-color-theme1;
  }
  [data-theme=theme2] & {
    background: $background-color-theme2;
  }
}
@mixin bg_sub_color(){
  background: $background-color-sub-theme;
  [data-theme=theme1] & {
    background: $background-color-sub-theme1;
  }
  [data-theme=theme2] & {
    background: $background-color-sub-theme2;
  }
}

@mixin font_color(){
  color: $font-color-theme;
  [data-theme=theme1] & {
    color: $font-color-theme1;
  }
  [data-theme=theme2] & {
    color: $font-color-theme2;
  }
}
@mixin font_active_color(){
  color: $font-active-color-theme;
  [data-theme=theme1] & {
    color: $font-active-color-theme1;
  }
  [data-theme=theme2] & {
    color: $font-active-color-theme2;
  }
}

@mixin border_color(){
  border-color: $border-color-theme;
  [data-theme=theme1] & {
    border-color: $border-color-theme1;
  }
  [data-theme=theme2] & {
    border-color: $border-color-theme2;
  }
}

@mixin bg_img($url){
  [data-theme=theme] & {
    background-image: url($url + '_163.png');
  }
  [data-theme=theme1] & {
    background-image: url($url + '_qq.png');
  }
  [data-theme=theme2] & {
    background-image: url($url + '_it666.png');
  }
  background-size: cover;
  background-repeat: no-repeat;

  [data-theme=theme][data-dpr='2'] & {
    background-image: url($url + '_163@2x.png');
  }
  [data-theme=theme][data-dpr='3'] & {
    background-image: url($url + '_163@3x.png');
  }
  [data-theme=theme1][data-dpr='2'] & {
    background-image: url($url + '_qq@2x.png');
  }
  [data-theme=theme1][data-dpr='3'] & {
    background-image: url($url + '_qq@3x.png');
  }
  [data-theme=theme2][data-dpr='2'] & {
    background-image: url($url + '_it666@2x.png');
  }
  [data-theme=theme2][data-dpr='3'] & {
    background-image: url($url + '_it666@3x.png');
  }
}
```

```
@import "./reset.scss";
@import "./variable.scss";
@import "./mixin.scss";

html, body{
  width: 100%;
  height: 100%;
  overflow: hidden;
  // 解决IScroll拖拽卡顿问题
  touch-action: none;
}
body{
  @include font_size($font_medium);//!!!
  //font-size: 50px;
  font-family: Helvetica,sans-serif,STHeiTi;
}
img{
  vertical-align: bottom;
}
//base.js
```

### 7.Px/Rem使用技巧

```
把px改成Px就没有就不会转成rem
```

### 8.vscode-Git提交

```
//新建连接远程仓库
git pull origin master -f强行推送覆盖线上版本。
git branch -d 分支名称    来删除本地的分支
```

### 9.头部组件-颜色换肤

```
//封装头部让后引入app.vue,进行渲染

methods: {
    myFn(theme){
    document.documentElement.setAttribute("data-theme",theme)
    }
},
为html标签设置全局属性data-theme，再区scss混合里根据data-theme判断选什么主题颜色
```

```javascript
@mixin bg_img($url){
  [data-theme=theme] & {
    background-image: url($url + '_163.png');
  }
  [data-theme=theme1] & {
    background-image: url($url + '_qq.png');
  }
  [data-theme=theme2] & {
    background-image: url($url + '_it666.png');
  }
  background-size: cover;
  background-repeat: no-repeat;

  [data-theme=theme][data-dpr='2'] & {
    background-image: url($url + '_163@2x.png');
  }
  [data-theme=theme][data-dpr='3'] & {
    background-image: url($url + '_163@3x.png');
  }
  [data-theme=theme1][data-dpr='2'] & {
    background-image: url($url + '_qq@2x.png');
  }
  [data-theme=theme1][data-dpr='3'] & {
    background-image: url($url + '_qq@3x.png');
  }
  [data-theme=theme2][data-dpr='2'] & {
    background-image: url($url + '_it666@2x.png');
  }
  [data-theme=theme2][data-dpr='3'] & {
    background-image: url($url + '_it666@3x.png');
  }
}

```

### 10.文字换肤-tabbar

```
如果点击router-link,会多一个router-link-active的类名
```

```
<template>
    <div class="tabbar">
        <router-link tag="div" class="item" to="/recommend"><span>推荐</span></router-link>
        <router-link tag="div" class="item" to="/singer"><span>歌手</span></router-link>
        <router-link tag="div" class="item" to="/rank"><span>排行</span></router-link>
        <router-link tag="div" class="item" to="/search"><span>搜索</span></router-link>
    </div>
</template>
```

### 11.vue项目-路由切换界面

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
import Recommend from '../views/Recommend.vue'
import Singer from '../views/Singer.vue'
import Rank from '../views/Rank.vue'
import Search from '../views/Search.vue'

Vue.use(VueRouter)

const routes = [
  { path: '/', redirect: '/recommend' },
  { path: '/recommend', component: Recommend },
  { path: '/singer', component: Singer },
  { path: '/rank', component: Rank },
  { path: '/search', component: Search }
]

const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})

export default router





注意点：
import from 加载组件无论加载进来有没有用到，都会加载组件，有性能问题
所以要路由按需加载！！！
```

### 12.路由按需加载（异步加载）*

```javascript
const Foo = () => import('./Foo.vue')
```

![批注 2021-01-13 172032](Vue%E9%A1%B9%E7%9B%AE-%E7%A7%BB%E5%8A%A8%E7%AB%AF%E7%BD%91%E6%98%93%E4%BA%91.assets/%E6%89%B9%E6%B3%A8%202021-01-13%20172032.png)

### 13.网络工具类封装

```javascript
npm install axios
一个模块只能由一个export default 输出
箭头函数如果函数体只有一个表达式，那么表达式将作为函数的返回值，这种写法无须加上return关键字
```

```javascript
import axios from 'axios'
axios.defaults.baseURL = 'http://127.0.0.1:3000';
axios.defaults.timeout = 3000;
// axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
// axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';

//封装自己的get,post请求
//network.js
export default{
    get:function(path='',data={}){
        return new Promise(function(resolve,reject){
            axios.get(path,{
                params:data
            })
            .then(function(response){
                resolve(response)
            })
            .catch(function(error){
                reject(error)
            })
        });

    },
    post:function(path='',data={}){
        return new Promise(function(resolve,reject){
            axios.post(path,data)
            .then(function(response){
                resolve(response)
            })
            .catch(function(error){
                reject(error)
            })
        });

    }
}
```

```
//index.js
搞了半天原来接受export default 传来的参数不用写{}
import Network from './network'

export const getBanner = ()=>network.get('banner?type=2')
```

```
//Recommend.vue
        created(){
             getBanner().then(function(data){
                console.log(data);
            })
            .catch(function(error){
                console.log(error);
            })
        },
```

### 14.Banner组件封装

```
注意swiper的版本号
vue2.x用swiper5
vue3.x同swiper6
```

```javascript
<script>
import { Swiper, SwiperSlide, directive } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'
    export default {
        name:'',
        props:[''],
        data() {
            return {
            wiperOption: {
                loop: true, // 循环模式选项
                    autoplay: {
                    delay: 1000, // 自动切换的时间间隔，单位ms
                    stopOnLastSlide: false, // 当切换到最后一个slide时停止自动切换
                    disableOnInteraction: false // 用户操作swiper之后，是否禁止autoplay。
                },
                // 如果需要分页器
                pagination: {
                    el: '.swiper-pagination'
                },
                //当数据是异步加载的时候
                observer: true,
                observeParents: true,
                observeSlideChildren: true
            }
            }
        },
        components: {
            Swiper,
            SwiperSlide
        },
        directives: {
            swiper: directive
        },
        computed: {},
        beforeMount() {},
        mounted() {},
        methods: {},
        watch: {}

    }

</script>
```

### 15.箭头函数注意点

```
https://blog.csdn.net/weixin_42618289/article/details/80959445
```

### 16.scoped注意点

```
scoped注意点：是模块样式私有化，防止污染全局的样式
所有dom添加了一个唯一不重复的动态属性，然后，给CSS选择器额外添加一个对应的属性选择器来选择该组件中dom，这种做法使得样式私有化。

<div data-v-fed36922 class="scoped">Vue.js scoped</div>
.scoped[data-v-fed36922]{
	font-size:14px;
}

如果想覆盖第三方插件：
<style lang='scss' scoped>
.banner{   
    .item{
        img{
            width: 100%;
            height: 300px;
        }
    }
}
</style>
<style lang="scss">
.banner{
    .swiper-pagination-bullet{
        width: 16px;
        height: 16px;
        background-color: #fff;
        opacity: 1;
    }

}
</style>
```

### 17.组件复用

```javascript
<!--  -->
<template>
    <div class="recommend">
        <Banner :banners="banners"></Banner>
        <Personalized :personalized=personalized title="推荐歌单"></Personalized>
        <Personalized :personalized=albums title="最新专辑"></Personalized>
    </div>
</template>

<script>
import {getBanner,getPersonalized,getAlbum,getNewSong} from '../api/index.js'
import Banner from '../components/Banner'
import Personalized from '../components/personalized'

    export default {
        created(){
            getBanner().then((data)=>(
                this.banners=data.banners
                ))
            .catch(function(error){
                console.log(error);
            }),
             getPersonalized().then((data)=>(
                this.personalized=data.result
                ))
            .catch(function(error){
                console.log(error);
            }),
            getAlbum().then((data)=>(
                this.albums=data.albums.splice(0,6)
                ))
            .catch(function(error){
                console.log(error);
            }),
            getNewSong().then((data)=>(
                 this.newsong=data.result
                ))
            .catch(function(error){
                console.log(error);
            })
        },
        name:'',
        props:[''],
        data () {
            return {
                banners:[],
                personalized:[],
                albums:[],
                newsong:[],
            };
        },
        components: {
            Banner:Banner,
            Personalized:Personalized,

        },
        computed: {},
        beforeMount() {},
        mounted() {},
        methods: {},
        watch: {},
    }

</script>

<style lang='' scoped>

</style>
```

```
   props:{
            personalized:{
                type:Array,
                default:()=>[],
                require:true,
            },
            albums:{
                type:Array,
                default:()=>[],
                require:true,
            },
            title:{
                type:String,
                default:"",
                require:true
            }
        }
```

### 18.图片懒加载(npm-vue-lazyload)

```javascript
npm i vue-lazyload -S

//main.js
import VueLazyload from 'vue-lazyload'
 
Vue.use(VueLazyload)
 
// or with options
Vue.use(VueLazyload, {
  preLoad: 1.3,
  error: 'dist/error.png',
  loading: 'dist/loading.gif',
  attempt: 1
})

<img v-lazy="img.src" >
```

### 19.滚动组件封装（iscroll）

```
html, body{
  width: 100%;
  // height: 100%;
  // overflow: hidden;
  // 解决IScroll拖拽卡顿问题,原因是Iscroll和系统都监听了拖拽事件
  // touch-action: none;
}
```

```
import IScroll from 'iscroll/build/iscroll-probe'
```

```
MutationObserver()
```

```
<!--  -->
<template>
    <div id="wrapper" ref="wrapper">
        <slot></slot>
    </div>
</template>

<script>
import IScroll from 'iscroll/build/iscroll-probe'
    export default {
        name:'Scrollview',
        props:[''],
        data () {
            return {

            };
        },
        mounted() {
            this. iscroll = new IScroll(this.$refs.wrapper, {
            mouseWheel: true,
            scrollbars: false,
            probeType: 3,
            // 解决拖拽卡顿问题
            scrollX: false,
            scrollY: true,
            disablePointer: true,
            disableTouch: false,
            disableMouse: true
            })
            // setTimeout(()=>{
            //     console.log(this.iscroll.maxScrollY);
            //     this.iscroll.refresh();
            //     console.log(this.iscroll.maxScrollY);
            // },3000)
            //1.创建观察者对象
            //只要发生变化，就会调用回调函数
            //numation：发生变化的数组
            //Observer:观察者对象       
            const observer = new MutationObserver((mutationsList, observer)=>{
                this.iscroll.refresh();
            });
            //2.观察者对象的配置
             //subtree: true观察后代节点
            //   attributes: true,
            const config = { childList: true, subtree: true,attributeFilter:['height','offsetHeight']};
            //3.观察者对象(要观察谁,观察的内容)
            observer.observe(this.$refs.wrapper,config)
        },
        components: {},
        computed: {},
        beforeMount() {},
        methods: {},
        watch: {}

    }

</script>

<style scoped>
#wrapper{
    height: 100%;
    width: 100%;
}
</style>
```

### 20.二级路由(子组件调用父组件方法)*

```javascript
    fatherSelectItem(id){
                this.$router.push({
                    path:'/recommend/detail/${id}'
                })
            }
//父组件


   methods: {
            selectItem(id){
                console.log(id);
                this.$emit("select",id)
            },
        },
//子组件

  {
     pa	th: '/recommend', component: Recommend ,
     children:[
       {
         path:'detail/:id',
         component: Detail ,
       }
     ],
  },
//路由配置
/router/index.

//再写个路由出口
    <transition>
    <router-view></router-view>
     </transition>
```

### 21.this.$route首次登场

```javascript
//路由信息对象

this.$route.params.id
```

```
全局注册的行为必须在根 Vue 实例 (通过 new Vue) 创建之前发生
   back(){
                window.history.back();
         }
```

### 22.歌单详情动效

```javascript
       methods: {
            //提供一个监听滚动距离的方法给外界使用
            scrolling(fn){
                this.iscroll.on("scroll",function(){
                    fn(this.y)
                })
            }
        },
//scrollview.vue
            
            
          mounted() {
            let defaultHeight=this.$refs.top.$el.offsetHeight
            this.$refs.scrollview.scrolling((offsetY)=>{
                // console.log(offsetY);
                if(offsetY>0){
                    let scale=1+offsetY/defaultHeight
                    this.$refs.top.$el.style.transform=`scale(${scale})`
                }else{
                     let scale=10*Math.abs(offsetY)/defaultHeight
                    this.$refs.top.$el.style.filter=`blur(${scale}px)`
                }
            })
        },
//detail.vue

            let defaultHeight=this.$refs.top.$el.offsetHeight()
//获取组件根元素的高度



```

### 23.跳转界面添加过度动画

```javascript
        <transition>
        <router-view></router-view>
        </transition>
```

### 24.组件复用

```javascript
        created(){
            if(this.$route.params.type==="personalized"){
                getPlayList({id:this.$route.params.id})
                    .then((data)=>{
                        this.playlist=data.playlist
                        console.log(this.playlist);
                        // console.log(this.$route);
                    })
                    .catch((error)=>{
                        console.log(error);
                    })

            }else if(this.$route.params.type==="albums"){
                getAlbumList({id:this.$route.params.id})
                    .then((data)=>{
                        this.playlist={
                            name:data.album.name,
                            coverImgUrl:data.album.picUrl,
                            tracks:data.songs
                        }
                    })
                    .catch((error)=>{
                        console.log(error);
                    })
            }
        },
```

### 25.ios调试兼容

```javascript
.recommend-wrapper{
    width: 100%;
    height: 100%;
    overflow: hidden;
}


        <div class="recommend-wrapper">
        <scrollview>
            <div>
                <Banner :banners="banners"></Banner>
                <Personalized :personalized=personalized title="推荐歌单" @select="fatherSelectItem" :type="'personalized'"></Personalized>
                <Personalized :personalized=albums title="最新专辑" @select="fatherSelectItem" :type="'albums'"></Personalized>
                <Songlist :songs=songs></Songlist>
            </div>
        </scrollview>
        </div>

//外面包装一层容器，防止overflow穿透到组件内!!!!
.singer{
    width: 100%;
    height: 100%;
    .singer-wrapper{
        position: fixed;
        top: 184px;
        left: 0;
        right: 0;
        bottom: 0;
        overflow: hidden;

//高斯模糊极其消耗性能，建议移动端最多使用一次
//建议用模板
```

### 26.播放器界面初始化

```
//添加到全局
app.vue中

//各种封装播放器组件
```

### 27.vuex首次登场

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    isFullScreen:false,
  },
  mutations: {
    changeFullScreen(state,flag){
      state.isFullScreen=flag;
    }
  },
  //用于保存mutation中的方法的方法
  actions: {
      setFullScreen({commit},flag){
        commit('changeFullScreen',flag);
    }
  },
    //用法：this.$store.dispatch('setFullScreen',true);
  modules: {
  },
  getters:{
    isFullScreen(state){
      return state.isFullScreen
    }
  }
})
//this.$store.getters.isFullScreen  v-show 
```

### 28.vue-mapgetters辅助函数首次登场

```javascript
<div class="normal-player" v-show="this.isFullScreen">

import {mapGetters} from 'vuex'

computed: {
    ...mapGetters([
        'isFullScreen',
    ])
},
	<div class="normal-player" v-show="this.$store.getters.isFullScreen">
    效果 ： 
    <div class="normal-player" v-show="this.isFullScreen">


```

### 29.vue-mapActions

```javascript
import {mapActions} from 'vuex';

        methods: {
            ...mapActions([
                'setFullScreen'
            ]),
            selectMusic(){
				     //效果				this.$store.dispatch('setFullScreen',true);
                        this.setFullScreen(true);
            }
        },
```

### 30.vuex优化模块化，方便管理

```javascript
常量要想做方法名称，就必须使用[]包起来


import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
import state from './state'
import mutations from './mutations'
import actions from './actions'
import getters from './getters'
export default new Vuex.Store({
  state: state,
  mutations: mutations,
  //用于保存mutation中的方法的方法
  actions:actions,
  modules: {
  },
  getters:getters
})

```

```
export const SET_FULL_SCREEN ='SET_FULL_SCREEN';

//mutaions-type.js
```

```
import {SET_FULL_SCREEN} from './mutations-type'
export default{
        [SET_FULL_SCREEN](state,flag){
          state.isFullScreen=flag;
        }
}

//mutation.js
```

```
import {SET_FULL_SCREEN} from './mutations-type'
export default{
        setFullScreen({commit},flag){
          commit(SET_FULL_SCREEN,flag);
      }
}

//action.js
```

```
export default{
    isFullScreen(state){
        return state.isFullScreen;
      }
}

//getters.js
```

```
state.js
```

### 31.vue-velocity配合js钩子

```javascript
npm -i velocity-animate

import Velocity from 'velocity-animate'
import 'velocity-animate/velocity.ui'

百度velocity.js添加动画名称

        methods: {
                enter(el, done){
                // el.offsetWidth;
                // el.offsetHeight;
               Velocity(el,"transition.shrinkIn", { duration: 500 },function(){
                   done();
               });
                //注意点: 动画执行完毕之后一定要调用done回调函数
                // done();
            },
            leave(el){
               Velocity(el,"transition.shrinkOut", { duration: 500 },function(){
                   done();
               });
            }
        },
```

### 32.watch监听vuex中的数据

```javascript
        watch: {
            isPlaying(newvalue,oldvalue){
                if(newvalue){
                    this.$refs.play.classList.remove('active')
                    this.$refs.cd.classList.add('active')
                    }else{
                    this.$refs.play.classList.add('active')
                    this.$refs.cd.classList.remove('active')
                }
            }
        }
```

### 33.async-await首次登场

```javascript
    async function gen() {
        let res1 = await request();
        console.log(res1, 1);
        let res2 = await request();
        console.log(res2, 2);
        let res3 = await request();
        console.log(res3, 3);
    }
    gen();
    /*
    1.async函数
    async函数是ES8中新增的一个函数, 用于定义一个异步函数
    async函数函数中的代码会自动从上至下的执行代码

    2.await操作符
    await操作符只能在异步函数 async function 中使用
    await表达式会暂停当前 async function 的执行，等待 Promise 处理完成。
    若 Promise 正常处理(fulfilled)，其回调的resolve函数参数作为 await 表达式的值，然后继续执行 async function。
    * */

import { getSongDetail } from "./../api/index";




    async setSongDetail({commit},ids){
        let result =await getSongDetail({ids:ids.join(',')});
        console.log(result);
        let list=[];
        let obj={};
        let singer='';
        result.songs.forEach(function(value){
          obj.name=value.name;
          value.ar.forEach(function(value,index){
              if(index===0){
                singer=value.name;
              }else{
                singer+="-"+value.name;
              }
              obj.singer=singer;
          });
          obj.picUrl=value.al.picUrl;
        });
        list.push(obj);
        commit(SET_SONG_DETAIL,list);
       },
```

### 34.vuex保存歌曲详情信息！

```javascript
在Actions中发送请求获取数据
```

### 35.奇怪的写法和知识点

```javascript
<p>{{getLyric()}}<p>
方法也可以写在大括号里面

for(let key in this.currentLyric){
                    return this.currentLyric[key];
                    //返回第一个的值
}
//注意写法！好久没写都生疏了！

不用增删改查的话可以写index作为:key的值

<li v-for="(value,name,index) in currentLyric" :key="index">{{value}}</li>



        // 数组的map方法:
        // 将满足条件的元素映射到一个新的数组中
		//符合条件的到新数组中
        
        let newArray = arr.map(function (currentValue, currentIndex, currentArray) {
            // console.log(currentValue, currentIndex, currentArray);
            if(currentValue % 2 === 0){
                return currentValue;
            }
        });





        [SET_FULL_SCREEN](state,flag){
            state.isFullScreen=flag;
            if(flag){
                state.isMiniPlayer=false;
                state.isListPlay=false;
            }
        },


ref只能用来获取一个元素


为了避免穿透，子元素应该使用.stop！



currentIndex(newvalue,oldvalue){
    this.$refs.audio.canplay=()=>{

        if(this.isPlaying){
            this.$refs.audio.play();
        }else{
            this.$refs.audio.pause();
        }
    }
}


watch也能监听非vuex数据


//audio事件
 <audio :src="currentSong.url" ref="audio" @timeupdate ="timeupdate"></audio>

audio timeupdate事件！

timeupdate(el){
              this.currentTime=el.currentTarget.currentTime;
         }

:class="[{'active': true}]" 
//通过v-bind绑定类名!!!



transition 要想刚进来时有动画就用appear
```

### 36.有内容增删iscroll记得刷新

```
常刷新
  watch: {
            isListPlay(newvalue,oldvalue){
                this.$refs.list.refresh();
          }
}
```

### 37.拿到组件中的元素

```javascript
this.$refs.lyric.$el.offsetHeight
```

### 38.致命bug-歌词传输错乱问题

```javascript
歌曲的url 不是按照请求的id 顺序来返回的

   async setSongDetail({commit},ids){
        let list=[];
        let result =await getSongDetail({ids:ids.join(',')});
        let url =await getSongUrl({id:ids.join(',')});
        // console.log(result);
        result.songs.forEach(function(value,index){
          let obj={};
          let singer='';
          obj.name=value.name;
          obj.id=value.id;
          // obj.url=url.data[index].url;
          //歌曲的url 不是按照请求的id 顺序来返回的
          for(let i=0;i<url.data.length;i++){
              if(url.data[i].id===value.id){
                obj.url=url.data[i].url;
              }
          }
```

### 39.递归弱鸡

```javascript
      getActionLyricNum(lineNum){
                //设置歌词必高亮
                let result=this.currentLyric[lineNum+""];
                if(result===undefined||result===''){
                    lineNum--;
                    return this.getActionLyricNum(lineNum);
                }else{
                    return lineNum+"";
                }
            }


         currentTime(newvalue,oldvalue){
                //1.设置歌词高亮
                let lineNum=Math.floor(newvalue);
                this.currentLineTime=this.getActionLyricNum(lineNum);
                //2.设置歌词在视野中部
                let lyricTop=document.querySelector("li.active").offsetTop;
                console.log(lyricTop);
                let wrapperHeight=this.$refs.lyric.$el.offsetHeight;
                if(lyricTop>wrapperHeight/2){
                    this.$refs.scroll.scrollTo(0,wrapperHeight/2-lyricTop,100);
                }else{
                    this.$refs.scroll.scrollTo(0,0,100);
                }
                
                
            }
```

### 40.localStorage首次登场

```javascript
created 时期接受并储存！！！！！

  favoriteList(newvalue,oldvalue){
                window.localStorage.setItem('favoriteList', JSON.stringify(newvalue));
            },


  created(){
                    let favoriteLists = JSON.parse(window.sessionStorage.getItem('favoriteList'));
//注意要判断条件为非空
                    if(favoriteLists!==null){
                        this.setFavoriteList(favoriteLists);
        }
 },



  isFavorite(song){
                let result=this.favoriteList.find(function(value){
                    return value.id===song.id;
                });
                return result!==undefined;
            },
```

### 41.vue-mapMutation辅助函数首次登场

```javascript
    methods
				...mapMutations([
                    'SET_SONG_DETAIL'
                ]),

               this.SET_SONG_DETAIL(this.favoriteList)

```

### 42.ios播放状态切换到下一首异常

```javascript
注意点：在ios中不会自动加载歌曲，所以oncanplay不会自动执行
在pc和安卓端，系统会自动加载歌曲，所以oncanplay会自动执行

解决：ondurationchange代替
```

### 43.对接口返回的结果进行直接处理

```
export const getHotSinger = (data) => {
    return new Promise(function(resolve,reject){
        Network.get('/top/artists?offset=0&limit=30',data)
            .then(function(result){
                resolve(result.artists);
            })
            .catch(function(err){
                reject(err);
            })
    })
}
```

### 44.axios-all使用

```javascript
  all: function (list) {
    return new Promise(function (resolve, reject) {
      axios.all(list)
        .then(axios.spread(function (...result) {
          // 两个请求现在都执行完成
          resolve(result)
        }))
        .catch(function (err) {
          reject(err)
        })
    })
  }
```

```javascript
export const getHotSingers = () => {
    return new Promise(function (resolve, reject) {
      Network.get('top/artists?offset=0&limit=5')
        .then(function (result) {
          resolve(result.artists)
        })
        .catch(function (err) {
          reject(err)
        })
    })
  }
  export const getLetterSingers = (letter) => {
    return new Promise(function (resolve, reject) {
        let letterSingers=[];
      Network.all([
        Network.get(`/artist/list?offset=0&limit=5&type=1&area=7&initial=${letter}`),
        Network.get(`/artist/list?offset=0&limit=5&type=2&area=7&initial=${letter}`),
        Network.get(`/artist/list?offset=0&limit=5&type=1&area=96&initial=${letter}`),
        Network.get(`/artist/list?offset=0&limit=5&type=2&area=96&initial=${letter}`),
        Network.get(`/artist/list?offset=0&limit=5&type=1&area=8&initial=${letter}`),
        Network.get(`/artist/list?offset=0&limit=5&type=2&area=8&initial=${letter}`),
      ])
        .then(function (result) {
        result.forEach(function(value){
            letterSingers.push(...value.artists)
        })
        // console.log(letterSingers);
            resolve(letterSingers)
        })
        .catch(function (err) {
          reject(err)
        })
    })
  }

  export const getAllArtist=(letter)=>{
      return new Promise(function(resolve,reject){

          let keys=['热门']
          let list=[getHotSingers()]
          for(let i=65;i<91;i++){
              let char=String.fromCharCode(i);
              keys.push(char)
              list.push(getLetterSingers(char))
          }
          Network.all(list)
            .then(function(result){
                let obj={}
                obj.keys=keys
                obj.list=result
                resolve(obj)
            })
            .catch(function(err){
                reject(err)
            })

      })
  }
```

### 45....运算符神器

```javascript
注意接受数据的时候的this指向问题

scrollview 的内容不要设置h100% 应该为内容自动撑起来 

在使用组件模板时在模板内created分别按类型处理数据
```

### 46.this.$nextTick

```javascript
this.$nextTick()将回调延迟到下次 DOM 更新循环之后执行。在修改数据之后立即使用它，然后等待 DOM 更新。它跟全局方法 Vue.nextTick 一样，不同的是回调的 this 自动绑定到调用它的实例上。

  list(){
              this.$nextTick(function(){
                    console.log(this.$refs.group);
                })
         }


注意：watch只能监听数据的变化，数据变化的时候不一定渲染完成，为了保证渲染完成
，需借助vue的this.$nextTick(function(){
    
})
```

### 47.  vue中的touch事件

```javascript
 data-开头 （自定义属性) 保存在事件对象dataset属性上
 保存的属性值是字符串！！！
 
 
 移动端touch事件对象中比较重要的三个子对象
 touches:        当前屏幕上所有手指的列表
 targetTouches:  保存了元素上所有的手指里列表
 changedTouches: 当前屏幕上刚刚接触的手指或者离开的手指


 手指的位置
 1.screenX/screenY是相对于屏幕左上角的偏移位
2.clientX/clientY是相对于可视区域左上角的偏移位
3.pageX/pageY是相对于内容左上角的偏移位
    
```

```
        methods: {
            touchstart(e){
                let index=parseInt(e.target.dataset.index)
                this._selectKey(index)

                this.beginOffsetY=e.touches[0].pageY
            },
            touchmove(e){
                this.moveOffsetY=e.touches[0].pageY
                let offsetY=(this.moveOffsetY-this.beginOffsetY)/e.target.offsetHeight;
                //偏移多少个index
                let index=parseInt(e.target.dataset.index)+Math.floor(offsetY)
                if(index<0){
                    index=0;
                }else if(index>this.keys.length){
                    index=this.keys.length-1
                }
                this._selectKey(index)

            },
            _selectKey(index){
                this.currentIndex=index;
                this.$refs.scroll.scrollTo(0,-this.groupTop[index],500);
            }
        },
```

```
            <ul class="nav">
                <li v-for="(key,index) in keys" :key="key" @click.stop="selectKey(index)" :class="{'active':currentIndex===index}"
                    :data-index=index
                     @touchstart.stop.prevent="touchstart"                   
                     @touchmove.stop.prevent="touchmove"                   
                >
                    {{key}}
                </li>
            </ul>
```

### 48.scrollView的scrolling()方法-楼层滚动

```javascript
       mounted() {
            this.$refs.scroll.scrolling((y)=>{
                if(y>0){
                    this.currentIndex=0;
                    return;
                }
                //处理中间区域
                for(let i=0;i<this.groupTop.length-1;i++){
                    let prevTop=this.groupTop[i];
                    let nextTop=this.groupTop[i+1];
                    if(-y>=prevTop&&-y<=nextTop){
                        this.currentIndex=i;
                        return
                    }
                }
                //处理最后的区域
                this.currentIndex=this.groupTop.length-1;

            })
        },
```

### 49. 分组标题吸顶失败

```javascript
            this.$refs.scroll.scrolling((y)=>{
                this.scrollY=y;
                if(y>0){
                    this.currentIndex=0;
                    return;
                }
                //处理中间区域
                for(let i=0;i<this.groupTop.length-1;i++){
                    let prevTop=this.groupTop[i];
                    let nextTop=this.groupTop[i+1];
                    if(-y>=prevTop&&-y<=nextTop){
                        this.currentIndex=i;


                        //1.用下一组标题的偏移位+当前的滚动出去的偏移位
                        let diffOffsetY=nextTop+y
                        let fixTitleOffsetY=0;
                        //2.判断计算结果是否是0到60
                        if(diffOffsetY>=0&&diffOffsetY<=this.fixTitleHeight){
                            //需要移动
                            fixTitleOffsetY=diffOffsetY-this.fixTitleHeight
                        }else{
                            fixTitleOffsetY=0;
                        }
                        if (fixTitleOffsetY === this.fixTitleOffsetY) {
                                    return
                         }
                        this.fixTitleOffsetY=fixTitleOffsetY;
                        this.$refs.fixTitle.style.transfrom=`translateY(${fixTitleOffsetY}px)`
                        

                        return
                    }
                }
                //处理最后的区域
                this.currentIndex=this.groupTop.length-1;

            })
```

### 50.v-if/v-else

```javascript
                    <ul class="normal-group" v-if="value==='官方榜'">
                        <li>
                            <div class="rank-left"></div>
                            <div class="rank-right"></div>
                        </li>
                    </ul>
                     <ul class="normal-group" v-else>
                        <li>
                            <div class="rank-left"></div>
                            <div class="rank-right"></div>
                        </li>
                    </ul>
```

### 51.奇怪的知识点

```javascript
 @include no-wrap();
设置文字不换行  给父元素设宽度

解决换行后flex space around  换行后的对齐方式问题！！
.box:after {content: ""; width: 100px; }


```

### 52.模糊搜索

```javascript
v-modal 真是神器 v-show
```

### 53.函数节流-自定义指令 

```javascript
        directives: {
            throttle: {
                // 指令的定义
                inserted: function (el,obj) {
                    let flag =true;
                    el.addEventListener('input',function(){
                        if(!flag){
                            return;
                        }
                        flag = false;
                        setTimeout(function(){
                            flag =true;
                            obj.value();
                        },1000)
                    })
                }
            }
            }




  search(){
                getSearchList({keywords:this.keyword})
                    .then((data)=>{
                        console.log(data);
                        this.songs=data.result.songs;
                    })
                    .catch(function(err){
                        console.log(err);
                    })
            }
```

### 54.网络提示优化（插件）-   axios拦截器

```javascript
// 添加请求拦截器
let count= 0;
axios.interceptors.request.use(function (config) {
  // 在发送请求之前做些什么
  count++;
  Vue.showLoading();
  return config;
}, function (error) {
  // 对请求错误做些什么
  Vue.hiddenLoading();
  return Promise.reject(error);
});

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
  // 对响应数据做点什么
  count--;
  if(count===0){
    Vue.hiddenLoading();
  }
  return response;
}, function (error) {
  // 对响应错误做点什么
  Vue.hiddenLoading();
  return Promise.reject(error);
});
```

### 55.公共头部封装-插槽的使用

```javascript
不能直接设置插槽样式，必须用个标签把它包裹起来

   .left,.right{
        margin-top: 8px;
        width: 84px;
        height: 84px;
        *{
			//通配符选择器的神器用法--代表所有子元素
            width: 100%;
            height: 100%;
        }
    }
```

```
//模板
不能直接设置插槽样式，必须用个标签把它包裹起来
<template>
     <div class="header" @click="changetheme">
        <div class="left">
            <slot name="left"></slot>
        </div>
        <slot name="center"></slot>
        <div class="right">
            <slot name="right"></slot>
        </div>
    </div>
</template>

//使用
import Header from './Header'
  <div slot="left" class="header-left"></div>
        <p slot="center" class="header-title">IMUSIC</p>
<div slot="right" class="header-right"  @click.stop="accountClick"></div>
```

### 56.特定组件缓存优化（防止歌手界面重复渲染）

### 	keep-alive首次登场

```javascript
keep-alive
Props：

include - 字符串或正则表达式。只有名称匹配的组件会被缓存。
exclude - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
max - 数字。最多可以缓存多少组件实例。
用法：

<keep-alive> 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 <transition> 相似，<keep-alive> 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在组件的父组件链中。


<!-- 逗号分隔字符串 -->
<keep-alive include="a,b">
  <component :is="view"></component>
</keep-alive>

<!-- 正则表达式 (使用 `v-bind`) -->
<keep-alive :include="/a|b/">
  <component :is="view"></component>
</keep-alive>

<!-- 数组 (使用 `v-bind`) -->
<keep-alive :include="['a', 'b']">
  <component :is="view"></component>
</keep-alive>
```

### 57.部署刷新404问题

```javascript
vue router index.js  mode为history是不能刷新页面

1.不要使用history ,使用hash
2.服务端配置
```

### 58.SPA缺点/优点

```javascript
seo难度高   只有一个界面，无法针对不同内容编写不同的seo信息
初次加载耗时多  vue中可以使用按需加载

有良好的交互体验，不会重新加载网页，只是局部更新
实现前后端分离开发
减轻服务器压力 只用处理数据不用处理界面
共用一套后端程序代码
  
```

### 59.客户端渲染-服务端渲染-预渲染

![批注 2021-03-14 233834](Vue%E9%A1%B9%E7%9B%AE-%E7%A7%BB%E5%8A%A8%E7%AB%AF%E7%BD%91%E6%98%93%E4%BA%91.assets/%E6%89%B9%E6%B3%A8%202021-03-14%20233834.png)![批注 2021-03-14 234320](Vue%E9%A1%B9%E7%9B%AE-%E7%A7%BB%E5%8A%A8%E7%AB%AF%E7%BD%91%E6%98%93%E4%BA%91.assets/%E6%89%B9%E6%B3%A8%202021-03-14%20234320-1615736643186.png)![批注 2021-03-14 233240](Vue%E9%A1%B9%E7%9B%AE-%E7%A7%BB%E5%8A%A8%E7%AB%AF%E7%BD%91%E6%98%93%E4%BA%91.assets/%E6%89%B9%E6%B3%A8%202021-03-14%20233240-1615736623439-1615736650236.png)

### 60.预渲染插件解决SEO困难问题

```javascript
vue-cli-plugin-prerender-spa
=>   vue add prerender-spa

 将spa变为多页应用 
 会在main.js  和  vue.config.js添加代码

vue.config.js添加需要渲染界面的路由地址并且router的mode不能是hash，只能是history，然后各个页面要按照eslint规范来修改格式才行



    pluginOptions: {
      prerenderSpa: {
        registry: undefined,
        renderRoutes: [
          '/',
          '/recommend',
          '/singer',
          '/rank',
          '/account',
          '/detail',
          '/search'
        ],
        useRenderEvent: true,
        headless: true,
        onlyProduction: true，
		//注意！！！在配置文件加这段代码解决移动端兼容问题
      postProcess: route => {
        // 预渲染内容写入之前的额外操作
        let reg = /<meta name="viewport".*user-scalable=no">/gi
        let res = route.html.match(reg)
        route.html = route.html.replace(res[1], '')

        // 1.根据字符串创建一个网页
        let html = new JSDOM(route.html)
        // 2.从创建好的网页中拿到document对象
        let dom = html.window.document
        // 3.找到对应的元素, 删除对应的元素
        let loadingEle = dom.querySelector('.container')
        dom.body.removeChild(loadingEle)

        route.html = html.serialize()
        return route
      }
      }
    }
```

### 61.vue-meta-info 插件统一管理seo三大标签

```
npm install vue-meta-info --save
安装后在main.js中导入

再新建vue-meta-info.js统一管理

import MetaInfo from './../../vue-meta-info'
     export default {
        metaInfo:MetaInfo.account,
        name:'',
        props:[''],
再注释掉index.js的seo三大标签
```

```
module.exports={
    configureWebpack:{
        module: {
            rules: [
              {
                test: /\.html$/i,
                loader: 'html-loader',
                options:{
                    minimize:true,//进行压缩
                }
              },
            ],
          }, 
        
    },

    pluginOptions: {
      prerenderSpa: {
        registry: undefined,
        renderRoutes: [
          '/',
          '/recommend',
          '/singer',
          '/rank',
          '/account',
          '/detail',
          '/search'
        ],
        useRenderEvent: true,
        headless: true,
        onlyProduction: true
      }
    }
}
```

### 62.预渲染移动端适配问题**

```
解决预渲染时meta标签重复覆盖问题

解决网络提示覆盖问题？？？jsdom插件将字符串转换成document对象
npm install  jsdom --save -d
```

![批注 2021-03-15 192859](Vue%E9%A1%B9%E7%9B%AE-%E7%A7%BB%E5%8A%A8%E7%AB%AF%E7%BD%91%E6%98%93%E4%BA%91.assets/%E6%89%B9%E6%B3%A8%202021-03-15%20192859-1615807771007.png)

### 63.The end-first project

### 64.播放器v1.5版本启动

```javascript
优化播放器背景图片显示,优化动画,修复播放器离场动画失效
优化迷你播放器标题显示
优化列表播放器动画和标题显示
解决歌单第一次点击不是第一首歌曲失效
优化标题到导致换行问题
新增歌曲评论界面
删除接口失效的歌曲排行榜界面,更改为mv界面
多处小地方显示优化
解决字体过小问题
```

### 65.路由跳转类名动画问题

```
父元素不穿透,子元素穿透
```

### 66.史诗级bug-歌单第一次点击不是第一首的歌曲自动播放第一首歌曲

```
第一次尝试
由于songs是通过网络异步获取的,而设置currentIndex是同步的，设置currentIndex为setTimeOut后可以，但是要用户等待根据网络状况等待400ms左右的时间,而且很不稳定
第二次尝试
取消songs异步，用mapMutaion辅助函数直接赋值！！！！！理论上可以
但是失败了！！！因为上一级接口中没有url数据！！！（这不怪我），得根据id重新获歌曲！！！服了又回到第一条
第三次尝试
async神器！！！！！

async selectMusic (id, index) {
  const list = this.playlist.filter(function (value, index) {
    // console.log(value.name);
    if (value.name !== '') {
      return true
    }
  })
  const ids = list.map(function (value) {
    return value.id
  })
  // ids已经是一个数组了
  await this.setSongDetail(ids)
  this.setCurrentIndex(index)
  this.setPlaying(true)
  this.setFullScreen(true)
  // this.$store.dispatch('setFullScreen',true);
},

成功！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！
```

### 67.filter首次使用

```javascript
      filters: {
        // key: 过滤器名称
        // value: 过滤器处理函数
        'formartNum': getFormattedNumber
    }

import { getFormattedNumber } from "../tools/tools";
```

### 67.iscroll容器配置之一

```javascript
.mv{
    overflow: hidden;
    position: fixed;
    top: 184px;
    left: 0;
    right: 0;
    bottom: 0;
    .mv-wrapper{
        width:100%;
        height: 100%;
```

### 68.视频铺满

```
        video{
            width: 100%;
            object-fit: cover;
            height: 100%;
            vertical-align:top;

        }

  <CommentList :type="'mv'"></CommentList>传递字符串
```

### 69.评论显示问题

```
由于在评论组件隐藏时初始化iscroll导致显示滑动不了,通过vuex判断组件是否是显示状态，更改初始化判断条件
```

### 70.微任务MutationObserver--配合iscroll使用

```javascript
    // 1.创建观察者对象
    // 只要发生变化，就会调用回调函数
    // numation：发生变化的数组
    // Observer:观察者对象
    const observer = new MutationObserver((mutationsList, observer) => {
      this.iscroll.refresh()
    })
    // 2.观察者对象的配置
    // subtree: true观察后代节点
    //   attributes: true,
    const config = { childList: true, subtree: true, attributeFilter: ['height', 'offsetHeight'] }
    // 3.观察者对象(要观察谁,观察的内容)
    observer.observe(this.$refs.wrapper, config)
  },
      
    //微任务先执行,再到宏任务
    
    //每次执行完宏任务之后会立即查看微任务队列的内容
      
    //执行所有的同步代码再执行异步代码！！！！！！！
```

### 71.iscroll在ios下点击两次的bug

```
    function iScrollClick(){
    if (/iPhone|iPad|iPod|Macintosh/i.test(navigator.userAgent)) return false;
    if (/Chrome/i.test(navigator.userAgent)) return (/Android/i.test(navigator.userAgent));
    if (/Silk/i.test(navigator.userAgent)) return false;
    if (/Android/i.test(navigator.userAgent)) {
       var s=navigator.userAgent.substr(navigator.userAgent.indexOf('Android')+8,3);
       return parseFloat(s[0]+s[3]) < 44 ? false : true
    }
  }
    this.iscroll = new IScroll(this.$refs.wrapper, {
      // 点击失效问题
      // click: true,
      click:iScrollClick(), //调用判断函数
      mouseWheel: true,
      scrollbars: false,
      probeType: 3,
      // 解决拖拽卡顿问题
      scrollX: false,
      scrollY: true,
      disablePointer: true,
      disableTouch: false,
      disableMouse: true
    })

```

