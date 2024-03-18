<!--
 * @Description: 前端面试
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2024-03-15 09:04:10
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## JS

> 宏任务与微任务：宏任务（script，setTimeout，setInterval），微任务分为(Promise，process.nextTick，async)。先执行一个宏任务-在执行微任务

> typeof、instanceof（确定一个对象实例的原型链上是有原型）、[object].construcetor、object.property.toString.call

> 多线程（JavaScript 的主要用途是与用户互动，以及操作 dom，所以它只能是单线程，HTML5 允许脚本创建多个线程，但是子线程完全受主线程控制，且不得操作 dom）

> http 请求优化

> 事件冒泡与捕获。冒泡：事件源触发事件后，会将事件反馈到他的父元素，一直到 document；捕获：与冒泡相反。一般我们使用事件委托（就是利用事件冒泡）

> 事件循环：任务队列，同步任务，异步任务（宏任务-微任务）

> 原型链和作用域链 函数都存在 property；每个对象都有一个属性**proto**，指向自己构造函数的原型;可以通过设置原型给对象添加自定义的方法。

> JavaScript 执行上下文（对代码的变量和函数表达式进行声明，对代码中 this 进行赋值，对函数声明进行赋值，对自由变量进行赋值，并确定作用域。函数在定义的时候就已经确定了自由变量的作用域）

> 闭包（在函数 A 中返回 B 函数给一个外部变量，同时在函数 B 中访问函数 A 的变量，这就是闭包）优点：防止变量污染，局部作用域；缺点：内存泄露

> 浅拷贝-对值的拷贝、对对象地址的复制

> 深拷贝-开辟一个新的栈，返回一个新的对象

> promise 三种状态 pending fulfilled rejected（进行、成功、失败），resolve 方法的参数除了正常值，还有一个可能是 promise 对象的实例，then 方法接受两个回调函数作为参数，第一个为状态改变为成功时候调用，第二个为状态变为失败时候调用

> 权限校验 分别接口权限和页面权限。接口使用 token，页面分为 1：只加载当前用户拥有的路由、2：初始化挂在全部路由，每次路由跳转前做校验

## nuxt 的优点

- 1：自动代码分层
- 2：服务端渲染
- 3：强大的路由功能，支持异步数据
- 4：静态文件服务
- 5：ES6/ES7 语法支持
- 6：打包和压缩 JS 和 CSS
- 7：HTML 头部标签管理
- 8：本地开发支持热加载
- 9：集成 ESLint
- 10：支持各种样式预处理器： SASS、LESS、 Stylus 等等
- 11：支持 HTTP/2 推送

## nuxt

## React

## next

- next 能够同时部署静态站点文件和服务器端渲染文件，这样就可以在不同的场景下使用不同的渲染方式，比如在 CDN 上部署静态站点文件，而在服务器上部署服务器端渲染文件，这样就可以兼顾到静态站点的性能和服务器端渲染的 SEO 优化。比 nuxt 更加灵活



## CSS

> 重绘：当操作的节点不导致元素位置发生变化（颜色，背景颜色）；回流：当节点发生改变时，浏览器重新渲染部分节点或者整个文档。回流一定重绘

> 居中的方式 text-align:center;margin:0 auto;positon:relative,left:50%;tansform:translate(-50%);flex 布局

> 元素命名空间 我采用的 BEM 的方式 B 代表区块 E 代表元素 M 代表修饰符

> rgba() 和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有内容的透明度；而 rgba() 只作用于元素的颜色或其背景色，设置 rgba() 透明的元素的子元素不会继承透明效果。

#### 移动端适配方案

> media queries、flex 布局、rem+vieport、vh-vw、

> IE 盒模型 width = border+padding+content 标准和模型 width=content

## ES6

> let const 不存在变量提升、不允许重复定义、存在块级作用域。const 实际上保证的，并不是变量的值不能改动，而是变量指向的那个内存地址所保存的值不得改动、不属于全局变量



## 前端性能

> 减少首屏的请求加载，减少加载文件的大小，利用文件的缓存

> 骨架屏的使用，对于一些组件使用缓存和预加载

> 图片转为 base64 ,对于一些第三库使用 cdn，然后结合 nginx 做优化

> 对一些输入的数据进行编码，尽量避免使用拼接的 html

#### 缓存

> 接口请求缓存分为强制缓存和协商缓存，cache-control 是一个相对时间，命中则使缓存，否则把请求参数放到 request header 中，如果返回 304 击中协商缓存，否则重新请求

## Node

## 网络

> cookie 存放在浏览器中数据，限制大小，并且会随着 http 请求一起被发生。sessionstorage 有效期为一次会话中，localstorage 存在本地永久

> localStorage 和 sessionStorage 存储大、拥有同源策略。不同点在于生命周期吧

> http

> url 的流程 判断是否命中缓存把、dns 解析、tcp 三次握手、获取服务器资源(有没有命中协商缓存)、浏览器获取数据(dom 树构建 css 规则树 tree render 布局 回执)

