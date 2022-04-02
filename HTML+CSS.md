# 「学习笔记」HTML基础



## 一、认识WEB

**「网页」**主要是由`文字`、`图像`和`超链接`等元素构成，当然除了这些元素，网页中还可以包括音频、视频以及Flash等。

**「浏览器」**是网页显示、运行的平台。

**「浏览器内核」**(排版引擎、解释引擎、渲染引擎)

> 负责读取网页内容，整理讯息，计算网页的显示方式并显示页面。

| 浏览器  |      内核      | 备注                                                         |
| :------ | :------------: | :----------------------------------------------------------- |
| IE      |    Trident     | IE、猎豹安全、360极速浏览器、百度浏览器                      |
| firefox |     Gecko      | 可惜这几年已经没落了，打开速度慢、升级频繁、猪一样的队友flash、神一样的对手chrome。 |
| Safari  |     webkit     | 现在很多人错误地把 webkit 叫做 chrome内核（即使 chrome内核已经是 blink 了）。苹果感觉像被别人抢了媳妇，都哭晕在厕所里面了。 |
| chrome  | Chromium/Blink | 在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。Blink 其实是 WebKit 的分支。大部分国产浏览器最新版都采用Blink内核。二次开发 |
| Opera   |     blink      | 现在跟随chrome用blink内核。                                  |

### Web标准

**「构成」**👉 **结构标准，表现标准和行为标准**

- 结构标准用于对网页元素进行整理和分类(HTML)
- 表现标准用于设置网页元素的版式、颜色、大小等外观属性(CSS)
- 行为标准用于对网页模型的定义及交互的编写(JavaScript)

**「Web标准的优点」**👇

- 易于维护：只需更改CSS文件，就可以改变整站的样式
- 页面响应快：HTML文档体积变小，响应时间短
- 可访问性：语义化的HTML（结构和表现相分离的HTML）编写的网页文件，更容易被屏幕阅读器识别
- 设备兼容性：不同的样式表可以让网页在不同的设备上呈现不同的样式
- 搜索引擎：语义化的HTML能更容易被搜索引擎解析，提升排名



------

## 二、HTML初识

### HTML初识

**「HTML」**(Hyper Text Markup Language):超文本标记语言

**「所谓超文本，有2层含义：」**

- 因为它可以加入图片、声音、动画、多媒体等内容（超越文本限制 ）
- 不仅如此，它还可以从一个文件跳转到另一个文件，与世界各地主机的文件连接（超级链接文本）。

**「HTML骨架格式」**

```
<!-- 页面中最大的标签 根标签 -->
<html>
    <!-- 头部标签 -->
    <head>     
        <!-- 标题标签 -->
        <title></title> 
    </head>
    <!-- 文档的主体 -->
    <body>
    </body>
</html>
```

**「团队约定大小写」**

- HTML标签名、类名、标签属性和大部分属性值统一用小写

**「HTML元素标签分类」**

- 常规元素(双标签)
- 空元素(单标签)

```
  常规元素(双标签)
  <标签名> 内容 </标签名>   比如<body>我是文字</body>

  空元素(单标签)
  <标签名 />  比如 <br />或<br>
```

**「HTML标签关系」**

- 嵌套关系父子级包含关系
- 并列关系兄弟级并列关系
- 如果两个标签之间的关系是嵌套关系，子元素最好缩进一个tab键的身位（一个tab是4个空格）。如果是并列关系，最好上下对齐。

### 文档类型<!DOCTYPE >

**「文档类型」**用来说明你用的XHTML或者HTML是什么版本。<!DOCTYPE html>告诉浏览器按照HTML5标准解析页面。

### 页面语言lang

lang指定该html标签内容所用的语言

```
  <html lang="en">  
  en 定义语言为英语 zh-CN定义语言为中文
```

**「lang的作用」**

- 根据根据lang属性来设定不同语言的css样式，或者字体
- 告诉搜索引擎做精确的识别
- 让语法检查程序做语言识别
- 帮助翻译工具做识别
- 帮助网页阅读程序做识别

### 字符集

**「字符集」**(Character set)是多个字符的集合,计算机要准确的处理各种字符集文字，需要进行字符编码，以便计算机能够识别和存储各种文字。

- UTF-8是目前最常用的字符集编码方式
- 让 html 文件是以 UTF-8 编码保存的， 浏览器根据编码去解码对应的html内容。

```
  <meta charset="UTF-8" />
```

**「meta viewport的用法」**
  通常viewport是指视窗、视口。浏览器上(也可能是一个app中的webview)用来显示网页的那部分区域。在移动端和pc端视口是不同的，pc端的视口是浏览器窗口区域，而在移动端有三个不同的视口概念：布局视口、视觉视口、理想视口

  meta有两个属性name 和 http-equiv

**name属性的取值**

