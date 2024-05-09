<!--
 * @Description:
 * @Author: prui
 * @Date: 2024-05-09 08:40:42
 * @LastEditTime: 2024-05-09 10:05:56
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 基于 hexo-theme-Fomalhaut 开源仓库的博客主题修改

## 首页 swiper 轮播图修改

-[基于 Butterfly 主题的轮播手动置顶文章](https://akilar.top/posts/8e1264d1/)

## 首页swiper 下次冰贴修改
```
magnet:
  enable: true
  priority: 2
  enable_page: /
  type: categories
  devide: 3
  display:
    - name: 算法
      display_name: 小Fの算法学习笔记
      icon: 🍡
    - name: 计算机基础
      display_name: 小Fの计算机基础笔记
      icon: 🍼
    - name: 魔改教程
      display_name: 小Fの博客魔改教程
      icon: 🍉
    - name: Java基础
      display_name: 小FのJava基础笔记
      icon: 🍟
    - name: 数据库
      display_name: 小Fの数据库笔记
      icon: 🍨
    - name: 演示
      display_name: 小Fの案例演示笔记
      icon: 🍥
  color_setting:
    text_color: black # 文字默认颜色
    text_hover_color: white # 文字鼠标悬浮颜色
    background_color: "#e9e9e9" # 文字背景默认颜色
    background_hover_color: var(--text-bg-hover) # 文字背景悬浮颜色
  layout:
    type: id
    name: recent-posts
    index: 0
  temple_html: '<div class="recent-post-item" style="width:100%;height: auto"><div id="catalog_magnet">${temple_html_item}</div></div>'
  plus_style: ""
```

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

## 社交图标设置
```
social:
  Github: https://github.com/wesweet || icon-github || faa-tada
  微信: /assets/QRCode.jpg || icon-weixin || faa-tada
  QQ: https://res.abeim.cn/api/qq/?qq=1547177202 || icon-QQ || faa-tada
  QQ邮箱: mailto:1547177202@qq.com || icon-youxiang || faa-tada
```


## 修改右侧公告栏

## 通过js设置背景图片



## 文字内容含有表情包


最后更新时间：2024-5-9 10:05:49
