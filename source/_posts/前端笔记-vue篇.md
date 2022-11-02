---
title: 前端笔记(vue篇)
date: 2022-02-07 13:12:19
swiper: true # 将改文章放入轮播图中
swiperImg: '/medias/6.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
swiperDesc: '前端vue笔记总结' #文字描述
top: true
categories: "前端笔记" #分类
tags: 前端笔记
---
# vue笔记总结
## 什么是Vue？
Vue是一套用于构建用户界面的渐进式JavaScript框架
形成Vue渐进式框架的核心概念为：{% span red, 组件化，MVVM，响应式和生命周期 %}
## vue指令
指令: {% span  red, v-on，v-model，v-cloak，v-once，v-pre，v-text，v-html，v-for，v-show，v-if，
v-else，v-else-if %}
```js
v-on 是事件绑定，可以缩写为@
常用的修饰符也有很多：
比如
.stop用来取消冒泡事件；
.prevent阻止默认事件；
.once只执行一次；当然还有许多。

v-model 是双向绑定，一般用于文本框、单选、复选、下拉；
常用的修饰符有
.lazy - 取代 input 监听 change 事件
.number - 输入字符串转为有效的数字
.trim - 输入首尾空格过滤

v-cloak使用 v-cloak 能够解决插值表达式闪烁的问题

v-once只渲染一次

v-pre跳出渲染

v-text 可以将data中的文本放入元素中

v-html 可以识别标签

v-for 和原生JS的for循环差不多

v-show 判断元素显示还是隐藏
v-show=“true/false”

v-if是条件判断,判断元素显示还是隐藏
当然还有配套的v-else、v-else-if
```
## 怎么理解mvvm这种设计模式

```js
Model–View–ViewModel（MVVM）是一个软件架构设计模式，是一种简化用户界面的事件驱动编程方式。
MVVM
 M Model 模型 指的是数据层
 V View  视图 指的是用户页面
 VM ViewModel 视图模型
视图模型是MVVM模式的核心，它是连接view和model的桥梁，MVVM实现了view和model的自动同步，
当model的属性改变时，我们不用自己手动操作DOM元素，来改变view的显示，称之为数据的双向绑定。
```

## v-if和v-show的区别，使用场景区别
```js
v-if和v-show看起来似乎都是元素显示和隐藏，但是这两个选项是有区别的:
1、v-if在条件切换时，会对标签进行适当的创建和销毁，而v-show则仅在初始化时加载一次，
因此v-if的开销相对来说会比v-show大。
2、v-if是惰性的，只有当条件为真时才会真正渲染标签；如果初始条件不为真，则v-if不会去渲染标签。
v-show则无论初始条件是否成立，都会渲染标签，它仅仅做的只是简单的CSS（display）切换。
3、v-if适用于不需要频繁切换元素显示和隐藏的情况
   v-show适用于需要频繁切换元素的显示和隐藏的场景。
```

## vue事件修饰符和按键修饰符有哪些
```js
事件修饰符：
  .prevent  阻止事件默认行为
  .stop     阻止事件冒泡
  .capture  设置事件捕获机制
  .self     只有点击元素自身才能触发事件
  .once     事件只触发一次
 按键修饰符：
  .tab      空格
  .enter    回车
  .esc      返回 
  .space    空格
  .delete   捕获"删除"和"空格"键
  .up       上
  .down     下
  .left     左
  .right    右
```

## v-model修饰符有哪些
```js
.trim   去除首尾空格
.lazy   只在输入框失去焦点或按回车键时更新内容，不是实时更新
.number 将数据转换成number类型(原本是字符串类型)
```

## v-for中为什么要加key，原理是什么
```js
作用：
  1.key的作用主要是为了高效的更新虚拟DOM，提高渲染性能。
  2.key属性可以避免数据混乱的情况出现。
原理：
  1.vue实现了一套虚拟DOM，使我们可以不直接操作DOM元素只操作数据，就可以重新渲染页面
  2.当页面数据发生变化时，Diff算法只会比较同一层级的节点；
  3.如果节点类型不同，直接干掉前面的节点，再创建并插入新的节点，
  不会再比较这个节点后面的子节点；如果节点类型相同，则会重新设置该节点属性，从而实现节点更新
```

