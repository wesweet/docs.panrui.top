## 介绍

```
1:  Dotenv 是一个零依赖的模块，它能将环境变量中的变量从 .env 文件加载到 process.env 中
```

## 安装依赖

```js
npm install dotenv --save
```

## 使用

```js
// 1: 在根目录创建.env文件
const dotenv = require('dotenv')
const envFound = dotenv.config();
if (envFound.error) {
    // This error should crash whole process

    throw new Error("⚠️  Couldn't find .env file  ⚠️");
}

// 2. 直接使用 process.env
```
