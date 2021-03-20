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