## v-for和v-if的优先级
```js
 v-for优先级高于v-if
如果同时出现v-for和v-if，无论判断条件是否成立，都会执行一遍v-for循环，
这样浪费性能，所以要尽可能的避免两者一起使用。
```

## 插槽（solt）
```js
1、什么是插槽
	1.1 插槽（Slot）是Vue提出来的一个概念，插槽用于决定将所携带的内容，
  插入到指定的某个位置，从而使模板分块，具有模块化的特质和更大的重用性。
	1.2 插槽显不显示、怎样显示是由父组件来控制的，而插槽在哪里显示就由子组件来进行控制
2、插槽使用
	2.1 默认插槽  在子组件中写入slot，slot所在的位置就是父组件要显示的内容
  2.2 具名插槽  在子组件中定义了三个slot标签，其中有两个分别添加了name属性header和footer
    在父组件中使用template并写入对应的slot名字来指定该内容在子组件中现实的位置
  2.3 作用域插槽  在子组件的slot标签上绑定需要的值
    <slot :data="user"></slot>
在父组件上使用slot-scope=“user”来接收子组件传过来的值 
```

## 组件中的data为什么是函数,new Vue 实例里，data 可以直接是一个对象
```js
1、组件是用来复用的，组件中的data写成一个函数,数据以函数返回值形式定义,函数有独立的作用域，
这样每复用一次组件,就会返回一份新的data,类似于给每个组件实例创建一个私有的数据空间,
让各个组件实例维护各自的数据。
2、而单纯的写成对象形式,由于对象是引用类型，就使得所有组件实例共用了一份data,
就会造成一个变了全都会变的结果。
3、因为new vue里面的代码是不存在复用的情况，所以可以写成对象形式
```

## vue 中怎么给 data 动态添加数据，为什么要这样写
```js
1.官方文档定义：如果在vue实例创建之后添加新的属性到实例上，她不会触发视图更新。
2.原因：受现代JavaScript的限制，vue不能检测到对象属性的添加或删除。由于vue会在初始化实例是
对属性执行getter/setter转换过程（使用Object.defineProperty进行数据的劫持）。
所以属性必须在data对象上存在才能让vue转换它，这样才能让它是响应的。
    方法：1.this.$set(对象名，属性，值)或 Vue.set(对象名，属性，值)
          2.Object.assign(target,source)添加多个属性
          例如：
            const target = {a:1, b:2}
            const source = {b:4, d:5}
            const returnedTarget = Object.assign(target,source)
            console.log(returnedTarget); //{ a: 1, b: 4, c: 5 }
```

## computed和watch的区别是什么
```js
计算属性computed：
1、支持缓存，只有依赖数据发生改变，才会重新进行计算
2、不支持异步，当computed内有异步操作时无效，无法监听数据的变化
3、如果computed需要对数据修改，需要写get和set两个方法，当数据变化时，调用set方法。
4、computed擅长处理的场景：一个数据受多个数据影响，例如购物车计算总价
侦听属性watch：
1、不支持缓存，数据变，直接会触发相应的操作；
2、watch支持异步；监听的函数接收两个参数，第一个参数是最新的值；第二个参数是输入之前的值；
3、immediate：组件加载立即触发回调函数执行
4、deep:true的意思就是深入监听，任何修改obj里面任何一个属性都会触发这个监听器里的 handler方法来处理逻辑
5、watch擅长处理的场景：一个数据影响多个数据，例如搜索框
```

## 组件化和模块化的区别
```js
1、组件相当于库，把一些能在项目里或者不同类型项目中可复用的代码进行工具性的封装。
2、模块相应于业务逻辑模块，把同一类型项目里的功能逻辑进行进行需求性的封装。
```

