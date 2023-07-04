<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-06-06 08:37:32
 * @LastEditTime: 2023-06-06 08:38:37
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-06-06 08-38-37

## Form 表单

#### 表单多层次嵌套校验

```html
<a-form-item
  label="学校名称"
  :name="['educationInfo', 'school_name']"
  :rules="[{ required: true, message: '请输入学校名称' }]"
>
  <a-input v-model:value="formResume.educationInfo.school_name" />
</a-form-item>
```

#### 表单循环渲染校验

```html
<template
  v-for="(workInfoList, index) in formResume.workInfoList"
  :key="workInfoList.id"
>
  <a-form-item
    label="公司名称"
    :name="['workInfoList', index, 'company_name']"
    :rules="[{ required: true, message: '请输入公司名称' }]"
  >
    <a-input v-model:value="workInfoList.company_name" />
  </a-form-item>
</template>
```
