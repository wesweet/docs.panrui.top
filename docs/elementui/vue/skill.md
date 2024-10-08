<!--
 * @Description: elementui组件使用技巧
 * @Author: panrui
 * @Date: 2023-05-22 15:40:54
 * @LastEditTime: 2024-09-10 13:30:59
 * @LastEditors: panr99 1547177202@qq.com
 * 不忘初心,不负梦想
-->

## 修改 element-ui 组件默认样式(通过::v-deep)

```css
::v-deep .el-dialog {
  height: 70%;
  overflow: auto;
}
```

## Loading 组件 (实用*****)

- Element 提供了两种调用 Loading 的方法：指令和服务。对于自定义指令v-loading，只需要绑定Boolean即可。默认状况下，Loading 遮罩会插入到绑定元素的子节点，通过添加body修饰符，可以使遮罩插入至 DOM 中的 body 上。

- 通过指令的方法是
```html
<el-table
    v-loading="loading"
    :data="tableData"
    style="width: 100%">
  </el-table>
```

- 通过服务的方法
```js
import { Loading } from 'element-ui';
Loading.service(options);
```

## MessageBox 组件

- 从场景上说，MessageBox 的作用是美化系统自带的 alert、confirm 和 prompt，因此适合展示较为简单的内容。如果需要弹出较为复杂的内容，请使用 Dialog。

```js
this.$alert("这是一段内容", "标题名称", {
  confirmButtonText: "确定",
  callback: (action) => {
    this.$message({
      type: "info",
      message: `action: ${action}`,
    });
  },
});

this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
  confirmButtonText: "确定",
  cancelButtonText: "取消",
  type: "warning",
})
  .then(() => {
    this.$message({
      type: "success",
      message: "删除成功!",
    });
  })
  .catch(() => {
    this.$message({
      type: "info",
      message: "已取消删除",
    });
  });

this.$prompt("请输入邮箱", "提示", {
  confirmButtonText: "确定",
  cancelButtonText: "取消",
  inputPattern:
    /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/,
  inputErrorMessage: "邮箱格式不正确",
})
  .then(({ value }) => {
    this.$message({
      type: "success",
      message: "你的邮箱是: " + value,
    });
  })
  .catch(() => {
    this.$message({
      type: "info",
      message: "取消输入",
    });
  });
```

## Checkbox 组件

- v-model 绑定的值类型设定

绑定的值类型必须为数组类型，如果绑定为字符串时候，会存在选择一个，其他全部选中的 bug。

## Radio 组件

- 添加 change 事件
- 使用 v-for 循环选项

```js
<template>
  <el-radio-group v-model="selectedOption" @change="handleChange">
    <el-radio
      v-for="(option, index) in identifyTypeList"
      :key="index"
      :label="option.status"
    >
      {{ option.name }}
    </el-radio>
  </el-radio-group>
</template>
```

## table 组件

- 表格组件多选功能，设置某些项无法选中效果。

```js
setCheckboxDisabled() {
  const table = this.$refs.myTable; // 通过ref获取组件实例
  const bodyWrapper = table.$el.querySelector(".el-table__body-wrapper");
  table.data.forEach((item, index) => {
    if (item.isGrey == 1) {
      const original = bodyWrapper.querySelectorAll(
        ".el-checkbox__original"
      );
      original[index].setAttribute("disabled", true);
      const input = bodyWrapper.querySelectorAll(".el-checkbox__input");
      input[index].setAttribute("class", "el-checkbox__input is-disabled");
    }
  });
},
```

## form 组件

- el-form-item 标签添加自定义 label

```html
<el-form-item prop="propName">
  <template #label>
    <!-- 在这里添加自定义的 label 内容 -->
    <span class="custom-label">项目名称</span>
  </template>
  <el-input v-model="baseForm.propName" @change="changeName"></el-input>
</el-form-item>
```

- 动态表单校验

```html
<el-form
  :model="dynamicValidateForm"
  ref="dynamicValidateForm"
  label-width="100px"
  class="demo-dynamic"
>
  <el-form-item
    v-for="(domain, index) in dynamicValidateForm.domains"
    :label="'域名' + index"
    :key="domain.key"
    :prop="'domains.' + index + '.value'"
    :rules="{
      required: true, message: '域名不能为空', trigger: 'blur'
    }"
  >
    <el-input v-model="domain.value"></el-input
    ><el-button @click.prevent="removeDomain(domain)">删除</el-button>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('dynamicValidateForm')"
      >提交</el-button
    >
    <el-button @click="addDomain">新增域名</el-button>
    <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>
  </el-form-item>
</el-form>
```

```js
export default {
  data() {
    return {
      dynamicValidateForm: {
        domains: [
          {
            value: "",
          },
        ],
      },
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    removeDomain(item) {
      var index = this.dynamicValidateForm.domains.indexOf(item);
      if (index !== -1) {
        this.dynamicValidateForm.domains.splice(index, 1);
      }
    },
    addDomain() {
      this.dynamicValidateForm.domains.push({
        value: "",
        key: Date.now(),
      });
    },
  },
};
```

- 动态表达传递参数

