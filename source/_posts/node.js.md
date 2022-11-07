---
title: node
swiper: true # 将改文章放入轮播图中
swiperImg: '/medias/14.jpg' # 该文章在轮播图中的图片
swiperDesc: ''
categories: 'node' #分类
top: false #推荐文章
tags: node
---

### node 写接口

#### 框架

##### NestUS 官网：<https://nestjs.bootcss.com/first-steps>

下载依赖

```js
npm i -g @nestjs/cli
```

创建项目

```js
nest new project-name
```

启动项目

```js
npm run start
```

项目地址：<http://localhost:3000>

#### 抒写接口

创建接口名 user

```js
nest g resource user
```

创建 get,post 请求
{% asset_img api.jpg %}

返回参数
{% asset_img data.jpg %}

快捷键
{% asset_img nest.jpg %}
