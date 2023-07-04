<!--
 * @Description: 自定义组件库开发指南
 * @Author: panrui
 * @Date: 2021-07-08 11:36:43
 * @LastEditTime: 2021-07-15 16:00:01
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 项目目录结构

- ├── example // 测试组件的项目目录
  - └── assets // 静态资源
  - └── components // 项目组件
  - └── mds // 组件使用说明文档
  - └── router // 路由配置文件
  - └── store // 状态库
  - └── views // 页面
- ├── lib // 发布到 npm 仓库的文件
- ├── package // 组件源码目录
  - └── componentName // 组件
  - └── index.js // 注册组件

## 组件开发

```html
在package文件夹下面创建对应组件文件夹 例如：
- ├── citypicker // 城市联动组件 
  - └── src // 组件源码目录 
    - └── CityPicker // 组件源码
  - └── index.js // 为组件添加install方法
```

## 组件命名

```html
所有组件name属性字段必须使用Mj开头
```

```js
// 例如城市联动组件
export default {
  name: "MjCityPicker",
};
```

## 组件注册
```js
在 package 文件夹下 index.js 文件中,注册对应的组件,为组件添加installed方法
```

## 组件库测试
```js
在 example 文件目录下，新增相关页面，引入自定义组件测试功能 
```

## 组件库发布

#### 打包组件库

```js
npm run lib
```

#### 组件库发布

```js
//登录 输入对应的账号、密码、邮箱
npm login

//发布
npm publish
```
