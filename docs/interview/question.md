## 使用 element-ui upload 组件问题

自定义组件当中使用 upload 组件，组件的数据格式如下

```js
export default {
  props: {
    mtData: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      data: this.mtData,
    };
  },
  watch: {
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

在上述这种情况下，使用 upload 组件，并配置可以同时多选时，会触发只保存第一张图片的 bug

```js
handleThumbChange(file, fileList) {
    // 此处直接更新data
    this.data.thumb = fileList
}
```

> 1. 解决办法时： upload 组件的 show-file-list 属性设置为 false，同时手动展示文件列表(不使用 upload 组件中的展示)。
> 2. 深层次的原因：使用input file上传文件时，浏览器会将文件保存到一个临时内存，此时会设置一个状态。等到文件真正上传成功，在修改对应的状态。这也就是为什么我们在fileList中会拿到Blob对象这种数据的原因。
> 3. 之所以不使用upload组件展示图片的原因，也是因为我们数据进行了深度监听，当图片数据发生变化时，组件会进行重新渲染，从而影响后续的操作
