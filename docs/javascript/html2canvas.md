<!--
 * @Description: html2canvas使用文档
 * @Author: panrui
 * @Date: 2023-07-14 15:09:45
 * @LastEditTime: 2024-06-11 15:00:29
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

- [英文文档](http://html2canvas.hertzen.com/getting-started)

## 基础用法

```js
// 生成图片
const handleShare = async () => {
  const element = document.getElementById("elementId");
  ignoreElement.value = true;
  await nextTick();
  html2canvas(element, {
    scale: 3,
    ignoreElements: (element) => {
      if (element.classList.contains("ignore")) {
        return true;
      }
    },
  }).then((canvas) => {
    const img = canvas.toDataURL("image/png");
    if (img) {
      imageUrl.value = img;
      showOverlay.value = true;
    }
  });
};

// 下载图片
const handleDown = () => {
  try {
    const base64Data = imageUrl.value; // 假设这是你的Base64字符串
    const fileName = "fileName.png"; // 假设文件名和类型

    // 将Base64转换为Blob
    const byteCharacters = atob(base64Data.split(",")[1]); // 去掉"data:image/png;base64,"前缀
    const byteArrays = [];
    for (let i = 0; i < byteCharacters.length; i++) {
      byteArrays.push(byteCharacters.charCodeAt(i));
    }
    const blob = new Blob([new Uint8Array(byteArrays)], { type: "image/png" }); // 根据实际类型调整

    // 创建Object URL
    const url = URL.createObjectURL(blob);

    // 创建隐藏的<a>元素并触发点击下载
    const a = document.createElement("a");
    a.style.display = "none";
    a.href = url;
    a.download = fileName;
    document.body.appendChild(a);
    a.click();

    // 清理Object URL以避免内存泄漏
    setTimeout(() => {
      URL.revokeObjectURL(url);
      document.body.removeChild(a);
    }, 100); // 延迟一点时间以确保下载开始
  } catch (error) {
    console.log(error);
  }
};
```

## 选项配置

## 问题

> 1. 生成图片不完整，解决方案就是再父元素设置滚动条，这样就能生成完整的图片了
> 2. 在 iOS 中，如果要生成的模版中有使用图片，尽量避免使用 svg 图片。(使用 svg 图片会导致生成图片不完整，右侧产生一块空白)

最后更新时间：2024-6-11 15:00:22
