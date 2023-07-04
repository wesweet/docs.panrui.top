<!--
 * @Description: 状态管理器知识
 * @Author: panrui
 * @Date: 2021-12-17 10:22:29
 * @LastEditTime: 2021-12-17 11:20:35
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## State

```js
computed: {
    localComputed () { /* ... */ },
    ...mapState({
        // 箭头函数可使代码更简练
        count: (state) => state.count,

        // 传字符串参数 'count' 等同于 `state => state.count`
        countAlias: "count",

        // 为了能够使用 `this` 获取局部状态，必须使用常规函数
        countPlusLocalState(state) {
            return state.count + this.localCount;
        },

        // 使用了命名空间的数据
        // 基本方式 没有借助辅助函数 this.$store.state.moduleA.conutB
        count: (state) => state.moduleA.conutB
    })
};
```

## Getter

```js
computed: {
    ...mapGetters([
        'doneTodosCount',
        'anotherGetter',

        // 使用了命名空间
        // 基本方式 this.$store.getters['moduleA/moduleGetter']
        // 不带别名 ...mapGetters('moduleA', ['moduleGetter'])
        // 下面是带别名状态
        paramGetter: 'moduleA/moduleGetter'
    ])
}
```

## Mutation

## Action

## Module
