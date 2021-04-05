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

