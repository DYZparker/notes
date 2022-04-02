# CSS基础

#### 引入方法

1. 行内样式：开始标签内style属性

2. 内部样式：`<head>`中`<style>`内

3. 外部样式：`<link href="" rel="stylesheet" type="text/css">`（页面和CSS同时加载）

4. 导入式：在样式代码最开始处@import（页面加载完后再加载CSS）

5. 优先级：行内样式>内部样式>导入式/外部样式（style表中最下面优先）

6. 自定义class

#### 页面结构

- 页头：header
- 页面主体：main
- 页尾：footer
- 内容：content
- 容器：container
- 导航：nav
- 侧栏：sidebar
- 栏目：column
- 页面外围控制：wrapper

#### 导航

- 主导航：mainnav
- 子导航：subnav
- 顶导航：topnav
- 边导航：sidebar
- 菜单：menu
- 子菜单：submenu
- 摘要：summary

#### 功能

- 标志：logo
- 广告：banner
- 登录：login
- 登录条：loginbar
- 注册：register
- 搜索：search
- 功能区：shop
- 标题：title

#### 指针样式cursor

- default默认光标

- auto浏览器默认光标

- pointer链接小手

#### 轮廓

- input输入框的border

- outline: out-width out-style out-color

- outline: none

#### 取消拖拽

- 输入框取消拖拽大小

- resize: none

#### 滑动门

- 核心技术是利用CSS精灵(主要是背景位置)和盒子padding撑开宽度，以便适应不同字数的导航栏

- ```html
  <li>
      <a href="#">
          <span>导航栏内容</span>
      </a>
  </li>
  ```

- a设置背景左侧，padding撑开合适宽度

- span设置背景右侧，padding撑开合适宽度，剩下由文字继续撑开宽度

  

# CSS样式

## 字体

#### font

- font-family:"字体1","字体2",字体集
- font-size:

  - 绝对单位：xx-small/x-small/small/medium/large/x-large/xx-large
  - 相对单位

    - px：受显示器分辨率影响
    - em和%：针对父元素

- font-weight:

  - normal（400）
  - bold（700）
  - bolder
  - lighter
  - 100~900

- font-style:

  - normal
  - italic：斜体
  - oblique：倾斜

- font-variant:字体变形

  - normal
  - small-caps：将单词全部转换成小型的大写

- font缩写：顺序固定style, variant, weight, size/line-height, family

  - size和family必须写

#### color

- 颜色单词：
- RGB：rgb(0,100,255)
- 十六进制：#f0f0f0

#### CSS3