## 怎么理解vue中的虚拟DOM
```js
原理：	
	用 JavaScript 对象模拟真实 DOM 树，对真实 DOM 进行抽象；
diff 算法 — 比较两棵虚拟 DOM 树的差异；
pach 算法 — 将两个虚拟 DOM 对象的差异应用到真正的 DOM 树。

好处：
	1、性能优化
  2、无需手动操作DOM
  3、可以跨平台，服务端渲染等
```

## 怎么理解vue的生命周期
```js
 vue的生命周期：vue实例从创建到销毁的全过程，这个过程可以分为3个阶段
    第一阶段：初始化阶段   创建vue实例,准备数据,准备模板,渲染视图
    第二阶段：数据更新阶段 当数据变化时，会进行新旧DOM的对比，对比出差异的部分进行差异化更新。
    第三阶段：实例销毁阶段 当vm.$destroy()被调用，vue实例就会被销毁，
    释放相关资源，此时再更新数据，视图不会再变化。
```

## vue 钩子函数有哪些，有哪些使用的场景
```js
1、各阶段包含钩子： 
beforeCreate  在data数据注入到vm实例之前，此时vm身上没有数据    
created       在data数据注入到vm实例之前，此时vm身上有数据   
beforeMount   生成的结构替换视图之前，此时DOM还没更新   
mounted       生成的结构替换视图之前，此时DOM已经更新完成    
beforeUpdate  数据变化了，dom更新之前    
updated       数据变化了，dom更新之后        
activated     被keep-alive缓存的组件激活时调用    
deactivated   被keep-alive缓存的组件停用时调用    
beforeDestroy 实例销毁，是否资源之前    
destroyed     实例销毁，是否资源之后    

这些钩子函数会在vue的生命周期的不同阶段，自动被vue调用2、常用的钩子函数使用场景：    
beforeCreate  做loading的一些渲染    
created       结束loading， 发送数据的请求，拿数据    
mounted       可以对dom进行操作    
updated       监视数据的更新    
beforeDestroy 销毁非vue资源，防止内存泄漏，例如清除定时器    
activated     当我们运用了组件缓存时，如果想每次切换都发送一次请求的话，
需要把请求函数写在activated中，而写在created或mounted中其只会在首次加载该组件的时候起作用。
```

## Vue 的父组件和子组件生命周期钩子函数执行顺序
```js
Vue 的父组件和子组件生命周期钩子函数执行顺序可以归类为以下 4 部分：  
1）加载渲染过程  
父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created 
-> 子 beforeMount -> 子 mounted -> 父 mounted  
2）子组件更新过程     
父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated  
3）父组件更新过程     父 beforeUpdate -> 父 updated  4）
4）销毁过程  父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed 
```

## vue组件传值的方式
```js
1、父传子
    通过props传递
    父组件： <child :list = 'list' />
    子组件: props['list'],接收数据,接受之后使用和data中定义数据使用方式一样

2、子传父
	在父组件中给子组件绑定一个自定义的事件，子组件通过$emit()触发该事件并传值。
    父组件： <child @receive = 'getData' />
            getData(value){value就是接收的值}
    子组件: this.$emit('receive',value)

3、兄弟组件传值
	通过中央通信 let bus = new Vue()
    A组件：methods :{ 
    	    sendData(){
                bus.$emit('getData',value)
              } 发送
    B组件：created(){
        bus.$on(‘getData’,(value)=>{value就是接收的数据})
    } 进行数据接收

```

## vue 钩子函数有哪些
```js
beforeCreate 属性 方法加载之前
created    属性和方法加载完成  数据接口加载的时候就在 created
beforeMount 组件渲染之前
mounted   组件加载完成以后   获取元素就在mounted
beforeUpdate 数据更新之前
updated   数据更新完成
beforeDestory 组件即将销毁
destoryed   组件销毁完成
deactivated：在被包裹组件停止使用时调用
activate：是在被包裹组建被激活的状态下使用的生命周期钩子
errorCaptured(错误调用)：当捕获一个来自后代组件的错误时被调用
```