- keywords(关键字) 告诉搜索引擎，该网页的关键字
- description(网站内容描述) 用于告诉搜索引擎，你网站的主要内容。
- viewport(移动端的窗口)
- robots(定义搜索引擎爬虫的索引方式) robots用来告诉爬虫哪些页面需要索引，哪些页面不需要索引
- author(作者)
- generator(网页制作软件）
- copyright(版权)

**http-equiv有以下参数**

http-equiv相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容

- content-Type 设定网页字符集(Html4用法，不推荐)
- Expires(期限) ,可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。
- Pragma(cache模式),是用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出
- Refresh(刷新),自动刷新并指向新页面。
- cache-control（请求和响应遵循的缓存机制）

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### HTML标签的语义化

- 方便代码的阅读和维护，样式丢失的时候能让页面呈现清晰的结构。
- 有利于SEO，搜索引擎根据标签来确定上下文和各个关键字的权重。
- 方便其他设备解析，如盲人阅读器根据语义渲染网页

**「拓展」** 标签：规定页面上所有链接的默认 URL 和设置整体链接的打开状态

```
<head>
    <base href="http://www.baidu.com" target="_blank">
    <base target="_self">
</head>
<body>
    <a href="">测试</a> 跳转到 百度
</body>
```



------

## HTML常用标签

### 常用标签

**「1. 排版标签」**主要和css搭配使用，显示网页结构的标签，是网页布局最常用的标签。

- 标题标签h(h1~h6)
- 段落标签p,可以把 HTML 文档分割为若干段落
- 水平线标签hr
- 换行标签br
- div和span标签:是没有语义的,是我们网页布局最主要的2个盒子。

**「2. 排版标签」**

- b和strong 文字以粗体显示
- i和em 文字以斜体显示
- s和del 文字以加删除线显示
- u和ins 文字以加下划线显示

**「3. 标签属性(行内式)」**

使用HTML制作网页时，如果想让HTML标签提供更多的信息，可以使用HTML标签的属性加以设置。

```
<标签名 属性1="属性值1" 属性2="属性值2" …> 内容 </标签名>
<手机 颜色="红色" 大小="5寸">  </手机>
```

**「4. 图像标签img」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**注意：**

- 标签可以拥有多个属性，必须写在开始标签中，位于标签名后面。
- 属性之间不分先后顺序，标签名与属性、属性与属性之间均以空格分开。
- 采取  键值对 的格式  key="value"  的格式

```
<img src="cz.jpg" width="300" height="300" border="3" title="这是个小蒲公英" />
```

**「5. 链接标签(重点)」**

```
<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
target="_self"  默认窗口弹出方式
target="_blank" 新窗口弹出
```

| 属性   | 作用                                                         |
| :----- | :----------------------------------------------------------- |
| href   | 用于指定链接目标的url地址，（必须属性）当为标签应用href属性时，它就具有了超链接的功能 |
| target | 用于指定链接页面的打开方式，其取值有_self和_blank两种，其中_self为默认值，_blank为在新窗口中打开方式。 |

**src 和 href 的区别**

一句话概括:**src 是引入资源的 href 是跳转url的**

1. src用于替换当前元素，href用于在当前文档和引用资源之间确立联系。
2. src是source的缩写，指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求src资源时会将其指向的资源下载并应用到文档内，例如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。
3. href是Hypertext Reference的缩写，指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接。如果我们在文档中添加那么浏览器会识别该文档为css文件，就会并行下载资源并且不会停止对当前文档的处理。这也是为什么建议使用link方式来加载css，而不是使用@import方式。

**注意：**

1. 外部链接 需要添加 http:// www.baidu.com
2. 内部链接 直接链接内部页面名称即可 比如 < a href="index.html"> 首页
3. 如果当时没有确定链接目标时，通常将链接标签的href属性值定义为“#”(即href="#")，表示该链接暂时为一个空链接。
4. 不仅可以创建文本超链接，在网页中各种网页元素，如图像、表格、音频、视频等都可以添加超链接。

**锚点定位：通过创建锚点链接，用户能够快速定位到目标内容。**

```
1. 使用相应的id名标注跳转目标的位置。 (找目标)
  <h3 id="two">第2集</h3> 

2. 使用<a href="#id名">链接文本</a>创建链接文本（被点击的） 
  <a href="#two">   
```

**「6. 注释标签」**

```
 <!-- 注释语句 -->     
  快捷键是：    ctrl + /       
  或者 ctrl +shift + / 
```

**团队约定：**注释内容前后各一个空格字符，注释位于要注释代码的上面，单独占一行

**「7. 路径」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「8. 其他知识」**

预格式化文本pre标签元素中的文本通常会保留空格和换行符。而文本也会呈现为等宽字体。格式化文本就是 ，按照我们预先写好的文字格式来显示页面， 保留空格和换行等。

特殊字符![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)什么是XHTML

- XHTML 指**「可扩展超文本标签语言」**（EXtensible HyperText Markup Language）。
- XHTML 的目标是取代 HTML。
- XHTML 与 HTML 4.01 几乎是相同的。
- XHTML 是更严格更纯净的 HTML 版本。
- XHTML 是作为一种 XML 应用被重新定义的 HTML,是严格版本的HTML。例如它要求标签必须小写，标签必须被正确关闭，标签顺序必须正确排列，对于属性都必须使用双引号等。
- XHTML 是一个 W3C 标准。



**写HTML代码时应注意什么？**

- 尽可能少的使用无语义的标签div和span；
- 在语义不明显时，既可以使用div或者p时，尽量用p, 因为p在默认情况下有上下间距，对兼容特殊终端有利；
- 不要使用纯样式标签，如：b、font、u等，改用css设置。
- 需要强调的文本，可以包含在strong或者em标签中（浏览器预设样式，能用CSS指定就不用他们），strong默认样式是加粗（不要用b），em是斜体（不用i）；
- 使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。表头和一般单元格要区分开，表头用th，单元格用td；
- 表单域要用fieldset标签包起来，并用legend标签说明表单的用途；
- 每个input标签对应的说明文本都需要使用label标签，并且通过为input设置id属性，在lable标签中设置for来让说明文本和相对应的input关联起来。

------

## 表格

**「1. 表格」**

现在还是较为常用的一种标签，但不是用来布局，常见显示、展示表格式数据。因为它可以让数据显示的非常的规整，可读性非常好。特别是后台展示数据的时候表格运用是否熟练就显得很重要，一个清爽简约的表格能够把繁杂的数据表现得很有条理。

**「2. 创建表格」**

```
<table>
  <tr>
    <td>单元格内的文字</td>
    ...
  </tr>
  ...
</table>
```

table、tr、td，他们是创建表格的基本标签，缺一不可

- table用于定义一个表格标签。
- tr标签 用于定义表格中的行，必须嵌套在 table标签中。
- td 用于定义表格中的单元格，必须嵌套在<tr></tr>标签中。
- 字母 td 指表格数据（table data），即数据单元格的内容，现在我们明白，表格最合适的地方就是用来存储数据的。td像一个容器，可以容纳所有的元素。![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**表头单元格标签th**:一般表头单元格位于表格的第一行或第一列，并且文本加粗居中,只需用表头标签<th></th>替代相应的单元格标签<td></td>即可。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**表格标题caption**通常这个标题会被居中且显示于表格之上。caption 标签必须紧随 table 标签之后。这个标签只存在 表格里面才有意义。你是风儿我是沙

```
<table>
   <caption>我是表格标题</caption>
</table>
```

**「3. 表格属性」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)三参为0，平时开发的我们这三个参数   border  cellpadding  cellspacing 为  0

**「4. 合并单元格」**,合并的顺序我们按照  先上 后下   先左  后右 的顺序 ,合并完之后需要删除多余的单元格。

- 跨行合并：rowspan="合并单元格的个数"
- 跨列合并：colspan="合并单元格的个数"

**「5. 总结表格」**

| 标签名              | 定义           | 说明                                         |
| :------------------ | :------------- | :------------------------------------------- |
| <table></table>     | 表格标签       | 就是一个四方的盒子                           |
| <tr></tr>           | 表格行标签     | 行标签要再table标签内部才有意义              |
| <td></td>           | 单元格标签     | 单元格标签是个容器级元素，可以放任何东西     |
| <th></th>           | 表头单元格标签 | 它还是一个单元格，但是里面的文字会居中且加粗 |
| <caption></caption> | 表格标题标签   | 表格的标题，跟着表格一起走，和表格居中对齐   |
| clospan 和 rowspan  | 合并属性       | 用来合并单元格的                             |

**「6. 表格划分结构」**

  对于比较复杂的表格，表格的结构也就相对的复杂了，所以又将表格分割成三个部分：题头、正文和脚注。而这三部分分别用:thead,tbody,tfoot来标注， 这样更好的分清表格结构。

**注意：**
1.<thead></thead>：用于定义表格的头部。用来放标题之类的东西。<thead> 内部必须拥有<tr> 标签！
\2. <tbody></tbody>：用于定义表格的主体。放数据本体 。
\3. <tfoot></tfoot>放表格的脚注之类。
\4. 以上标签都是放到table标签中。



------

## 列表

**「列表ul」**容器里面装载着结构，样式一致的文字或图表的一种形式，叫列表。

列表最大的特点就是整齐 、整洁、 有序，跟表格类似，但是它可组合自由度会更高。

**「1. 无序列表 ul」**

- <ul></ul>中只能嵌套<li></li>，直接在<ul></ul>标签中输入其他标签或者文字的做法是不被允许的。
- <li>与</li>之间相当于一个容器，可以容纳所有元素。

```
<ul>
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ......
</ul>
```

**「2. 有序列表 ol」**

- <ol>标签中的type属性值为排序的序列号，不添加type属性时，有序列表默认从数字1开始排序。
- 常用的type属性值分别为是1，a，A，i，I
- <ol reversed="reversed">中的reversed属性能够让有序列表中的序列倒序排列。
- <ol start="3">中的start属性值为3，有序列表中的第一个序列号将从3开始排列。

```
<ol type="A"> 
  <li>列表项1</li>
  <li>列表二</li>
  <li>列表三</li>
</ol>
```

**「2. 自定义列表 dl」**

- 定义列表常用于对术语或名词进行解释和描述，定义列表的列表项前没有任何项目符号。

```
<dl>
  <dt>名词1</dt>
  <dd>名词1解释1</dd>
  <dd>名词1解释2</dd>
  ...
  <dt>名词2</dt>
  <dd>名词2解释1</dd>
  <dd>名词2解释2</dd>
  ...
</dl>
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)



------

## 表单

在HTML中，一个完整的表单通常由表单控件（也称为表单元素）、提示信息和表单域3个部分构成。表单目的是为了收集用户信息。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**表单控件：**
 包含了具体的表单功能项，如单行文本输入框、密码输入框、复选框、提交按钮、重置按钮等。
**提示信息：**
 一个表单中通常还需要包含一些说明性的文字，提示用户进行填写和操作。
**表单域：** 
 它相当于一个容器，用来容纳所有的表单控件和提示信息，可以通过他定义处理表单数据所用程序的url地址，以及数据提交到服务器的方法。如果不定义表单域，表单中的数据就无法传送到后台服务器。

**「1. input 控件」**

```
<input type="属性值" value="你好">
```

- input 输入的意思
- <input />标签为单标签
- type属性设置不同的属性值用来指定不同的控件类型
- 除了type属性还有别的属性

**常用属性：**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
用户名: <input type="text" /> 
密  码：<input type="password" />
```

**value属性**

- value 默认的文本值。有些表单想刚打开页面就默认显示几个文字，就可以通过这个value 来设置。

```
用户名:<input type="text"  name="username" value="请输入用户名"> 
```

**name属性**

- name表单的名字， 这样，后台可以通过这个name属性找到这个表单。 页面中的表单很多，name主要作用就是用于区别不同的表单。

- - name属性后面的值，是我们自己定义的。
  - radio  如果是一组，我们必须给他们命名相同的名字 name  这样就可以多个选其中的一个啦
  - name属性，我们现在用的较少，但是，当我们学ajax 和后台的时候，是必须的。

```
<input type="radio" name="sex"  />男
<input type="radio" name="sex" />女
```

**checked属性**

- 表示默认选中状态。 较常见于 单选按钮和复选按钮。

```
性    别:
<input type="radio" name="sex" value="男" checked="checked" />男
<input type="radio" name="sex" value="女" />女 
```

**input 属性小结**

| 属性    | 说明     | 作用                                                   |
| :------ | :------- | :----------------------------------------------------- |
| type    | 表单类型 | 用来指定不同的控件类型                                 |
| value   | 表单值   | 表单里面默认显示的文本                                 |
| name    | 表单名字 | 页面中的表单很多，name主要作用就是用于区别不同的表单。 |
| checked | 默认选中 | 表示那个单选或者复选按钮一开始就被选中了               |

**「2.  label标签」**

- label 标签为 input 元素定义标注（标签）。
- label标签主要目的是为了提高用户体验。为用户提高最优秀的服务。

**作用：**用于绑定一个表单元素, 当点击label标签的时候, 被绑定的表单元素就会获得输入焦点。

**如何绑定元素呢**

- 第一种用法就是用label标签直接包含input表单， 适合单个表单选择
- 第二种用法 for 属性规定 label 与哪个表单元素绑定(通过id)。

```
  第一种
  <label> 用户名： 
    <input type="radio" name="usename" value="请输入用户名">   
  </label>
  
  第二种
  <label for="sex">男</label>
  <input type="radio" name="sex"  id="sex">
```

**「3.  textarea控件(文本域)」**

- 通过textarea控件可以轻松地创建多行文本输入框.
- cols="每行中的字符数" rows="显示的行数"  我们实际开发不用

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
  <textarea >
    文本内容
  </textarea>
```

**文本框和文本域区别**

| 表单              |  名称  |       区别       |                  默认值显示 |             用于场景 |
| :---------------- | :----: | :--------------: | --------------------------: | -------------------: |
| input type="text" | 文本框 | 只能显示一行文本 | 单标签，通过value显示默认值 | 用户名、昵称、密码等 |
| textarea          | 文本域 | 可以显示多行文本 |  双标签，默认值写到标签中间 |               留言板 |

**「4.  select下拉列表」**

- 如果有多个选项让用户选择，为了节约空间，我们可以使用select控件定义下拉列表。
- 在option 中定义selected =" selected "时，当前项即为默认选中项。
- 我们实际开发会用的比较少

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
<select>
  
  <option>选项1</option>
  <option>选项2</option>
  <option>选项3</option>
  ...
</select>
```

### form表单域

- 收集的用户信息怎么传递给服务器？

- - 通过form表单域

- 目的：

- - 在HTML中，form标签被用于定义表单域，以实现用户信息的收集和传递，form中的所有内容都会被提交给服务器。

```
<form action="url地址" method="提交方式" name="表单名称">
  各种表单控件
</form>
```

**常用属性：**

- 每个表单都应该有自己表单域。后面学 ajax 后台交互的时候，必须需要form表单域。

| 属性   | 属性值   | 作用                                               |
| :----- | :------- | :------------------------------------------------- |
| action | url地址  | 用于指定接收并处理表单数据的服务器程序的url地址。  |
| method | get/post | 用于设置表单数据的提交方式，其取值为get或post。    |
| name   | 名称     | 用于指定表单的名称，以区分同一个页面中的多个表单。 |

**GET 和 POST 的区别**

- GET在浏览器回退时是无害的，而POST会再次提交请求。
- GET请求会被浏览器主动cache，而POST不会，除非手动设置。
- GET请求只能进行url编码，而POST支持多种编码方式。
- GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
- GET请求大小一般是(1024字节)，http协议并没有限制，而与服务器，操作系统有关，POST理论上来说没有大小限制，http协议规范也没有进行大小限制，但实际上post所能传递的数据量根据取决于服务器的设置和内存大小。
- 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
- GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。

**团队约定：**

- 元素属性值使用双引号语法
- 元素属性值可以写上的都写上

```
推荐
<input type="text" /> 
<input type="radio" name="name" checked="checked" />
```



------

## 从输入url到页面展示发生了什么(面试)

> 作者：Twinkle_
> 链接：https://juejin.im/post/6869279683230629896
> 来源：掘金

### **浏览器的多进程架构**

从浏览器输入 URL 到页面渲染的整个过程都是由 浏览器架构中的各个进程之间的配合完成。

1. 浏览器主进程: 管理子进程、提供服务功能
2. 渲染进程：将HTML、CSS、JS渲染成界面，js引擎v8和排版引擎Blink就在上面，他会为每一个tab页面创建一个渲染进程
3. GPU进程：本来是负责处理3Dcss的，后来慢慢的UI界面也交给GPU来绘制
4. 网络进程：就是负责网络请求，网络资源加载的进程
5. 插件进程：负责插件的运行的，因为插件很容易崩溃，把它放到独立的进程里不要让它影响别人

**浏览器的多进程架构**

从用户输入信息到页面展示的不同阶段，是不同的进程在发挥作用，示意图如下：![图片](https://mmbiz.qpic.cn/mmbiz/y7EkeCWAzmrC7zFuibKPfkDKFUfyH6Iibve8jRDxSGUqRqh8bLPOC9QicJEzXxIiaKqMp3IiaHxMY7UEc7Z3ZTBicWWA/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)从图中可以看出，整个过程是需要各个进程之间相互配合完成的，过程大致可以描述为：

1. 用户输入url,处理输入信息，主进程开始导航，交给网络进程干活
2. 网络进程发起网络请求，其中有可能会发生重定向
3. 服务器响应URL之后，主进程就要通知渲染进程，你要开始干活了
4. 渲染进程准备好了，要想渲染进程提交数据，这个时间叫做提交文档
5. 渲染进程接受到数据，完成页面渲染。

**具体过程**

1. 输入url

用户输入url，处理输入信息：如果为非url结构的字符串，交给浏览器默认引擎去搜索改字符串；若为url结构的字符串，浏览器主进程会交给 网络进程 ,开始干活。2.1 查找浏览器缓存网络进程会先看看是否存在本地缓存，如果有就直接返回资源给浏览器进程，无则下一步 DNS-> IP -> TCP2.2 DNS解析网络进程拿到url后，先会进行DNS域名解析得到IP地址。如果请求协议是HTTPS，那么还需要建立TLS连接。2.2 建立TCP连接，三次握手接下来就是利用IP地址和服务器建立TCP连接。连接建立之后，向服务器发送请求。
服务器响应服务器收到请求信息后，会根据请求信息生成响应行、响应头、响应体，并发给网络进程。网络进程接受了响应信息之后，就开始解析响应头的内容。网络进程解析响应行和响应头信息的过程：3.1 重定向如果响应行状态码为301（永久重定向）和302（临时），那么说明需要重定向到其他url。这时候网络进程会从响应头中的Location字段里读取重定向的地址，并重新发起网络请求。3.2 响应数据处理导航会通过请求头的Content-type字段判断响应体数据的类型。浏览器通过这个来决定如何显示响应体的内容。比如：若为application/octet-stream，则会按照下载类型来处理这个请求，导航结束。若为text/html，这就告诉浏览器服务器返回的是html格式，浏览器会通知渲染进程，你要干活了。准备渲染进程默认情况，每个页面一个渲染进程。但若处于同一站点（同根域名+协议），那么渲染进程就会复用。提交文档渲染进程准备好后，浏览器进程发出“提交文档的消息”，渲染进程接受了消息之后，会跟网络进程简历传输数据的管道。等数据传输完成了，渲染进程会告诉浏览器进程，确认文档提交，这时候浏览器会更新页面，安全状态，url，前进后退的历史。到这里导航结束，进入渲染阶段。
注：当浏览器刚开始加载一个地址之后，标签页上的图标便进入了加载状态。但此时图中页面显示的依然是之前打开的页面内容，并没立即替换为百度首页的页面。因为需要等待提交文档阶段，页面内容才会被替换。前端HTML基础面试题iframe有哪些缺点？iframe是一种框架，也是一种很常见的网页嵌入方式。**「iframe的优点」**iframe能够原封不动的把嵌入的网页展现出来。如果有多个网页引用iframe，那么你只需要修改iframe的内容，就可以实现调用的每一个页面内容的更改，方便快捷。网页如果为了统一风格，头部和版本都是一样的，就可以写成一个页面，用iframe来嵌套，可以增加代码的可重用。如果遇到加载缓慢的第三方内容如图标和广告，这些问题可以由iframe来解决。**「iframe的缺点」**会产生很多页面，不容易管理。iframe框架结构有时会让人感到迷惑，如果框架个数多的话，可能会出现上下、左右滚动条，会分散访问者的注意力，用户体验度差。代码复杂，无法被一些搜索引擎索引到，这一点很关键，现在的搜索引擎爬虫还不能很好的处理iframe中的内容，所以使用iframe会不利于搜索引擎优化。很多的移动设备（PDA 手机）无法完全显示框架，设备兼容性差。iframe框架页面会增加服务器的http请求，对于大型网站是不可取的。现在基本上都是用Ajax来代替iframe，所以iframe已经渐渐的退出了前端开发。label的作用是什么？是怎么用的？例子1: 点击" 用户名:" 就可以定位光标到输入框`<form><label for="myid "> 用户名:</label><input type="text" id="myid" /></form> `例子2: 点击" 用户名:" 或按键alt+1, 都可以定位光标到输入框`<form>  <label for="myid" accesskey="1"> 用户名:</label>  <input type="text" id="myid" tabindex="1" /></form> `**for 属性**功能：表示Label 标签要绑定的HTML 元素，你点击这个标签的时候，所绑定的元素将获取焦点。**acesskey 属性**
功能：表示访问Label 标签所绑定的元素的热键，当您按下热键，所绑定的元素将获取焦点。
局限性：accessKey 属性所设置的快捷键不能与浏览器的快捷键冲突，否则将优先激活浏览器的快捷键。HTML5的form如何关闭自动完成功能？  HTML的输入框可以拥有自动完成的功能，当你往输入框输入内容的时候，浏览器会从你以前的同名输入框的历史记录中查找出类似的内容并列在输入框下面，这样就不用全部输入进去了，直接选择列表中的项目就可以了。
  但有时候我们希望关闭输入框的自动完成功能，例如当用户输入内容的时候，我们希望使用AJAX技术从数据库搜索并列举而不是在用户的历史记录中搜索。**关闭输入框的自动完成功能有3种方法：**在IE的Internet选项菜单里的内容--自动完成里面设置设置form的autocomplete为"on"或者"off"来开启或者关闭自动完成功能设置输入框的autocomplete为"on"或者"off"来开启或者关闭该输入框的自动完成功能将 HTML5 看作成开放的网络平台**「什么是 HTML5 的基本构件（building block）？」**语义 - 提供更准确地描述内容。连接 - 提供新的方式与服务器通信。离线和存储 - 允许网页在本地存储数据并有效地离线运行。多媒体 - 在 Open Web 中，视频和音频被视为一等公民（first-class citizens）。2D/3D 图形和特效 - 提供更多种演示选项。性能和集成 - 提供更快的访问速度和性能更好的计算机硬件。设备访问 - 允许使用各种输入、输出设备。外观 - 可以开发丰富的主题。浏览器是怎么对HTML5的离线储存资源进行管理和加载的呢？  在浏览器的html头部加上manifest属性，如果是第一次访问浏览器会根据manifest的内容进行下载存储离线内容，如果已经访问过则从离线存储中进行加载，然后在比对服务器如果有新内容在更新离线存储
  离线的情况下，浏览器就直接使用离线存储的资源。浏览器的渲染过程？`1、将获取的html解析成dom树2、处理css，构成层叠样式表模型CSSOM3、将dom树和CSSOM合并为渲染树4、根据CSSOM将渲染树的节点布局计算5、将渲染树节点样式绘制到页面上 // 注意在渲染的过程中是自上而下渲染，js会阻塞页面的渲染，优先等js执行完成如果在渲染的过程中改变了样式，会造成回流需要重新渲染`link和@import的区别？`1、从属关系区别：link属于html标签，而@import是css提供的。2、加载顺序区别：页面被加载时，link会同时被加载，而@import引用的css会等到页面被加载完再加载。3、兼容性区别：import只在IE5以上才能识别，而link是html标签，无兼容问题。4、dom可操作性区别：可以通过JS 操作 DOM ，插入link标签来改变样式；由于 DOM 方法是基于文档的，无法使用@import的方式插入样式5、权重区别：如果已经存在相同样式，@import引入的这个样式将被该 CSS 文件本身的样式层叠掉，表现出link方式的样式权重高于@import的权重这样的直观效果。（简而言之，link和@import，谁写在后面，谁的样式就被应用，后面的样式覆盖前面的样式。） `src与href的区别？`1、href 是指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。2、src是指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求src资源时会将其指向的资源下载并应用到文档内，例如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。`❤️ 感谢大家









# 「学习笔记」CSS基础

原创 饭老板 [前端fan](javascript:void(0);) *2020-09-14*

收录于话题

\#前端入门4

\#CSS基础2

![图片](https://mmbiz.qpic.cn/mmbiz_png/y7EkeCWAzmqtcdL7HZYccBic0jicaWzR8bbR15tNSZ1yJyAEDlN79yVia3G1a50u7S6uToLgN9VCQiaoXYO2xXGFbA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**「学习笔记」CSS基础**

## 前言

拖延了一周的CSS学习笔记终于利用周末去补齐了，本篇文章着重梳理之前所学的CSS知识点，查漏补缺。同时，试着用git将重点案例存放到远程仓库中，更近一步贴近公司流程。💪💪

## CSS构造块

**「1. HTML的局限性」**

- HTML满足不了设计者的需求，可以将网页结构与样式相分离，这样就可以在不更改网页结构的前提下，更换网站的样式。
- 操作html属性不方便
- HTML里面添加样式带来的是无尽的臃肿和繁琐

**「2. CSS网页的美容师」**

- 让我们的网页更加丰富多彩，布局更加灵活自如。
- CSS最大的贡献：让HTML从样式中脱离，实现了HTML专注去做结构呈现，样式交给CSS

**「3. CSS」**CSS(Cascading Style Sheets)通常称为CSS样式表或层叠样式表(级联样式表)。

- **作用**

- - 主要用于设置HTML页面中的文本内容(字体、大小、对齐方式等)\图片的外形(宽高、边框样式、边距等)以及版面的布局和外观显示样式。
  - CSS以HTML为基础，提供了丰富的功能，如字体、样式、背景的控制及整体排版等，而且可以针对不同的浏览器设置不同的样式。

**「4. CSS注释」**

```
/* 这是注释 */
```

### 引入CSS样式表

**「1.行内式(内联样式)」**

通过标签的style属性来设置元素的样式

- style其实就是标签的属性
- 样式属性和值中间是:
- 多组属性值直接用;隔开
- 只能控制当前的标签和以及嵌套在其中的字标签，造成代码冗余。
- **缺点:**没有实现样式和结构相分离。

```
<标签名 style="属性1:属性值1; 属性2:属性值2; 属性3:属性值3;"> 内容 </标签名>
例如：
<div style="color: red; font-size: 12px;">青春不常在，抓紧谈恋爱</div>
```

**「2.内部样式表(内嵌样式表)」**

也称为内嵌式，将CSS代码集中写在HTML文档的head头部标签中，并且用style标签定义。

- style标签一般位于head标签中，当然理论上他可以放在HTML文档的任何地方。
- type="text/css"  在html5中可以省略。
- 只能控制当前的页面
- **缺点:**没有彻底分离结构与样式

```
<head>
<style type="text/CSS">
    选择器（选择的标签） { 
      属性1: 属性值1;
      属性2: 属性值2; 
      属性3: 属性值3;
    }
</style>
</head>
```

**「3.外部样式表(外链式)」**

也称链入式，是将所有的样式放在一个或多个以.css为扩展名的外部样式表文件中，通过link标签将外部样式表文件链接到HTML文档中。

- `rel`:定义当前文档与被链接文档之间的关系，在这里需要指定为“stylesheet”，表示被链接的文档是一个样式表文件。
- `href`:定义所链接外部样式表文件的URL，可以是相对路径，也可以是绝对路径。

```
<link rel="stylesheet" href="index.css">
```

**「4.团队约定-代码风格」**

```
/*1.紧凑格式 (Compact)*/
h3 { color: deeppink;font-size: 20px;}
// 2.一种是展开格式（推荐）
h3 {
 color: deeppink;
    font-size: 20px;    
}

/* 团队约定-代码大小写*/
/* 样式选择器，属性名，属性值关键字全部使用小写字母书写，属性字符串允许使用大小写。*/
/* 推荐 */
h3{
 color: pink;
}
 
/* 不推荐 */
H3{
 COLOR: PINK;
}
```



------

## CSS基础选择器

#### CSS选择器作用

找到指定的HTML页面元素，选择标签。

### CSS基础选择器

**「1. 标签选择器」**

- 标签选择器（元素选择器）是指用HTML标签名称作为选择器，按标签名称分类，为页面中某一类标签指定统一的CSS样式。
- 作用：可以把某一类标签全部选择出来。
- 优点：快速为网页中同类型的标签统一样式
- 缺点：不能设计差异化样式。

```
标签名{属性1:属性值1; 属性2:属性值2; 属性3:属性值3; } 
```

**「2. 类选择器」**

- 类选择器使用"."(英文点号)进行标识，后面紧跟类名。
- 语法：类名选择器

```
.类名  {   
    属性1:属性值1; 
    属性2:属性值2; 
    属性3:属性值3;     
}
<p class='类名'></p>
```

- `优点`：可以为元素对象定义单独或相同的样式。可以选择一个或者多个标签。

- `注意`：类选择器使用“.”（英文点号）进行标识，后面紧跟类名(自定义，我们自己命名的)

- - 长名称或词组可以使用中横线来为选择器命名。
  - 不要纯数字、中文等命名， 尽量使用英文字母来表示。
  - 多类名选择器：各个类名中间用空格隔开。

**「3. id选择器」**id选择器使用`#`进行标识，后面紧跟id名

- 元素的id值是唯一的，只能对应于文档中某一个具体的元素。

```
#id名 {属性1:属性值1; 属性2:属性值2; 属性3:属性值3; }
<p id="id名"></p>
```

**「4. 通配符选择器」**

通配符选择器用`*`号表示，`*` 就是选择所有的标签。它是所有选择器中作用范围最广的，能匹配页面中所有的元素。

- `注意`：会匹配页面所有的元素，降低页面响应速度，不建议随便使用

```
* { 属性1:属性值1; 属性2:属性值2; 属性3:属性值3; }
```

例如下面代码，使用通配符选择器定义CSS样式，清除所有HTML标记的默认边距。

```
* {
  margin: 0;                    /* 定义外边距*/
  padding: 0;                   /* 定义内边距*/
}
```

**「5. 基础选择器总结」**

| 选择器       | 作用                          | 缺点                     | 使用情况   | 用法                 |
| :----------- | :---------------------------- | :----------------------- | :--------- | :------------------- |
| 标签选择器   | 可以选出所有相同的标签，比如p | 不能差异化选择           | 较多       | p { color：red;}     |
| 类选择器     | 可以选出1个或者多个标签       | 可以根据需求选择         | 非常多     | .nav { color: red; } |
| id选择器     | 一次只能选择器1个标签         | 只能使用一次             | 不推荐使用 | #nav {color: red;}   |
| 通配符选择器 | 选择所有的标签                | 选择的太多，有部分不需要 | 不推荐使用 | * {color: red;}      |

**「6. 团队约定-选择器」**

1. 尽量少用通配符选择器 `*`。
2. 尽量少用ID选择器
3. 不使用无具体语义定义的标签选择器。

```
/* 推荐 */
.jdc {}
li {}
p{}

/* 不推荐 */
*{}
#jdc {}
div{}   因为div 没有语义，我们尽量少用
```



### CSS复合选择器

复合选择器是由两个或多个基础选择器，通过不同的方式组合而成的

**「1. 后代选择器」**又称为包含选择器

- 用来选择元素或元素组的子孙后代
- 其写法就是把外层标签写在前面，内层标签写在后面，中间用**「空格」**分隔，先写父亲爷爷，再写儿子孙子。
- 子孙后代都可以这么选择。或者说，它能选择任何包含在内 的标签。

```
父级 子级{属性:属性值;属性:属性值;}

.class h3 {color:red;font-size:16px;}
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 当标签发生嵌套时，内层标签就成为外层标签的后代。
- 子孙后代都可以这么选择。或者说，它能选择任何包含在内的标签。

**「2. 子元素选择器」**

- 子元素选择器只能选择作为某元素子元素(亲儿子)的元素。
- 其写法就是把父级标签写在前面，子级标签写在后面，中间跟一个 `>` 进行连接
- 这里的子,指的是亲儿子。不包含孙子 重孙子之类。

```
.class>h3 {color:red;font-size:14px;}
```

**「3. 交集选择器」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 其中第一个为标签选择器，第二个为class选择器，两个选择器之间`不能有空格`，如h3.special。

```
交集选择器是并且的意思,即...又...的意思
比如：   p.one   选择的是： 类名为 .one 的段落标签。 
/*用的相对来说比较少，不建议使用。*/
```

**「4. 并集选择器」**如果某些选择器定义的相同样式，就可以利用并集选择器，可以让代码更简洁。并集选择器（CSS选择器分组）是各个选择器通过`,`连接而成的，通常用于集体声明。

- 任何形式的选择器（包括标签选择器、class类选择器 id选择器等），都可以作为并集选择器的一部分。
- 并集选择器通常用于集体声明 ，逗号隔开的，所有选择器都会执行后面样式，逗号可以理解为和的意思。

```
比如  
.one, 
p , 
#test {color: #F00;}  
表示   .one 和 p  和 #test 这三个选择器都会执行颜色为红色。 
通常用于集体声明。  
```

**「5. 链接伪类选择器」**

用于向某些选择器添加特殊的效果。写的时候，他们的顺序尽量不要颠倒,按照lvha的顺序。否则可能引起错误。

链接伪类，是利用交集选择器.

- `a:link` 未访问的链接
- `a:visited` 已访问的链接
- `a:hover` 鼠标移动到链接上
- `a:active` 选定的链接

##### 实际工作中，很少写全四个状态，一般写法如下：

```
a {   /* a是标签选择器  所有的链接 */
   font-weight: 700;
   font-size: 16px;
   color: gray;
      text-decoration: none; /* 清除链接默认的下划线*/
}
a:hover {   /* :hover 是链接伪类选择器 鼠标经过 */
   color: red; /*  鼠标经过的时候，由原来的 灰色 变成了红色 */
}
```

**「6. 复合选择器总结」**

| 选择器         | 作用                     | 特征                 | 使用情况 | 隔开符号及用法                          |
| :------------- | :----------------------- | :------------------- | :------- | :-------------------------------------- |
| 后代选择器     | 用来选择元素后代         | 是选择所有的子孙后代 | 较多     | 符号是`空格` .nav a                     |
| 子代选择器     | 选择 最近一级元素        | 只选亲儿子           | 较少     | 符号是`>`  .nav>p                       |
| 交集选择器     | 选择两个标签交集的部分   | 既是 又是            | 较少     | `没有符号` p.one                        |
| 并集选择器     | 选择某些相同样式的选择器 | 可以用于集体声明     | 较多     | 符号是`逗号` .nav, .header              |
| 链接伪类选择器 | 给链接更改状态           |                      | 较多     | 重点记住 a{} 和 a:hover  实际开发的写法 |

------

## CSS字体样式

### font字体

**「1. font-size」**

- font-size属性用于设置字号(字体大小)
- `谷歌浏览器`默认的文字大小为16px
- 不同浏览器可能默认显示的字号大小不一致，我们尽量给一个明确值大小，不要默认大小。一般给body指定整个页面文字的大小。

```
p { font-size:20px; }
```

#### 单位

- 相对长度单位、绝对长度单位

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「2. font-family」**

- font-family属性用于设置哪一种字体。

```
p { font-family:"微软雅黑";}
```

- 指定多个字体，如果浏览器不支持第一个字体就会尝试下一个直到找到合适的字体，如果都没有，以电脑默认字体为准。

```
p {font-family: Arial,"Microsoft Yahei", "微软雅黑";}
```

- CSS Unicode字体

- - 在 CSS 中设置字体名称，直接写中文是可以的。但是在文件编码（GB2312、UTF-8 等）不匹配时会产生乱码的错误。
  - xp 系统不支持 类似微软雅黑的中文。
  - 解决方案：英文来替代。比如`font-family:"Microsoft Yahei"`。在 CSS 直接使用 Unicode 编码来写字体名称可以避免这些错误。使用 Unicode 写中文字体名称，浏览器是可以正确的解析的。

```
font-family: "\5FAE\8F6F\96C5\9ED1";   表示设置字体为“微软雅黑”。
```

**「3. font-weight」**

| 属性值  | 描述                                                        |
| :------ | :---------------------------------------------------------- |
| normal  | 默认值（不加粗的）                                          |
| bold    | 定义粗体（加粗的）                                          |
| 100~900 | 400 等同于 normal，而 700 等同于 bold  (数字表示粗细用的多) |

**「4. font-weight」**

font-style属性用于定义字体风格，如设置斜体、倾斜或正常字体，其可用属性值如下：

| 属性   | 作用                                                    |
| :----- | :------------------------------------------------------ |
| normal | 默认值，浏览器会显示标准的字体样式  font-style: normal; |
| italic | 浏览器会显示斜体的字体样式。                            |

**「5. font:综合设置字体样式」**

```
选择器 { font: font-style  font-weight  font-size/line-height  font-family;}
```

- 注意：使用font属性时，必须按上面语法格式中的顺序书写，不能更换顺序，各个属性以`空格`隔开

- - 其中不需要设置的属性可以省略(取默认值),但必须保留`font-size`和`font-family`属性，否则font属性将不起作用。

**「6. font总结」**

| 属性        | 表示     | 注意点                                                       |
| :---------- | :------- | :----------------------------------------------------------- |
| font-size   | 字号     | 我们通常用的单位是px 像素，一定要跟上单位                    |
| font-family | 字体     | 实际工作中按照团队约定来写字体                               |
| font-weight | 字体粗细 | 记住加粗是 700 或者 bold  不加粗 是 normal 或者  400  记住数字不要跟单位 |
| font-style  | 字体样式 | 记住倾斜是 italic   不倾斜 是 normal  工作中我们最常用 normal |
| font        | 字体连写 | 1. 字体连写是有顺序的  不能随意换位置 2. 其中字号 和 字体 必须同时出现 |

### CSS外观属性

**「1. color」**

color属性用于定义文本的颜色
其取值方式有以下3种：

- 实际工作中，用16进制的写法是最多的，且我们更喜欢简写方式比如#f0代表红色。

| 表示表示       | 属性值                        |
| :------------- | :---------------------------- |
| 预定义的颜色值 | red，green，blue，pink        |
| 十六进制       | #FF0000，#FF6600，#29D794     |
| RGB代码        | rgb(255,0,0)或rgb(100%,0%,0%) |

**「2.text-align」**

text-align属性用于设置文本内容的水平对齐方式，相当于html中的align对齐属性。

- 注意：是让盒子里面的文本内容水平居中， 而不是让盒子居中对齐

其可用属性值如下：

| 属性   |       解释       |
| :----- | :--------------: |
| left   | 左对齐（默认值） |
| right  |      右对齐      |
| center |     居中对齐     |

**「3. line-height」**line-height属性用于设置行间距，就是行与行之间的距离，即字符的垂直间距，一般称为行高。

- line-height常用的属性值单位有三种，分别为像素px，相对值em和百分比%，实际工作中使用最多的是像素px

```
一般情况下，行距比字号大7--8像素左右就可以了。
line-height: 24px;
```

#### 行高测量

行高测量方法：![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)`行高测量方法`行高我们利用最多的一个地方是：可以让单行文本在盒子中垂直居中对齐。

> **文字的行高等于盒子的高度。**行高  =  上距离 +  内容高度  + 下距离
> 上距离和下距离总是相等的，因此文字看上去是垂直居中的。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 行高与高度的三种关系

- 如果 行高 等 高度  文字会 垂直居中
- 如果行高 大于 高度  文字会 偏下
- 如果行高小于高度  文字会  偏上

```
  /*line-height 要设置在font属性下面，否则无效，例如：*/
  height: 80px;
  text-align: center;
  font: normal bold 30px "宋体";
  line-height: 80px;
```

可以使用display:flex;布局方式让文字水平垂直居中

```
  display: flex;
  align-items: center;     /* 侧轴对齐方式*/
  justify-content: center; /* 主轴对齐方式 */
```

**「4. text-indent」**

text-indent属性用于设置首行文本的缩进

- 其属性值可为不同单位的数值、em字符宽度的倍数、或相对于浏览器窗口宽度的百分比%，允许使用负值。
- 建议使用em作为设置单位。
- 1em 就是一个字的宽度。如果是汉字的段落，1em 就是一个汉字的宽度

```
p {
      /*行间距*/
      line-height: 25px;
      /*首行缩进2个字  em  1个em 就是1个字的大小*/
      text-indent: 2em;  
 }
```

**「5. text-decoration」**文本的装饰

text-decoration,通常我们用于给链接修改装饰效果

| 值           | 描述                                                  |
| :----------- | :---------------------------------------------------- |
| none         | 默认。定义标准的文本。取消下划线（最常用）            |
| underline    | 定义文本下的一条线。下划线 也是我们链接自带的（常用） |
| overline     | 定义文本上的一条线。（不用）                          |
| line-through | 定义穿过文本下的一条线。（不常用）                    |

**「6. CSS外观属性总结」**

| 属性            | 表示     | 注意点                                                 |
| :-------------- | :------- | :----------------------------------------------------- |
| color           | 颜色     | 我们通常用  十六进制  比如 而且是简写形式 #fff         |
| line-height     | 行高     | 控制行与行之间的距离                                   |
| text-align      | 水平对齐 | 可以设定文字水平的对齐方式                             |
| text-indent     | 首行缩进 | 通常我们用于段落首行缩进2个字的距离  text-indent: 2em; |
| text-decoration | 文本修饰 | 记住 添加 下划线  underline  取消下划线  none          |



------

## 标签显示模式(display)

`标签显示模式`是标签以什么方式进行显示。HTML标签一般分为块标签和行内标签两种类型，它们也称为块元素和行内元素。

#### 标签显示模式转换 display

- 块转行内：display:inline;
- 行内转块：display:block;
- 块、行内元素转换为行内块：display: inline-block;

**「1. 块级元素(block-level)」**

> 常见的块元素有<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>等，其中<div>标签是最典型的块元素。

- ##### 块级元素的特点

- - 独占一行
  - 高度，宽度，外边距以及内边距都可以控制。
  - 宽度默认是容器(父级宽度)的100%
  - 是一个容器及盒子，里面可以放行内或者块级元素
  - **注意**：只有文字才能组成段落，因此p标签里面不能放块级元素，特别是p不能放div。同理，还有h1~h6，dt,它们都是文字类块级标签，里面不能放其他块级元素。

**「2. 行内元素(inline-level)」**

> 有的地方也称为`内联元素`
>
> 常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中<span>标签最典型的行内元素。

- ##### 行内元素的特点

- 1. 相邻行内元素在一行上，一行可以显示多个。
  2. 高度、宽度直接设置是无效的。
  3. 默认高度就是它本身内容的宽度。
  4. 行内元素只能容纳文本或其他行内元素。

###### 注意

- 链接里面不能再放链接
- 特殊情况a里面可以放块级元素，但是给a转换一下块级模式最安全。

**「3. 行内块元素(inline-block)」**

> 在行内元素中有几个特殊的标签——<img>、<input >、<td>，可以对它们设置宽高和对齐属性，有些资料可能会称它们为行内块元素。

- **行内块元素的特点**

- 1. 和相邻行内元素(行内块)在一行上，但是之间会有空白风险。一行可以显示多个
  2. 默认宽度就是它本身内容的宽度。
  3. 高度，行高，外边距以及内边距都可以控制。

#### 三种模式总结

| 元素模式   | 元素排列               | 设置样式               | 默认宽度         | 包含                     |
| :--------- | :--------------------- | :--------------------- | :--------------- | :----------------------- |
| 块级元素   | 一行只能放一个块级元素 | 可以设置宽度高度       | 容器的100%       | 容器级可以包含任何标签   |
| 行内元素   | 一行可以放多个行内元素 | 不可以直接设置宽度高度 | 它本身内容的宽度 | 容纳文本或则其他行内元素 |
| 行内块元素 | 一行放多个行内块元素   | 可以设置宽度和高度     | 它本身内容的宽度 |                          |



------

## CSS背景(background)

**「1. 背景颜色」**

```
background-color: 颜色值;   默认的值是 transparent  透明的
```

**「2. 背景图片(image)」**

```
语法：
background-image : none | url (url) ;
例如:
background-image: url(images/1.png);
```

**「3. 背景平铺（repeat）」**

```
background-repeat : repeat | no-repeat | repeat-x | repeat-y 
```

| 参数      |                 作用                 |
| :-------- | :----------------------------------: |
| repeat    | 背景图像在纵向和横向上平铺（默认的） |
| no-repeat |            背景图像不平铺            |
| repeat-x  |         背景图像在横向上平铺         |
| repeat-y  |          背景图像在纵向平铺          |

**「4. 背景位置(position)」**

```
background-position : length || length
background-position : position || position 
```

| 参数     |                              值                              |
| :------- | :----------------------------------------------------------: |
| length   |         百分数 \| 由浮点数字和单位标识符组成的长度值         |
| position | top \| center \| bottom \| left \| center \| right  方位名词 |

#### 注意：

- 必须先指定background-image属性
- position 后面是x坐标和y坐标。可以使用方位名词或者 精确单位。
- 如果指定两个值，两个值都是方位名字，则两个值前后顺序无关，比如left  top和top  left效果一致
- 如果只指定了一个方位名词，另一个值默认居中对齐。
- 如果position 后面是精确坐标， 那么第一个，肯定是 x 第二个一定是y
- 如果只指定一个数值,那该数值一定是x坐标，另一个默认垂直居中
- 如果指定的两个值是 精确单位和方位名字混合使用，则第一个值是x坐标，第二个值是y坐标

#### 背景简写：

- background：属性的值的书写顺序官方没有强制的标准。为了可读性，建议如下写：
- background: 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置;

```
/* 有背景图片背景颜色可以不用写*/
background: transparent url(image.jpg) repeat-y  scroll center top ;
```

**「5. 背景半透明(CSS3)」**

```
background: rgba(0, 0, 0, 0.3);
background: rgba(0, 0, 0, .3);
```

- 等同于background-color: rgba(0, 0, 0, .3)
- 最后一个参数是alpha 透明度 取值范围 0~1之间
- 我们习惯把0.3 的 0 省略掉 这样写 background: rgba(0, 0, 0, .3);
- 注意：背景半透明是指盒子背景半透明，盒子里面的内容不受影响
- 低于IE 9的版本不支持

##### 盒子半透明 opacity

- 设置opacity元素的所有后代元素会随着一起具有透明性，一般用于调整图片或者模块的整体不透明度

```
opacity: .2;
```

**「6. 背景总结」**

| 属性                  | 作用             | 值                                                           |
| :-------------------- | :--------------- | :----------------------------------------------------------- |
| background-color      | 背景颜色         | 预定义的颜色值/十六进制/RGB代码                              |
| background-image      | 背景图片         | url(图片路径)                                                |
| background-repeat     | 是否平铺         | repeat/no-repeat/repeat-x/repeat-y                           |
| background-position   | 背景位置         | length/position   分别是x  和 y坐标， 切记 如果有 精确数值单位，则必须按照先X 后Y 的写法 |
| background-attachment | 背景固定还是滚动 | scroll/fixed                                                 |
| 背景简写              | 更简单           | 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置;  他们没有顺序 |
| 背景透明              | 让盒子半透明     | background: rgba(0,0,0,0.3);  后面必须是 4个值               |



------

## CSS三大特性

**「1. CSS 层叠性」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

-`概念`：

- 所谓层叠性是指多种CSS样式的叠加
- 是浏览器处理冲突的一个能力,如果一个属性通过两个相同选择器设置到同一个元素上，那么这个时候一个属性就会将另一个属性层叠掉

-`原则`：

- 样式冲突，遵循的原则是就近原则。 那个样式离着结构近，就执行那个样式。
- 样式不冲突，不会层叠。

**「2. CSS 继承性」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)-`概念`：

- 子标签会继承父标签的某些样式，如文本颜色和字号。
- 想要设置一个可继承的属性，只需将它应用于父元素即可。

-`注意`：

- 恰当地使用继承可以简化代码，降低CSS样式的复杂性。比如有很多子级孩子都需要某个样式，可以给父级指定一个，这些孩子继承过来就好了。
- 子元素可以继承父元素的样式（**text-，font-，line-这些元素开头的可以继承，以及color属性**）

**「3. CSS 优先级(CSS特殊性)」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)-`概念`：定义CSS样式时，经常出现两个或更多规则应用在同一元素上，此时，

- 选择器相同，则执行层叠性
- 选择器不同，就会出现优先级的问题。

-`权重计算公式`：

| 标签选择器               | 计算权重公式 |
| :----------------------- | :----------- |
| 继承或者 *               | 0,0,0,0      |
| 每个元素（标签选择器）   | 0,0,0,1      |
| 每个类，伪类             | 0,0,1,0      |
| 每个ID                   | 0,1,0,0      |
| 每个行内样式 style=""    | 1,0,0,0      |
| 每个!important  最重要的 | ∞ 无穷大     |

- 值从左到右，左面的最大，一级大于一级，数位之间没有进制，级别之间不可超越。
- 关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity（特殊性）
- div { color: pink !important; }

-`权重叠加`：

```
 div ul  li   ------>      0,0,0,3
 .nav ul li   ------>      0,0,1,2
 a:hover      -----—>      0,0,1,1
 .nav a       ------>      0,0,1,1
```

-`继承的权重是0`：

- 我们修改样式，一定要看该标签有没有被选中
- 如果选中了，那么以上面的公式来计权重。谁大听谁的。
- 如果没有选中，那么权重是0，因为继承的权重为0.



------

## 盒子模型

css学习三大重点： css 盒子模型 、 浮动 、 定位  

**网页布局的本质**

- 首先利用CSS设置好盒子的大小，然后摆放盒子的位置。
- 最后把网页元素比如文字图片等等，放入盒子里面。

### 1. 盒子模型(Box Model)

- 盒子模型就是把HTML页面中的布局元素看作是一个矩形的盒子，也就是一个盛装内容的容器。
- 盒子模型由元素的内容、边框（border）、内边距（padding）、和外边距（margin）组成。
- 盒子里面的文字和图片等元素是 内容区域
- 盒子的厚度 我们称为为盒子的边框
- 盒子内容与边框的距离是内边距
- 盒子与盒子之间的距离是外边距

**W3c标准盒子模型**

标准 w3c 盒子模型的范围包括 margin、border、padding、content

当设置为box-sizing: content-box;时，将采用标准模式解析计算，也是默认模式；

```
内盒尺寸计算(元素实际大小)
```

- 宽度：Element Height = content height + padding + border （Height为内容高度）
- 高度：Element  Width = content width + padding + border （Width为内容宽度）
- 盒子的实际大小：**内容的宽度和高度 +  内边距  +  边框**  ![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**IE盒子模型**

IE 盒子模型的 content 部分包含了 border 和 pading

当设置为box-sizing: border-box时，将采用怪异模式解析计算；

### 2. 盒子边框(border)

| 属性         |          作用          |
| :----------- | :--------------------: |
| border-width | 定义边框粗细，单位是px |
| border-style |       边框的样式       |
| border-color |        边框颜色        |

**边框的样式：**

- none：没有边框即忽略所有边框的宽度（默认值）
- solid：边框为单实线(最为常用的)
- dashed：边框为虚线
- dotted：边框为点线

```
边框综合设置
border : border-width || border-style || border-color 

border: 1px solid red;  没有顺序要求  
```

**盒子边框写法总结表：**

很多情况下，我们不需要指定4个边框，我们是可以单独给4个边框分别指定的。

| 上边框                     | 下边框                        | 左边框                      | 右边框                       |
| :------------------------- | :---------------------------- | :-------------------------- | :--------------------------- |
| border-top-style:样式;     | border-bottom-style:样式;     | border-left-style:样式;     | border-right-style:样式;     |
| border-top-width:宽度;     | border- bottom-width:宽度;    | border-left-width:宽度;     | border-right-width:宽度;     |
| border-top-color:颜色;     | border- bottom-color:颜色;    | border-left-color:颜色;     | border-right-color:颜色;     |
| border-top:宽度 样式 颜色; | border-bottom:宽度 样式 颜色; | border-left:宽度 样式 颜色; | border-right:宽度 样式 颜色; |

**表格的细线边框：**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 通过表格的`cellspacing="0"`,将单元格与单元格之间的距离设置为0，

- 但是两个单元格之间的边框会出现重叠，从而使边框变粗

- 通过css属性：table{ border-collapse:collapse; }  

- - `collapse` 单词是合并的意思,`border-collapse: collapse;`表示相邻边框合并在一起。

```
<style>
 table {
  width: 500px;
  height: 300px;
  border: 1px solid red;
 }
 td {
  border: 1px solid red;
  text-align: center;
 }
 table, td {
  border-collapse: collapse;  /*合并相邻边框*/
 }
</style>
```

### 2. 内边距(padding)

padding属性用于设置内边距。是指边框与内容之间的距离。

**设置**

| 属性           | 作用     |
| :------------- | :------- |
| padding-left   | 左内边距 |
| padding-right  | 右内边距 |
| padding-top    | 上内边距 |
| padding-bottom | 下内边距 |

**padding简写**

| 值的个数 | 表达意思                                        |
| :------- | :---------------------------------------------- |
| 1个值    | padding：上下左右内边距;                        |
| 2个值    | padding: 上下内边距   左右内边距 ；             |
| 3个值    | padding：上内边距  左右内边距  下内边距；       |
| 4个值    | padding: 上内边距 右内边距 下内边距 左内边距 ； |

当我们给盒子指定padding值之后， 发生了2件事情：

1. 内容和边框 有了距离，添加了内边距。
2. 盒子会变大

**解决措施：**通过给设置了宽高的盒子，减去相应的内边距的值，维持盒子原有的大小。

**padding不影响盒子大小情况：👉**如果没有给一个盒子指定宽度， 此时，如果给这个盒子指定padding， 则不会撑开盒子。

### 3. 外边距（margin）

margin属性用于设置外边距。margin就是控制`盒子和盒子之间的距离`

**设置**

| 属性          | 作用     |
| :------------ | :------- |
| margin-left   | 左外边距 |
| margin-right  | 右外边距 |
| margin-top    | 上外边距 |
| margin-bottom | 下外边距 |

margin值的简写 （复合写法）代表意思  跟 padding 完全相同。

**块级盒子水平居中**

- 盒子必须指定宽度（width）
- 然后就给左右的外边距都设置为auto

实际工作中常用这种方式进行网页布局，示例代码如下：

```
.header  { width: 960px; margin: 0 auto;}
```

常见的写法，以下下三种都可以👇👇。

- margin-left: auto;  margin-right: auto;
- margin: auto;
- margin: 0 auto;

**文字居中和盒子居中区别👇👇**

1. 盒子内的文字水平居中是 text-align: center; 而且还可以让 行内元素和行内块居中对齐
2. 块级盒子水平居中  左右margin 改为 auto

**插入图片和背景图片区别👇👇**

1. `插入图片`我们用的最多 比如产品展示类  移动位置只能靠盒模型 padding margin
2. `背景图片`我们一般用于小图标背景或者超大背景图片、背景图片，移动位置只能通过  background-position

**清除元素的默认内外边距👇👇**

- 行内元素为了照顾兼容性,尽量只设置左右内外边距，不要设置上下内外边距。

```
* {
   padding:0;         /* 清除内边距 */
   margin:0;          /* 清除外边距 */
}
```

### 4.外边距合并

使用margin定义块元素的**「垂直外边距」**时，可能会出现外边距的合并。

###### (1). 相邻块元素垂直外边距的合并

- 当上下相邻的两个块元素相遇时，如果上面的元素有下外边距margin-bottom
- 下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和
- **「取两个值中的较大者」**这种现象被称为相邻块元素垂直外边距的合并（也称外边距塌陷）。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「解决方案：尽量给只给一个盒子添加margin值」**。

#### (2). 嵌套块元素垂直外边距的合并（塌陷）

- 对于两个嵌套关系的块元素，如果父元素没有上内边距及边框
- 父元素的上外边距会与子元素的上外边距发生合并
- 合并后的外边距为两者中的较大者

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「解决方案：」**

1. 可以为父元素定义上边框。
2. 可以为父元素定义上内边距
3. 可以为父元素添加overflow: hidden。

还有其他方法，比如浮动、固定、绝对定位的盒子不会有问题，后面咱们再总结。。。

#### 盒子模型布局稳定性

优先使用  宽度 （width）  其次 使用内边距（padding）   再次  外边距（margin）

```
width >  padding  >   margin   
```

**原因：**

- margin 会有外边距合并 还有 ie6下面margin 加倍的bug（讨厌）所以最后使用。
- padding  会影响盒子大小， 需要进行加减计算（麻烦） 其次使用。
- width  没有问题（嗨皮）我们经常使用宽度剩余法 高度剩余法来做。

### 5. CSS3 新增

```
圆角边框：
border-radius:length;

border-top-left-radius   定义了左上角的弧度
border-top-right-radius   定义了右上角的弧度
border-bottom-right-radius   定义了右下角的弧度
border-bottom-left-radius   定义了左下角的弧度
```

- 其中每一个值可以为 数值或百分比的形式。
- 技巧：让一个正方形 变成圆圈

```
border-radius: 50%;
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)如果要在四个角上一一指定，可以使用以下规则👇👇：

```
border-radius: 左上角 右上角  右下角  左下角;
```

1. 四个值: 第一个值为左上角，第二个值为右上角，第三个值为右下角，第四个值为左下角。
2. 三个值: 第一个值为左上角, 第二个值为右上角和左下角，第三个值为右下角
3. 两个值: 第一个值为左上角与右下角，第二个值为右上角与左下角
4. 一个值：四个圆角值相同

```
盒子阴影(box-shadow)：
box-shadow: offset-x offset-y [blur [spread]] [color] [inset]
```

| 值       | 描述                                           |
| :------- | :--------------------------------------------- |
| offset-x | 阴影的水平偏移量。正数向右偏移，负数向左偏移。 |
| offset-y | 阴影的垂直偏移量。正数向下偏移，负数向上偏移。 |
| blur     | 可选。阴影模糊距离，不能取负数。               |
| spread   | 可选。阴影大小                                 |
| color    | 可选。阴影的颜色                               |
| inset    | 可选。表示添加内阴影，默认为外阴影             |

```
div {
   width: 200px;
   height: 200px;
   border: 10px solid red;
   /* box-shadow: 5px 5px 3px 4px rgba(0, 0, 0, .4);  */
   /* box-shadow:水平位置 垂直位置 模糊距离 阴影尺寸（影子大小） 阴影颜色  内/外阴影； */
   box-shadow: 0 15px 30px  rgba(0, 0, 0, .4);   
}
```



------



## 浮动

### 浮动

**「1. CSS布局的三种机制」**

> 网页布局的核心——就是**用CSS来摆放盒子**。

CSS 提供了3种机制来设置盒子的摆放位置，分别是普通流（标准流）、浮动和定位，其中：

**A. 普通流（标准流）**

- 块级元素会独占一行，从上向下顺序排列；

- - 常用元素：div、hr、p、h1~h6、ul、ol、dl、form、table

- 行内元素会按照顺序，从左到右顺序排列，碰到父元素边缘则自动换行；

- - 常用元素：span、a、i、em等

**B. 浮动**

- 让盒子从普通流中浮起来,主要作用让多个块级盒子一行显示。

**C. 定位**

- 将盒子定在浏览器的某一个位置——CSS 离不开定位，特别是后面的 js 特效。

**「2. 什么是浮动」**元素的浮动是指设置了浮动属性的元素会

- 脱离标准普通流的控制,不占位置，脱标
- 移动到指定位置。

##### 作用

1. 让多个盒子(div)水平排列成一行，使得浮动称为布局的重要手段。
2. 可以实现盒子的左右对齐等等。
3. 浮动最早是用来控制图片，实现文字环绕图片效果。
4. float属性会改变元素的display属性，任何元素都可以浮动。浮动元素会生成一个块级框，而不论它本身是何种元素。生成的块级框和我们前面的行内块极其相似。

##### 语法

```
选择器 { float: 属性值; }
```

| 属性值 | 描述                 |
| :----- | :------------------- |
| none   | 元素不浮动（默认值） |
| left   | 元素向左浮动         |
| right  | 元素向右浮动         |



> 浮动只会影响当前的或者是后面的标准流盒子，不会影响前面的标准流。
> **建议:**如果一个盒子里面有多个子盒子，如果其中一个盒子浮动了，其他兄弟也应该浮动。防止引起问题

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**浮动(float)小结**

| 特点 | 说明                                                         |
| :--- | :----------------------------------------------------------- |
| 浮   | 加了浮动的盒子**「是浮起来」**的，漂浮在其他标准流盒子的上面。 |
| 漏   | 加了浮动的盒子**「是不占位置的」**，它原来的位置**「漏给了标准流的盒子」**。 |
| 特   | **「特别注意」**：浮动元素会改变display属性， 类似转换为了行内块，但是元素之间没有空白缝隙 |

### 清除浮动

因为父级盒子很多情况下，不方便给高度，但是子盒子浮动就不占有位置，最后父级盒子高度为0，就影响了下面的标准流盒子。![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**总结：**

- 由于浮动元素不再占用原文档流的位置，所以它会对后面的元素排版产生影响
- 准确地说，并不是清除浮动，而是清除浮动后造成的影响

**清除浮动本质**清除浮动主要为了解决父级元素因为子级浮动引起内部高度为0 的问题。清除浮动之后， 父级就会根据浮动的子盒子自动检测高度。父级有了高度，就不会影响下面的标准流了

#### 清除浮动的方法

```
选择器 { clear: 属性值; }   clear 清除  
```

| 属性值 | 描述                                       |
| :----- | :----------------------------------------- |
| left   | 不允许左侧有浮动元素（清除左侧浮动的影响） |
| right  | 不允许右侧有浮动元素（清除右侧浮动的影响） |
| both   | 同时清除左右两侧浮动的影响                 |

实际工作中,几乎只用clear: both

**1).额外标签法(隔墙法)**

是W3C推荐的做法是通过在浮动元素末尾添加一个空的标签例如 <div style=”clear:both”></div>，或则其他标签br等亦可。

- 优点：通俗易懂，书写方便
- 缺点：添加许多无意义的标签，结构化较差。

**2).父级添加overflow属性方法**

```
可以给父级添加： overflow为 hidden| auto| scroll  都可以实现。
```

- 优点： 代码简洁
- 缺点： 内容增多时候容易造成不会自动换行导致内容被隐藏掉，无法显示需要溢出的元素。

**3).使用after伪元素清除浮动**:after 方式为空元素额外标签法的升级版，好处是不用单独加标签了

