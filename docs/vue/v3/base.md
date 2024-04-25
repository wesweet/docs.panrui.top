<!--
 * @Description: vue3基础文档
 * @Author: prui
 * @Date: 2024-04-25 15:14:04
 * @LastEditTime: 2024-04-25 16:03:24
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->


## 最后更新时间(2024-04-25)

- v3 使用指南

## setup 钩子函数使用情况

> 1.  需要在非单文件组件中使用组合式 API 时
> 2.  需要在基于选项式 API 的组件中集成基于组合式 API 的代码时

## 组合式 API (待修改)

!> 将以前的许多选项式 API 通过 setup 这个选项 组合在一起 称之为组合式 API

#### setup 组件选项

新的 setup 组件选项在创建组件之前执行，一旦 props 被解析，就作为组合式 API 的入口点

!> 由于在执行 setup 时，组件实例尚未被创建，因此在 setup 选项中没有 this。这意味着，除了 props, context 之外，你将无法访问组件中声明的任何属性——本地状态(data)、计算属性(computed)或方法(methods)。

```js
export default {
  props: {
    user: {
      type: String,
      required: true,
    },
  },
  // 接受 props 和 context 的函数
  setup(props, context) {
    console.log(props); // { user: '' }
    console.log(context);

    return {}; // 这里返回的任何内容都可以用于组件的其余部分
  },
  // 组件的“其余部分”
};
```

```
export default {
  setup(props, context) {
    // Attribute (非响应式对象)
    console.log(context.attrs)

    // 插槽 (非响应式对象)
    console.log(context.slots)

    // 触发事件 (方法)
    console.log(context.emit)
  }
}
```

##### 声明响应式状态 reactive

```
// 返回响应式副本 转换是“深层”——影响所有嵌套property
const obj = reactive({ count: 0 })
```

##### 带 ref 的响应式变量

```js
// ref 接受参数，并将其包裹在一个带有 value property 的对象中返回，然后可以使用该 property 访问或更改响应式变量的值
import { ref } from "vue";

const counter = ref(0);

console.log(counter); // { value: 0 }
console.log(counter.value); // 0

counter.value++;
console.log(counter.value); // 1
```

!> reactive 相当于创建了一个响应式对象给指定的变量 ref 相当于给创建一个响应式变量并初始化

##### toRefs

```
1. setup 中的变量除了 props 是响应式之外 都不是响应式的，所以为了创建响应式对象，提供了 ref 方法
2. 如果 title 是可选的 prop，则传入的 props 中可能没有 title 。在这种情况下，toRefs 将不会为 title 创建一个 ref 。你需要使用 toRef 替代它
```

!> 因为 props 是响应式的，所以不能使用 ES6 结构，因为会消除 prop 的响应式，如果需要解构 prop ,可以使用 toRefs 来完成此操作。后面会有 toRefs 的使用

##### 生命周期钩子注册内部 setup

```js
// 组合式 API 上的生命周期钩子与选项式 API 的名称相同，但前缀为 on：即 mounted 会看起来像 onMounted

// 这些函数接受一个回调，当钩子被组件调用时，该回调将被执行

// src/components/UserRepositories.vue `setup` function
import { fetchUserRepositories } from '@/api/repositories'
import { ref, onMounted } from 'vue'

// 在我们的组件中
setup (props) {
  const repositories = ref([])
  const getUserRepositories = async () => {
    repositories.value = await fetchUserRepositories(props.user)
  }

  onMounted(getUserRepositories) // 在 `mounted` 时调用 `getUserRepositories`

  return {
    repositories,
    getUserRepositories
  }
}
```

| 选项式 API      | Hook inside setup |
| --------------- | ----------------- |
| beforeCreate    | Not needed        |
| created         | Not needed        |
| beforeMount     | onBeforeMount     |
| mounted         | onMounted         |
| beforeUpdate    | onBeforeUpdate    |
| updated         | onUpdated         |
| beforeUnmount   | onBeforeUnmount   |
| unmounted       | onUnmounted       |
| errorCaptured   | onErrorCaptured   |
| renderTracked   | onRenderTracked   |
| renderTriggered | onRenderTriggered |

