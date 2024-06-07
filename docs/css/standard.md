<!--
 * @Description: css使用标准
 * @Author: panrui
 * @Date: 2021-10-15 14:00:00
 * @LastEditTime: 2023-04-27 10:20:19
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## CSS class 命名 (BEM 规范)

- B 代表区块
- E 代表元素
- M 代表修饰符

```scss
// 区块
.stick-man {
  // 具体元素样式
  .stick-man__head {
  }
  // 区块中修饰符
  .stick--bule {
  }
}
```

## 文件命名规范

| 类型       | 命名                            |
| ---------- | ------------------------------- |
| 主要       | master.css, style.css, main.css |
| 布局       | layout.css                      |
| 专栏       | columns.css                     |
| 文字       | font.css                        |
| 打印       | print.css                       |
| 主题       | themes.css                      |
| 附加       | attach.css                      |
| 模块       | module.css                      |
| 基本共用   | base.css                        |
| 布局，版面 | layout.css                      |
| 主题       | themes.css                      |
| 专栏       | columns.css                     |
| 表单       | forms.css                       |
| 补丁       | mend.css                        |

## 图片命名规范

> 1、文件命名：以小写英文字母、数字、符号、中划线组合
> （示例：banner@2x.png，icon-footer@2x.png，pic-header.png，logo-top@2x.png）

## 页面命名规范

> 1、html 页面命名规范：以英文字母、数字、符号，下划线组合
> （示例：index.html，navTab.html，footer_bar.html，header_1.html）

## class 名称

> 1、class 类名命名：以英文字母，数字，中划线组合
> 2、ID 类名命名：以英文字母，数字，下划线组合
> 3、以英文为主或拼音易理解，易懂的单词来标注
> 4、所以命名全部用块\_\_子元素 这种形式 然后在带上状态

```json
-   中划线 ：仅作为连字符使用，表示某个块或者某个子元素的多单词之间的连接记号。
__  双下划线：双下划线用来连接块和块的子元素
_   单下划线：单下划线用来描述一个块或者块的子元素的一种状态
```

| 语义化             | 布局               | 通用部件                   | 组件                     | 状态            |
| ------------------ | ------------------ | -------------------------- | ------------------------ | --------------- |
| 品牌 brand         | 文档 doc           | 列表 list                  | 按钮 btn                 | 前一个 prev     |
| 标志 logo          | 头部 hd            | 列表项 item                | 字体 icon                | 后一个 next     |
| 额外部件 addon     | 主体 body          | 表格 table                 | 下拉菜单 dropdown        | 当前的 current  |
| 版权 copyright     | 尾部 ft            | 表单 form                  | 工具栏 toolbar           | 显示的 show     |
| 注册 regist(reg)   | 主栏 main          | 链接 link                  | 分页 page                | 隐藏的 hide     |
| 登录 login         | 侧栏 slide         | 标题 caption/heading/title | 缩略图 thumbnail         | 打开的 open     |
| 搜索 search        | 容器 box/container | 菜单 menu                  | 警告弹框 alert           | 关闭的 close    |
| 热点 hot           | ----------         | 集合 group                 | 进度条 progress          | 选中的 selected |
| 帮助 help          | ----------         | 条 bar                     | 导航条 navbar            | 有效的 active   |
| 信息 info          | ----------         | 内容 content               | 导航 nav                 | 默认的 default  |
| 提示 tips          | ----------         | 结果 result                | 子导航 subnav            | 反转的 toggle   |
| 开关 toggle        | ----------         | ----------                 | 面包屑 breadcrumb(crumb) | 禁用的 disabled |
| 新闻 news          | ----------         | ----------                 | 标签 label               | 危险的 danger   |
| 广告 advertise(ad) | ----------         | ----------                 | 徽章 badge               | 主要的 primary  |
| 排行 top           | ----------         | ----------                 | 巨幕 jumbotron           | 成功的 success  |
| 下载 download      | ----------         | ----------                 | 面板 panel               | 提醒的 info     |
| 登录条 loginbar    | ----------         | ----------                 | 洼地 well                | 警告的 warning  |
| ----------         | ----------         | ----------                 | 标签页 tab               | 出错的 error    |
| ----------         | ----------         | ----------                 | 提示框 tooltip           | 大型的 lg       |
| ----------         | ----------         | ----------                 | 弹出框 popover           | 小型的 sm       |
| ----------         | ----------         | ----------                 | 轮播图 carousel          | 超小的 xs       |
| ----------         | ----------         | ----------                 | 手风琴 collapse          | ----------      |
| ----------         | ----------         | ----------                 | 定位浮标 affix           | ----------      |
| ----------         | ----------         | ----------                 | ----------               | ----------      |
| ----------         | ----------         | ----------                 | ----------               | ----------      |
| ----------         | ----------         | ----------                 | ----------               | ----------      |
| ----------         | ----------         | ----------                 | ----------               | ----------      |
| ----------         | ----------         | ----------                 | ----------               | ----------      |



最后更新时间：2024-4-30 13:52:59