## $nextTick是什么？原理是什么？使用的场景
```js
背景：
	1、简单来说，Vue 在修改数据后，视图不会立刻更新，
  而是等同一事件循环中的所有数据变化完成之后，再统一进行视图更新。
    
定义：
	2、在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，
  获取更新后的 DOM。nextTick()，是将回调函数延迟在下一次dom更新数据后调用，
  简单的理解是：当数据更新了，在dom中渲染后，自动执行该函数。
    
原理
	3、vue用异步队列的方式来控制DOM更新和nextTick回调先后执行。
	简单来说，nextTick是做了promise加上setTimeout的封装,利用事件换行机制，
  来确保当nextTick出现时，都是在我们所有操作DOM更新之后的。

场景：
	4.1 点击获取元素宽度
  4.2 使用swiper插件通过 ajax 请求图片后的滑动问题
  4.3 点击按钮显示原本以 v-show = false 隐藏起来的输入框，并获取焦点
```

## vue是如何获取DOM
```js
1、先给标签设置一个ref值，再通过this.$refs.domName获取，这个操作要在mounted阶段进行。
2、例如：<template><div ref="test"></div></template>
mounted(){ const dom = this.$refs.test }
```

## v-on可以监听多个方法吗
```js
可以例如：<input type="text" v-on="{ input:onInput,focus:onFocus }">
```

## 谈谈你对 keep-alive 的了解
```js
1、keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，避免重新渲染
2、一般结合路由和动态组件一起使用，用于缓存组件
3、对应两个钩子函数 activated 和 deactivated ，当组件被激活时，触发钩子函数 activated，
当组件被移除时，触发钩子函数 deactivated4、提供 include 和 exclude 属性，两者都支持字符串或正则表达式，
include 表示只有名称匹配的组件会被缓存，exclude 表示任何名称匹配的组件都不会被缓存 ，
其中 exclude 的优先级比 include 高；例如：
<keep-alive include="a"> 
<component> <!-- name 为 a 的组件将被缓存！--> </component>
</keep-alive>
<keep-alive exclude="a"> 
<component>  <!-- 除了 name 为 a 的组件都将被缓存！--> </component>
</keep-alive>
```

## vue中动态组件如何使用
```js
1、在某个中使用 is 特性来切换不同的组件：	
<component :is="TabComponent"></component>  
TabComponent:已注册组件的名字
```

## v-model的原理是什么
```js
1、v-model主要提供了两个功能，view层输入值影响data的属性值，属性值发生改变会更新层的数值变化.
2、v-model指令的实现：	
  3.1 v-bind:绑定响应式数据	
  3.2 触发input事件并传递数据 (核心和重点)
3、其底层原理就是(双向数据绑定原理)：	
  3.1 一方面modal层通过defineProperty来劫持每个属性，一旦监听到变化通过相关的页面元素更新。    
  3.2 另一方面通过编译模板文件，为控件的v-model绑定input事件，从而页面输入能实时更新相关data属性值。
```

## vue响应式的原理
```js
1、原理：
	Vue 的响应式原理是核心是通过 ES5 的 Object.defindeProperty 进行数据劫持，
  然后利用 get 和 set 方法进行获取和设置，data 中声明的属性都被添加到了get和set中，
  当读取 data 中的数据时自动调用 get 方法，当修改 data 中的数据时，自动调用 set 方法，
  检测到数据的变化，会通知观察者 Wacher，观察者 Wacher自动触发重新render 当前组件
  （子组件不会重新渲染）,生成新的虚拟 DOM 树，
  Vue 框架会遍历并对比新虚拟 DOM 树和旧虚拟 DOM 树中每个节点的差别，
  并记录下来，最后，加载操作，将所有记录的不同点，局部修改到真实 DOM 树上。

2、底层代码实现：
	   let data = {
        name: "lis",
        age: 20,
        sex: "男"
    }
//  vue2.0实现  使用Object.defineProperty进行数据劫持
    for(let key in data){
        let temp = data[key]
        Object.defineProperty(data, data[key], {
            get(){
                return temp
            },
            set(value){
                temp = value
            }
        })
    }
// vue3.0实现 使用Proxy 进行数据的代理
    let newData = new Proxy(data, {
        get(target, key){
            return target[key]
        },
        set(target, key, value){
            target[key] = value
        }
    })
```

