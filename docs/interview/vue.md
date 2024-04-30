<!--
 * @Description: Vue面试题
 * @Author: prui
 * @Date: 2023-11-24 10:55:23
 * @LastEditTime: 2024-03-14 09:56:55
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 双向绑定原理

> 通过 Object.defineProperty 的 get、set 方法对对象的属性进行劫持，每一个属性拥有自己的消息订阅器 dep，用于存放所有订阅了该属性的观察者对象，watcher 观察者对象再监听到结果后，主动触发回调进行响应

> V2 所有 property 必须在 data 对象上存在才能让他将它转化内响应式， V3 采用 proxy

```
vue2：`Object.defineProperty(obj,key,descriptor)`拦截对象属性访问，当数据被访问或改变时，感知并作出反应。结合发布订阅者模式。

第一步：需要observe对数据对象进行递归遍历，都加上setter和getter这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化

第二步：在数据发生改变时告诉订阅者、

第三步：解析器解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

vue3：中利用`ES6`的`Proxy`机制代理需要响应化的数据。可以同时支持对象和数组，动态属性增、删都可以拦截
```

## vue 添加 key 的作用

```
`key`的作用主要是`为了更加高效的更新虚拟 DOM`。

Vue 判断两个节点是否相同时，主要是判断两者的`key`和`元素类型tag`。因此，如果不设置`key` ，它的值就是 undefined，则可能永远认为这是两个相同的节点，只能去做更新操作，将造成大量的 DOM 更新操作。
```

## 路由钩子

> 全局路由钩子 router.beforeEach、beforeResolve、afterEach

> 页面路由钩子 beforeEnter（to、form、next）、

## 什么是虚拟 DOM

> 通过以对象的方式来表示 DOM 结构，将页面的状态抽象成 JS 对象，配合不同的工具，使跨平台渲染成为可能。

## DIFF 算法

> 是一种对同层的树节点进行比较的高级算法 只会同级比较，不跨层级；diff 比较循环往两边中间靠拢 （旧头-新头、旧尾-新尾、旧头-新尾、旧尾-新头）

## V3 与 V2 的差别

> 通过 ref 调用子组件方法和属性的区别

```
vue2 默认子组件实例的所有公共方法和属性都是暴露，可以只用通过ref进行调用
vue3 子组件需要使用defineExpose 暴露公共方法和属性，从而达到父组件进行调用
```

> API 形式的差别

```js
// vue2采用选项是api形式
export default {
  // data() 返回的属性将会成为响应式的状态
  // 并且暴露在 `this` 上
  data() {
    return {
      count: 0,
    };
  },

  // methods 是一些用来更改状态与触发更新的函数
  // 它们可以在模板中作为事件处理器绑定
  methods: {
    increment() {
      this.count++;
    },
  },

  // 生命周期钩子会在组件生命周期的各个不同阶段被调用
  // 例如这个函数就会在组件挂载完成后被调用
  mounted() {
    console.log(`The initial count is ${this.count}.`);
  },
};

// vue3 采用组合式api形式
import { ref, onMounted } from "vue";

// 响应式状态
const count = ref(0);

// 用来修改状态、触发更新的函数
function increment() {
  count.value++;
}

// 生命周期钩子
onMounted(() => {
  console.log(`The initial count is ${count.value}.`);
});
```

> computed 本质是一个惰性求值的观察者，具有缓存性，只有当依赖变化后，第一次访问 computed 属性才会重新计算值。computed 适用于一个数据被多个数据影响 watch 相反

> Vue 重写了数组的 push、pop、shirf、等几个方法。所以数组更新页面会改变

> 通过 Vue.$set 新增动态属性

> Vuex action 和 Mutation。通过 store.dispatch 来触发 action 或者通过 mapAction 辅助函数；通过 store.commit 调用 mutation

> vuex 存储在内存中、localstorage 以文件的方式存储在本地

> 为什么 data 返回的是一个函数而不是一个对象 组件复用的时候，如果是一个对象，那么就会互相影响，复用也只是 copy 了对象的内存地址。函数返回的对象内存地址并不同

## 全局变量

> 通过在 Vue 的原型链上面添加全局方法、通过 mixin 混入的形式添加全局方法、this.$root.$on 添加全局函数

## SEO 优化

> 使用 SSR 服务器渲染、使用 nuxt 静态化、使用预渲染插件对部门页面生成静态 html 文件

## 组件通信

[组件通信](https://wesweet_admin.gitee.io/docs.panrui.top/#/vue/base?id=%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)

## vue.use 与 vue 原型链区别

> use 适用于生态内、原型链适用于生态外。use 主要是执行 install 方法，而原型链不需要实现该方法、use 在功能方面更加灵活，原型链使用更方便

## Vue 路由传递参数的区别

> params 传参类似于网络请求中的 post 请求，params 传过去的参数不会显示在地址栏中（但是不能刷新）只能使用 name

> query 传参类似于网络请求中的 get 请求，query 传过去的参数会拼接在地址栏中（?name=xx 可以使用 name 也可以使用 path

## keep-alive 的实现原理

> 新提供两个钩子函数、缓存在内容当中，不会再次调用 create 等钩子函数


最后更新时间：2024-4-30 13:44:48