---
title: webpack打包
date: 2022-02-07 13:13:57
swiper: true # 将改文章放入轮播图中
swiperImg: '/medias/7.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
swiperDesc: '项目打包' #文字描述
top: true
categories: '项目' #分类
tags: 项目打包
---

# webpack 打包

## webpack 在项目中的常见配置

```js
// webpack.config.js
module.exports = {
    mode: 'development', // development|production
	entry: './src/js/entry.js, // 入口配置
	output: {// 输出配置
     filename : 'index.js',// 打包输出文件名
     path : __dirname + '/out'// 打包输出路径（必须绝对路径，否则报错）
    },
	module: {
     rules: [
           {test: /.js$/, use: ['babel-loader']},
           {test: /.css$/, use: ['style-loader', 'css-loader']},
        ]}, // 放置loader加载器，webpack本身只能打包commonjs规范的js文件，用于处理其他文件或语法
	plugins: [], // 插件，扩展功能
	// 以下内容进阶篇再涉及
	resolve: {}, // 为引入的模块起别名
	devServer: {} // webpack-dev-server
};
```

## webpack 打包 vue 项目之后生成的 dist 文件该怎么启动运行

```js
1.安装express-generator生成器
npm install express-generator -g
2. 创建一个express项目
express expressDemo （expressDemo是项目名）
3.进入项目目录，安装相关项目依赖
cd expressDemo
  npm install
4.将dist文件夹下的所有文件复制到express项目的publick文件夹下面
5.运行 npm start 来启动express项目
6.输入localhost:3000
```

## vue-loader 是做什么的

```js
    概念：vue-loader是基于webpack的一个loader，解析和转换.vue文件。
提取出其中的逻辑代码script，样式代码style，以及HTML模板template，
再分别把他们交给对应的loader去处理。
    用途：js可以写es6、style样式可以是less或scss等
```

## webpack 的作用是什么

```js
webpack是一个打包器（bundler），它能将多个js文件打包成一个文件（其实不止能打包js文件，也能打包其他类型的文件，比如css文件，json文件等）
```

## webpack 打包的流程是什么

```js
Webpack首先会把配置参数和命令行的参数及默认参数合并，并初始化需要使用的插件和配置插件等执行环境所需要的参数；初始化完成后会调用Compiler的run来真正启动webpack编译构建过程，webpack的构建流程包括compile、make、build、seal、emit阶段，执行完这些阶段就完成了构建过程.
大概阶段：1、初始化参数(加载插件和处理入口等)
        2、编译阶段(读取文件-编译模块-分析模块依赖关系)
        3、文件输出(渲染源码-执行文件输出-全部完成)
```
