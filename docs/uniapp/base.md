<!--
 * @Description:
 * @Author: prui
 * @Date: 2023-11-17 08:43:09
 * @LastEditTime: 2023-11-30 14:35:55
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-17)

## 文件上传

> uni.chooseImage 文件选择
> uni.uploadFile 文件上传

```js
// 单文件
const uploadFile = () => {
  uni.chooseImage({
    count: 1,
    success: (res) => {
      uni.uploadFile({
        url: HTTP_REQUEST_URL + appApi.uploadFile,
        filePath: res.tempFilePaths[0],
        name: "file",
        formData: {
          a: 1,
          b: 2,
        },
        success: (res) => {
          console.log(res);
        },
      });
    },
  });
};
```

```js
// 多文件上传
const uploadFile = () => {
  uni.chooseImage({
    success: (res) => {
      let files = [];
      for (let i = 0; i < res.tempFilePaths.length; i++) {
        files.push({
          name: "file" + i,
          uri: res.tempFilePaths[i],
        });
      }
      uni.uploadFile({
        url: HTTP_REQUEST_URL + appApi.uploadFile,
        files: files,
        formData: {
          a: 1,
          b: 2,
        },
        success: (res) => {
          console.log(res);
        },
      });
    },
  });
};
```
