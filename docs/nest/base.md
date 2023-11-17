## 最后更新时间(2023-11-15)

## 模块(module)

> 使用@Module()装饰器提供元数据的类，Nest 使用这些元数据来组织应用程序的结构

- 使用@Global()装饰器定义的模块称之为全局模块，只注册一次，最好由根模块或者核心模块注册
- 动态模块(文档更新中...)

```js
@Module({
  imports: [], // 导入模块的列表，这些模块导出了此模块中所需提供者
  exports: [], // 可以导出服务、模块
  controllers: [], // 必须创建的一组控制器
  providers: [], // 这个模块有那些服务,策略,守卫
})
export class AppModule {
  // 用于配置目的的话，也可以注入服务
  constructor(private readonly connection: Connection) {}
}
```

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

| nest              | express        | 描述                                         |
| ----------------- | -------------- | -------------------------------------------- |
| @Get()            | app.get()      | 定义路由                                     |
| @Post()           | app.post()     | 定义路由                                     |
| @Req(),@Request() | req            | 定义请求                                     |
| @Res()            | res            | 定义响应                                     |
| @UploadedFile()   | req.file       | 常用于接受 formData 表单传递的 file 文件参数 |
| @Next()           | next           |                                              |
| @Session()        | req.session    |                                              |
| @Param()          | req.params     | 定义参数                                     |
| @Body()           | req.body       | 常用于接受 POST 请求发出的参数               |
| @Query()          | req.query      | 常用于使用 GET 请求发出的参数                |
| @Header()         | req.headers    |                                              |
| @Ip()             | req.ip         |                                              |
| @HostParam()      | req.hosts      |                                              |
| @HttpCode()       | res.status()   |                                              |
| @Redirect()       | res.redirect() |                                              |

## 提供者(provider)

> 提供者的主要思想是它可以作为依赖项注入

- 提供者是普通的 JavaScript 类，在模块中声明为 providers
- 使用@Injectable()装饰器提供元数据，声明这个类是一个可以由 Nest IoC 容器管理的类。
- 提供者都是通过类构造函数注入的。

```js
import { CatsService } from './cats.service';
@Controller('cats')
export class CatsController {
  constructor(private catsService: CatsService) {}
  @Post()
  async create(@Body() body: any) {
    this.catsService.create(body); // 通过this调用
  }
}
```

## 中间件(Middleware)

> Middleware 是在路由处理程序之前调用的函数(例如验证、日志记录、数据转换等)。中间件函数可以访问请求和响应对象，以及应用程序的请求-响应周期中的 next()中间件函数。通常，next 中间件函数由一个名为 next 的变量表示

> _路由处理之前、可以访问请求和响应对象,以及 next()中间件函数_

- 执行任何代码。
- 对请求和响应对象进行更改。
- 结束请求-响应周期。
- 调用堆栈中的下一个中间件函数
- 如果当前中间件函数未结束请求-响应周期，则必须调用 next()将控制权传递给下一个中间件函数。否则，请求将被搁置。
- Nest 中间件完全支持依赖注入。与提供者和控制器一样，它们能够在同一模块内注入依赖项。与往常一样，这是通过 constructor 来实现的。

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

```js
// 应用中间件
// 中间件不能在@Module()装饰器列出，必须使用模块类的 configure()方法来配置。并且包含中间件的模块必须实现 NestModule 接口
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

```js
// 全局中间件
const app = await NestFactory.create(AppModule);
app.use(logger); // 通过use方法全局注册
await app.listen(3000);
```

## 异常过滤器(Exception filters)

> Nest 框架内置了一个异常处理层(默认情况下，全局异常过滤器)，负责处理应用程序中的所有未处理异常(处理类型为 HttpException（以及其子类）的异常)。

- 所有的异常过滤器都应该实现通用的 ExceptionFilter<T> 接口,这要求您提供具有指定签名的 catch(exception: T, host: ArgumentsHost) 方法。其中，T 表示异常的类型。
- 使用@UseFilters()进行绑定
- 使用 app.useGlobalFilters()绑定全局过滤器

```js
// 如果一个异常未识别(既不是HttpException，也不是继承自HttpException的类），内置的异常过滤器会生成以下默认的JSON响应)
{
  "statusCode": 500,
  "message": "Internal server error"
}
```

## 管道(Pipes)

> 管道应用的场景(1:转换数据、2:验证数据)

- 管道是具有 @Injectable() 装饰器的类。管道应实现 PipeTransform 接口

| nest             | express        | 描述                           |
| ---------------- | -------------- | ------------------------------ |
| ValidationPipe   | -------------- | ------------------------------ |
| ParseIntPipe     | -------------- | ------------------------------ |
| ParseFloatPipe   | -------------- | ------------------------------ |
| ParseBoolPipe    | -------------- | ------------------------------ |
| ParseArrayPipe   | -------------- | ------------------------------ |
| ParseUUIDPipe    | -------------- | ------------------------------ |
| ParseEnumPipe    | -------------- | ------------------------------ |
| DefaultValuePipe | -------------- | ------------------------------ |
| ParseFilePipe    | -------------- | ------------------------------ |

## 守卫(Guards)

> 守卫具有单一职责。它们根据运行时的某些条件（如权限、角色、ACL 等）确定是否将处理给定请求，这通常称为授权。

- 守卫是一个使用 @Injectable() 装饰器的类。 守卫应该实现 CanActivate 接口。
- _守卫在所有中间件之后执行，但在拦截器或管道之前执行_

## 拦截器(Interceptors)

- 拦截器是使用 @Injectable() 装饰器注解的类。拦截器应该实现 NestInterceptor 接口。
- 在函数执行之前/之后绑定额外的逻辑
- 转换从函数返回的结果
- 转换从函数抛出的异常
- 扩展基本函数行为
- 根据所选条件完全重写函数 (例如, 缓存目的)
- 每个拦截器都有 intercept() 方法，它接收 2 个参数。
  | nest | express | 描述 |
  | ------------------ | ------- | ---------------------------------------------------- |
  |FileInterceptor|--------------|拦截单个文件|

## 自定义装饰器(Custom decorators)

## 内置装饰器

| nest               | express | 描述                                                 |
| ------------------ | ------- | ---------------------------------------------------- |
| @Controller()      |         | 定义控制器                                           |
| @Injectable()      |         | 定义提供者、定义管道、定义守卫、定义拦截器、定义策略 |
| @Module()          |         | 定义模块                                             |
| @Catch             |         | 定义过滤器                                           |
| @UseFilters()      |         | 绑定过滤器                                           |
| @UseGuards()       |         | 绑定守卫                                             |
| @UseInterceptors() |         | 绑定拦截器                                           |
| @UsePipes()        |         | 绑定管道                                             |
| @UploadedFile()    |         | 从请求中读取file                                         |