```
    .clearfix:after {
        content: "";
        display: block;
        height: 0;
        clear: both;
        visibility: hidden;
    }
  
    /* IE6、7 专有 */
    .clearfix {
        *zoom: 1;
    }
        
```

- 优点：符合闭合浮动思想  结构语义化正确
- 缺点：由于IE6-7不支持:after，使用 zoom:1触发 hasLayout。

**4).使用双伪元素清除浮动**

```
    .clearfix:before,
    .clearfix:after {
        content: "";
        display: table;
    }

    .clearfix:after {
        clear: both;
    }

    .clearfix {
       *zoom: 1;
    }
```

- 优点： 代码更简洁
- 缺点： 由于IE6-7不支持:after，使用 zoom:1触发 hasLayout。

#### 清除浮动总结

```
什么时候用清除浮动呢？
```

1. 父级没高度
2. 子盒子浮动了
3. 影响下面布局了，我们就应该清除浮动了。



| 清除浮动的方式       | 优点               | 缺点                               |
| :------------------- | :----------------- | :--------------------------------- |
| 额外标签法（隔墙法） | 通俗易懂，书写方便 | 添加许多无意义的标签，结构化较差。 |
| 父级overflow:hidden; | 书写简单           | 溢出隐藏                           |
| 父级after伪元素      | 结构语义化正确     | 由于IE6-7不支持:after，兼容性问题  |
| 父级双伪元素         | 结构语义化正确     | 由于IE6-7不支持:after，兼容性问题  |

