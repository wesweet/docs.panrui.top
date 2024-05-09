<!--
 * @Description:
 * @Author: prui
 * @Date: 2024-05-09 08:40:42
 * @LastEditTime: 2024-05-09 10:05:56
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 基于 hexo-theme-Fomalhaut 开源仓库的博客主题修改

## 修改首页 swipe

-[基于 Butterfly 主题的轮播手动置顶文章](https://akilar.top/posts/8e1264d1/)

## 修改首页欢迎语(网页副标题)

```
# 主页subtitle
subtitle:
  enable: false
  # Typewriter Effect (打字效果)
  effect: true
  startDelay: 300 # time before typing starts in milliseconds
  typeSpeed: 150 # type speed in milliseconds
  backSpeed: 50 # backspacing speed in milliseconds
  # loop (循环打字)
  loop: true
  # source 调用第三方服务
  # source: false 关闭调用
  # source: 1  调用一言网的一句话（简体） https://hitokoto.cn/
  # source: 2  调用一句网（简体） http://yijuzhan.com/
  # source: 3  调用今日诗词（简体） https://www.jinrishici.com/
  # subtitle 会先显示 source , 再显示 sub 的内容
  source: false
  # 如果关闭打字效果，subtitle 只会显示 sub 的第一行文字
  sub:
    - 今日事&#44;今日毕
    - Never put off till tomorrow what you can do today
```

## 文字内容含有表情包


最后更新时间：2024-5-9 10:05:49
