## HTML基础

### IE9以下兼容

- html中引入script

```htmml
<!--[if lt IE 9]>
  <script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js"></script>
<![endif]-->
```

- CSS中添加

```css
/*html5*/
article,aside,dialog,footer,header,section,nav,figure,menu{display:block}
```



### 常用标签

```html
<div></div>                块元素
<span></span>              内联元素，行内元素
<p></p>                    段落
<q></q>                    短引用，自动加双引号
<blockquote></blockquote>  长引用，缩进自成一段落
<pre></pre>                预格式文本，保留空格和换行，显示代码
<code></code>              显示代码
<i></i>                    文字斜体
<em></em>                  文字斜体
<b></b>                    文字加粗
<strong></strong>          强调文本
<sup></sup>                上标
<sub></sub>                下标
<ins></ins>                下划线
<del></del>                删除线
<br>                       换行
<hr>                       水平线（属性：width;color;align;noshade无阴影）
```




### 语义元素

```html
<aside>	                   定义页面的侧边栏内容。
<bdi>                      允许您设置一段文本，使其脱离其父元素的文本方向设置。
<command>	               定义命令按钮，比如单选按钮、复选框或按钮
<details>                  用于描述文档或文档某个部分的细节
<dialog>	               定义对话框，比如提示框
<summary>	               标签包含 details 元素的标题
<figure>	               规定独立的流内容（图像、图表、照片、代码等等）。
<figcaption>	           定义 <figure> 元素的标题
<footer>	               定义 section 或 document 的页脚。
<header>                   定义了文档的头部区域
<mark>	                   定义带有记号的文本。
<meter>	                   定义度量衡。仅用于已知最大和最小值的度量。
<nav>                      定义导航链接的部分。
<progress>	               定义任何类型的任务的进度。
<ruby>                     定义 ruby 注释（中文注音或字符）。
<rt>	                   定义字符（中文注音或字符）的解释或发音。
<rp>                       在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容。
<section>                  定义文档中的节（section、区段）。
<time>                     定义日期或时间。
<wbr>                      规定在文本中的何处适合添加换行符。
```



### 引入图片

```html
<img src=" " alt=" " />
```



### a链接

```
<a href=" " title=" ">文字</a>
```

- 去掉下划线：text-decoration:none;
- target属性：
  - _self	默认当前窗口打开
  - _blank	新窗口打开

- 锚标签：

  - 同一页面：

    ```html
    <a href="#锚名">目录</a>
    ```

  - 不同页面：

    ```html
    <a href="网页名称#锚名">目录</a>
    ```

- 电子邮件：

  ```html
  <a href="mailto:邮件地址">...</a>
  ```

- 下载链接：

  ```html
  <a href="文件地址">...</a>
  ```



## 列表

### 标签

- 有序列表：

  ```html
  <ol type="行内样式">
      <li>type属性为1：数字列表</li>
      <li>type属性为a：小写字母列表</li>
      <li>type属性为A：大写字母列表</li>
      <li>type属性为i：小写罗马数字列表</li>
      <li>type属性为I：大写罗马数字列表</li>
  </ol>
  ```

- 无序列表

  ```html
  <ul type="行内样式">
      <li>type属性为"disc":实心圆图标列表</li>
      <li>type属性为"circle":空心圆图标列表</li>
      <li>type属性为"square":正方形图标列表</li>
      <li>type属性为"none":无图标列表</li>
  </ul>
  ```

- 自定义列表

  ```html
  <dl>
      <dt>一级</dt>
      	<dd>二级</dd>
      	<dd>二级</dd>
      <dt>一级</dt>
      	<dd>二级</dd>
      	<dd>二级</dd>
      	<dd>二级</dd>
  </dl>
  ```

### 外部样式：list-style

- list-style-type 列表项标志类型

  - 有序列表
    - decimal 从1开始的整数
    - lower-alpha 小写英文字母
    - upper-alpha 大写英文字母
    - lower_roman 小写罗马数字
    - upper-roman 大写罗马数字

  - 无序列表
    - disc 实心圆点
    - circle 空心圆点
    - square 实心方块
    - none 无图标

- list-type-image 将图像设为列表项标志
- list-style-position 列表项标记的位置
  - inside 多行文本环绕图标
  - outside 多行文本不环绕图标（默认）

```css
list-style 缩写：无顺序，空格隔开，image会覆盖type
```



## 表格

```html
<table>
    <caption>标题</caption>
    <thead>
        <tr>
            <th>表头</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>主体</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>脚注</td>
        </tr>
    </tfoot>
</table>
```

### 行内样式

1. `<table>`属性：

- width表格宽度
- height表格高度
- align表格相对周围元素的对齐方式
- border表格边框的宽度
- bgcolor表格背景颜色
- cellpadding单元边沿与其内容之间的距离
- cellspacing单元格之间的距离
- frame规定外侧边框的哪个部分是可见的
  - vold不显示
  - above显示上部
  - below显示下部
  - hsides显示上下部
  - vsides显示左右
  - lhs左边
  - rhs右边
  - box四个边

- rules规定内侧边框的哪个部分是可见的
  - groups位于行组和列组之间的线条
  - rows位于行之间的线条
  - cols位于列之间的线条
  - all位于行和列之间的线条

2. `<tr><th><td>`属性：

- align行/单元格内容水平对齐
  - left/right/center/justify/char
- valign行/单元格内容垂直对齐
  - top/middle/bottom/baseline
- bgcolor背景颜色
- colspan合并列
- rowspan合并行

### 外部样式

- border-spacing单元格之间的距离
- border-collapse:collapse;折叠两个边框为一个



## 表单