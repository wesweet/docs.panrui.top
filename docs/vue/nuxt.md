<!--
 * @Description: nuxt文档
 * @Author: panrui
 * @Date: 2021-08-13 13:34:20
 * @LastEditTime: 2024-05-08 15:46:16
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 文档

- [nuxt](https://www.nuxtjs.cn/guide)
- [中文文档](https://www.nuxt.com.cn/)

```
npm i -g create-nuxt-app
```

## 基础知识

#### 入口

> 1. 默认情况下会将根路径的App.vue 作为入口点

#### 组件

> 1. 所有组件都创建在components 目录下，并且他们会自动导入整个应用，无需显式导入

##### 页面

> 1. 默认情况下，Nuxt.js 会自动将所有页面文件（.vue 文件）放在 pages 目录下，并且会自动生成路由。

#### 布局


#### 数据获取

- useFetch、useAsyncData 和 $fetch (内置函数和内置库)

```
1. useFetch  这个组合函数是 useAsyncData 组合函数和 $fetch 工具的封装。
事实上，useFetch(url) 几乎等同于 useAsyncData(url, () => $fetch(url)) - 它是为最常见的用例提供的开发者体验糖
```

```
2. $fetch 是ofetch工具库的全局别名
```

```
3. useAsyncData
```


## 使用

- 通过<nuxt-link></nuxt-link>切换路由

> 1. 在已有的 web 服务器中作为中间件使用 SPA
> 2. 服务端渲染 SSR
> 3. 静态站点生成 SSG

#### 做为服务端渲染使用

#### 作为站点生成使用

#### 做为中间件使用

> 1. 在已有的 web 服务器中使用，则可以作为中间件使用 SPA

<!-- ```js
// server.js
const { Nuxt, Builder } = require('nuxt')
const app = require('express')()

// 传入配置初始化 Nuxt.js 实例
const config = require('./nuxt.config.js')
const nuxt = new Nuxt(config)

// 生产模式不需要 build
if (config.dev) {
  const builder = new Builder(nuxt)
  builder.build()
}

app.use(nuxt.render)

app.listen(3000)
``` -->

## 使用 less css 预处理器

- Rule can only have one resource source (provided resource and test + include + exclude)

  > 1. 降低 webpack 版本 webpack@4.6.0

- Module build failed (from ./node_modules/less-loader/dist/cjs.js): TypeError: this.getOptions is not a function

> 1. 降低 less-loader 版本 less-loader@7.3.0

## 使用 axios

> 1. 安装 @nuxtjs/axios
> 2. 在 nuxt.config.js 中配置 axios
> 3. 在页面中使用 axios

```js
npm i @nuxtjs/axios

// nuxt.config.js
module.exports = {
  modules: ['@nuxtjs/axios'],
  axios: {
    proxy: true,
    prefix: '/api',
    credentials: true,
  },
  proxy: {
    '/api': {
      target: 'http://localhost:3000',
      pathRewrite: {
        '^/api': '/',
      },
    },
  },
}

// pages/index.vue
export default {
  asyncData({ $axios }) {
    return $axios.$get('/api/users')
  },
}
```

最后更新时间：2024-5-8 15:46:09
