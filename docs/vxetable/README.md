<!--
 * @Description:
 * @Author: panrui
 * @Date: 2022-12-14 11:06:30
 * @LastEditTime: 2022-12-14 11:11:55
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

# VxeTable

## [文档](https://vxetable.cn/v3/#/table/start/install)

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
