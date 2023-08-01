<!--
 * @Description: nest
 * @Author: panrui
 * @Date: 2023-07-27 08:47:00
 * @LastEditTime: 2023-07-28 14:15:14
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-07-28 14-15-14

## 文档

- [nest](https://docs.nestjs.cn/)
- [TypeORM](https://typeorm.biunav.com/zh/embedded-entities.html)

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

## 模块

- 模块是一个由 @Module() 装饰器函数修饰的类
- 根模块引入其他模块，其他模块也可以引入其他模块，最终组成一个模块树(也就是一个应用程序的路由树)

```
@Module({
  imports: [引入的模块],
  exports: [导出的模块],
  controllers: [AppController], // 这个模块有那些控制器
  providers: [AppService], // 这个模块有那些服务,策略,守卫
})
export class AppModule {}
```

## 策略

## 中间件

- 中间件功能可以执行任何操作，但是它们通常用于在路由处理程序之前执行额外的操作，例如验证、日志记录、数据转换等。可以访问请求和响应对象，以及应用程序请求响应周期中的 next()函数
- 中间件不能在@Module()装饰器列出，必须使用模块类的 configure()方法来配置。并且包含中间件的模块必须实现 NestModule 接口

## 异常过滤器

## 管道

## 守卫

- guard 是由 @Injectable() 装饰器修饰的类，实现 CanActivate 接口
- 守卫的主要目的是保护路由，根据运行时候的某些条件来确定请求是否应该被处理

## 拦截器

## 自定义装饰器

- 装饰器是一个表达式，它返回一个可以将目标、名称和属性描述符作为参数的函数。通过在装饰器前面添加一个 @ 字符并将其放置在你要装饰的内容的最顶部来应用它。可以为类、方法或属性定义装饰器。

## 技术

## 安全

#### 认证

#### 权限

#### 加密和散列

#### Helmet

#### CORS

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

#### 装饰器

> 1. 装饰器是一种特殊类型的声明，它能够被附加到类声明、方法、属性或参数上，可以修改类的行为

```
@Module() 模块
@Controller() 控制器
@Injectable() 服务
@Get()、@Post()、@Put()、@Delete()、@Patch()、@Options()、@Head()、@All() 路由
@Req() 请求对象
@Res() 响应对象
@Next() 下一个中间件
@UseGuards() 守卫
@UseInterceptors() 拦截器
@UseFilters() 过滤器
@UsePipes() 管道
@Param() 路由参数
@Query() 查询参数
@Body() 请求体
```

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
