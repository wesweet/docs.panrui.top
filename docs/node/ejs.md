<!--
 * @Description: ejs 在不同文件中输入方式
 * @Author: panrui
 * @Date: 2021-10-14 15:13:31
 * @LastEditTime: 2021-10-14 15:24:54
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 使用指南

#### 在 html 文件当中

```html
<body>
  <h1><%= projectName %></h1>
</body>
```

#### 在 json 文件当中

```js
{
  "author": "<%= author %>"
}
```

#### 在 js 文件中

```js
const a = "<%= author %>";
```

#### 在 Vue 文件中

```vue
<template>
  <div id="app">
    <Header />
    <div class="contain">
      <router-view></router-view>
      <h1><%= projectName %></h1>
    </div>
    <Footer />
  </div>
</template>
```


最后更新时间：2024-4-30 09:56:21