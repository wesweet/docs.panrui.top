<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-07-07 08:59:33
 * @LastEditTime: 2024-04-25 10:00:21
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