## vue2.0和vue3.0响应式的区别
```js
1、Object.defineProperty 
  1) 用于监听对象的数据变化
  2) 无法监听数组变化(下标，长度)
  3) 只能劫持对象的自身属性，动态添加的劫持不到
2、Proxy
  1) proxy返回的是一个新对象， 可以通过操作返回的新的对象达到目的
  2）可以监听到数组变化，也可以监听到动态添加的数据
```

## router和route的区别
```js
1、$router对象    
  1）$router对象是全局路由的实例，是router构造方法的实例    
  2）$router对象上的方法有：push()、go()、replace()
2、$route对象    
  1）$route对象表示当前的路由信息，包含了当前 URL 解析得到的信息。
  包含当前的路径，参数，query对象等    
  2）$route对象上的属性有：path、params、query、hash等等   
```

## 路由传参params和query区别
```js
  方式：params 和 query2
区别：
  1）params用的是name，传递的参数在地址栏不会显示，类似于post        
  2）query用的是path,传递的参数会在地址栏显示出来，类似于get      
3、举例说明：   
  1）params 传参  
  传： this.$router.push({ name: 'particulars', params: { id: id } })     
  接：this.$route.params.id        
  2）query传参     
  传：this.$router.push({ path: '/particulars', query: { id: id } })     
  接：this.$route.query.id
```

## Vue模版编译原理知道吗，能简单说一下吗
```js
1、简单说，Vue的编译过程就是将template转化为render函数的过程。
2、首先解析模版，生成AST语法树(一种用JavaScript对象的形式来描述整个模板)。
使用大量的正则表达式对模板进行解析，遇到标签、文本的时候都会执行对应的钩子进行相关处理。
3、Vue的数据是响应式的，但其实模板中并不是所有的数据都是响应式的。
有一些数据首次渲染后就不会再变化，对应的DOM也不会变化。
那么优化过程就是深度遍历AST树，按照相关条件对树节点进行标记。
这些被标记的节点(静态节点)我们就可以跳过对它们的比对，对运行时的模板起到很大的优化作用。
4、编译的最后一步是将优化后的AST树转换为可执行的代码。
```

## SSR了解吗
```js
1、SSR也就是服务端渲染，也就是将Vue在客户端把标签渲染成HTML的工作放在服务端完成，
然后再把html直接返回给客户端。
2、SSR有着更好的SEO、并且首屏加载速度更快等优点。不过它也有一些缺点，
比如我们的开发条件会受到限制，服务器端渲染只支持beforeCreate和created两个钩子，
当我们需要一些外部扩展库时需要特殊处理，服务端渲染应用程序也需要处于Node.js的运行环境。
还有就是服务器的压力比较大。
```

## 你都做过哪些Vue的性能优化
```js
1、v-if和v-for不能连用
2、页面采用keep-alive缓存组件
3、合理使用v-if和v-show
4、key保证唯一
5、使用路由懒加载、异步组件、组件封装
6、防抖、节流
7、第三方模块按需导入
8、图片懒加载
9、精灵图的使用
10、代码压缩
```

## Vue-router 路由有哪些模式
```js
  hash 模式和history 模式
1、hash 模式：后面的 hash 值的变化，浏览器既不会向服务器发出请求，浏览器也不会刷新，
每次 hash 值的变化会触发 hashchange 事件。
2、history 模式：利用了 HTML5 中新增的 pushState() 和 replaceState() 方法。
这两个方法应用于浏览器的历史记录栈，在当前已有的 back、forward、go 的基础之上，
它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，
但浏览器不会立即向后端发送请求。
```

## Vuex 是什么？有哪几种属性？
```js
1、Vuex 是专为Vue设计的状态管理工具，采用集中式储存管理 Vue 中所有组件的状态。
2、属性
（1）state属性：基本数据
（2）getters属性：从 state 中派生出的数据
（3）mutation属性：更新 store 中数据的唯一途径，其接收一个以 state 为第一参数的回调函数
（4）action 属性：提交 mutation 以更改 state，其中可以包含异步操作，数据请求
（5）module 属性：用于将 store分割成不同的模块。
```

