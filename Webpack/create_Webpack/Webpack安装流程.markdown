# Webpack安装流程
## 前提

已经安装了Node运行环境
<br/>
<br/>
## 第一步：初始化项目
<br/>

**1.** 创建项目文件夹

**2.** 输入命令行初始化项目：`npm init`
   *  `package name：` 项目名
   *  `version(1.0.0)：` 项目版本
   *  `description：` 关于项目的描述
   *  `entry point：` 入口文件
   *  `test command：` script快捷测试命令
   *  `git repository：` git存储仓库地址
   *  `keyword：` 项目关键字
   *  `author：` 作者
   *  `license：` 证书(ISC)


**3.** 最后选择Yes，初始化完成
<br/>
<br/>

## 第二步：安装webpack
 
   * **本地**（建议）
     * 安装命令： `npm i -D webpack@4.32.2` 
     * 建议使用这个版本的webpack
   * **全局**（不建议：不同项目依赖不同版本的webpack从而导致冲突）
        * 安装命令：`npm i -g webpack@4.32.2`
<br/>
<br/>

## 第三步：安装webpack-cli
<br/>

    webpack-cli在webpack4之前都是在同一个包里面的，之后就分离出来成为一个独立的包

**注意：** webpack和webpack-cli之间存在版本冲突，极其容（踩）易（坑）报（之）错（路）
<br/>
<br/>
在这里推荐webpack-cli@3.3.2版本，是和上面的webpack版本兼容的
<br/>
<br/>
安装命令（还是建议本地安装）

    npm i -D webpack-cli@3.3.2 

<br/>

## 第四步：创建webpack运行所需要的文件
<br/>

### 1. 创建webpack.config.js配置文件
<br/>

```
// 导入node的path模块
const path = require('path')

// 向外暴露对象
export.modole = {
    // 入口配置
    entry: './main.js',
    // 输出配置
    output: {
        // 打包路径
        path: path.resolve(__dirname, './dist'),
        // 打包文件名
        filename: 'bundle.js'
    }
}
```
这样一个简单的webpack.config.js文件就创建好了
<br/>
<br/>

### 2. 创建index.html文件来调用打包好的bundle.js文件
<br/>

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8"/>
    <title>Document</title>
</head>
<body>
    <div id="app"></div>

    // 导入打包好的压缩文件
    <script src="./dist/bundle.js"></script>
</body>
</html>
```
<br/>

### 3. 创建功能模板文件show.js
<br/>

```
// 通过DOM操作app元素并往里面添加内容
function show(content) {
    window.document.querySelector('#app').innerText = 'Hello，' + content;
}

// 暴露show函数
module.exports = show;
```
<br/>

### 4. 创建入口文件main.js 
<br/>

```
// 导入show.js功能模块
const show = require('./show.js')

// 调用show函数
show('Webpack')
```
<br/>

### 5. 在package.json创建webpack运行命令
<br/>

```
scripts: {
    build: 'webpack --config webpack.config.js'
}
```

### 6. 最后运行本地终端运行命令
<br/>

运行命令：`npm run build`

<br/>

当前目录结构：
```
──项目名
    |
    |──── dist 打包文件夹
    |      |
    |      |_____ bundle.js 打包文件
    |
    |──── node_modules 依赖包
    |
    |──── index.html 主页
    |
    |──── main.js 入口文件
    |
    |──── show.js 功能模板文件
    |
    |──── package.json 项目描述问件
    |
    |──── package-lock.json 项目依赖描述文件
    |
    |──── webpack.config.js webpack配置文件

```

### **最后用浏览器打开index.html文件就可以看到Hello，Webpack**