<!--
 * @Description: html使用规范
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2023-05-19 09:12:47
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-14)

## 语义化标签

```html
<html>
  <head 定义文档的信息>
    <meta 定义关于html文档的元信息 />
    <style 定义文档的样式信息></style>
  </head>
  <body>
    <header 定义section或page的页眉></header>
    <main 定义文档的主要内容>
      <div 定义文档中的节></div>
      <article 定义文章></article>
      <table 定义表格>
        <caption 定义表格标题></caption>
        <thead 表头>
          <tr 表格行>
            <th 表头单元格></th>
          </tr>
        </thead>
        <tbody 主体>
          <tr 表格行>
            <td 表体单元格></td>
          </tr>
        </tbody>
        <tfoot 表尾></tfoot>
      </table>
      <ul 无序列表>
        <li></li>
      </ul>
      <ol 有序列表>
        <li></li>
      </ol>
      <a 定义锚></a>
      <link 定义文档与外部资源的关系 />
      <nav 定义导航链接></nav>
      <audio 定义声音内容></audio>
      <video 定义视频></video>
      <img 定义图片 />
      <form HTML表单>
        <label 定义input元素的标注></label>
        <input 输入控件 />
        <textarea 多行文本输入></textarea>
        <button 定义按钮></button>
        <select 定义下拉列表>
          <option 下拉列表选项></option>
        </select>
      </form>
      <b 定义粗体></b>
      <bdo 定义文字方向></bdo>
      <em 强调文本></em>
      <i 定义斜体文本></i>
      <p 定义段落></p>
      <br 定义简单的换行 />
      <hr 定义水平线 />
    </main>
    <aside 定义页面内容之外的内容></aside>
    <footer 定义section或page的页脚></footer>
    <script 定义客户端脚本></script>
  </body>
</html>
```

## 其他

