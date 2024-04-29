<!--
 * @Description: vue2技巧文档
 * @Author: prui
 * @Date: 2024-04-25 15:11:18
 * @LastEditTime: 2024-04-25 15:31:54
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 通过 this.$options.data()来还原默认值

```js
this.obj = this.$options.data().obj; // this.$options.data() 函数返回的是一个对象，包含组件创建时属性的默认值
```

## 通过设置 key 来阻止组件缓存

当一个页面不通区块使用同一个组件的时候，并且对组件进行传值 props 传值的时候，会存在组件缓存的原因，使用 key 来阻止组件缓存

## 深度监听组件接收的数据

```js
export default {
  // 接收数据
  props: {
    mtData: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      // 绑定自定义数据
      data: this.mtData,
    };
  },
  watch: {
    // 监听自定义数据
    data: {
      handler(val) {
        // 触发父组件更新数据，执行单项数据流
        this.$emit("update:mtData", val);
      },
      deep: true,
      immediate: false,
    },
  },
};
```

## 动态设置 class

```js
// 表示 active 这个 class 存在与否将取决于数据 property isActive
<div :class="{ active: isActive }"></div>
// 动态与静态 class 共存
<div :class="{ 'static-class': true, 'dynamic-class': isDynamic }"></div>
// 数组语法
<div :class="['static-class', dynamicClass]"></div>
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
    handInputDate() {
        console.log(123)
    },
    //触发
    getDate() {
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


最后更新时间：2024-4-29 14:09:30