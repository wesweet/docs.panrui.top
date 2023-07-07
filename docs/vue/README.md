<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-07-07 08:54:33
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# Vue 最后更新时间：2023-05-18 09-58-17

> 1. [Vue Cli3](https://cli.vuejs.org/zh/guide/mode-and-env.html#%E6%A8%A1%E5%BC%8F)

> 2. [vue-awesome-swiper](https://www.npmjs.com/package/vue-awesome-swiper)

> 3. [前端持久化插件](https://github.com/robinvdvleuten/vuex-persistedstate)

> 4. [vxe-table](https://xuliangzhan_admin.gitee.io/vxe-table/#/table/start/use)


#### 待删除

<!-- ## v-for 中的 Ref 数组

```
// 在 Vue 2 中，在 v-for 里使用的 ref attribute 会用 ref 数组填充相应的 $refs property
// 在 Vue 3 中，这样的用法将不再在 $ref 中自动创建数组 要从单个绑定获取多个 ref，请将 ref 绑定到一个更灵活的函数上 (这是一个新特性)
<div v-for="item in list" :ref="setItemRef"></div>
```

## 异步组件

1. 新的 defineAsyncComponent 助手方法，用于显式地定义异步组件
2. component 选项被重命名为 loader
3. Loader 函数本身不再接收 resolve 和 reject 参数，且必须返回一个 Promise

```
// 以前，异步组件是通过将组件定义为返回 Promise 的函数来创建
const asyncModal = () => import('./Modal.vue')

//3.x语法
// 不带选项的异步组件
const asyncModal = defineAsyncComponent(() => import('./Modal.vue'))
/ 带选项的异步组件
const asyncModalWithOptions = defineAsyncComponent({
  loader: () => import('./Modal.vue'),
  delay: 200,
  timeout: 3000,
  errorComponent: ErrorComponent,
  loadingComponent: LoadingComponent
})
```

## $attrs 包含 class & style

```
// 这个语法感觉我用的很少
// 3.x $attrs 现在包含了所有传递给组件的 attribute，包括 class 和 style
```

## $children 移除不在提供

```
// 2.x 可以使用 this.$children 访问当前直接子组件
// 3.x 访问子组件实例 需要使用 this.$refs
```

## 自定义指令

## 与自定义元素的互操作性

## Data 选项

1. data 不再接受纯 JavaScript object ，而是接受一个 function
2. 合并来自 mixin 或 extendd 的多个 data 返回值时，合并操作现在是浅层次的而非深层次(只合并根级属性)

## emits 选项

1. 强烈建议使用 emits 记录每个组件所触发的所有事件
2. 移除了.native 修饰符

```
// 2.x
默认情况下，传递给带有 v-on 的组件的事件监听器只能通过 this.$emit 触发
要将原生 DOM 监听器添加到子组件的根元素中，可以使用 .native 修饰符

// 3.x
移除了.native
```

## 事件 API

1. $on，$off 和 $once 实例方法已被移除

## 过滤器

1. 过滤器已经被移除
2. 3.x 使用方法或者计算属性来替换他们

## 片段

1. 3.x 组件可以包含多个根节点，但是需要显式定义 attribute 应该分布在哪里

## 函数式组件

1. 通过函数创建组件，接收 props 和 context。context 参数是一个对象，包含组件的 attrs、slots 和 emit property

## 全局 API

1. 使用 createApp 创建应用实例

```js
import { createApp } from "vue";

const app = createApp({});
```

2. Vue.prototype 替换为 config.globalProperties

3. 移除 Vue.extend(2.x 用于创建一个基于 Vue 构造函数的子类 3.x 中已经不存在组件构造器的概念)

4. 使用组合式 API 来替代继承与 mixin

5. Vue.use 安装插件将不再支持，必须在应用实例上面显示指定使用此插件

```
const app = createApp(MyApp)
app.use(VueRouter)
```

## 全局 API Treeshaking

## 内联模板 attribute

## key attribute

1. template v-for 的 key 应该设置在 template 标签上 (而不是设置在它的子节点上)
2. 2.x 中 template 不允许设置 key

## 按键修饰符

## 移除$listeners

## 挂在 API 变化

1. 在 Vue 2.x 中，当挂载一个具有 template 的应用时，被渲染的内容会替换我们要挂载的目标元素。在 Vue 3.x 中，被渲染的应用会作为子元素插入，从而替换目标元素的 innerHTML

## propsData

## 在 prop 的默认函数中访问 this

## 渲染函数 API

## 插槽统一

1. 统一了普通插槽和作用域插槽

## 过渡的 class 名更改

1. 过渡类名 v-enter 修改为 v-enter-from、过渡类名 v-leave 修改为 v-leave-from

## v-model

## v-if 与 v-for 的优先级对比

1. 2.x 版本中在一个元素上同时使用 v-if 和 v-for 时，v-for 会优先作用
2. 3.x v-if 会拥有比 v-for 更高的优先级

## v-bind 合并行为

## VNode 生命周期事件

## 侦听数组

1. 当侦听一个数组时，只有当数组被替换时才会触发回调。如果你需要在数组被改变时触发回调，必须指定 deep 选项 -->

## 组合式 API

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

## provide && inject

```js
// 父组件提供方法
provide('fnLogin', () => { console.log('fnLogin') })

//子组件接收方法并使用
const fnLogin = inject('fnLogin') as any
```

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

## unref的使用
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