## axios封装请求拦截器和响应拦截器
```js
interceptors：【ɪntərˈsɛptərz】
1、项目中会在utils文件中，封装一个request.js文件
2、通过axios.create()配置baseURL，并得到一个request实例
3、通过request.interceptors.request.use来配置请求拦截
4、通过request.interceptors.response.use来配置响应拦截
```

## vue怎么实现强制刷新组件
```js
第一.使用this.$forceUpdate强制重新渲染    
<template>  
<button @click="reload()">刷新当前组件</button>    
</template>   
 <script>    
 export default {  name: 'comp',  methods: { reload() { this.$forceUpdate() }  }  }    
 </script>
 第二.使用v-if指令
 <template>   
  <comp v-if="update"></comp>    
  <button @click="reload()">刷新comp组件</button>
 </template>
 <script>
  import comp from '@/views/comp.vue'
  export default {  
    name: 'parentComp', 
    data() {
      return {  
        update: true  
      }},  
  methods: { 
    reload() {   
    // 移除组件  this.update = false            
    // 在组件移除后，重新渲染组件   // this.$nextTick可实现在DOM 状态更新后，执行传入的方法。           
    // this.$nextTick(() => {    this.update = true  })  }  }}
  </script>
```

## 在使用计算属性的时,函数名和data数据源中的数据可以同名吗?
```js
不可以	
在初始化vm的过程，因为不管是计算属性还是data还是props 都会被挂载在vm实例上，
会把data覆盖了,因此 这三个都不能同名
```

## vue中data的属性可以和methods中的方法同名吗?
```js
不可以
vue源码中的 initData() 方法会取出 methods 中的方法进行判断，如果有重复的就会报错
```

## 你知道style加scoped属性的用途和原理吗
```js
用途：防止全局同名CSS污染
原理：在标签加上v-data-something属性，再在选择器时加上对应[v-data-something]，
即CSS带属性选择器，以此完成类似作用域的选择方式.
scoped会在元素上添加唯一的属性（data-v-x形式），css编译后也会加上属性选择器，
从而达到限制作用域的目的。
```

## 如何在子组件中访问父组件的实例
```js
Vue中子组件调用父组件的方法，这里有三种方法提供参考：
  1：直接在子组件中通过this.$parent.event来调用父组件的方法
  2：在子组件里用$emit向父组件触发一个事件，父组件监听这个事件
  3：父组件把方法传入子组件中，在子组件里直接调用这个方法
```

## watch的属性用箭头函数定义结果会怎么样
```js
不应该使用箭头函数来定义 watch :
例如：
    watch: {
      a: () => {  //  这里不应该用箭头函数
        console.log(this);
        this.sum = this.a + this.b;
      }
    })。
理由是箭头函数绑定了父级作用域的上下文，所以 this 将不会按照期望指向 Vue 实例，
this.a 将是 undefined。
注意：methods里面定义的方法也不要用箭头函数
```

## 怎么解决vue打包后静态资源图片失效的问题
```js
在vue-cli 需要在根目录下建一个vue.config.js 在里面配置publicPath即可
默认值为/，更改为./就好了
```

## 怎么解决vue动态设置img的src不生效的问题
```js
因为动态添加src被当做静态资源处理了，没有进行编译，所以要加上require。
<img :src="require('@/assets/images/xxx.png')" />
```

## EventBus注册在全局上时，路由切换时会重复触发事件，如何解决呢
```js
原因：因为我们的事件是全局的，它并不会随着组件的销毁而自动注销，需要我们手动调用注销方法来注销。
解决：我们可以在组件的 beforeDestroy ,或 destroy 生命周期中执行注销方法，手动注销事件
```

## 你认为vue的核心是什么
```js
组件化
双向数据绑定
```

## 在.vue文件中style是必须的吗？那script是必须的吗
```js
在.vue 文件中，template是必须的，而script与style都不是必须的。
都没有的话那就是一个静态网页
```