### CSS属性书写顺序

建议遵循以下顺序：

1. 布局定位属性：display / position / float / clear / visibility / overflow（建议 display 第一个写，毕竟关系到模式）
2. 自身属性：width / height / margin / padding / border / background
3. 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word
4. 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient …

```
.jdc {
    display: block;
    position: relative;
    float: left;
    width: 100px;
    height: 100px;
    margin: 0 10px;
    padding: 20px 0;
    font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif;
    color: #333;
    background: rgba(0,0,0,.5);
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    -o-border-radius: 10px;
    -ms-border-radius: 10px;
    border-radius: 10px;
}
```



------

## 定位(position)

**「1. 定位详解」**

将盒子**「定」**在某一个**「位」**置  自由的漂浮在其他盒子(包括标准流和浮动)的上面。

所以，我们脑海应该有三种布局机制的上下顺序👇👇
标准流在最底层 (海底)  -------   浮动 的盒子 在 中间层  (海面)  -------  定位的盒子 在 最上层  （天空）

**定位**是用来布局的，它有两部分组成：定位 = 定位模式 + 边偏移在 CSS 中，通过 `top`、`bottom`、`left` 和 `right` 属性定义元素的**「边偏移」**：（方位名词）

| 边偏移属性 | 示例           | 描述                                                         |
| :--------- | :------------- | :----------------------------------------------------------- |
| `top`      | `top: 80px`    | **「顶端」**偏移量，定义元素相对于其父元素**「上边线的距离」**。 |
| `bottom`   | `bottom: 80px` | **「底部」**偏移量，定义元素相对于其父元素**「下边线的距离」**。 |
| `left`     | `left: 80px`   | **「左侧」**偏移量，定义元素相对于其父元素**「左边线的距离」**。 |
| `right`    | `right: 80px`  | **「右侧」**偏移量，定义元素相对于其父元素**「右边线的距离」** |

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**「2. 定位模式(position)」**在 CSS 中，通过 `position` 属性定义元素的**「定位模式」**，语法如下：