## 安全性能方面

## 小程序

## 前端性能优化

1：使用缓存、压缩响应、使用多个域名、避免图片 src 为空

2：将 css 放入到 header、降低 css 的复杂度、不适用 css 表达式

3：使用外联的 css 和 js

4：使用字体图标 iconfont 代替图片

5：使用骨架图还有按需加载

6：使用事件委托、防抖、节流、

7：使用渐进式 jpeg 图片、使用 css3 代替图片

## 微信小程序

#### 渲染流程

小程序的渲染层和逻辑层分别由两个线程管理：渲染层的界面使用 WebView 进行渲染；逻辑层采用 JSCore 运行 JavaScript 代码。一个小程序存在多个界面，所以渲染层存在多个 WebView。这两个线程间的通信经由小程序 Native 侧中转，逻辑层发送网络请求也经由 Native 侧转发

## http

#### 请求头包含的内容

host、content-type、origin、User-Agent、Accept

#### 返回头

1.  Access-Control-Allow-Credentials:

    True 允许携带 cookie

1.  Access-Control-Allow-Headers:

    Content-Type,AccessToken,X-CSRF-Token,Authorization,Token  允许携带的请求

1.  Access-Control-Allow-Methods:

    POST,GET,OPTIONS  允许方式

1.  Access-Control-Allow-Origin:

    - 跨域

1.  Access-Control-Expose-Headers:

    Content-Length,Access-Control-Allow-Origin,Access-Control-Allow-Headers,Content-Type

1.  Connection:

    keep-alive

1.  Content-Type:

    application/json; charset=utf-8

1.  Date:

    Tue, 07 Mar 2023 09:11:03 GMT

## webpack

#### loader

- `image-loader`：加载并且压缩图片文件
- `babel-loader`：把 ES6 转换成 ES5
- `css-loader`：加载 CSS，支持模块化、压缩、文件导入等特性
- `vue-loader`：加载 Vue.js 单文件组件
- `style-loader`：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS

#### plugin

- `html-webpack-plugin`：简化 HTML 文件创建 (依赖于 html-loader)
- `clean-webpack-plugin`: 目录清理

#### 差别

`Loader`  本质就是一个函数，在该函数中对接收到的内容进行转换，返回转换后的结果。

`Plugin`  就是插件，基于事件流框架  `Tapable`，插件可以扩展 Webpack 的功能，在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。

`Loader`  在 module.rules 中配置，作为模块的解析规则，类型为数组。每一项都是一个 Object，内部包含了 test(类型文件)、loader、options (参数)等属性。

`Plugin`  在 plugins 中单独配置，类型为数组，每一项是一个 Plugin 的实例，参数都通过构造函数传入。

初始化参数、开始编译、`确定入口、编译模块`

<!-- ## Vue

### vue $on 与$emit的

$on 监听自定义事件，$emit 触发指定事件，也可以当作组件传递的一种方式

### vue的优点

1：双向绑定

2：组件化

3：视图、数据、结构分离

4：虚拟dom

5：轻量级

### watch与computer的差距与使用场景

1：异步与同步

2：无缓存与有缓存

3：一个数据影响多个数据、一个数据被多个数据影响

### vue3的新特性

1：监测机制的改变

2：多个根节点

3：使用组合式的API

4：穿梭组件

### Vue路由传递参数的区别

**params 传参类似于网络请求中的 post 请求，params 传过去的参数不会显示在地址栏中（但是不能刷新）只能使用name**

**query 传参类似于网络请求中的 get 请求，query 传过去的参数会拼接在地址栏中（?name=xx 可以使用name 也可以使用path****  
**

**  
**

## HTML

### BFC

是一个独立的渲染区域，规定了内部 box 如何布局，且这个区域内的子元素不会影响到外面的元素  


### 浏览器渲染机制

生成DOM树 --> 生成CSS规则树 --> 构建渲染树 --> 布局 --> 绘制

<!-- ### 回流与重绘

`回流`：当 DOM 的变化影响了元素的几何信息


当一个元素的外观发生改变，重新把元素外观绘制出来的过程，叫做重绘


### rgba与opacity

rgba() 和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有内容的透明度；而 rgba() 只作用于元素的颜色或其背景色，设置 rgba() 透明的元素的子元素不会继承透明效果。


### script

async script 解析完就执行


defer 解析完不执行

### 作用域与作用域链

`作用域`，即变量（变量作用域又称上下文）和函数生效（能被访问）的区域或集合


`作用域链`：当在 JS 中使用一个变量时，JS 引擎会尝试在当前作用域下寻找该变量，如果没找到，再到它的上层作用域寻找，以此类推


**js 采用的是静态作用域，所以函数的作用域在函数定义时就确定了**


### 闭包

闭包就是能够读取其他函数内部变量的函数   -->

