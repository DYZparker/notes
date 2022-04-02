



css3被划分为模块，最重要的几个模块包括：选择器、框模型、背景和边框、文本效果、2D/3D 转换、动画、多列布局、用户界面

### border边框

新增属性	说明
border-radius	边框圆角
border-shadow	边框阴影
border-image	边框图片
background-size	规定背景图片的尺寸
border-origin	规定背景图片的定位区域
border-clip	规定背景的绘制区域

### 文本效果(常用)

text-shadow：设置文字阴影

word-wrap：强制换行

word-break：规定自动换行的处理方法

css3提出@font-face规则，规则中定义了font-family、font-weight、font-style、font-stretch、src、unicode-range

### 2/3D转换

transform：向元素应用2/3D转换

transition：过渡

### 动画

@keyframes规则：

animation、animation-name、animation-duration等

### 用户界面(常用)

box-sizing、resize

### css3新增伪类

：nth-child()

：nth-last-child()

：only-child

：last-child

：nth-of-type()

：only-of-type()

：empty

：target 这个伪类允许我们选择基于URL的元素，如果这个元素有一个识别器(比如跟着一个#)，那么:target会对使用这个ID识别器的元素增加样式。

：enabled

：disabled

：checked

：not
————————————————



**零. transition（a标签hover渐隐效果）**

 a:hover{transition: color 0.15s linear 0s, background-color 0.3s linear 0s;}

-webkit-transition:color 0.15s linear 0s, background-color 0.3s linear 0s;

-moz-transition:color 0.15s linear 0s, background-color 0.3s linear 0s;

-o-transition:color 0.15s linear 0s, background-color 0.3s linear 0s;

-ms-transition:color 0.15s linear 0s, background-color 0.3s linear 0s;

transition:color 0.15s linear 0s, background-color 0.3s linear 0s;

**一. box-shadow(阴影效果)**

使用:
box-shadow: 20px 10px 0 #000;

-moz-box-shadow: 20px 10px 0 #000;

-webkit-box-shadow: 20px 10px 0 #000;

支持: 
    FF3.5, Safari 4, Chrome 3

 
**二. border-colors(为边框设置多种颜色)**

使用:
    border: 10px solid #000; 
    -moz-border-bottom-colors: #555 #666 #777 #888 #999 #aaa #bbb #ccc; 
    -moz-border-top-colors: #555 #666 #777 #888 #999 #aaa #bbb #ccc; 
    -moz-border-left-colors: #555 #666 #777 #888 #999 #aaa #bbb #ccc; 
    -moz-border-right-colors: #555 #666 #777 #888 #999 #aaa #bbb #ccc;

说明: 
    颜色值数量不固定, 且FF的私有写法不支持缩写: -moz-border-colors: #333 #444 #555;

支持:
    FF3+
 
 
**三. boder-image(图片边框)**

使用:
    -moz-border-image: url(exam.png) 20 20 20 20 repeat;

​    -webkit-border-image: url(exam.png) 20 20 20 20 repeat;

说明:
(1). 20 20 20 20 ---> 边框的宽度, 分别对应top, right, bottom, left边框, 改变宽度可以实现不同的效果;

(2). 边框图片效果(目前仅实现了两种): 

​    repeat --- 边框图片会平铺, 类似于背景重复;

​    stretch --- 边框图片会以拉伸的方式来铺满整个边框;

(3). 必须将元素的边框厚度设置为非0非auto值.

支持:
    FF 3.5, Safari 4, Chrome 3

 
**四. text-shadow(文本阴影)**

使用: 
    text-shadow: [<颜色><水平偏移><纵向偏移><模糊半径>] || [<水平偏移><纵向偏移><模糊半径><颜色>];

说明:
(1) <颜色>和<模糊半径>是可选的, 当<颜色>未指定时, 将使用文本颜色; 当<模糊半径>未指定时, 半径值为0;

(2) shadow可以是逗号分隔的列表, 如:

   text-shadow: 2px 2px 2px #ccc, 3px 3px 3px #ddd;

(3) 阴影效果会按照shadow list中指定的顺序应用到元素上;

(4) 这些阴影效果有可能相互重叠, 但不会叠加文本本身;

(5) 阴影可能会跑到容器的边界之外, 但不会影响容器的大小.

支持:
    FF 3.5, Opera 10, Safari 4, Chrome 3

**五. text-overflow(文本截断)**

使用:
    text-overflow: inherit | ellipsis | clip ;

​    -o-text-overflow: inherit | ellipsis | clip;

说明: 
(1) 还有一个属性ellipsis-word, 但各浏览器均不支持.

支持: 
    IE6+, Safari4, Chrome3, Opera10

**六. word-wrap(自动换行)**

使用:
    word-wrap: normal | break-word;

支持:
    IE6+, FF 3.5, Safari 4, Chrome 3

**七. border-radius(圆角边框)**

使用:
     -moz-border-radius: 5px;

-webkit-border-radius: 5px;

支持:
FF 3+,  Safari 4 , Chrome 3 

 
 
**八.  opacity(不透明度)**  

使用:
    opacity: 0.5;

​    filter: alpha(opacity=50); /* for IE6, 7 */

​    -ms-filter(opacity=50); /* for IE8 */

支持:
    all
**九. box-sizing(控制盒模型的组成模式)**

使用:
    box-sizing: content-box | border-box; // for opera

​    -moz-box-sizing: content-box | border-box;

​    -webkit-box-sizing: content-box | border-box;

说明:
    \1. content-box: 

​    使用此值时, 盒模型的组成模式是, 元素宽度 = content + padding + border;

​    \2. border-box: 

​    使用此值时, 盒模型的组成模式是, 元素宽度 = content(即使设置了padding和border, 元素的宽度

​    也不会变).

支持:
    FF3+, Opera 10, Safari 4, Chrome 3

 
**十. resize(元素缩放)**

使用: 
    resize: none | both | horizontal | vertical;

说明:
    \1. 必须将元素的overflow属性设置为auto或hidden, 该属性才能起作用(overflow设置为visible时, 无效);

​    \2. 属性值说明:

​    (1). none --> 禁用缩放;

​    (2). both --> 可同时缩放宽度和高度;

​    (3). horizontal --> 仅能缩放宽度;

​    (4). vertical --> 仅能缩放高度;

支持:
    safari 4, chrome 3

**十一. outline(外边框)**

使用:
    outline: 边框厚度 边框样式 边框颜色;

​    outline-offset: 偏移值;

说明:
    outline-offset需要独立写, 简写是无效的.

支持:
    FF3+, safari 4, chrome 3, opera 10

**十二. background-size(指定背景图片的尺寸)**

使用:
    -o-background-size: [length | percentage] {1, 2};

​    -webkit-background-size: [length | percentage] {1, 2};

例如:
    -o-background-size: 50px 60px;

​    -webkit-background-size: 50px 60px;

​    这会将背景图片的宽设置了50px, 高60px.

支持:
     safari 4, chrome 3, opera 10  

 
 
**十三. background-origin(指定背景图片从哪里开始显示)** 

使用: 
    -webkit-background-origin: border | padding | content;

​    -moz-background-origin: border | padding | content; 

说明:
    (1) border --> 从border区域开始显示背景;

​    (2) padding --> 从padding区域开始显示背景;

​    (3) content --> 从content区域开始显示背景;

注意:
    \1. 必须先指定background属性, 然后才能指定该属性, 如果该属性出现在background属性之前, 

会无效.
支持:
     safari 4, chrome 3, FF 3+      

**十四. background-clip(指定背景图片从什么位置开始裁切)**

使用: 
    -webkit-background-origin: border-box | padding-box | content-box | no-clip;

说明:
    (1) border-box --> 从border区域向外裁剪背景;

​    (2) padding-box --> 从padding区域向外裁剪背景;

​    (3) content-box --> 从content区域向外裁剪背景;

​    (4) no-clip --> 不裁切背景.

注意:
    \1. 必须先指定background属性, 然后才能指定该属性, 如果该属性出现在background属性之前, 

会无效.
支持:
     safari 4, chrome 3

**十五.  background(为一个元素指定多个背景)**

使用: 
    background: [background-image] | [background-origin] | [background-clip] |[background-repeat] | [background-size] | [background-position]

例子:
    background: url(bg1.png) no-repeat left top, url(bg2.png) no-repeat right bottom;

支持:
     safari 4, chrome 3

**十六. hsl(通过色调, 饱和度, 亮度来指定颜色值)**

使用:
    hsl: ( <length> || <percentage> || <percentage>);

说明:
    (1) length: h(色调),  0(或360)表示红色, 120表示绿色, 240表示蓝色;

​    (2) percentage: s(饱和度),  取值为0%到100%之间的值;

​    (3) percentage: l(亮度),  取值为0%到100%之间的值;

例子:
    background: hsl(240, 50%, 100%);

​    color: hsl(100, 80, 100%);

支持:
     safari 4, chrome 3, FF3, opera 10

**十七. hsla(在hsl的基础上上增加了一个透明度设置)**

使用:
    hsla: ( <length> || <percentage> || <percentage> || <opacity>);

说明:
    (1) opacity: a(透明度), 取值在0到1之间;

例子:
    background: hsl(240, 50%, 100%, 0.5);

​    color: hsl(240, 50%, 100%, 0.5);

支持:
     safari 4, chrome 3, FF3, opera 10

**十八. rgba(基于r,g,b三个颜色通道来设置颜色值, 通过a来设置透明度)**

使用:
    rgba: (r, g, b, opacity);

说明:
    (1) r: 红色, 正整数 | 百分数;

​    (2) g: 绿色, 正整数 | 百分数;

​    (3) b: 蓝色, 正整数 | 百分数;

​    (4) a: 透明度, 取值在0到1之间;

​    (5) 正整数在0到255之间, 百分数在0%到100%之间.

例子:
    rgba: (100%, 244, 0, 0.5);

支持:
     safari 4, chrome 3, FF3, opera 10