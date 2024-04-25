<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-07-07 08:59:33
 * @LastEditTime: 2024-04-25 13:25:32
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2024-04-25)

## mixin 使用

!> 在 Vue 2 中，mixins 是创建可重用组件逻辑的主要方式。尽管在 Vue 3 中保留了 mixins 支持，但对于组件间的逻辑复用，使用组合式 API 的组合式函数是现在更推荐的方式。

#### 局部混入

1. 定义 mixin

```js
const mixin = {
  data() {
    return {
      name: "mixin",
    };
  },
  methods: {
    mixinMethod() {
      console.log("mixinMethod");
      this.mixinMethod2();
    },
    mixinMethod2() {},
  },
};
export default mixin;
```

2. 使用 mixin

```js
import mixin from "./mixin";
export default {
  mixins: [mixin],
  data() {
    return {
      name: "v2",
    };
  },
  methods: {
    v2Method() {
      console.log("v2Method");
      this.mixinMethod();
    },
  },
};
```

#### 全局混入

```js
import mixin from "./mixin";
Vue.mixin(mixin);
```

## ref 使用(获取原生 DOM 与组件实例)

!> 用于获取 DOM 元素或子组件实例的引用。
!> ref 引用在组件挂载后才能访问到。在 mounted 生命周期钩子中或其后的钩子（如 updated）中使用 ref 是安全的。在 created 钩子或更早阶段，$refs 中的引用可能还不可用

```html
<!-- 获取 DOM 元素引用 -->
<div ref="myDiv">Hello, World!</div>

<!-- 获取子组件引用 -->
<child-component ref="myChild"></child-component>

<script>
  export default {
    methods: {
      doSomething() {
        const myDiv = this.$refs.myDiv; // 获取 DOM 元素
        const myChild = this.$refs.myChild; // 获取子组件实例
      },
    },
  };
</script>
```

#### 数组形式的 ref

```html
<div v-for="(item, index) in items" :ref="`itemRef-${index}`"></div>
<script>
  this.$refs.itemRef.forEach((item, index) => {
    // ...
  });
</script>
```
