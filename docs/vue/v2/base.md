<!--
 * @Description: vue2基础文档
 * @Author: prui
 * @Date: 2024-04-25 15:10:39
 * @LastEditTime: 2024-04-25 15:29:26
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-04-25)

## v-for 中的 Ref 数组

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