## 说说vue的优缺点
```js
优点：
    1.数据驱动
    2.组件化
    3.轻量级
    4.SPA(单页面)
    5.版本3.0的界面化管理工具比较好使
    6.vue易入门
    7.中文社区强大，入门简单，提升也有很多的参考资料。
缺点：
    1.不支持IE8及以下浏览器
    2.吃内存（每个组件都会实例化一个Vue实例，实例的属性和方法很多）
    3.定义在data里面的对象，实例化时，都会递归的遍历转成响应式数据，
    然而有的响应式数据我们并不会用到，造成性能上的浪费
```

## 库和框架的区别
```js
库 本质上是一个函数的集合，每一次调用函数，实现一个特定的功能，使用库的时候，
   把库当成工具使用，需要自己控制代码的执行逻辑。
框架 是一套完整的解决方案，使用框架的时候，框架实现了大部分的功能，
     我们只需要按照框架的规则书写代码即可，使用框架开发比库开发效率更高，更容易维护。
```

## MVC 和 MVVM 的区别
```js
 MVVM
 M Model 模型 指的是数据层
 V View  视图 指的是用户页面
 VM ViewModel 视图模型
 视图模型是MVVM模式的核心，它是连接view和model的桥梁，MVVM实现了view和model的自动同步，
 当model的属性改变时，我们不用自手动操作DOM元素，来改变view的显示，称之为数据的双向绑定。

 MVC
 M Model 模型 指的是数据层
 V View  视图 指的是用户页面
 C controller 控制器 指的是页面业务逻辑
 view传送指令到controller，controller完成业务逻辑后，要求model改变状态，
 model将新的数据发送给view，用户得到反馈。所 信都是单向的。
```

## 自己实现一个 v-model 的效果
```js
答:
    <input type="text">
    <script>
    
     // vue2.0
    let data = {
      msg: 'hello vue'
    }
    let input = document.querySelector('input')
    input.value = data.msg
    input.addEventListener('input', function () {
      data.msg = this.value
    })
    let temp = data.msg
    Object.defineProperty(data, 'msg', {
      get() {
        return temp
      },
      set(value) {
        input.value = value
        return (temp = value)
      }
    })

    // vue3.0
    let data = {
      msg: 'hello vue'
    }
    let input = document.querySelector('input')
    input.value = data.msg
    input.addEventListener('input', function () {
      obj.msg = this.value
    })
    const obj = new Proxy(data, {
      get(target, key) {
        return target[key]
      },
      set(target, key, value) {
        target[key] = value
        input.value = value
      }
    })
   </script>
```

## Object.defineProperty和proxy的区别
```js
1、Object.defineProperty  用于监听对象的数据变化
缺点：
    1）无法监听数组变化
    2）只能劫持对象的属性,属性值也是对象那么需要深度遍历
2、proxy  可以理解为 在被劫持的对象之前 加了一层拦截
   proxy返回的是一个新对象， 可以通过操作返回的新的对象达到目的
总结：
当使用 defineProperty 时，我们修改原来的 obj 对象就可以触发拦截
而使用 proxy，就必须修改代理对象，即 Proxy 的实例才可以触发拦截
```

## vue 中怎么操作 dom
```js
答: 要在mounted中使用，在执行mounted的时候，vue已经渲染了dom节点，可以获取dom节点。
    方法：
      1）在标签中添加ref="name"
      2）在方法中用this.$refs.name拿到这个元素，
```

