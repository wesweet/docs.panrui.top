<!--
 * @Description: nuxt文档
 * @Author: panrui
 * @Date: 2021-08-13 13:34:20
 * @LastEditTime: 2023-08-01 09:50:04
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 文档

- [nuxt](https://www.nuxtjs.cn/guide)

```
npm i -g create-nuxt-app
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




最后更新时间：2024-4-29 14:03:11