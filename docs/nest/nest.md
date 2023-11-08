<!--
 * @Description: nest
 * @Author: panrui
 * @Date: 2023-07-27 08:47:00
 * @LastEditTime: 2023-11-08 10:02:08
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-11-08

## 文档

- [nest](https://docs.nestjs.cn/9/introduction)

```js
// 创建项目
npm i -g @nestjs/cli
nest new project-name --strict

// 创建模块
nest g module cats

// 创建控制器
nest g controller cats

// 创建服务
nest g service cats
```

## 模块(module)

普通模块

- 模块是一个由 @Module() 装饰器函数修饰的类
- 根模块引入其他模块，其他模块也可以引入其他模块，最终组成一个模块树(也就是一个应用程序的路由树)
- 由于循环依赖的关系，模块类不能注入到服务中

```js
@Module({
  imports: [],
  exports: [], // 可以导出服务、模块
  controllers: [], // 这个模块有那些控制器
  providers: [], // 这个模块有那些服务,策略,守卫
})
export class AppModule {
  // 用于配置目的的话，也可以注入服务
  constructor(private readonly connection: Connection) {}
}
```

全局模块

- 全局模块是一个模块，它影响整个应用程序
- 通常，全局模块由 @Global() 装饰器修饰
- 全局模块应该只由根模块引入

```js
@Global()
@Module({
  imports: [],
  exports: [],
  controllers: [],
  providers: [],
})
export class AppModule {}
```

动态模块(功能正在开发中)

## 中间件

中间件

- 中间件功能可以执行任何操作，但是它们通常用于在路由处理程序之前执行额外的操作，例如验证、日志记录、数据转换等。可以访问请求和响应对象，以及应用程序请求响应周期中的 next()函数

```js
// 在函数中或在类中使用 @Injectable() 装饰器来注入中间件，这个类必须实现 NestMiddleware 接口
@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log("Request...");
    next();
  }
}
```

依赖注入(代码开发中)

- Nest 中间件是可注入的，这意味着它们可以依赖注入其他服务或者模块(通过 constructor 注入)

应用中间件

- 中间件不能在@Module()装饰器列出，必须使用模块类的 configure()方法来配置。并且包含中间件的模块必须实现 NestModule 接口

```js
import { Module, NestModule, MiddlewareConsumer } from "@nestjs/common";
import { LoggerMiddleware } from "./common/middleware/logger.middleware";
import { CatsModule } from "./cats/cats.module";
@Module({
  imports: [CatsModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes("cats");
  }
}
```

## 控制器

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

## 服务(提供者)

- Provider 是一个纯粹的 JavaScript 类，帮助控制器处理一些复杂的任务
- Provider 是由 @Injectable() 装饰器修饰的类
- 服务可以注入到控制器、其他服务中

## 策略

## 异常过滤器

## 管道

## 守卫(guard)

- guard 是由 @Injectable() 装饰器修饰的类，实现 CanActivate 接口
- 守卫的主要目的是保护路由，根据运行时候的某些条件来确定请求是否应该被处理

```js
import { ExecutionContext, Injectable } from '@nestjs/common';
import { Reflector } from '@nestjs/core';
import { AuthGuard } from '@nestjs/passport';
import { IS_PUBLIC_KEY } from './public.decorator';

@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {
  constructor(private reflector: Reflector) {
    super();
  }

  canActivate(context: ExecutionContext) {
    // Add your custom authentication logic here
    // for example, call super.logIn(request) to establish a session.
    const isPublic = this.reflector.getAllAndOverride<boolean>(IS_PUBLIC_KEY, [
      context.getHandler(),
      context.getClass(),
    ]);
    if (isPublic) {
      return true;
    }
    return super.canActivate(context);
  }
}
```

## 拦截器

## 技术

## 安全

#### 认证

#### 权限

#### 加密和散列

#### Helmet

#### CORS

```
1：再mian.ts中使用
app.enableCors(); // 允许跨域 尽量放在其他中间件前面
2：enableCors方法可以接受一个参数，是一个CorsOptions对象，可以配置跨域的一些参数
app.enableCors({
  origin: '*', // 允许访问所有域
  credentials: true, // 允许携带cookie
});
```

#### CSRF

#### 限速

## GraphQL

## 数据库

## 静态文件

## RESTful API

## Redis

## 配置

## 单元测试

## E2E 测试

## 装饰器

> 1. 装饰器是一种特殊类型的声明，它能够被附加到类声明、方法、属性或参数上，可以修改类的行为

| nest               | express        | 描述                           |
| ------------------ | -------------- | ------------------------------ |
| @Module()          |                | 定义模块                       |
| @Controller()      |                | 定义控制器                     |
| @Injectable()      |                | 定义服务                       |
| @Get()             | app.get()      | 定义路由                       |
| @Post()            | app.post()     | 定义路由                       |
| @Req()             | req            | 定义请求                       |
| @Res()             | res            | 定义响应                       |
| @Next()            | next           | 定义管道                       |
| @Param()           | req.params     | 定义参数                       |
| @Query()           | req.query      | 常用于使用 GET 请求发出的参数  |
| @Body()            | req.body       | 常用于接受 POST 请求发出的参数 |
| @Put()             | app.put()      |                                |
| @Delete()          | app.delete()   |                                |
| @Patch()           | app.patch()    |                                |
| @Options()         | app.options()  |                                |
| @Head()            | app.head()     |                                |
| @UseGuards()       | app.use()      | 定义守卫                       |
| @UseInterceptors() | app.use()      |                                |
| @UseFilters()      | app.use()      |                                |
| @UsePipes()        | app.use()      |                                |
| @UseInterceptors() | app.use()      |                                |
| @UseFilters()      | app.use()      |                                |
| @UsePipes()        | app.use()      |                                |
| @Headers()         | req.headers    |                                |
| @Session()         | req.session    |                                |
| @File()            | req.file       |                                |
| @Files()           | req.files      |                                |
| @Cookie()          | req.cookies    |                                |
| @UploadedFile()    | req.file       |                                |
| @UploadedFiles()   | req.files      |                                |
| @Render()          | res.render()   |                                |
| @Redirect()        | res.redirect() |                                |
| @SetMetadata()     |                |                                |
| @HttpCode()        | res.status()   |                                |
| @Header()          | res.set()      |                                |
| @Location()        | res.location() |                                |
| @Redirect()        | res.redirect() |                                |
| @Ip()              | req.ip         |                                |
| @HostParam()       | req.host       |                                |

#### 自定义装饰器

#### 操作响应选项

> 1. 标准

当请求处理程序返回一个 JavaScript 对象或数组时，它将自动序列化为 JSON。但是，当它返回一个 JavaScript 基本类型（例如 string、number、boolean）时， Nest 将只发送值，而不尝试序列化它

> 2. 自定义响应

在函数中使用 `@Res()` 装饰器来注入响应对象，然后使用它来自定义响应

```js
@Get()
findAll(@Res() response) {
  response.status(200).send('This action returns all cats');
}
// 注意！Nest 检测处理程序何时使用 @Res() 或 @Next()，表明你选择了特定于库的选项。如果在一个处理函数上同时使用了这两个方法，那么此处的标准方式就是自动禁用此路由, 你将不会得到你想要的结果。如果需要在某个处理函数上同时使用这两种方法（例如，通过注入响应对象，单独设置 cookie / header，但把其余部分留给框架），你必须在装饰器 @Res({ passthrough: true }) 中将 passthrough 选项设为 true
```

## 参数接受

#### multipart/form-data
