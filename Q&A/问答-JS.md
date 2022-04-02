### 如何理解执行上下文？

主要指代码执行环境的抽象概念，

每一段代码执行都会先创建一个上下文环境，包含了变量、作用域链和this

执行上下文分为三种：全局执行上下文、函数执行上下文、eval执行上下文

### 如何理解作用域链？

就是从当前环境向父级一层一层查找变量的过程

### 如何理解原型链？

每个函数都有一个prototype属性，每个实例对象都有一个```__proto__```属性并指向函数的prototype，当我们访问实例对象的属性和方法时，会先从自身查找，如果没有就通过```__proto__```去原型链中查找，这个查找的过程就是原型链

### 什么是闭包？

解析：

### 继承有哪些方法？

- 原型继承
- 构造继承
- 实例继承
- 组合继承（call/apply继承）
- ES6使用class extends继承

### 什么深/浅拷贝？有哪些方式？

JS数据类型分为基本类型和引用类型，基本类型保存的是值，引用类型保存的是引用地址

浅拷贝共用一个引用地址，深拷贝会创建新的内存地址

浅拷贝方法：

- 直接对象复制

			- Object.assign()

深拷贝：

- JSON.stringify转为字符串再JSON.parse
- 深度递归遍历

### 如何准确判断一个对象是数组？

Object.prototype.toString.call(对象)返回""[Object Array]"

扩展：对象 instanceof Array可类型判断

​			Array.isArray()存在兼容性问题

### 数组有哪些常用方法？

改变原数组的方法：push\unshift\pop\shift\reverse\splice\sort

不改变原数组的方法：concat\every\some\map\fliter\forEach\slice\reduce\join\indexOf\includes

### DOM节点创建和修改有哪些常用API？

创建：document.createElement\createTextNode\DocumentFragment(临时节点)

修改：appendChild\insertBefore\removeChild\replaceChild

### CSS清除浮动有哪些方法？

- 浮动元素结尾增加空标签，设置clear: both
- 父元素设置overflow: hidden
- 父元素设置高度，手动撑开
- 父元素添加伪类：after和 zoom

### CSS选择器优先级？

!important>行内样式>id选择器>类/属性/伪类>元素/关系

### CSS实现三列布局（左右固定宽度，中间自适应）

- CSS浮动

  第一个float: left;第二个float: right;第三个设置margin-left和margin-right

- 绝对定位法

  第一个定位到left，第二个定位到right，第三个设置margin-left和margin-right

- flex布局

  ？？？？？？？？？？？？？？？？

### 谈一下flex布局

flex是一种弹性布局，包含flex-container和flex-item

常用的属性包括：flex-direction\flex-justify-content\align-items

水平居中：justify-content: center

水平两头居中：justify-content: space-between

垂直居中：align-items: center

### 谈一下盒模型

盒模型包括：content\padding\border\margin

盒模型分为：IE盒模型和标准W3C盒模型

IE盒模型宽度包含了padding和border，W3C盒模型宽度就是内容宽度

### transition动画和animation有什么区别？

都可以做出动画效果，但transition主要做简单的过度效果，而animation可以做复杂的动画效果，在语法和用法上有非常大的区别

### H5自适应方案

rem：是一种相对单位，它基于html的font-size值来进行调整

### call\apply\bind作用和区别？

都可以改变函数的作用域

call和apply可以直接执行该函数，bind不会立刻执行

call的第二个参数是参数列表，apply的第二个参数是数组

### 观察者和发布订阅者区别？

它们都属于观察者模式，只不过有不同的实现方法

发布订阅相比观察者多了一个调度中心，发布者通过调度中心向订阅者发布消息

观察者模式中目标和观察者相互依赖，观察者订阅目标主题，当目标发生变化后，会通知对应观察者

？？？？？？？？？？

### 浏览器解析渲染页面过程

- 解析HTML,生成DOM树
- 解析CSS，生成CSSOM树
- 将DOM树和CSSOM树关联，生成渲染树（Render Tree）
- 布局render树（Layout/reflow），负责个元素尺寸、位置的计算
- 绘制render树（paint），绘制页面像素信息
- 将像素发送给GPU，展示在页面上（Display）

### 谈一下EventLoop

JS本身是单线程，同一时刻只能干一件事，JS任务包含了同步任务和异步任务，遇到执行函数会将其放入调用栈（先进后出），遇到setTimeout/setInterval等异步任务时，会把它放入到消息队列中，等主线程的任务执行完成以后，再回过头执行消息队列中的异步任务，如果异步任务中仍然有异步任务，会继续放入消息队列，以此类推，便形成了一个事件循环

### GET和POST有什么区别？

- 大小方面

  GET传输一般2K~8K，IE限制2K，POST没有大小限制

- 安全方面

  GET通过url明文传输，POST通过body传输，本身都不安全，因为HTTP就是明文传输

- 浏览器记录

  GET请求浏览器会记录，POST不会

- 浏览器后退

  GET无害，POST会再次提交

- 浏览器收藏

  GET可以收藏，POST不可以

- 浏览器缓存

  GET可以缓存，POST不会

- 编码方式

  GET通过url编码，POST支持多种编码

- TCP数据包

  GET产生一个数据包，POST产生两个数据包

- 使用方式

  GET主要拉取数据，POST主要提交数据

### 谈一下防抖和节流

防抖和节流都是希望在同一时间内不要重复出发请求，一般用在搜索和网页滚动事件

区别：

防抖主要是在规定时间内触发一次，如果再次调用，时间从新计算

节流主要是在固定时间内只触发一次，比如每间隔一秒触发一次

### 数组如何去重？

