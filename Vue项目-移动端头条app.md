### 1.项目初始化

```javascript
1、安装vue-cli最新版本
如果有旧版本，卸载旧版本 npm uninstall vue-cli -g
暗转新版本 npm install -g @vue/cli

2、安装指定版本 vue-cli
查询可用版本 npm view vue-cli versions --json
安装指定版本 npm install -g vue-cli@2.9.6
npm install -g @vue/cli@版本号 （vue-cli3以上）

3、查看当前版本
vue -V


# 添加远端仓库地址
git remote add origin 你的远程仓库地址

# 推送提交
git push -u origin master

git add 文件
git commit -m "提交日志"
git push

# 如果修改了提交信息，则重新
git push -u 远程仓库 分支信息
```

### 2.lib-flexible插件设置rem基准值

```javascript
npm install amfe-flexible

import 'amfe-flexible'
```

### 3.postcss-pxtorem实现自动将px转换成rem

```
npm i -D postcss-pxtorem

module.exports = {
  plugins: {
    autoprefixer: {
      //browsers: ['Android >= 4.0', 'iOS >= 8'],
      (写到.browserslistrc里面
      
     > 1%
    #兼容超过百分之一的用户使用的浏览器
    last 2 versions
    #兼容到最后两个版本
    not dead

    Android >= 4.0
    iOS >= 8
    
	)
      
    },
    'postcss-pxtorem': {
      rootValue: 37.5,
      propList: ['*'],
    },
  },
};
```

### 4.nvm命令

```javascript
nvm命令行操作命令
1,nvm nvm list 是查找本电脑上所有的node版本

- nvm list 查看已经安装的版本
- nvm list installed 查看已经安装的版本
- nvm list available 查看网络可以安装的版本

2,nvm install 安装最新版本nvm

3,nvm use <version> ## 切换使用指定的版本node

4,nvm ls 列出所有版本

5,nvm current显示当前版本

6,nvm alias <name> <version> ## 给不同的版本号添加别名

7,nvm unalias <name> ## 删除已定义的别名

8,nvm reinstall-packages <version> ## 在当前版本node环境下，重新全局安装指定版本号的npm包

9,nvm on 打开nodejs控制

10,nvm off 关闭nodejs控制

11,nvm proxy 查看设置与代理

12,nvm node_mirror [url] 设置或者查看setting.txt中的node_mirror，如果不设置的默认是 https://nodejs.org/dist/
　　nvm npm_mirror [url] 设置或者查看setting.txt中的npm_mirror,如果不设置的话默认的是： https://github.com/npm/npm/archive/.

13,nvm uninstall <version> 卸载制定的版本

14,nvm use [version] [arch] 切换制定的node版本和位数

15,nvm root [path] 设置和查看root路径

16,nvm version 查看当前的版本
```

### 5.引入字体图标

### 6. VantUl

```javascript
    <!--  开启路由模式-->
    <van-tabbar v-model="active" route>
    	<van-tabbar-item icon="home-o" to="/">资讯</van-tabbar-item>


```

### 7.路由管理+布局配置

```

```

