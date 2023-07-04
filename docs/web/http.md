<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-06-07 13:24:24
 * @LastEditTime: 2023-06-07 13:56:17
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间：2023-06-07 13-24-27

> 1.  [文档](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP)

## HTTP

http 是一个基于请求与响应模式的、无状态的、应用层的协议，常基于 TCP(TLS) 的连接方式，HTTP1.1 版本中给出了一种持久连接的机制，绝大多数的 Web 开发都是构建在 HTTP 协议之上的 Web 应用。

## HTTP 标头

```
Accept: 告知（服务器）客户端可以处理的内容类型
Accept-Language: 告知（服务器）客户端可以处理的语言
Cache-Control: 告知所有的缓存机制是否可以缓存及哪种类型

Content-Type: 请求正文的类型
当 Content-Type 的值为 application/json 时，表示请求正文中包含的是 JSON 格式的数据。
当 Content-Type 的值为 application/x-www-form-urlencoded 时，表示请求正文中包含的是 URL 编码的表单数据。这种格式通常用于 HTML 表单提交时，表单数据会被编码为键值对的形式，每个键值对之间用 & 分隔，键和值之间用 = 分隔。例如，key1=value1&key2=value2。

Connection: 控制网络连接在当前会话完成后是否仍然保持打开状态。如果发送的值是 keep-alive，则连接是持久的，不会关闭，允许对同一服务器进行后续请求
Content-Length: 指明发送给接收方的消息主体的大小，即用十进制数字表示的八位元组的数目

Host: 指明了请求将要发送到的服务器主机名和端口号
Origin: 表示了请求的来源（协议、主机、端口）
Referer: 当前请求页面的来源页面的地址，即表示当前页面是通过此来源页面里的链接进入的。



Accept-Charset: 告知（服务器）客户端可以处理的字符集
Accept-Encoding: 告知（服务器）客户端可以处理的压缩编码
Accept-Ranges: 告知（服务器）客户端是否可以请求部分资源
Authorization: 用于证明客户端有权查看某个资源
Cookie: 当前页面设置的任何 Cookie
Content-MD5: 请求的内容 MD5 校验值
Date: 请求发送的日期和时间
Expect: 请求的特定的服务器行为
From: 发送请求的用户的 Email
If-Match: 只有请求内容与实体相匹配才有效
If-Modified-Since: 如果请求的部分在指定时间之后被修改则请求成功，未被修改则返回304代码
If-None-Match: 如果内容未改变返回304代码，参数为服务器先前发送的 ETag，否则返回200 ok和新的内容
If-Range: 如果实体未改变，服务器发送客户端丢失的部分，否则发送整个实体。参数也为 ETag
If-Unmodified-Since: 只在实体在指定时间之后未被修改才请求成功
Max-Forwards: 限制信息通过代理和网关传送的时间
Pragma: 包括实现特定的指令，它可应用到响应链上的任何接收方
Proxy-Authorization: 连接到代理的授权证书
Range: 只请求实体的一部分，指定范围

TE: 客户端愿意接受的传输编码，并通知服务器接受接受尾加头信息
Upgrade: 向服务器指定某种传输协议以便服务器进行转换（如果支持）
User-Agent: User-Agent 的内容包含发出请求的用户信息
Via: 通知中间网关或代理服务器地址，通信协议
Warning: 关于消息实体的警告信息
```

## HTTP 状态码

```
1xx: 指示信息--表示请求已接收，继续处理
2xx: 成功--表示请求已被成功接收、理解、接受
3xx: 重定向--要完成请求必须进行更进一步的操作
4xx: 客户端错误--请求有语法错误或请求无法实现
5xx: 服务器端错误--服务器未能实现合法的请求
```

## HTTP 方法

```
GET: 请求指定的页面信息，并返回实体主体
HEAD: 类似于 get 请求，只不过返回的响应中没有具体的内容，用于获取报头
POST: 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST 请求可能会导致新的资源的建立和/或已有资源的修改
PUT: 从客户端向服务器传送的数据取代指定的文档的内容
DELETE: 请求服务器删除指定的页面
CONNECT: HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器
OPTIONS: 允许客户端查看服务器的性能
TRACE: 回显服务器收到的请求，主要用于测试或诊断
```