```html
<el-form-item
  v-for="(item, index) in formList"
  :key="index"
  :label="item.label"
  :prop="item.prop"
  :rules="item.rules"
>
  <el-select
    v-model="obj.dept"
    size="mini"
    @change="getEnableLicenseList(index, obj.dept)"
    placeholder="请选择"
    filterable
  >
  </el-select>
</el-form-item>
```

```js
getEnableLicenseList(index, val) {}
```

## DatePicker 组件

- 单个日期设置时间范围

```html
<el-date-picker
  v-model="date"
  type="date"
  :picker-options="pickerOptions"
  placeholder="选择日期"
>
</el-date-picker>
```

```js
// 单个时间
data() {
  return {
    date: '', // 绑定的日期值
    pickerOptions: {
      disabledDate(date) {
        // 设置时间范围从今天开始
        return date && date < new Date(new Date().toLocaleDateString());
        // 设置最大为今天
        return date.getTime() > Date.now();
      }
    }
  }
}
```

- 时间范围

```html
<el-date-picker
  @change="handleDateRangeChange"
  format="yyyy-MM-dd"
  v-model="date"
  type="daterange"
  :picker-options="pickerOptionRange"
  size="mini"
  range-separator="至"
  start-placeholder="开始日期"
  end-placeholder="结束日期"
  :disabled-date="disabledDate"
  :clearable="true"
>
</el-date-picker>
```

```js
// 时间范围
data() {
  return {
    date: [],
    pickerOptionRange:{
        shortcuts: [
            {
                text: '最近一个月',
                onClick(picker) {
                    const end = new Date();
                    const start = new Date();
                    start.setMonth(start.getMonth() - 1);
                    picker.$emit('pick', [start, end]);
                }
            },
            {
                text: '最近一年',
                onClick(picker) {
                    const end = new Date();
                    const start = new Date();
                    start.setFullYear(end.getFullYear() - 1);
                    picker.$emit('pick', [start, end]);
                }
            }
        ]
    },
  }
},
// 设置时间跨度为30天  这里才是真正的控制时间范围
handleDateRangeChange() {
    const startDate = this.date[0];
    const endDate = this.date[1];

    // 计算两个日期的时间差（以天为单位）
    const timeDiff = Math.abs(endDate - startDate) / (1000 * 60 * 60 * 24);

    if (timeDiff > 30) {
        // 如果时间跨度超过30天，则自动调整结束日期
        const adjustedEndDate = new Date(startDate.getTime() + 30 * 24 * 60 * 60 * 1000);
        this.date[1] = adjustedEndDate;
        this.$message.error('时间跨度不能超过一个月');
    }
},
// 设置时间跨域 这里的bug在于从当前时间往前推
disabledDate(time) {
    const oneYearAgo = new Date(new Date() - 315360000000); // 当前时间减去一年
    return time.getTime() < oneYearAgo || time.getTime() > Date.now(); // 日期最大跨度不超过一年
},
// 设置默认时间
setDefaultDate() {
    const end = new Date();
    const start = new Date();
    start.setMonth(start.getMonth() - 1);
    this.date = [start, end]
},

```

## Upload 组件

```js
// 阻止默认提交
设置el-upload 中 action 参数值为#，auto-upload为false

// 调用组件的外部方法
给el-upload 添加ref属性,通过ref调用相关方法

// 上传图片显示本地地址
const handChange = (uploadFile) => {
  form.file = uploadFile.raw
  imageurl = URL.createObjectURL(uploadFile.raw)
}

// 删除指定的图片
handleRemove(file) {
  // 实现缩略图模板时删除文件
  let fileList = this.$refs.upload.uploadFiles;
  let index = fileList.findIndex( fileItem => {
    return fileItem.uid === file.uid
  })
  fileList.splice(index, 1)
}

```

## Pagination 组件

- 分页组件事件传递额外参数 
- 无法直接通过已有事件解决

```js
// 通过封装Pagination组件解决
<template>
  <el-pagination
    :key="logicType"
    @current-change="handleCurrentChange"
    :total="total"
    :page-size="pageSize"
    :current-page.sync="currentPage"
  ></el-pagination>
</template>

<script>
export default {
  props: {
    logicType: String,
    total: Number,
    pageSize: Number,
    currentPage: {
      type: Number,
      required: true,
      default: 1,
    },
  },
  methods: {
    handleCurrentChange(pageNumber) {
      this.$emit('custom-current-change', pageNumber, this.logicType);
    },
  },
};
</script>

// 父组件当中使用
<my-pagination
  :logic-type="'A'"
  :total="total"
  :page-size="pageSize"
  :current-page.sync="currentPage"
  @custom-current-change="onPageChange"
></my-pagination>
<script>
export default {
  methods: {
    onPageChange(pageNumber, logicType) {
      switch (logicType) {
        case 'A':
          console.log('当前页码:', pageNumber);
          console.log('执行逻辑 A');
          // 在此处实现逻辑 A
          break;
        case 'B':
          console.log('当前页码:', pageNumber);
          console.log('执行逻辑 B');
          // 在此处实现逻辑 B
          break;
        // 添加更多逻辑类型...
        default:
          console.warn('未知逻辑类型:', logicType);
      }
    },
  },
};
</script>
```


最后更新时间：2024-9-10 13:34:17