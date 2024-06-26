<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-29 13:12:22
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 文档

> 1. [axios](http://www.axios-js.com/zh-cn/docs/)

## Axios 如何取消重复请求

```js
// 新建 map 对象
const pendingRequest = new Map();

// 创建 map 对象的key
function generateReqKey(config) {
  const { method, url, params, data } = config;
  return [method, url, Qs.stringify(params), Qs.stringify(data)].join("&");
}

// 通过 executor 函数到 CancelToken 的构造函数来创建 cancel token
function addPendingRequest(config) {
  const requestKey = generateReqKey(config);
  config.cancelToken =
    config.cancelToken ||
    new axios.CancelToken((cancel) => {
      if (!pendingRequest.has(requestKey)) {
        pendingRequest.set(requestKey, cancel); // 此处的 cancel 是一个函数 可以取消请求的
      }
    });
}

// 移除 map key 同时取消 axios 请求
function removePendingRequest(config) {
  const requestKey = generateReqKey(config);
  if (pendingRequest.has(requestKey)) {
    const cancel = pendingRequest.get(requestKey);
    cancel(requestKey);
    pendingRequest.delete(requestKey);
  }
}

// 请求前拦截
axios.interceptors.request.use(
  function (config) {
    removePendingRequest(config); // 检查是否存在重复请求，若存在则取消已发的请求
    addPendingRequest(config); // 把当前请求添加到pendingRequest对象中
    return config;
  },
  (error) => {
    return Promise.reject(error);
  }
);

// 返回前拦截
axios.interceptors.response.use(
  (response) => {
    removePendingRequest(response.config); // 从pendingRequest对象中移除请求
    return response;
  },
  (error) => {
    removePendingRequest(error.config || {}); // 从pendingRequest对象中移除请求
    if (axios.isCancel(error)) {
      console.log("已取消的重复请求：" + error.message);
    } else {
      // 添加异常处理
    }
    return Promise.reject(error);
  }
);
```


## 使用axios下载文件
```js
export const downloadFile = (
  url,
  params,
  loading = true,
  filename = "download"
) => {
  return new Promise((resolve, reject) => {
    instance({
      url: url,
      method: "GET",
      params: params,
      responseType: "blob", // 指示服务器响应的数据类型
      headers: {
        loading: loading,
      },
    })
      .then((response) => {
        const contentType =
          response.headers["content-type"] || "application/octet-stream";
        const blob = new Blob([response.data], { type: contentType });
        const downloadUrl = URL.createObjectURL(blob);
        const link = document.createElement("a");
        link.href = downloadUrl;
        link.download = filename;
        document.body.append(link);
        link.click();
        URL.revokeObjectURL(link.href);
        link.remove(); // 正确的移除方式
        resolve();
      })
      .catch((error) => {
        console.error("Download error:", error);
        reject(error);
      })
      .finally(() => {
        if (loading) $da.hideLoading();
      });
  });
};
```

最后更新时间：2024-5-17 12:57:13
