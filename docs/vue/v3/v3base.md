<!--
 * @Description: v3使用指南
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2024-04-25 10:58:42
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-04-25)

## 组合式函数(mixin)

!> 利用 Vue 的组合式 API 来封装和复用有状态逻辑的函数

> 1. 替代 v2 中的 mixin 功能
> 2. vue-composable 或 @vueuse/core (专门支持 Composition API 的第三方库)

1. 封装无状态逻辑的函数

```js
// 按照惯例，组合式函数名以“use”开头
import { ref } from "vue";

export default function useUser(initialName = "", initialAge = 0) {
  const userName = ref(initialName);
  const userAge = ref(initialAge);

  const greetUser = (name) => `Hello, ${name}!`;

  return { userName, userAge, greetUser };
}
```

2. 使用组合式函数

```vue
<template>
  <div>
    <h1>{{ greetUser }}</h1>
    <!-- ... -->
  </div>
</template>

<script setup>
import { defineComponent } from "vue";
import useUser from "@/composables/useUser";
const { userName, userAge, greetUser } = useUser("John", 25);
</script>
```

## defineComponent(待修改)

> 1. 定义组件的函数，接收一个配置对象，返回一个组件对象，可以通过 app.component 方法注册到应用中

```js
export default defineComponent({
  name: "UserBasicPage",
});
```

## setup

> 1. 组件配置的一个选项，是一个函数。接受两个参数：props 和 context。setup 函数必须返回一个对象，这个对象中包含组件的模板中需要使用的数据、方法以及生命周期钩子函数。

```js
setup(props, context){
  return {}
}
```

## ref

> 1. 接收一个参数并返回一个响应式对象，这个对象有一个.value 属性，他是一个可变的值

```js
const emailType = ref < string > "@qq.com";
console.log(emailType.value);
```

## reactive

> 1. 将一个普通对象转换成响应式对象，reactive 函数返回的是一个 Proxy 对象

```js
interface FormState {
  username: string;
  password: string;
  remember: boolean;
}
const formState =
  reactive <
  FormState >
  {
    username: "",
    password: "",
    remember: true,
  };
```

## onMounted

> 1. 钩子函数，它在组件挂载后执行，只能在 setup 函数中使用，而不能在模板中使用。接收一个回调函数作为参数

```js
setup() {
    onMounted(() => {
      console.log('Component mounted')
      // 执行一些操作，比如请求数据、初始化变量等
    })
  }
```