- rgba(R,G,B,A透明度0~1)
- 渐变色彩

  - 线性渐变

    - linear-gradient(方向(角度90deg/英文to top), 起点颜色#999, 结束颜色#666(颜色可为多个，且可用长度或百分比添加起止色位置))

      - transparent  透明色

    - repeating-linear-gradient（语法同上）

      - 重复的线性渐变

  - 径向渐变

    - radial-gradient([<起点>]?[<形状>||<大小>]?<点>,<点>...)
    - 起点：可以是关键字（left,top,right,bottom）,具体数值或百分比
    - 形状：ellipse、circle
    - 大小：具体数值或百分比，也可以是关键字（最近段closest-side，最近角closest-corner，最远端farthest-side，最远角farthest-corner，包含contain，覆盖cover）

## 文本

#### text-align

（对块级元素有效）

- left
- right
- center
- justify：两端对齐

#### vertical-align

垂直对齐方式（对行内元素/单元格有效）

- super：上标
- sub：下标
- top：顶部对齐
- text-top：顶线对齐
- middle：中线对齐
- baseline：基线对齐
- text-bottom：底线对齐
- bottom：底部对齐
- 长度值

  - 正值px向上移
  - 负值px向下移

- 百分比

  - 正%向上移
  - 负%向下移

#### 水平垂直居中

- 单行：1，子块元素line-height行高和父元素height一样；2，子块元素text-align:center;
- 多行：1，父块元素display:table；2，子块元素display:table-cell;text-align:center;vertical-align:middle;

#### line-height

文本行高

- 长度值
- em或%（推荐）

#### text-decoration

文本修饰

- underline下划线
- overline上划线
- line-through中划线
- blink闪烁效果
- none

#### text-transform

文本大小写

- capitalize首字母大写
- uppercase全部大写
- lowercase全部小写
- none

#### word-spacing

元素内单词之间间距（以空格判断）

#### letter-spacing

元素内字母之间间距

#### text-indent

首行缩进

#### 溢出的文字隐藏

- word-break

  - 处理英文单词
  - normal

    - 使用浏览器默认的换行规则

  - break-all

    - 允许在单词内换行

  - keep-all

    - 只能在半角空格或连字符处换行

- white-space

  - normal

    - 默认处理方式

  - nowrap

    - 强制在同一行显示所有文本

- text-overflow

  - 要和white-space: nowrapl overflow: hidden;搭配使用
  - clip

    - 不显示省略号，而是简单的裁剪

  - ellipsis

    - 溢出时显示省略号

#### CSS3

- 文本阴影

  - text-shadow: X-Offset Y-Offset blur color;（前三个参数单位px，可多层阴影，之间用逗号隔开）

- 文本描边

  - -webkit-text-stroke: 3px color

- 文本排版

  - direction

    - rtl 从右向左排列
    - ltr 从左向右排列

  - unicode-bidi：bidi-override

    - 文本倒序

- 省略标记

  - text-overflow: clip(剪切) | ellipsis(显示省略标记)

- 显示省略号

  - text-overflow:ellipsis;

    - 要配合overflow:hidden和white-space:nowrap一起使用

- 溢出内容隐藏

  - overflow:hidden; 

- 强制文本在一行

  - white-space:nowrap;

- 文本行为

  - word-wrap: normal(控制连续文本换行) | break-word(内容在边界内换行)

- 嵌入字体

  - @font-face {
    font-family : 字体名称;
    src : 字体文件在服务器上的相对或绝对路径;
    }

## 背景

#### 原始起始位置

- background-origin ： border-box(边框) | padding-box(内边距默认) | content-box(内容区域);
- ps：此属性必须背景no-repeat

#### 剪裁

- background-clip ：

  - border-box(默认，边框向里有背景)
  - padding-box(内填充向里有背景)
  - content-box(只有内容区域有背景)
  - no-clip(不裁剪)

- ps：图片从边框开始，从clip位置显示

#### 大小

- background-size: 

  - auto(默认不改变)
  - <长度值>(宽px、高px)
  - <百分比>(宽%、高%) 
  - cover(图像等比缩放到完全覆盖容器，图像超出部分会被隐藏)
  - contain(图像等比缩放到宽度或高度与容器的宽度或高度相等，图像始终被包含在容器内)

#### 颜色

- background-color

#### 图片

- background-image：url(...)

#### 位置

- background-position 图像起始位置

  - top
  - right
  - bottom
  - left
  - center
  - 水平和垂直百分比（x%，y%）
  - 水平和垂直值 （x，y）

#### 重复

- background-repeat

  - repeat
  - repeat-x
  - repeat-y
  - no-repeat

#### 滚动

- background-attachment

  - scroll 随滚动条滚动
  - fixed 不会移动（相对于网页位置）

#### 滤镜

- filter： blur(px)

  - 元素和里面的子元素全部都会被滤镜

#### 遮罩

- mask-image
- mask-position
- mask-repeat

#### 不透明度

- 标准浏览器

  - opacity:0~1;

- IEl滤镜

  - filter:alpha(opacity=0~100);

#### 旋转图片

- transform:rotate(*deg);

#### 简写

- background 缩写：无顺序，无数量限制，空格隔开



# CSS3选择器

## 通用选择器

1. 标签

2. 类：.class

3. ID：#id

4. 全局：*通配符

5. 群组：选择器之间用逗号隔开

6. 后代：父级和子级用空格隔开（父级可以是标签/#id/标签.class）

7. 伪类

   - 链接伪类（顺序不能变）

     - :link 未访问的链接

     - :visited 已访问的链接

     - :hover 鼠标悬停状态

     - :active 激活的链接

8. 优先级：!important>ID>类>标签（同级看在style表中最下面优先）

9. 权值

   - 通配符：0

   - 标签：1

   - 类和伪类：10

   - ID：100

   - 行内样式：1000

   - !important

## 属性选择器

#### E[attr]

- 属性名

#### E[attr=val]

- 属性名和值

#### E[attr~=val]

- 在一个属性值列表中包含一项val

#### E[attr^=val]

- 属性值是以val开头

#### E[attr$=val]

- 属性值是以val结尾

#### E[attr*=val]

- 属性值中包含了val

#### E[attr|=val]

- 属性值是val或者以val-开头的值

## 结构性伪类选择器

#### 根选择器

- :root

  - 匹配元素E所在文档的根元素。在HTML文档中，根元素始终是<html>。

#### 否定选择器

- :not

  - 选择除某个元素之外的所有元素

#### 空选择器

- :empty

  - 选择没有任何内容的元素

#### 目标选择器

- :target

  - 匹配文档(页面)的url的某个标志符的目标元素（#hash值）

#### 无类型差别

- :first-child

  - 定位父元素的第一个子元素

- :last-child

  - 定位父元素的最后一个子元素

- :nth-child(n)

  - 定位父元素的一个或多个特定的子元素
  - n可以为整数，倍数2n，关键字odd、even
  - ps：整数的起始值为1，表达式中n的起始值为0

- :nth-last-child(n)

  - 从某父元素的最后一个子元素开始计算，来选择特定的元素

- :only-child

  - 定位父元素下有且仅有一个的子元素

- PS：如找到的元素不是此类型则无效

#### 有类型差别

- :first-of-type

  - 定位父元素下的某个类型的第一个子元素

- :last-of-type

  - 定位父元素下的某个类型的最后一个子元素

- :nth-of-type(n)

  - 定位父元素下的某个类型的子元素

- :nth-last-of-type(n)

  - 从某父元素的最后一个某类子元素开始计算，来选择特定的元素

- :only-of-type

  - 定位父元素下有且仅有一个类型的子元素（可由多种其他类型元素）

## 其他选择器

#### :enabled

- 定位可用状态下的表单元素

#### :disabled

- 定位不可用状态下的表单元素

#### :checked

- 定位选中状态下的单选或复选按钮

####  :read-only

- 定位只读状态的元素，即元素中设置了“readonly=’readonly’”

#### :read-write

- 定位非只读状态的元素

#### ::selection

- 定位用鼠标拖拽覆盖后的文本（默认样式：深蓝的背景，白色的字体）

#### ::before

- 给元素前面插入内容

#### ::after

- 子给元素后面插入内容

#### +

- 元素的下一个兄弟元素

#### ~

- 元素后面的兄弟元素

#### p::first-line

- p元素下的第一行文本

#### p::first-letter

- p元素下的第一个文字

