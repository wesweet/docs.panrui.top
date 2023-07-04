<!--
 * @Description: laravel 基础教程
 * @Author: panrui
 * @Date: 2021-11-24 10:43:48
 * @LastEditTime: 2021-12-13 16:09:39
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 目录结构

- ├── app // 包含应用程序的核心代码 几乎所有的类都位于此项目
  - └── Console // 包含应用所有自定义的 Artisan 命令
  - └── Exceptions // 包含应用的异常处理器
  - └── Http // 包含了控制器、中间件以及表单请求等，几乎所有通过 Web 进入应用的请求的逻辑都在这里进行
  - └── Providers // 包含程序中所有的 服务提供者 。服务提供者通过在服务容器中绑定服务、注册事件或执行任何其他任务来引导应用程序以应对传入请求
  - └── User.php //
- ├── bootstrap // 包含了框架的启动文件 app.php
  - └── cache // 包含框架生成的文件
  - └── app.php // 根据 envmark.text 加载不同的环境文件
- ├── config // 应用程序的所有配置文件
- ├── database // 数据库迁移，模型工厂和种子生成器文件
- ├── public // 包含 index.php 文件，该文件是进入你应用程序的所有请求的入口，并配置自动加载
- ├── resources // 包含了 views 以及未编译的资源文件
- ├── routes // 包含应用程序的所有路由定义
  - └── web.php // 包含 RouteServiceProvider 放置在 web 中间件组中的路由
  - └── api.php // 包含 RouteServiceProvider 放置在 api 中间件组中的路由
  - └── console.php // 定义所有基于闭包的控制台命令
  - └── channels.php // 你可以注册应用程序支持的所有 事件广播 频道的位置
- ├── storage // 包含了你的日志文件，已编译的 Blade 模版，基于文件的会话，文件缓存以及框架生成的其他文件
  - └── app // 用于存储应用程序生成的任何文件
  - └── framework // 用于存储框架生成的文件和缓存
  - └── logs // 包含应用程序的日志文件
- ├── tests // 自动化测试类
- ├── vendor // 包含你的 Composer 依赖
- ├── .editorconfig //
- ├── .env // 生成环境配置文件
- ├── .env.example //
- ├── .envdevelopment // 开发环境配置文件
- ├── .envpre // 预发布环境配置文件
- ├── .gitattributes //
- ├── .gitignore //
- ├── artisan //
- ├── composer.json //
- ├── composer.lock //
- ├── envmark.text // 当前开发环境
- ├── package.json //
- ├── phpunit.xml //
- ├── readme.en.md //
- ├── readme.md //
- ├── server.php //
- ├── webpack.mix.js //

## 请求生命周期

```
1: Laravel 应用程序的所有请求的入口点都是 public/index.php 文件。所有请求都由你的 web 服务器（Apache/Nginx）配置定向到此文件。该 index.php 文件将加载 Composer 生成的自动加载器定义，然后从 bootstrap/app.php 中检索 Laravel 应用程序的实例
2: 传入请求被发送到 HTTP 内核还是 Console 内核，具体取决于进入应用的请求类型
```

## 路由

## 中间件

## CSRF 保护

## 控制器

## 请求

## 响应

## 视图

## Blade 模板

## 生成 URL

## 会话

## 表单处理

## 错误处理

## 日志
