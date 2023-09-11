<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-05-18 17:17:52
 * @LastEditTime: 2023-09-11 09:56:11
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

## ecosystem.config.js

```js
module.exports = {
  apps: [
    {
        name: 'app', // 项目名
        script: './app.js', // 执行文件
        cwd: './', // app启动的路径
        args: '', // 传递给脚本的参数
        interpreter: '', // 指定的脚本解释器 默认是node
        interpreter_args: '', // 传递给解释器的参数
        node_args: '', // 传递给node的参数

        exec_mode: 'fork', // 应用启动模式，支持fork和cluster模式 默认是fork
        instances: 1, // 启动实例个数，仅在cluster模式有效 默认为fork；或者 max
        watch: true, // 是否监听文件变动然后重启
        ignore_watch: [ // 不用监听的文件
            'node_modules',
            'logs'
        ],
        max_memory_restart: '1G', // 最大内存限制数，超出自动重启
        env: {
            NODE_ENV: 'production', // 环境参数，当前指定为生产环境 process.env.NODE_ENV
        },
        env_dev: {
            NODE_ENV: 'development', // 环境参数，当前指定为开发环境 pm2 start app.js --env_dev
        },
        env_test: { // 环境参数，当前指定为测试环境 pm2 start app.js --env_test
            NODE_ENV: 'test'
        },
        appendEnvToName: true, // 是否将NODE_ENV环境变量值追加到应用名后面
        source_map_support: true, // 启用源码调试，这样出错的时候会显示源代码的错误位置（如果有）
        instance_var: 'INSTANCE_ID', // 环境变量名，如果设置了，可以通过`pm2 env`命令查看
        filter_env: ['NODE_ENV', 'APP_KEY'], // 过滤部分环境变量，将只保留指定的环境变量到进程中

        log_date_format: 'YYYY-MM-DD HH:mm:ss', // 指定日志文件的时间格式
        error_file: './logs/app-err.log', // 错误日志文件路径
        out_file: './logs/app-out.log', // 正常日志文件路径
        log_file: './logs/app-combined.log', // 综合日志文件路径
        combine_logs: true, // 是否合并日志文件到一个
        merge_logs: true, // 进程退出后，日志是否归并到主进程日志中
        time: true, // 是否在日志中显示时间
        pid_file: './pids/app.pid', // pid文件路径

        min_uptime: '60s', // 应用运行少于时间被认为是异常启动
        listen_timeout: 3000, // 启动等待超时时间
        kill_timeout: 3000, // 进程关闭超时时间
        shutdown_with_message: true, // 在进程准备退出时，pm2是否发送一条带有用户自定义消息的消息给应用程序
        wait_ready: true, // 进程启动等待应用程序发送ready信号，默认为false
        max_restarts: 30, // 最大异常重启次数，即小于min_uptime运行时间重启次数；为0时，永不重启
        restart_delay: 60, // 异常重启情况下，延时重启时间
        autorestart: true, // 默认为true, 发生异常的情况下自动重启
        cron_restart: '', // crontab时间格式重启应用，目前只支持cluster模式;
        vizion: false, // 是否启用vizion特性，默认为false，即禁用
        post_update: ['npm install'], // 在应用程序重启之后执行的脚本列表
        force: false, // 默认为false，如果true，可以重复启动一个脚本

        key: '', // SSH秘钥路径
        user: 'root', // 以哪个用户启动
        host: '', // 主机名
        ssh_options: '', // 选项
        ref: 'origin/master', // Git分支
        repo: '', // Git地址，用于deploy功能
        path: '/var/www/development', // 项目路径
        pre-setup: 'npm install', // 在安装应用程序之前执行的脚本
        post-setup: 'ls -la', // 在安装应用程序之后执行的脚本
        pre-deploy-local: 'echo \'This is a local executed command\'', // 在push代码到远程仓库之前执行
        post-deploy: 'npm install', // 在成功部署之后执行的脚本
    }
  ],
};
```

## 重启所有 pm2 进程

```js
// 查看PM2 文件有那些进程
[PM2] Successfully saved in /root/.pm2/dump.pm2
```