## 导航钩子有几种（导航守卫）具体怎么用的
```js
答: 分类：
    1、全局守卫： router.beforeEach
    2、全局解析守卫： router.beforeResolve
    3、全局后置钩子： router.afterEach
    4、路由独享的守卫： beforeEnter
    5、组件内的守卫： beforeRouteEnter、beforeRouteUpdate (2.2 新增)、beforeRouteLeave
    使用：
    1、全局守卫： router.beforeEach
       const router = new VueRouter({ ... })
          router.beforeEach((to, from, next) => {
          // ...
        })
    2、全局解析守卫： router.beforeResolve
       可以用 router.beforeResolve 注册一个全局守卫。这和 router.beforeEach 类似，区别是：在导航被确认之前，同时在所有组件内守卫和异步路由组件被解析之后，解析守卫就被调用。
    3、全局后置钩子： router.afterEach
       router.afterEach((to, from) => {
          // ...
        })
    4、路由独享的守卫： beforeEnter
       const router = new VueRouter({
          routes: [
            {
              path: '/foo',
              component: Foo,
              beforeEnter: (to, from, next) => {
                // ...
              }
            }
          ]
        })
    5、组件内的守卫： beforeRouteEnter、beforeRouteUpdate (2.2 新增)、beforeRouteLeave
       const Foo = {
          template: `...`,
          beforeRouteEnter (to, from, next) {
            // 在渲染该组件的对应路由被 confirm 前调用
            // 不能获取组件实例 `this`
            // 因为当守卫执行前，组件实例还没被创建
          },
          beforeRouteUpdate (to, from, next) {
            // 在当前路由改变，但是该组件被复用时调用
            // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
            // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
            // 可以访问组件实例 `this`
          },
          beforeRouteLeave (to, from, next) {
            // 导航离开该组件的对应路由时调用
            // 可以访问组件实例 `this`
          }
        }
```

## 什么是promise，特点是什么
```js
	首先，它是一个对象，也就是说与其他JavaScript对象的用法，没有什么两样；其次，它起到代理作用（proxy），充当异步操作与回调函数之间的中介。它使得异步操作具备同步操作的效果，使得程序具备正常的同步运行的流程，回调函数不必再一层层嵌套。
	简单说，它的思想是，每一个异步任务立刻返回一个Promise对象，由于是立刻返回，所以可以采用同步操作的流程。这个Promises对象有一个then方法，允许指定回调函数，在异步任务完成后调用。
 特点：
    1、Promise对象只有三种状态。
        异步操作“未完成”（pending）
        异步操作“已完成”（resolved，又称fulfilled）
        异步操作“失败”（rejected）
        异步操作成功，Promise对象传回一个值，状态变为resolved。
        异步操作失败，Promise对象抛出一个错误，状态变为rejected。
    2、promise的回调是同步的，then是异步的
    3、可以链式调用
```
## promise的方法有哪些，能说明其作用
```js
原型上的方法：
1、Promise.prototype.then()
	1）作用是为 Promise 实例添加状态改变时的回调函数。接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。其中，第二个函数是可选的，不一定要提供。
    2）返回的是另一个Promise对象，后面还可以接着调用then方法。
2、Promise.prototype.catch()
	1）用于指定发生错误时的回调函数。
    2）返回的也是一个 Promise 对象，因此还可以接着调用then方法
3、Promise.prototype.finally()
	1）finally方法用于指定不管 Promise 对象最后状态如何，都会执行的回调函数。
    2）finally方法的回调函数不接受任何参数，这意味着没有办法知道，前面的 Promise 状态到底是fulfilled还是rejected。

自身API:
1、Promise.resolve()
	1）不带参数传递 — 返回一个新的状态为resolve的promise对象
    2）参数是一个 Promise 实例— 返回 当前的promise实例
2、Promise.reject()
	1)返回的是一个值
    2）返回的值会传递到下一个then的resolve方法参数中
3、Promise.all() 
	1）并行执行异步操作的能力
    2）所有异步操作执行完后才执行回调
4、Promise.race()
	1）那个结果返回来的快就是，那个结果，不管结果是成功还是失败
```
## async和await是干什么的
```js
 async和await可以说是异步终极解决方案了。
1、async 用于申明一个 function 是异步的，而 await 用于等待一个异步方法执行完成。
2、await 只能出现在 async 函数中。
3、async 函数返回的是一个 Promise 对象，后面可以用then方法。

缺点：因为await将异步代码改造成了同步代码，如果多个异步代码都使用了await会导致性能上的降低。
```

## 什么是宏任务和微任务，执行顺序是什么
```js
1、宏任务一般是：包括整体代码script，setTimeout，setInterval。
2、微任务：Promise(then、catch、finally)，process.nextTick（node.js）。
3、先执行主代码块，然后执行微任务，最后在执行宏任务（异步）
```