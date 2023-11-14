## 最后更新时间(2023-11-14)

## 模块(module)

## 控制器(controller)

> 控制器负责处理传入的请求并向客户端返回响应

- 控制器的目的是接收应用的特定请求
- 每个控制器有多个路由，不同路由执行不同操作
- 路由机制控制那个控制器接收那些请求
- 基本的控制器由类和装饰器(@Controller())组成
- 控制器里面的路由，有许许多多的装饰器来装饰此路由

```js
// cats.controller.ts 可能最前面还有全局守卫策略等装饰器
@Controller("cats")
export class CatsController {
  @SkipAuth() // 自定义装饰器
  @UseGuards(AuthGuard("local")) // 使用本地策略装饰器
  @Get() // 路由方式装饰器
  findAll(): string {
    return "This action returns all cats";
  }
}
```

## 提供者(provider)

## 中间件(Middleware)

> Middleware 是在路由处理程序之前调用的函数(例如验证、日志记录、数据转换等)。中间件函数可以访问请求和响应对象，以及应用程序的请求-响应周期中的 next()中间件函数。通常，next 中间件函数由一个名为 next 的变量表示

- 执行任何代码。
- 对请求和响应对象进行更改。
- 结束请求-响应周期。
- 调用堆栈中的下一个中间件函数
- 如果当前中间件函数未结束请求-响应周期，则必须调用 next()将控制权传递给下一个中间件函数。否则，请求将被搁置。

```js
// 可以在函数中或带有@Injectable()装饰器的类中实现自定义的Nest中间件。类应该实现NestMiddleware接口，而函数没有任何特殊要求。
import { Injectable, NestMiddleware } from "@nestjs/common";
import { Request, Response, NextFunction } from "express";

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log("Request...");
    next();
  }
}
```

## 异常过滤器(Exception filters)

## 管道(Pipes)

## 守卫(Guards)

## 拦截器(Interceptors)

## 自定义装饰器(Custom decorators)