```
选择器 { position: 属性值; }
```

| 值         |       语义       |
| :--------- | :--------------: |
| `static`   | **「静态」**定位 |
| `relative` | **「相对」**定位 |
| `absolute` | **「绝对」**定位 |
| `fixed`    | **「固定」**定位 |

**「3. 静态定位(static)」**

- 静态定位是元素的默认定位方式，无定位的意思。它相当于border里面的none，不要定位的时候用。
- 静态定位 按照标准流特性摆放位置。它没有边偏移。
- 静态定位在布局时几乎不用

**「4. 相对定位(relative)」**

- 相对定位是元素相对于它原来在标准流中的位置来说的。![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)
- 相对于自己原来在标准流中位置来移动的
- 原来在标准流的区域继续占有，后面的盒子仍然以标准流的方式对待它。

**「5. 绝对定位(absolute)」**

绝对定位是元素以带有定位的父级元素来移动位置

- 完全脱表--完全不占位置；
- 父元素没有定位，则以浏览器为准定位(Document文档)。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 父元素有定位

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

##### 定位口诀--子绝父相

**「6. 固定定位(fixed)」**

固定定位是绝对定位的一种特殊形式;

- 完全脱标--完全不占位置；

- 只认**浏览器的可视窗口**--浏览器可视窗口+边偏移属性来设置元素的位置

