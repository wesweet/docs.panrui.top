<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-05-18 17:17:52
 * @LastEditTime: 2023-07-24 14:00:01
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-07-24 14-00-01

## 文档

- [pm2](https://pm2.keymetrics.io/docs/usage/quick-start/)

```js
npm install pm2@latest -g
```

## 基本操作

```js
// 启动
pm2 start app.js
// 停止
pm2 stop app.js
// 重启
pm2 restart app.js
// 杀死指定进程
pm2 delete appname | id
// 杀死全部进程
pm2 kill
// 查看日志
pm2 logs
// 查看状态
pm2 list
// 查看详细状态信息
pm2 show appname | id
// 监控每个node进程的cpu和内存使用情况
pm2 monit
// 监控运行的机器的状态
pm2 web
// 清除日志
pm2 flush
```

## 重启所有pm2进程

```js
// 查看PM2 文件有那些进程
[PM2] Successfully saved in /root/.pm2/dump.pm2
```
