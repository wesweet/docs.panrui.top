<!--
 * @Description:
 * @Author: prui
 * @Date: 2024-04-29 15:27:29
 * @LastEditTime: 2024-04-29 15:28:37
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 常规跨域解决方案

```js
// 解决前端跨域显示问题
app.all("*", function (req, res, next) {
  // 此处可以使用通配符
  res.header("Access-Control-Allow-Origin", "*");
  res.header(
    "Access-Control-Allow-Headers",
    "Content-Type, Content-Length, Authorization, Accept, X-Requested-With"
  );
  res.header("Access-Control-Allow-Methods", "PUT, POST, GET, DELETE, OPTIONS");
  if (req.method == "OPTIONS") {
    res.send(200);
  } else {
    next();
  }
});
```

## 携带 cookie 跨域请求

```js
app.all('*',function (req, res, next) {
    // 这里需要设置成指定请求地址
    res.header('Access-Control-Allow-Origin', '设置成指定了请求地址');
    res.header('Access-Control-Allow-Headers', 'Content-Type, Content-Length, Authorization, Accept, X-Requested-With');
    res.header('Access-Control-Allow-Methods', 'PUT, POST, GET, DELETE, OPTIONS');
  	// 这里需要设置成允许携带cookie
    res.header('Access-Control-Allow-Credentials': true)
    if (req.method == 'OPTIONS') {
      res.send(200);
    }
    else {
      next();
    }
});
```

## 携带 token 跨域请求

```js
// 一般前端会设置请求头 添加 Access-Token 等字段
if (token) {
  config.headers["Access-Token"] = token;
}

// Access-Token
app.all("*", function (req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  // 需要在这里添加 Access-Token
  // 如果请求头中还添加了其他的字段 也需要在header 当中添加对应的字段
  res.header(
    "Access-Control-Allow-Headers",
    "Content-Type, Content-Length, Authorization, Accept, X-Requested-With, Access-Token"
  );
  res.header("Access-Control-Allow-Methods", "PUT, POST, GET, DELETE, OPTIONS");
  if (req.method == "OPTIONS") {
    res.send(200);
  } else {
    next();
  }
});
```

## nginx 做接口转发处理

```json
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    server {
        listen       80;
        server_name  localhost;
        location / {
            proxy_pass   http://www.example.org:8000;
            proxy_set_header Host $host;
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
            add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range';
            add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range';
        }
    }
}
```



最后更新时间：2024-4-29 15:30:40