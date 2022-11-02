---
title: vue搭建项目
date: 2022-02-07 13:14:14
swiper: true # 将改文章放入轮播图中
swiperImg: '/medias/10.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
swiperDesc: 'vue2项目搭建' #文字描述
top: false #推荐文章
categories: '项目' #分类
tags: 项目搭建
---

## 搭建开发环境

Vscode：<https://code.visualstudio.com/>
Node：<http://nodejs.cn/>
npm 淘宝镜像:<http://npm.taobao.org/>

```js
#经过下面的配置，以后所有的 npm install 都会经过淘宝的镜像地址下载
npm config set registry https://registry.npm.taobao.org
#查看npm配置信息
npm config list
```

## 脚手架工具 Vue-Cli

安装 vue-cli:

```js
# 安装vue2.X
npm install vue-cli -g
# 安装vue3.X
npm install -g @vue/cli
# 输出版本号说明安装成功
vue --version
# 进入你的项目目录
cd workspace
vue init webpack 项目名
```

创建一个基于 webpack 模板的 vue 应用程序:

```js
# 这里的 mytest 是项目名称
vue init webpack mytest

# 初始化并运行
npm install
npm run dev
```

![](1.jpg)

## 安装 vuex、axios、elemnet-ui、sass、less 等依赖

Axios 依赖:

```js
npm install axios
```

在项目根目录下添加文件夹 utils，新建文件 interceptor.js，添加如下代码：

```js
// 在官方的axios的基础上封装一个添加拦截器的axios
import axios from 'axios'
// 引入路由
import router from '../src/router'

// 配置默认的请求地址头（process.env.VUE_APP_Back）这是走得配置文件中配置的地址，需要改成自己的地址
axios.defaults.baseURL = process.env.VUE_APP_Back

// 全局添加拦截器的作用是可以在每个API前面加上headers的token验证
axios.interceptors.request.use(config => {
  // 判断token是否存在和是否需要token验证的路由
  if (sessionStorage.getItem('token')) {
    config.headers.Authorization = sessionStorage.getItem('token')
  }
  return config
})

// 处理退出响应的拦截器 err可以捕获状态，来进行响应的处理
axios.interceptors.response.use(
  response => {
    // 当状态码等于200时
    if (response.status === 200) {
      const res = response.data
      // 如果code是-1 说明用户注销或者token已经过期了 需要消除localstorage中的token
      if (res.code === -1) {
        clearHandler()
      }
    }
    return response
  },
  err => {
    if (!err.response) {
      this.$message.error('服务器出现问题，请稍后重试！')
      // 跳转到登录界面
      router.push('login')
      return
    }
    // 获取状态码
    const status = err.response.status
    switch (
      status // 其他情况补充处理
    ) {
      case 500:
      case 400:
        this.$message.error('服务器出现问题，请稍后重试！')
        router.push({
          name: 'login'
        })
        break
      case 401:
        this.$message.error('访问资源未授权，请登陆后重试！')
        router.push({
          name: 'login'
        })
        break
      case 403:
        this.$message.error('请求资源暂时不可用，请登陆后重试！')
        router.push({
          name: 'login'
        })
        break
      case 404:
        this.$message.error('请求资源暂不存在，请稍后重试！')
        router.push({
          name: 'login'
        })
        break
    }
    return Promise.reject(error)
  }
)
// 消除localstorage和vuex中的token
function clearHandler() {
  localStorage.removeItem('token')
  // 跳转首页
  router.push({
    path: '/home',
    query: {
      redirect: router.currentRoute.path
    }
  })
}
export default axios
```

main.js 中引入拦截器文件

```js
import axios from '../utils/interceptor'
Vue.prototype.$axios = axios
```

Element 依赖:

```js
npm install element-ui --save
```

main.js 中添加：

```js
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI)
```

Sass 依赖:

```js
npm install node-sass sass-loader --save-dev
```

使用 sass 的地方添加 lang=scss

```js
<style lang="scss" >
ps: 依赖安装失败可能是版本不一致，或者太高所导致
```

Less 依赖:

```js
npm install less less-loader --save
```

使用 less 的地方添加 lang=less

```js
<style lang="less" >
```

## 目录详解

```js
1、build：构建脚本目录
　1）build.js ==> 生产环境构建脚本；
　2）check-versions.js ==> 检查npm，node.js版本；
　3）utils.js ==> 构建相关工具方法；
　5）webpack.base.conf.js ==> webpack基本配置；
　6）webpack.dev.conf.js ==> webpack开发环境配置；
　7）webpack.prod.conf.js ==> webpack生产环境配置；

2、config：项目配置
　1）dev.env.js ==> 开发环境变量；
　2）index.js ==> 项目配置文件；
　3）prod.env.js ==> 生产环境变量；

3、node_modules：npm 加载的项目依赖模块

4、src：这里是我们要开发的目录，基本上要做的事情都在这个目录里。里面包含了几个目录及文件：
　1）assets：资源目录，放置一些图片或者公共js、公共css。这里的资源会被webpack构建；
　2）components：组件目录，我们写的组件就放在这个目录里面；
　3）router：前端路由，我们需要配置的路由路径写在index.js里面；
　4）App.vue：根组件；
　5）main.js：入口js文件；

5、static：静态资源目录，如图片、字体等。不会被webpack构建

6、index.html：首页入口文件，可以添加一些 meta 信息等

7、package.json：npm包配置文件，定义了项目的npm脚本，依赖包等信息

8、README.md：项目的说明文档，markdown 格式

9、.xxxx文件：这些是一些配置文件，包括语法配置，git配置等
```

## 小技巧

解决 vue 不能自动打开浏览器的问题：

```js
1）打开config ==> index.js
2）module.exports配置中找到autoOpenBrowser，默认设置的是false
3) 改为true重启一下，就能自动打开浏览器了
```

为了避免端口冲突，也可以修改 port，打开目录同上

```js
port: 8010
```

解决每次启动需改 IP 地址的问题：

```js
const os = require('os')
//自动获取本机局域网ip地址
function getNetworkIp() {
  let needHost = '' // 打开的host
  try {
    // 获得网络接口列表
    let network = os.networkInterfaces()
    for (let dev in network) {
      let iface = network[dev]
      for (let i = 0; i < iface.length; i++) {
        let alias = iface[i]
        if (alias.family === 'IPv4' && alias.address !== '127.0.0.1' && !alias.internal) {
          needHost = alias.address
        }
      }
    }
  } catch (e) {
    needHost = 'localhost'
  }
  return needHost
}
```

修改 host 即可：

```js
host: getNetworkIp(),
```

## 参考地址

<https://blog.csdn.net/liul99/article/details/95603254>
<https://blog.csdn.net/m0_37508531/article/details/107321292>
<https://blog.csdn.net/weixin_47906106/article/details/119057019>
