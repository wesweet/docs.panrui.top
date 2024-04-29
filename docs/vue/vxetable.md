<!--
 * @Description:
 * @Author: prui
 * @Date: 2024-04-29 15:09:19
 * @LastEditTime: 2024-04-29 15:09:38
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

- [文档](https://vxetable.cn/v3/#/table/start/install)

## 设置某列不展示

```js
this.tableColumn.push({
  field: e,
  title: this.$t("tabletitle.product." + e),
  sortable,
  minWidth,
  fixed,
  slots,
  visible: e !== "thumb", // 设置某列是否显示
});
```


最后更新时间：2024-4-29 15:10:11