- - 跟父元素没有任何关系；单独使用
  - 不随滚动条滚动

### 定位(position)的扩展

#### 绝对定位的盒子居中

> 绝对定位/固定定位的盒子不能通过设置margin: auto设置水平居中 在使用绝对定位时要向实现水平居中，可以按照下面的方法：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

1. left : 50%:让盒子的左侧移动到父级元素的水平中心位置；
2. margin-left: -100px;让盒子向左移动自身宽度的一半。
3. 同理垂直居中。

#### 堆叠顺序（z-index）

在使用**「定位」**布局时，可能会**「出现盒子重叠的情况」**。

加了定位的盒子，默认**「后来者居上」**， 后面的盒子会压住前面的盒子。

应用 `z-index` 层叠等级属性可以**「调整盒子的堆叠顺序」**。如下图所示：

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)z-index的特性如下:

1. **属性值**：正整数、负整数或 0，默认值是 0，数值越大，盒子越靠上；
2. 如果属性值相同，则按照书写顺序，后来居上；
3. 数字后面不能加单位
4. z-index只能用于相对定位、绝对定位和固定定位的元素，其他标准流、浮动和静态定位无效。

#### 定位改变display属性

前面提过， display 是 显示模式， 可以通过以下方式改变显示模式:

- 可以用inline-block  转换为行内块
- 可以用浮动 float 默认转换为行内块（类似，并不完全一样，因为浮动是脱标的）
- 绝对定位和固定定位也和浮动类似， 默认转换的特性 转换为行内块。

所以说， 一个行内的盒子，如果加了**「浮动」**、**「固定定位」**和**「绝对定位」**，不用转换，就可以给这个盒子直接设置宽度和高度等。

#### 定位小结

| 定位模式         | 是否脱标占有位置     | 移动位置基准           | 模式转换（行内块） | 使用情况                 |
| :--------------- | :------------------- | :--------------------- | :----------------- | :----------------------- |
| 静态static       | 不脱标，正常模式     | 正常模式               | 不能               | 几乎不用                 |
| 相对定位relative | 不脱标，占有位置     | 相对自身位置移动       | 不能               | 基本单独使用             |
| 绝对定位absolute | 完全脱标，不占有位置 | 相对于定位父级移动位置 | 能                 | 要和定位父级元素搭配使用 |
| 固定定位fixed    | 完全脱标，不占有位置 | 相对于浏览器移动位置   | 能                 | 单独使用，不需要父级     |

**注意：**

1. `边偏移` 需要和 `定位模式` 联合使用，`单独使用无效`；
2. `top` 和 `bottom` 不要同时使用；
3. `left` 和 `right` 不要同时使用。



------

## CSS高级技巧

### 元素的显示与隐藏

- **目的:**让一个元素在页面中消失或者显示出来
- **场景:**类似网站广告，当我们点击关闭就不见了，但是我们重新刷新页面，会重新出现！

#### 1.1 display 显示（重点）

display设置或检索对象是否显示或如何显示。

- display: none 隐藏对象

- - 特点：隐藏之后，不再保留位置。

- display: block 除了转换为块级元素之外，同时还有显示元素的意思。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)实际开发场景：配合后面js做特效，比如下拉菜单，原先没有，鼠标经过，显示下拉菜单， 应用极为广泛

#### 1.2 visibility 可见性

设置或检索是否显示对象

```
visibility：visible ;  对象可视

visibility：hidden;    对象隐藏
```

- 特点：隐藏之后，继续保留原有位置。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 1.3 overflow 溢出

检索或设置当对象的内容超过其指定高度及宽度时如何管理内容。

| 属性值  | 描述                                       |
| :------ | :----------------------------------------- |
| visible | 不剪切内容也不添加滚动条                   |
| hidden  | 不显示超过对象尺寸的内容，超出的部分隐藏掉 |
| scroll  | 不管超出内容否，总是显示滚动条             |
| auto    | 超出自动显示滚动条，不超出不显示滚动条     |

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)`实际开发场景`：

1. 清除浮动
2. 隐藏超出内容，隐藏掉,  不允许内容超过父盒子。

#### 1.4 显示与隐藏总结

| 属性       | 区别                   | 用途                                                         |
| :--------- | :--------------------- | :----------------------------------------------------------- |
| display    | 隐藏对象，不保留位置   | 配合后面js做特效，比如下拉菜单，原先没有，鼠标经过，显示下拉菜单， 应用极为广泛 |
| visibility | 隐藏对象，保留位置     | 使用较少                                                     |
| overflow   | 只是隐藏超出大小的部分 | 1. 可以清除浮动 2. 保证盒子里面的内容不会超出该盒子范围      |

### CSS用户界面样式

所谓的界面样式， 就是更改一些用户操作样式，以便提高更好的用户体验。

- 更改用户的鼠标样式
- 表单轮廓等。
- 防止表单域拖拽

#### 2.1 鼠标样式

设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。

| 属性值      | 描述       |
| :---------- | :--------- |
| default     | 小白  默认 |
| pointer     | 小手       |
| move        | 移动       |
| text        | 文本       |
| not-allowed | 禁止       |

```
<ul>
  <li style="cursor:default">我是小白</li>
  <li style="cursor:pointer">我是小手</li>
  <li style="cursor:move">我是移动</li>
  <li style="cursor:text">我是文本</li>
  <li style="cursor:not-allowed">我是文本</li>
</ul>
```

#### 2.2 轮廓线 outline

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

```
outline : outline-color ||outline-style || outline-width 
```

但是我们都不关心可以设置多少，我们平时都是去掉的。
最直接的写法是 ： outline: 0;  或者  outline: none;

#### 2.3 防止拖拽文本域resize

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
<textarea  style="resize: none;"></textarea>
```

#### 2.4 用户界面样式总结

| 属性     | 用途                 | 用途                                                         |
| :------- | :------------------- | :----------------------------------------------------------- |
| 鼠标样式 | 更改鼠标样式cursor   | 样式很多，重点记住 pointer                                   |
| 轮廓线   | 表单默认outline      | outline 轮廓线，我们一般直接去掉，border是边框，我们会经常用 |
| 防止拖拽 | 主要针对文本域resize | 防止用户随意拖拽文本域，造成页面布局混乱，我们resize:none    |

### vertical-align 垂直对齐

- 有宽度的块级元素居中对齐，是margin: 0 auto;
- 让文字居中对齐，是 text-align: center;

vertical-align 垂直对齐，它只针对于**「行内元素」**或者**「行内块元素」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
设置或检索对象内容的垂直对其方式。
vertical-align : baseline |top |middle |bottom 
```

注意：

vertical-align 不影响块级元素中的内容对齐，它只针对于**「行内元素」**或者**「行内块元素」**，

特别是行内块元素， 通常用来控制图片/表单与文字的对齐。

#### 3.1 图片、表单和文字对齐

我们可以通过`vertical-align` 控制图片和文字的垂直关系了。默认的图片会和文字基线对齐。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 3.2 去除图片底侧空白缝隙

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**原因：**图片或者表单等行内块元素，他的底线会和父级盒子的基线对齐。

就是图片底侧会有一个空白缝隙。

**解决方法：**

- 给img vertical-align:middle | top| bottom等等。 让图片不要和基线对齐。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 给img 添加 display：block; 转换为块级元素就不会存在问题了。

### 溢出的文字省略号显示

#### 4.1 white-space

- white-space设置或检索对象内文本显示方式。通常我们使用于强制一行显示内容

```
white-space:normal ；默认处理方式

white-space:nowrap ； 强制在同一行内显示所有文本，直到文本结束或者遭遇br标签对象才换行。
```

#### 4.2 text-overflow 文字溢出

- 设置或检索是否使用一个省略标记（...）标示对象内文本的溢出

```
text-overflow : clip ；不显示省略标记（...），而是简单的裁切 

text-overflow：ellipsis ； 当对象内文本溢出时显示省略标记（...）
```

**「注意」**：

一定要首先强制一行内显示，再次和overflow属性  搭配使用

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 4.3 总结三步曲

