<!--
 * @Description: Process 模块 提供当前Node 进程相关的全局环境信息
 * @Author: panrui
 * @Date: 2021-08-13 16:39:49
 * @LastEditTime: 2022-12-07 16:38:15
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->


## [文档](http://nodejs.cn/api/process.html)

## 基础使用

```js
const process = require("process");

process.cwd(); // 返回当前Node进程执行的目录

process.argv; // 返回终端通过Node执行命令时候 传入的命令行参数，返回值是一个数组 0：Node路径 1：被执行的JS文件路径 2~n：真实参数
const args = process.argv.slice(2);

process.env; // 返回一个存储当前环境相关的所有信息

process.platform; // 返回当前系统信息

// process.chdir() 方法更改 Node.js 进程的当前工作目录
```

## child_process 模块

```js

```