!> 因为 setup 是围绕 beforeCreate 和 created 生命周期钩子运行的，所以不需要显式地定义它们。换句话说，在这些钩子中编写的任何代码都应该直接在 setup 函数中编写。

##### watch 响应式更改

```js
import { ref, watch } from "vue";

const counter = ref(0);
watch(counter, (newValue, oldValue) => {
  console.log("The new counter value is: " + counter.value);
});
```

##### 独立的 computed 属性

```js
import { ref, computed } from "vue";

const counter = ref(0);
const twiceTheCounter = computed(() => counter.value * 2);

counter.value++;
console.log(counter.value); // 1
console.log(twiceTheCounter.value); // 2
```

## Teleport

## 片段

## 触发组件选项

## 来自 @vue/runtime-core 的 createRenderer API 创建自定义渲染器

## 单文件组件组合式 API 语法糖 (script setup)

## 单文件组件状态驱动的 CSS 变量 (script vars)

## 单文件组件 (script scoped)

## 父组件通过 ref 调用子组件方法

```js
// 父组件设置 ref
<Header ref="header"></Header>;

const header = ref(); // 创建实例

header.value.handLogin(); // 调用子组件方法

// 子组件
const handLogin = () => {};

// 暴露自身方法给父组件
defineExpose({
  handLogin,
});
```

## 通过 ref 获取组件高度

```js
<template>
  <Header ref="header"></Header>
</template>
const header = ref(null) as any
header.value.$el.clientHeight
// 但是组件如果是使用固定定位可能会有问题，导致获取不到
```

## slot 插槽使用

```html
<dialog>
  <template #[name]>
     
    <div>     123    </div>
  </template>
</dialog>
const name = ref('header')
```

#### 匿名插槽

```js
// 子组件
<template>
  <div>
    <!--插槽-->
    <slot></slot>    
  </div>
</template>

// 父组件
       
<dialog>
  <template v-slot>
    <div>Yang</div>
  </template>
</dialog>
```

#### 具名插槽

```js
// 子组件
<div>
  <!--名字叫header的插槽-->
  <slot name="header"></slot>
  <slot></slot>
  <slot name="footer"></slot>
</div>
// 父组件
<Dialog>
  <template #header>
     <div>1</div>
  </template>
  <template #default>
     <div>2</div>
  </template>
  <template #footer>
     <div>3</div>
  </template>
</Dialog>
```

#### 作用域插槽

```js
// 子组件

<div>
   <slot name="header"></slot>
   <div>
      <div v-for="item in 100">
         <slot :data="item"></slot>
      </div>
   </div>
   <slot name="footer"></slot>
</div>
// 父组件
<Dialog>
  <template #header>
    <div>1</div>
  </template>
  <template #default="{ data }">
    <div>{{ data }}</div>
  </template>
  <template #footer>
    <div>3</div>
  </template>
</Dialog>
```

#### 动态插槽

## setup

> 组合式 api 的入口，组件创建之前执行，一旦 props 被解析就会执行 setup。在 setup 中避免使用 this,(context 中提供了 this 最常用的三个属性,attrs,slot,emit)setup 函数 return 的内容，在模板中可以直接使用，包括变量和方法。

> setup 中接收的 props 是响应式的,所以不可以使用 ES6 解构，解构会消除它的响应式

## ref 与 reactive 的区别

>

## unref 的使用

```
在 Vue 3 中，unref 是一个全局方法，用于对响应式对象进行解包。它会返回原始值或非响应式对象，而不是一个响应式代理对象
```

## 路由传递参数与获取

```js
import router from "@/router"; // 路由实例 可以进行页面跳转及传参 这个路由是我们通过createRouter 创建的
router.push({
  path: "/product/detail", // 路径
  query: {
    id: value, // 参数
  },
});

import { useRouter } from "vue-router";
const router = useRouter();
console.log(router.currentRoute); // 这里面获取当前路由传递的参数
```
