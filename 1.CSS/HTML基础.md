# HTML基础

## H5

### <!DOCTYPE html>

- 写在第一行<html>之外

### <meta charset="utf-8">

- 写在<head>中

## IE9以下兼容

### JS

- <!--[if lt IE 9]>
    <script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js"></script>
<![endif]-->

### CSS

- /*html5*/
article,aside,dialog,footer,header,section,nav,figure,menu{display:block}

## 常用标签

### <div></div>块元素
<span></span>内联元素，行内元素
<p></p>段落
<q></q>短引用，自动加双引号
<blockquote></blockquote>长引用，缩进自成一段落
<pre></pre>预格式文本，保留空格和换行，显示代码
<code></code>显示代码
<i></i>文字斜体
<em></em>文字斜体
<b></b>文字加粗
<strong></strong>强调文本
<sup></sup>上标
<sub></sub>下标
<ins></ins>下划线
<del></del>删除线
<br>换行
<hr>水平线（属性：width;color;align;noshade无阴影）

## 语义元素

### <article>	定义页面独立的内容区域。
<aside>	定义页面的侧边栏内容。
<bdi> 允许您设置一段文本，使其脱离其父元素的文本方向设置。
<command>	定义命令按钮，比如单选按钮、复选框或按钮
<details>用于描述文档或文档某个部分的细节
<dialog>	定义对话框，比如提示框
<summary>	标签包含 details 元素的标题
<figure>	规定独立的流内容（图像、图表、照片、代码等等）。
<figcaption>	定义 <figure> 元素的标题
<footer>	定义 section 或 document 的页脚。
<header>定义了文档的头部区域
<mark>	定义带有记号的文本。
<meter>	定义度量衡。仅用于已知最大和最小值的度量。
<nav>定义导航链接的部分。
<progress>	定义任何类型的任务的进度。
<ruby>定义 ruby 注释（中文注音或字符）。
<rt>	 定义字符（中文注音或字符）的解释或发音。
<rp> 在 ruby 注释中使用，定义不支持 ruby 元素的浏览器所显示的内容。
<section>定义文档中的节（section、区段）。
<time> 定义日期或时间。
<wbr>规定在文本中的何处适合添加换行符。

## 图片<img src="#" alt=""/>

### height高

### width宽

## 链接<a href="#" title="">内容</a>

### target

- _self默认当前窗口
- _blank新窗口
- _top
- _parent

### 锚标签

- 同一页面：<a href="#锚名">目录</a>
不同页面：<a href="网页名称#锚名">目录</a>
- <a href="..." name="锚名">内容</a>
PS:不一定有内容，如<a name="锚名"></a>

### 电子邮件链接：<a href="mailto:邮件地址">...</a>

### 下载链接：<a href="文件地址">...</a>

### 去掉下划线：text-decoration:none;

## 特殊符号

### &lt;小于号或显示标记

### &gt;大于号或显示标记

### &reg;已注册

### &copy;版权

### &trade;商标

### &nbsp;不断行的空白

*XMind: ZEN - Trial Version*