```
  /*1. 先强制一行内显示文本*/
      white-space: nowrap;
  /*2. 超出的部分隐藏*/
      overflow: hidden;
  /*3. 文字用省略号替代超出的部分*/
      text-overflow: ellipsis;
```

### CSS精灵技术（sprite)

CSS精灵技术（也称CSS Sprites、CSS雪碧）。![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 图所示为网页的请求原理图，当用户访问一个网站时，需要向服务器发送请求，网页上的每张图像都要经过一次请求才能展现给用户。
- 然而，一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接受和发送请求，这将大大降低页面的加载速度。

**为什么需要精灵技术**：为了有效地减少服务器接受和发送请求的次数，提高页面的加载速度。

#### 5.1 精灵技术讲解

CSS 精灵其实是将网页中的一些背景图像整合到一张大图中（精灵图），然而，各个网页元素通常只需要精灵图中不同位置的某个小图，要想精确定位到精灵图中的某个小图。

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)这样，当用户访问该页面时，只需向服务发送一次请求，网页中的背景图像即可全部展示出来。

我们需要使用CSS的:

- background-image、
- background-repeat
- background-position属性进行背景定位，
- 其中最关键的是使用`background-position` 属性精确地定位。

#### 5.2 精灵技术使用的核心总结

首先我们知道，css精灵技术主要针对于背景图片，插入的图片img 是不需要这个技术的。

1. 精确测量，每个小背景图片的大小和 位置。
2. 给盒子指定小背景图片时， 背景定位基本都是 负值。

### 滑动门

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

#### 6.1 滑动门出现的背景

制作网页时，为了美观，常常需要为网页元素设置特殊形状的背景，比如微信导航栏，有凸起和凹下去的感觉，最大的问题是里面的字数不一样多，咋办？

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)为了使各种特殊形状的背景能够自适应元素中文本内容的多少，出现了CSS滑动门技术。它从新的角度构建页面，使各种特殊形状的背景能够自由拉伸滑动，以适应元素内部的文本内容，可用性更强。最常见于各种导航栏的滑动门。

#### 6.2 核心技术

核心技术就是利用`CSS精灵`（主要是背景位置）和 `盒子padding`撑开宽度, 以便能适应不同字数的导航栏。

一般的经典布局都是这样的：

```
<li>
  <a href="#">
    <span>导航栏内容</span>
  </a>
</li>
* {
    padding:0;
    margin:0;

   }
    body{
      background: url(images/wx.jpg) repeat-x;
    }
    .father {
      padding-top:20px;
    }
    li {
      padding-left: 16px;
      height: 33px;
      float: left;
      line-height: 33px;
      margin:0  10px;
      background: url(./images/to.png) no-repeat left ;
    }
    a {
      padding-right: 16px;
      height: 33px;
      display: inline-block;
      color:#fff;
      background: url(./images/to.png) no-repeat right ;
      text-decoration: none;
    }
    li:hover,
    li:hover a {
      background-image:url(./images/ao.png);
    }
```

总结：

1. a 设置 背景左侧，padding撑开合适宽度。
2. span 设置背景右侧， padding撑开合适宽度 剩下由文字继续撑开宽度。
3. 之所以a包含span就是因为 整个导航都是可以点击的。

### CSS 三角形

```
div {

    width: 0; 

    height: 0;
    line-height:0；
    font-size: 0;
   border-top: 10px solid red;

   border-right: 10px solid green;

   border-bottom: 10px solid blue;

   border-left: 10px solid #000; 

     }
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

1. 我们用css 边框可以模拟三角效果
2. 宽度高度为0
3. 我们4个边框都要写， 只保留需要的边框颜色，其余的不能省略，都改为 transparent 透明就好了
4. 为了照顾兼容性 低版本的浏览器，加上 font-size: 0;  line-height: 0;







# 「查漏补缺」HTML与CSS进阶

原创 饭老板 [前端fan](javascript:void(0);) *2020-09-17*

收录于话题

\#CSS基础2

\#前端入门4

![图片](https://mmbiz.qpic.cn/mmbiz_png/y7EkeCWAzmpOOT8MBs9Ge1VUwKs31Ic5icj7ZL9jsXLS4Rd88uYdLsJ8Ns8wLicUDtRE5WgkhL8FVibCwjKkBp6Fw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**「查漏补缺」HTML与CSS进阶**

## 前言

本文主要介绍H5新增内容以及CSS3中的新特性。在H5方面主要介绍拓展了哪些内容，CSS3方面介绍动画及转换。

## H5新增内容

**「1. 什么是HTML5」**

- 定义：**HTML5**定义了**HTML**标准的最新版本，是对**HTML**的第五次重大修改，号称下一代的HTML。

- 两个概念：

- - 是一个新版本的**HTML**语言，定义了新的标签、特性和属性
  - 拥有一个强大的技术集，这些技术集是指：**HTML5、CSS3、JavaScript**,这也是广义上的HTML5。

**「2. HTML5拓展了哪些内容」**

- 语义化标签
- 本地存储
- 兼容特性
- 2D、3D
- 动画、过渡
- CSS3特性
- 性能与集成

**「3. HTML5的现状」**

绝大多数新的属性，都已经被浏览器所支持，最新版本的浏览器已经开始陆续支持最新的特性，总的来说：HTML5已经是大势所趋。

### HTML5新增标签

**「1. 什么是语义化」**

语义化是指用HTML写出符合**内容的结构化**（内容语义化），选择**合适的标签**（代码语义化），能够便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析。

**「2. 新增了哪些语义化标签」**

- `header`  ---  头部标签
- `nav`     ---  导航标签
- `article` ---  内容标签
- `section` ---  块级标签
- `aside`   ---  侧边栏标签
- `footer`  ---  尾部标签

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「3. 新增多媒体音频标签」**

- 多媒体标签有两个，分别是音频 **audio**和视频**video**。

- `audio 标签说明`

- - 可以在不使用标签的情况下，也能够原生的支持音频格式文件的播放，
  - 但是：播放的格式是**有限**的。

- `audio支持的音频格式`

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- audio 的参数

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
<audio controls>
    <!-- 注意：在 chrome 浏览器中已经禁用了 autoplay 属性 -->
    <!-- <audio src="./media/snow.mp3" controls autoplay></audio> -->
    <!-- 
    因为不同浏览器支持不同的格式，所以我们采取的方案是这个音频准备多个文件 -->                             
  <source src="myAudio.mp3" type="audio/mpeg">
  <source src="myAudio.ogg" type="audio/ogg">
  <p>Your browser doesn't support HTML5 audio. Here is
     a <a href="myAudio.mp4">link to the audio</a> instead.</p>
</audio>
```

**「4. 新增多媒体视频标签」**

- video视频标签目前支持三种格式

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 语法格式

```
<video src="./media/video.mp4" controls="controls"></video>
```

- video的参数

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- video代码演示

```
<body>
  <!-- <video src="./media/video.mp4" controls="controls"></video> -->

  <!-- 谷歌浏览器禁用了自动播放功能，如果想自动播放，需要添加 muted 属性 -->
  <video controls="controls" autoplay muted loop poster="./media/pig.jpg">
    <source src="./media/video.mp4" type="video/mp4">
    <source src="./media/video.ogg" type="video/ogg">
  </video>
</body>
```

- 多媒体标签总结

- - 音频标签和视频标签使用基本一致
  - 多媒体标签在不同浏览器下情况不同，存在兼容性问题
  - 谷歌浏览器把音频和视频标签的自动播放都**禁止**了
  - 谷歌浏览器中视频添加**muted**属性就可以自己播放了
  - 注意：重点记住使用方法及自动播放即可，其他属性在使用时查找对应的手册

**「5. 新增input标签」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「6. 新增表单属性」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

## CSS3新增

**「1. CSS3属性选择器」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
  button {
    cursor: pointer;
  }
  button[disabled] {
    cursor: default;
  }
  input[type=search] {
    color: skyblue;
  }

  span[class^=black] {
    color: lightgreen;
  }

  span[class$=black] {
    color: lightsalmon;
  }

  span[class*=black] {
    color: lightseagreen;
  }
```

**「2. 结构伪类选择器」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
ul li:first-child {
  background-color: lightseagreen;
}

ul li:last-child {
  background-color: lightcoral;
}

ul li:nth-child(3) {
  background-color: aqua;
}
```

- **nth-child(n)**参数n详解

- - 注意：本质上就是选中第几个子元素
  - n 可以是数字、关键字、公式
  - n 如果是数字，就是选中第几个
  - 常见的关键字有 `even` 偶数、`odd` 奇数
  - 常见的公式如下(如果 n 是公式，则从 0 开始计算)
  - 但是第 0 个元素或者超出了元素的个数会被忽略

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
<style>
  /* 偶数 */
  ul li:nth-child(even) {
    background-color: aquamarine;
  }

  /* 奇数 */
  ul li:nth-child(odd) {
    background-color: blueviolet;
  }

  /*n 是公式，从 0 开始计算 */
  ul li:nth-child(n) {
    background-color: lightcoral;
  }

  /* 偶数 */
  ul li:nth-child(2n) {
    background-color: lightskyblue;
  }

  /* 奇数 */
  ul li:nth-child(2n + 1) {
    background-color: lightsalmon;
  }

  /* 选择第 0 5 10 15, 应该怎么选 */
  ul li:nth-child(5n) {
    background-color: orangered;
  }

  /* n + 5 就是从第5个开始往后选择 */
  ul li:nth-child(n + 5) {
    background-color: peru;
  }

  /* -n + 5 前五个 */
  ul li:nth-child(-n + 5) {
    background-color: tan;
  }
</style>
```

- `nth-child与nth-of-type区别`

- - `nth-child` 选择父元素里面的第几个子元素，不管是第几个类型
  - `nth-of-type` 选择指定类型的元素

```
<style>
  div :nth-child(1) {
    background-color: lightblue;
  }

  div :nth-child(2) {
    background-color: lightpink;
  }

  div span:nth-of-type(2) {
    background-color: lightseagreen;
  }

  div span:nth-of-type(3) {
    background-color: #fff;
  }
</style>
```

**「3. 伪元素选择器」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

- 伪元素选择器注意事项

- - `before` 和 `after` 必须有 `content` 属性
  - `before` 在内容前面，after 在内容后面
  - `before` 和 `after` 创建的是一个元素，但是属于行内元素
  - 创建出来的元素在 `Dom` 中查找不到，所以称为伪元素
  - 伪元素和标签选择器一样，权重为 1

```
<style>
    div {
      width: 100px;
      height: 100px;
      border: 1px solid lightcoral;
    }

    div::after,
    div::before {
      width: 20px;
      height: 50px;
      text-align: center;
      display: inline-block;
    }
    div::after {
      content: '德';
      background-color: lightskyblue;
    }

    div::before {
      content: '道';
      background-color: mediumaquamarine;
    }
  </style>
```

##### 伪元素字体图标

```
p {
   position: relative;
   width: 220px;
   height: 22px;
   border: 1px solid lightseagreen;
   margin: 60px;

}
p::after {
  content: '\ea50';
  font-family: 'icomoon';
  position: absolute;
  top: -1px;
  right: 10px;
}
```

**「4. 2D 转换之translate」**

- **2D转换**

- - **2D**转换是改变标签在二维平面上的位置和形状
  - 移动：**translate**
  - 旋转：**rotate**
  - 缩放：**scale**

- translate语法

- - x就是X轴上水平移动
  - y就是y轴上水平移动

```
  transform: translate(x, y)
  transform: translateX(n)
  transfrom: translateY(n)  
```

- 重点知识点

- - 2D的移动主要是指水平、垂直方向上的移动
  - translate最大的优点就是**不影响**其他元素的位置
  - translate中的100%单位，是相对于**本身**的宽度和高度来进行计算的
  - 行内标签没有效果

```
div {
  background-color: lightseagreen;
  width: 200px;
  height: 100px;
  /* 平移 */
  /* 水平垂直移动 100px */
  /* transform: translate(100px, 100px); */

  /* 水平移动 100px */
  /* transform: translate(100px, 0) */

  /* 垂直移动 100px */
  /* transform: translate(0, 100px) */

  /* 水平移动 100px */
  /* transform: translateX(100px); */

  /* 垂直移动 100px */
  transform: translateY(100px);
  /*百分比用法*/
  transform: translateY(100%);   
}
```

##### 让一个盒子水平垂直居中

```
div {
    position: relative;
    width: 500px;
    height: 500px;
    background-color: pink;
    /* 1. 我们tranlate里面的参数是可以用 % */
    /* 2. 如果里面的参数是 % 移动的距离是 盒子自身的宽度或者高度来对比的 */
    /* 这里的 50% 就是 50px 因为盒子的宽度是 100px */
    /* transform: translateX(50%); */
    }
        
p {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 200px;
    height: 200px;
    background-color: purple;
    /1.* margin-top: -100px;
    margin-left: -100px; */
  
    /2.* translate(-50%, -50%)  
      盒子往上走自己高度的一半   */
    transform: translate(-50%, -50%);
  }
        
span {
    /* translate 对于行内元素是无效的 */
    transform: translate(300px, 300px);
     }
```

**「5. 2D 转换之rotate」**

- **rotate**旋转

- - 2D旋转指的是让元素在二维平面内顺时针或者逆时针旋转

```
/* 单位是：deg */
img:hover {
  transform: rotate(360deg)
}
```

- rotate语法

- - `rotate` 里面跟度数，单位是 `deg`
  - 角度为**正**时，顺时针，角度为负时，逆时针
  - 默认旋转的中心点是元素的中心点

- **设置元素旋转的中心的(transform-origin)**

```
  transform-origin: x y;
