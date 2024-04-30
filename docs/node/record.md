<!--
 * @Description:
 * @Author: prui
 * @Date: 2024-04-29 15:27:29
 * @LastEditTime: 2024-04-30 10:07:07
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

## uuid

#### 基本使用

```js
// 基于时间戳生成
uuid.v1();

// 随机生成
uuid.v4();
```

## multer

- [multer](https://github.com/expressjs/multer/blob/master/doc/README-zh-cn.md)

```js
npm install multer -S
```

#### 使用

```js
const multer = require("multer");
const fs = require("fs");
const path = require("path");
const Logger = require("./logger");

// 上传文件所存储的位置和文件名
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    // 上传文件的目录
    let uploadDir = path.resolve(process.cwd(), "public/images");
    try {
      // 检测文件夹是否存在
      if (!fs.existsSync(uploadDir)) {
        fs.mkdirSync(uploadDir);
      }
    } catch (error) {
      Logger.error(error);
    }
    cb(null, uploadDir);
  },
  filename: function (req, file, cb) {
    // 上传文件的名称
    const originalname = file.originalname;
    const extension = originalname.substring(originalname.lastIndexOf(".") + 1);
    const filename = file.fieldname + "-" + Date.now() + "." + extension;
    cb(null, filename);
  },
});

// 上传文件的限制
const limits = {
  // 限制文件的大小为2M
  fileSize: 1024 * 1024 * 5,
  // 限制文件的数量为5个
  files: 5,
};

// 上传文件的类型
const fileFilter = function (req, file, cb) {
  // 限制文件的类型
  const allowedFileTypes = ["image/jpeg", "image/png", "image/gif"];
  if (allowedFileTypes.includes(file.mimetype)) {
    cb(null, true);
  } else {
    cb(new Error("请上传正确的文件类型"));
  }
};

// 上传文件的配置
const upload = multer({
  storage,
  limits,
  fileFilter,
});

module.exports = upload;
```

最后更新时间：2024-4-29 15:30:40
