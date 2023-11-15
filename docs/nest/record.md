<!--
 * @Description: 记录文档
 * @Author: panrui
 * @Date: 2023-11-15 09:25:43
 * @LastEditTime: 2023-11-15 09:29:59
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-15)

## 策略

## 技术

## 安全

## 认证

## 权限

## 加密和散列

## Helmet

## CORS

```
1：再mian.ts中使用
app.enableCors(); // 允许跨域 尽量放在其他中间件前面
2：enableCors方法可以接受一个参数，是一个CorsOptions对象，可以配置跨域的一些参数
app.enableCors({
  origin: '*', // 允许访问所有域
  credentials: true, // 允许携带cookie
});
```

## CSRF

## 限速

## GraphQL

## 数据库

## 静态文件

## RESTful API

## Redis

## 配置

## 单元测试

## E2E 测试

## NestFactory

> > NestFactory 是 Nest 应用程序实例的创建者。它也是一个基本的应用程序上下文，它是一个 NestApplicationContext 实例。它提供了一组方法，用于创建应用程序并创建一个可用于管理应用程序的应用程序实例。
