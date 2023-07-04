<!--
 * @Description: 
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-18 10:01:11
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-05-18 10-01-11

## 设置 class

```js
// 表示 active 这个 class 存在与否将取决于数据 property isActive
<div v-bind:class="{ active: isActive }"></div>
```

## 通过 style 动态设置图片

```js
<div :style="{'background-image': 'url('+data.image_url+')'}"></div>
```

## v-for 指令遍历添加 class

```js
<p :class="`userleve${index}`"></p>

<p :class="['strign' + index, {}]"></p>

// 通过设置函数 在函数中返回class
<span class="icon" :class="fnSetClass(item)"></span>
```

## 通过 ref 的形式触发元素的原生事件

```html
<input ref="inputResult" @click="handInputDate" />
```

```js
methods {
    //定义
    handInputDate: function () {
        console.log(123)
    },
    //触发
    getDate: function () {
        this.$refs.inputResult.click() //重点看这里
    },
}
```

## 使用引号来监听嵌套属性

```js
watch {
    '$route.query.id'() {
        // TODO
    }
}
```

## Vue filters 过滤器 访问 this 解决方案

```html
<template>
  <div>{{value|xxx(currentvm)}}</div>
</template>
```

```js
data() {
    return {
        currentvm:this
    }
},
filters: {
    xxx(v,vm) {
        console.log(vm)
    }
}
```

## 传入一个对象的所有属性作为 props

```js
// 使用不带参数的v-bind
post: {
  id: 1,
  title: 'My Journey with Vue'
}
<blog-post v-bind="post"></blog-post>
```

## input 标签 input 与 change 事件区别

```markup
input 事件在输入的过程中不断被触发
change 在输入之后,input标签blur才会触发
```