```html
<div class="container">
  <div
    class="row clearfix"
    style="display: flex;justify-content: space-between;margin-top: 10px"
  >
    <div
      class="col-md-6 column"
      style="margin-right: 5px;flex-grow: 1;border: solid 1px silver"
    >
      <h3>代码格式与元素属性</h3>
      <b>注释使用</b>
      <!-- 注释 -->
      <h1 class="m-logo"><a href="#">LOGO</a></h1>
      <!-- /注释 -->
      <b>代码本身的注释</b>
      <!-- <h1 class="m-logo"><a href="#">LOGO</a></h1> -->
      <!--
            <ul class="m-nav">
                <li><a href="#">NAV1</a></li>
                <li><a href="#">NAV2</a></li>
            </ul>
            -->
      <h5>
        单行代码的注释也保持同行，两端空格；多行代码的注释起始和结尾都另起一行并左缩进对齐
      </h5>
      <h5>如果两个浮动元素之间存在注释，那么可能导致布局错位或文字的BUG</h5>
      <h5>
        尽可能以最严格的xhtml
        strict标准来嵌套，比如内联元素不能包含块级元素,正确闭合标签且必须闭合
      </h5>
      <h5>属性和值全部小写，每个属性都必须有一个值，每个值必须加双引号</h5>
      <h5>
        没有值的属性必须使用自己的名称做为值（checked、disabled、readonly、selected等等）
      </h5>
    </div>
    <div class="col-md-6 column" style="flex-grow: 1;border: solid 1px silver">
      <h3>元素的正确使用及嵌套常见错误--初心2017.6.30</h3>
      <h5>a标签不能嵌套a标签button标签不能嵌套表单元素</h5>
      <h5>
        常见的表单元素--input select option textarea label filedset legend
      </h5>
      <h5>del文本删除标签,em强调文本标签,iframe内嵌一个网页,img图像,</h5>
      <h5>
        dd只能以dl为父容器，对应一个dt,dl只能嵌套dt和dd,dt只能以dl为父容器，对应多个dd与ui
        ol li与table,tbody,td,tr,th,tfoot,thead
      </h5>
      <h5>link,script,style都不可嵌套元素</h5>
      <h4>
        select只能嵌套option或optgroup,p不能嵌套块级元素,option仅用于select
      </h4>
    </div>
  </div>
  <div
    class="row clearfix"
    style="display: flex;justify-content: space-between;margin-top: 10px"
  >
    <div
      class="col-md-6 column"
      style="margin-right: 5px;flex-grow: 1;border: solid 1px silver"
    >
      <h3>CSS规范-分类方法</h3>
      <b>CSS文件引用的分类及顺序</b>
      <h5>
        将CSS文件分成“公共型样式”、“特殊型样式”、“皮肤型样式”，并以此顺序引用
      </h5>
      <h5>
        公共型样式：“标签的重置和设置默认值”、“统一调用背景图和清除浮动或其他需统一处理的长样式”、“网站通用布局”、“通用模块和其扩展”、“元件和其扩展”、“功能类样式”、“皮肤类样式”。
      </h5>
      <h5>
        特殊型样式：当某个栏目或页面的样式与网站整体差异较大或者维护率较高时，可以独立引用一个样式：“特殊的布局、模块和元件及扩展”、“特殊的功能、颜色和背景”，也可以是某个大型控件或模块的独立样式
      </h5>
      <h5>
        皮肤型样式：如果产品需要换肤功能，那么我们需要将颜色、背景等抽离出来放在这里
      </h5>
      <h3>HTML属性顺序一次排列</h3>
      <h5>class,id,name,data-*,src,for,type,href,title,alt,aria-*,role</h5>
      <h5>
        布尔型属性可以在声明时不赋值。XHTML 规范要求为其赋值，但是 HTML5
        规范不需要。
      </h5>
      <h5>尽可能的减少多余的父元素</h5>
    </div>
    <div class="col-md-6 column" style="flex-grow: 1;border: solid 1px silver">
      <h3>CSS内部的分类及其顺序</h3>
      <h5>
        重置（reset）和默认（base）（tags）：消除默认样式和浏览器差异，并设置部分标签的初始样式(公共型样式)
      </h5>
      <h5>
        统一调用背景图（这里指多个布局或模块或元件共用的图）和清除浮动（这里指通用性较高的布局、模块、元件内的清除）等统一设置处理的样式(公共型样式)
      </h5>
      <h5>
        布局（grid）（.g-）：将页面分割为几个大块，通常有头部、主体、主栏、侧栏、尾部等(公共型样式)
      </h5>
      <h5>
        模块（module）（.m-）：<strong>通常是一个语义化的可以重复使用的较大的整体！</strong>比如导航、登录、注册、各种列表、评论、搜索等！(公共型样式)
      </h5>
      <h5>
        元件（unit）（.u-）：通常是一个不可再分的较为小巧的个体，通常被重复用于各种模块中！比如按钮、输入框、loading、图标等(公共型样式)
      </h5>
      <h5>
        功能（function）（.f-）：为方便一些常用样式的使用，我们将这些使用率较高的样式剥离出来，按需使用，通常这些选择器具有固定样式表现，比如清除浮动等！不可滥用！
      </h5>
      <h5>
        皮肤（skin）（.s-）：如果你需要把皮肤型的样式抽离出来，通常为文字色、背景色（图）、边框色等，非换肤型网站通常只提取文字色！非换肤型网站不可滥用此类！
      </h5>
      <h5>
        状态（.z-）：为状态类样式加入前缀，统一标识，方便识别，她只能组合使用或作为后代出现（.u-ipt.z-dis{}，.m-list
        li.z-sel{}），具体详见命名规则的扩展相关项
      </h5>
    </div>
  </div>
  <div
    class="row clearfix"
    style="display: flex;justify-content: space-between;margin-top: 10px;min-height: 200px"
  >
    <div
      class="col-md-3 column"
      style="margin-right: 5px;border: solid 1px silver"
    ></div>
    <div
      class="col-md-3 column"
      style="margin-right: 5px;border: solid 1px silver"
    ></div>
    <div class="col-md-6 column" style="border: solid 1px silver"></div>
  </div>
  <div class="row clearfix text-center">
    <h1>js的操作小技巧</h1>
  </div>
  <div
    class="row clearfix"
    style="display: flex;justify-content: space-between;margin-top: 10px"
  >
    <div class="col-md-6" style="margin-right: 5px;border: solid 1px silver">
      <span
        >判断两个数据对比的时候请使用===代替==
        前者不仅会比较数值，还会比较数据的类型</span
      >
      <span
        >清空一个数组使用arrAy.length = 0 而不是arrAy = []
        后者会把先前的数组内容的引用继续保留在内存中，从而导致内存泄露</span
      >
      <span
        >测试一代js代码的性能console.time(label)和console.timeEnd(label)</span
      >
    </div>
    <div class="col-md-6" style="margin-right: 5px;border: solid 1px silver">
      <span
        >判断两个数据对比的时候请使用===代替==
        前者不仅会比较数值，还会比较数据的类型</span
      >
    </div>
  </div>

  <div
    class="row clearfix"
    style="display:flex;justify-content: space-between;margin-top: 10px"
  >
    <div
      class="col-md-6 column"
      style="margin-right: 5px;border: solid 1px silver"
    >
      <h3>判断语句的一般性写法</h3>
      <h5>if(a>0){a=1；}else{a=2;}</h5>
      <h5>if(num=0){a=1}else if(num=1){a=2}else if(num=2){a=3}else{a=0}</h5>
    </div>
    <div
      class="col-md-6 column"
      style="margin-right: 5px;border: solid 1px silver"
    >
      <h3>判断语句的最优写法</h3>
      <h5>三目运算符:</h5>
      <h5>
        表达式b?x:y，如果b的值为true，运算结果为x的值；否则运算结果为y的值,a?b:c?d:e将按a?b:（c?d:e）执行
      </h5>
      <h5>左边单个if else的可以改写为(a>0)?(a=1):(a=2)</h5>
      <h5>js 与或运算符 || && 妙用</h5>
      <h5>
        在js逻辑运算中，0、""、null、false、undefined、NaN都会判为false，其他都为true
      </h5>
      <h5>
        左边多个if else可以改写为:var a = (num==0 && 1) || (num==1 && 2) ||
        (num==2 && 3) || 0;
      </h5>
      <h5>更优写法:var a={'0':1,'1':2,'2'3}[num] || 0</h5>
    </div>
  </div>
  <div class="row clearfix text-center">
    <h1>JS,CSS.HTML注释规范</h1>
  </div>
  <div
    class="row clearfix"
    style="display:flex;justify-content: space-between;margin-top: 10px;min-height: 200px"
  >
    <div
      class="col-md-4 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>JS注释规范</h3>
    </div>
    <div
      class="col-md-4 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>CSS注释规范</h3>
    </div>
    <div
      class="col-md-4 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>HTML注释规范</h3>
    </div>
  </div>
  <div class="row clearfix text-center">
    <h1>编写高效的javascript代码</h1>
  </div>
  <div
    class="row clearfix"
    style="display: flex;justify-content: space-between;margin-top: 10px;min-height: 200px"
  >
    <div
      class="col-md-3 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>JS注释规范</h3>
    </div>
    <div
      class="col-md-3 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>JS注释规范</h3>
    </div>
    <div
      class="col-md-3 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>JS注释规范</h3>
    </div>
    <div
      class="col-md-3 column"
      style="margin-right:5px;border: solid 1px silver"
    >
      <h3>JS注释规范</h3>
    </div>
  </div>
</div>
```