- ES6 Set去重
- 利用Object key去重
- 两层循环逐一对比，生成新数组
- indexOf去重
- sort排序，再单层循环前后对比

### 数组如何排序？

- 数组sort排序

- 冒泡排序，两层循环，两两互换

  ```
  function bubbleSort(data) {
  	var temp = 0
  	for(var i=data.length; i>0; i--){
  		for(var j=0; j<i-1; j++){
  			if(data[j] > data[j+1]){
  				temp = data[j]
  				data[j] = data[j+1]
  				data[j+1] = temp
  			}
  		}
  	}
  	return data
  } 
  ```

- 选择排序

  ```
  function selectionSort(data) {
  	for(var i=0; i<data.length; i++){
  		var min = data[i]
  		var temp
  		var index = i
  		for(var j=i+1; j<data.length; j++){
  			if(data[j] < min){
  				min = data[j]
  				index = j
  			}
  		}
  		temp = data[i]
  		data[i] = min
  		data[index] = temp
  	}
  	return data
  }
  ```

- 插入排序

  ```
  function insertionSort(data) {
  	var len = data.length
  	for(var i=1; i<len; i++){
  		var key = data[i]
  		var j = i - 1
  		while(j>=0 && data[j]>key){
  			data[j+1] = data[j]
  			j--
  		}
  		data[j+1] = key
  	}
  	return data
  }
  ```

### 谈一下常用的设计模式，并选择一个进行场景分析？

- 单例模式

- 工厂模式

- 观察者模式

- 适配器模式

  在Vue中通过观察者模式触发视图更新

  Vue2通过Object.defineProperty劫持data数据，当数据变化后触发setter，setter内部通过订阅器来notify消息，notify会调用watcher更新视图

  当一套前端对接不同后端服务时，会出现数据解构不一致的情况，这个时候可以使用适配器模式来兼容不同后端，使他以统一的数据解构对接前端

### 谈一下for...of

for...of是ES2015版本引入的语法，它可以遍历数组，类数组，以及Map/Set/字符串等

- 数组迭代
- 类数组迭代
- 字符串迭代
- Map迭代
- Set迭代

### 前端常见攻击方式？

- XSS攻击
- CSRF攻击
- Sql注入
- html脚本注入

### 前端有哪些跨域方案？

- JSONP跨域（本质是JS调用）
- CORS（后台设置）
- Nginx反向代理（运维配置）

### 前端网站常规优化方案？

优化策略：减少请求次数、减小资源大小、提高相应和加载速度、优化资源加载时机、优化加载方法

- 合并、压缩、混淆html/css/js文件（webpack实现）
- Nginx开启Gzip，进一步压缩资源
- 图片资源使用CDN加速
- 符合条件的图标做base64处理
- 样式表放首部，JS放尾部
- link或者src添加rel属性，设置prefetch或preload可预加载资源
- 如果使用了UI组件库，采用按需加载
- SPA项目，通过import或者require做路由按需
- 服务端渲染SSR，加快首屏渲染，利于SEO
- 页面使用骨架屏，提高首页加载速度
- 使用JPEG2000、JPEG XR、webp的图片格式来代替现有的jpeg和png，当页面图片较多时，作用非常明显
- 使用图片懒加载lazyload 

### js垃圾回收机制知道哪些，v8引擎使用的哪一种

js的两种回收机制：

1 标记清除（mark and sweep）
 2 引用计数（reference counting）

javascript与V8引擎：

垃圾回收机制的好处和坏处

好处：大幅简化程序的内存管理代码，减轻程序猿负担，并且减少因为长时间运转而带来的内存泄露问题。

坏处：自动回收意味着程序猿无法掌控内存。ECMAScript中没有暴露垃圾回收的借口，我们无法强迫其进行垃圾回收，更加无法干预内存管理。



作者：O蚂蚁O
链接：https://www.jianshu.com/p/f1f39d5b2a2e
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### 网站攻击方法和预防

### 水平垂直居中

1. 第一种

   ```
   #container{
       position:relative;
   }
   
   #center{
       width:100px;
       height:100px;
       position:absolute;
       top:50%;
       left:50%;
       transform: translate(-50%,-50%);
   }
   ```

2. 第二种

   ```
   #container{
       position:relative;
   }
   
   #center{
       width:100px;
       height:100px;
       position:absolute;
       top:50%;
       left:50%;
       margin:-50px 0 0 -50px;
   }
   ```

3. 第三种

   ```
   #container{
       position:relative;
   }
   
   #center{
       position:absolute;
       margin:auto;
       top:0;
       bottom:0;
       left:0;
       right:0;
   }
   ```

4. 第四种

   ```
   #container{
       display:flex;
       justify-content:center;
       align-items: center;
   }
   ```

   

### js加载位置区别优缺点

html文件是自上而下的执行方式，但引入的css和javascript的顺序有所不同，css引入执行加载时，程序仍然往下执行，而执行到<script>脚本是则中断线程，待该script脚本执行结束之后程序才继续往下执行。
 所以，大部分网上讨论是将script脚本放在<body>之后，那样dom的生成就不会因为长时间执行script脚本而延迟阻塞，加快了页面的加载速度。

但又不能将所有的script放在body之后，因为有一些页面的效果的实现，是需要预先动态的加载一些js脚本。所以这些脚本应该放在<body>之前。

其次，不能将需要访问dom元素的js放在body之前，因为此时还没有开始生成dom，所以在body之前的访问dom元素的js会出错，或者无效

**script放置位置的原则“页面效果实现类的js应该放在body之前，动作，交互，事件驱动，需要访问dom属性的js都可以放在body之后**