```

- `注意`

- - 后面的参数 x 和 y 用空格隔开
  - x y 默认旋转的中心点是元素的中心(50% 50%),等价于**center center**
  - 还可以给x y 设置像素或者方位名词(top、bottom、left、right、center)

**「6. 2D 转换之scale」**

- **scale**的作用：用来控制元素的放大与缩小

```
transform: scale(x, y)
```

- `知识要点：`

- - 注意，x与y之间用逗号进行分隔
  - `transform: scale(1, 1)`: 宽高都放大一倍，相当于没有放大
  - `transform: scale(2, 2)`: 宽和高都放大了二倍
  - `transform: scale(2)`: 如果只写了一个参数，第二个参数就和第一个参数一致
  - `transform:scale(0.5, 0.5)`: 缩小
  - `scale` 最大的优势：可以设置转换中心点缩放，默认以中心点缩放，而且不影响其他盒子

```
   div:hover {
    /* 注意，数字是倍数的含义，所以不需要加单位 */
    /* transform: scale(2, 2) */
   
    /* 实现等比缩放，同时修改宽与高 */
    /* transform: scale(2) */
   
    /* 小于 1 就等于缩放*/
    transform: scale(0.5, 0.5)
   }
```

**「7. 2D 转换综合写法以及顺序问题」**

##### 知识要点

- 同时使用多个转换，其格式为 `transform: translate() rotate() scale()`
- 顺序会影响到转换的效果(先旋转会改变坐标轴方向)
- 当我们同时有位置或者其他属性的时候，要将位移放到最前面

```
div:hover {
  transform: translate(200px, 0) rotate(360deg) scale(1.2)
}
```

### 动画(animation)

**「动画」**是CSS3中最具颠覆性的特征之一，可通过设置多个节点来精确的控制一个或者一组动画，从而实现复杂的动画效果。

**「动画的使用」**

1. 先**定义**动画
2. 再**调用**定义好的动画

```
/*1. 定义动画*/
@keyframes 动画名称 {
    0% {
        width: 100px;
    }
    100% {
        width: 200px
    }
}
div {
 /* 调用动画 */
  animation-name: 动画名称;
  /* 持续时间 */
  animation-duration: 持续时间；
}
```

**「动画序列」**

- 0% 是动画的开始，100 % 是动画的完成，这样的规则就是**动画序列**
- 在 **@keyframs**中规定某项 CSS 样式，就由创建当前样式**逐渐**改为新样式的动画效果
- 动画是使元素从一个样式逐渐变化为另一个样式的效果，可以改变任意多的样式任意多的次数
- 用百分比来规定变化发生的时间，或用 `from` 和 `to`，等同于 0% 和 100%

```
<style>
    div {
      width: 100px;
      height: 100px;
      background-color: aquamarine;
      animation-name: move;
      animation-duration: 0.5s;
    }

    @keyframes move{
      0% {
        transform: translate(0px)
      }
      100% {
        transform: translate(500px, 0)
      }
    }
  </style>
```

**「动画常见属性」**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
div {
  width: 100px;
  height: 100px;
  background-color: aquamarine;
  /* 动画名称 */
  animation-name: move;
  /* 动画花费时长 */
  animation-duration: 2s;
  /* 动画速度曲线 */
  animation-timing-function: ease-in-out;
  /* 动画等待多长时间执行 */
  animation-delay: 2s;
  /* 规定动画播放次数 infinite: 无限循环 */
  animation-iteration-count: infinite;
  /* 是否逆行播放 */
  animation-direction: alternate;
  /* 动画结束之后的状态 */
  animation-fill-mode: forwards;
}

div:hover {
  /* 规定动画是否暂停或者播放 */
  animation-play-state: paused;
}
```

**「动画简写方式」**

```
/* animation: 动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 起始与结束状态 */
animation: name duration timing-function delay iteration-count direction fill-mode
```

**知识要点**

- 简写属性里面不包含 `animation-paly-state`
- 暂停动画 `animation-paly-state: paused`; 经常和鼠标经过等其他配合使用
- 要想动画走回来，而不是直接调回来：`animation-direction: alternate`
- 盒子动画结束后，停在结束位置：`animation-fill-mode: forwards`

```
animation: move 2s linear 1s infinite alternate forwards;
```

**「速度曲线细节」**

`animation-timing-function`: 规定动画的速度曲线，默认是**ease**

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
/*打字机效果*/
div {
  width: 0px;
  height: 50px;
  line-height: 50px;
  white-space: nowrap;
  overflow: hidden;
  background-color: aquamarine;
  animation: move 4s steps(24) forwards;
}

@keyframes move {
  0% {
    width: 0px;
  }

  100% {
    width: 480px;
  }
}
```



### CSS 过渡transition

通过过渡**transition**，可以让web前端开发人员不需要javascript就可以实现简单的动画交互效果。

> `深入理解CSS过渡transition`
> https://www.cnblogs.com/xiaohuochai/p/5347930.html

**「定义」**过渡transition是一个复合属性，包括**transition-property**、**transition-duration**、**transition-timing-function**、**transition-delay**这四个子属性。通过这四个子属性的配合来完成一个完整的过渡效果。

```
transition-property: 过渡属性(默认值为all)
transition-duration: 过渡持续时间(默认值为0s)
transiton-timing-function: 过渡函数(默认值为ease函数)
transition-delay: 过渡延迟时间(默认值为0s)
.test{
    height: 100px;
    width: 100px;
    background-color: pink;
    transition-duration: 3s;
/*     以下三值为默认值，稍后会详细介绍 */
    transition-property: all;
    transition-timing-function: ease;
    transition-delay: 0s;
}    
.test:hover{
    width: 500px;
}
~~~html
<div class="test"></div>
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**「复合属性」**过渡transition的这四个子属性只有<transition-duration>是必需且不能为0。其中，<transition-duration>和<transition-delay>都是时间。当两个时间同时出现时，第一个是<transition-duration>，第二个是<transition-delay>；当只有一个时间时，它是<transition-duration>，而<transition-delay>为默认值0s

- **注意:**

- - transition的这四个子属性之间不能用逗号隔开，只能用空格隔开。因为逗号隔开的代表不同的属性(transition属性支持多值，多值部分稍后介绍)；而空格隔开的代表不同属性的四个关于过渡的子属性。

```
.test{
    height: 100px;
    width: 100px;
    background-color: pink;
/*代表持续时间为2s，延迟时间为默认值0s*/
    transition；2s;
}    
.test:hover{
    width: 500px;
}
<div class="test"></div>
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)`延迟时间delay 案例`

```
.test{
    height: 100px;
    width: 100px;
    background-color: pink;
    /*代表持续时间为1s，延迟时间为2s*/
    transition: 1s 2s;
}    
.test:hover{
    width: 500px;
}
<div class="test"></div>
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**「过渡属性」**

- 值: none | all | <transition-property>[,<transition-property>]
- 初始值: all
- 应用于: 所有元素
- 继承性: 无

```
  none: 没有指定任何样式
  all: 默认值，表示指定元素所有支持transition-property属性的样式
  <transition-property>: 可过渡的样式，可用逗号分开写多个样式
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

**「过渡持续时间」**

- 值: <time>[,<time>]*
- 初始值: 0s
- 应用于: 所有元素
- 继承性: 无
- [注意]该属性不能为负值
- [注意]若该属性为0s则为默认值，若为0则为无效值。所以必须**带单位**
- [注意]该值为单值时，即所有过渡属性都对应同样时间；该值为多值时，过渡属性按照顺序对应持续时间

```
/*DEMO中的过渡属性值*/
transition-property: width,background;
```

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)**「过渡时间函数」**

**过渡时间函数**用于定义元素过渡属性随时间变化的过渡速度变化效果

- 值: <timing-function>[,<timing-function>]*
- 初始值: **ease**
- 应用于: 所有元素
- 继承性: 无

**「取值」** 过渡时间函数共三种取值，分别是**关键字**、**steps函数**和**bezier函数**

**「关键字」**其实是bezier函数或steps函数的特殊值

```
ease: 开始和结束慢，中间快。
linear: 匀速。
ease-in: 开始慢。
ease-out: 结束慢。
ease-in-out: 和ease类似，但比ease幅度大。
```

------

## 3D转换

### 认识3D转换

**「3D的特点」**近大远小，物体和面遮挡不可见

**「三维坐标系」**

- x 轴：水平向右  -- `注意：x 轴右边是正值，左边是负值`
- y 轴：垂直向下  -- `注意：y 轴下面是正值，上面是负值`
- z 轴：垂直屏幕  --  `注意：往外边的是正值，往里面的是负值`

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

### 3D转换

**1. 3D 转换知识要点**

- `3D` 位移：`translate3d(x, y, z)`
- `3D` 旋转：`rotate3d(x, y, z)`
- `透视` ：`perspctive`
- `3D`呈现 `transfrom-style`

**2. 3D 移动translate3d**

- `3D` 移动就是在 `2D` 移动的基础上多加了一个可以移动的方向，就是 z 轴方向
- `transform: translateX(100px)`：仅仅是在 x 轴上移动
- `transform: translateY(100px)`：仅仅是在 y 轴上移动
- `transform: translateZ(100px)`：仅仅是在 z 轴上移动
- `transform: translate3d(x, y, z)`：其中x、y、z 分别指要移动的轴的方向的距离
- `注意：x, y, z 对应的值不能省略，不需要填写用 0 进行填充`

```
  transform: translate3d(100px, 100px, 100px)
  /* 注意：x, y, z 对应的值不能省略，不需要填写用 0 进行填充 */
  transform: translate3d(100px, 100px, 0)
```

### 透视perspective

- 知识点讲解

- - 如果想要网页产生 `3D` 效果需要透视(理解成 `3D` 物体投影的 `2D` 平面上)
  - 实际上模仿人类的视觉位置，可视为安排一只眼睛去看
  - 透视也称为视距，所谓的视距就是人的眼睛到屏幕的距离
  - 距离视觉点越近的在电脑平面成像越大，越远成像越小
  - 透视的单位是像素

- 知识要点

- - **透视需要写在被视察元素的父盒子上面**
  - 注意下方图片
  - d：就是视距，视距就是指人的眼睛到屏幕的距离
  - z：就是 z 轴，z 轴越大(正值)，我们看到的物体就越大

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)代码演示

```
body {
  /*透视需要写在被视察元素的父盒子上面 */
  perspective: 1000px;
}
translateZ与perspective的区别
```

- `perspecitve` 给父级进行设置视距的，`translateZ` 给 子元素进行设置不同的大小

### 3D 旋转rotateX

**3D 旋转**指可以让元素在三维平面内沿着 x 轴、y 轴、z 轴 或者自定义轴进行旋转

- `语法：`

- - **transform: rotateX(45deg)** -- 沿着 x 轴正方向旋转 45 度
  - **transform: rotateY(45deg)** -- 沿着 y 轴正方向旋转 45 度
  - **transform: rotateZ(45deg)** -- 沿着 z 轴正方向旋转 45 度
  - **transform: rotate3d(x, y, z, 45deg)** -- 沿着自定义轴旋转 45 deg 为角度

- `左手法则：`

- - 左手的手拇指指向 x 轴的正方向
  - 其余手指的弯曲方向就是该元素沿着 x 轴旋转的方向

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
div {
  /*透视写在被视察元素的父盒子上面 */
  perspective: 300px;
}
/*被观察元素*/
img {
  display: block;
  margin: 100px auto;
  transition: all 1s;
}

img:hover {
  transform: rotateX(-45deg)
}
```

### 3D 旋转rotateY

- `左手法则：`

- - 左手的拇指指向 y 轴的正方向
  - 其余的手指弯曲方向就是该元素沿着 y 轴旋转的方向(正值)

![图片](data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg==)

```
div {
  perspective: 500px;
}

img {
  display: block;
  margin: 100px auto;
  transition: all 1s;
}

img:hover {
  transform: rotateY(180deg)
}
```

### 3D 旋转rotateZ

```
div {
  perspective: 500px;
}

img {
  display: block;
  margin: 100px auto;
  transition: all 1s;
}

img:hover {
  transform: rotateZ(180deg)
}
```

**「rotate3d」**

- **transform: rotate3d(x, y, z, deg)** -- 沿着自定义轴旋转 deg 为角度

- x, y, z 表示旋转轴的矢量，是标识你是否希望沿着该轴进行旋转，最后一个标识旋转的角度

- - **transform: rotate3d(1, 1, 0, 180deg)** -- 沿着对角线旋转 45deg
  - **transform: rotate3d(1, 0, 0, 180deg)** -- 沿着 x 轴旋转 45deg

```
div {
  perspective: 500px;
}

img {
  display: block;
  margin: 100px auto;
  transition: all 1s;
}

img:hover {
  transform: rotate3d(1, 1, 0, 180deg)
}
```

### 3D呈现transform-style

- 控制子元素是否开启三维立体环境
- `transform-style: flat` 代表子元素不开启 `3D` 立体空间，默认的
- `transform-style: preserve-3d` 子元素开启立体空间
- 代码写给父级，但是影响的是子盒子

```
<body>
    <div class="box">
        <div></div>
        <div></div>
    </div>
</body>
<style>
    body {
        perspective: 500px;
        }
        
    .box {
        position: relative;
        width: 200px;
        height: 200px;
        margin: 100px auto;
        transition: all 2s;
        /* 让子元素保持3d立体空间环境 */
        transform-style: preserve-3d;
        }
        
    .box:hover {
        transform: rotateY(60deg);
    }
        
    .box div {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: pink;
    }
        
    .box div:last-child {
        background-color: purple;
        transform: rotateX(60deg);
    }
</style>
```









