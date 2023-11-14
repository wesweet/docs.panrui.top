<!--
 * @Description: 文件上传
 * @Author: panrui
 * @Date: 2023-06-08 08:59:59
 * @LastEditTime: 2023-06-08 09:00:24
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-14)

- [multer](https://github.com/expressjs/multer/blob/master/doc/README-zh-cn.md)

```js
npm install multer -S
```

## 使用

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
