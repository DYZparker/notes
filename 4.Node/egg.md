





## 特点

- 在koa的基础上集成，添加规范

## 创建项目

1. 全局安装egg init
2. 在项目文件执行npm init egg --type=simple
3. 安装依赖包npm install
4. 启动服务npm run dev

#### index.js

```js
const express = require('express')
const app = express()
app.get('/', function(req,res) {
    res.send('xxx')
})
app.listen(3000)
```









## 一、架构概览
 

![img](https:////upload-images.jianshu.io/upload_images/1214547-b9957d0c16c8d204.png?imageMogr2/auto-orient/strip|imageView2/2/w/1000/format/webp)

egg.js项目架构


 绿色虚线框中的所有组件组成了一个Worker，这就是egg.js中实际执行代码逻辑的进程，是一个node服务器。

- request进来后，先穿过中间件，自己定义的中间件都放在projectDir/app/middleware下，并在config中启用。

- egg.js内置了[egg-static](https://github.com/eggjs/egg-static)中间件，将静态资源放在projectDir/app/public中，只会经过egg-static中间件之前的中间件，最后egg-static直接响应给客户端，不会到达其后的中间件以及Router。

- 如果不是public中的资源，将会穿越所有中间件，到达路由。一般所有的路由都放在router.js中，这个文件没有任何逻辑，而是直接指向一个处理请求的controller，只起到目录和索引的作用: 

  ```csharp
  router.get('/users', controller.user.getAll);
  ```

- Controller都放在projectDir/app/controller中，不含有具体的业务逻辑，业务逻辑都在Service中，Controller只负责调用并组合Service，最后将响应提交给客户端。

- Service放在projectDir/app/service中，负责调用Model，进行具体业务。

- 除此之外，Worker中还有定时任务，写在projectDir/app/schedule文件夹中。

- 各个部件的所有可操控行为，都可以在projectDir/confg/中的配置文件中定义，配置文件可以同时有很多份，default会被具体环境的配置文件中的同名字段覆盖，具体使用哪份配置，是根据EGG_SERVER_ENV这个环境变量的值。

## 二、扩展内置对象

内置对象可以被方便地获取到，不过功能有限，我们可以通过egg.js的扩展(Extend)功能去进一步加强、定制框架的能力。
 egg.js中有非常多新鲜的特性：“扩展”、“插件”、“多环境配置”，这些特性名称虽然不一样，但本质都是一样的：有则覆盖，无则增加。类似于[lodash中的defaults函数](https://lodash.com/docs/4.17.10#defaults)，也类似于继承。
 因此，如果我们想扩展Application对象，根据egg.js规范，应该在projectDir/app/extend/下增加application.js：

```rust
// app/extend/application.js
module.exports = {
  specialName: 'hj's app'
}
```

以后就可以方便地调用`app.specialName`获取这个值。

## 三、 扩展应用：插件

Extend特性可以扩展上层框架的内置对象，而[插件](http://eggjs.org/zh-cn/basics/plugin.html)则可以扩展除router和controller之外的整个app。插件拥有自己的package.json，因此可以独立发布到npm，每个人都可以install，享用你的扩展。
 如果我要为项目写一个管理微信公众号的功能，我会写一个WxService:

```jsx
// app/service/wx.js
const Service = require('egg').Service;
const request = require('request-promise');

class WxService extends Service{
  async getUserInfo(openId){
      return request.post({
        uri: 'https://wx.user.com',
        body:{
          openId
        }
      });          
  }
}
```

很多项目都可以用到这个Service，因此我会提取为一个插件，然后通过引入插件的形式去引入，我在应用中同样可以调用这个Service，等于是把插件中的文件往应用中复制了一份，和写在应用中没什么两样。
 关于如何提取插件，请参见：[渐进式开发](http://eggjs.org/zh-cn/tutorials/progressive.html)

## 四、定制自己的框架

定制自己的框架可以确定项目的技术选型、减少项目初期的工作，定制框架的思想其实和扩展内置对象、开插件是一样的，但是前置工作会比较多一些，参见：[egg.js框架开发](http://eggjs.org/zh-cn/advanced/framework.html)。
 这些前置工作比较重复、有固定格式，没有必要自己写，建议用骨架搭建。

```ruby
$ npm install egg-init -g
$ egg-init --type=framework myegg
$ cd myegg
```

## 五、 Loader加载顺序

当我们基于自己定制的框架framework1，并且在应用中依赖了插件plugin2、plugin3，开发了一个应用：



![img](https:////upload-images.jianshu.io/upload_images/1214547-f71028b699d673a6.png?imageMogr2/auto-orient/strip|imageView2/2/w/291/format/webp)

app结构



其中framework1直接基于egg并且内置了plugin1，此时整个app的加载顺序是怎样的呢？
 加载原则总结一句话是：从被依赖到依赖。



![img](https:////upload-images.jianshu.io/upload_images/1214547-43893c8eb1b00667.png?imageMogr2/auto-orient/strip|imageView2/2/w/326/format/webp)

依赖顺序

先来分析一下，谁被依赖，谁依赖：

-  **插件**可能被其他插件、框架和应用依赖

-  **框架**可能被上层框架和应用依赖

- 应用

  不被依赖

   插件处于被依赖队列的最前方，框架其次，应用最后，因此先加载顺序如图所示，那么我们刚刚的例子，加载顺序应该是：

  ![img](https:////upload-images.jianshu.io/upload_images/1214547-5f7747e5071742ed.png?imageMogr2/auto-orient/strip|imageView2/2/w/141/format/webp)

  从上至下加载

   更多关于Loader的信息请见官方文档：

  Loader

  。

## 六、多进程模型

为了最大程度利用多核、增强Node进程健壮性，一般我们会使用PM2一类的工具，如果使用egg.js，就完全不需要担心了，egg利用cluster模块（[了解cluster原理请看这篇文章](https://cnodejs.org/topic/56e84480833b7c8a0492e20c)）已经创建了一个非常稳定的多进程模型。
 

![img](https:////upload-images.jianshu.io/upload_images/1214547-4d00a79ae4bdca25.png?imageMogr2/auto-orient/strip|imageView2/2/w/942/format/webp)

多进程模型


 使用egg-bin命令启动时，会启动一个Master进程，Master进程会先fork一个Agent，再根据核数启动对应数量的Worker。Master会监听端口，将请求转发给相应Worker处理，当Worker出错时Master重新fork一个Worker保证服务器健壮性。 Agent是一个特殊的Worker，不做具体的业务逻辑，只负责调度Worker，比如哪个Worker执行定时任务。 Agent与Worker的通行时通过Master转发，也就是每个人只知道Master，而不能互相通信，两个Worker之间也需要通过Master转发消息。 总结：

- Master只负责Worker的初始化、重启、转发IPC消息等进程性工作。
- Agent负责egg中的Worker调度。
- Worker负责执行具体的业务逻辑。























## 请求的接收

#### 通用匹配

```js
app.use(function(req, res, next){})		//匹配任何请求路径和请求方法
app.use('/X', function(req, res, next){})		//匹配以/X开头的请求
```

#### 严格匹配

- get和post请求

  ```js
  app.get(',/X', function(req, res, next){})
  app.post(',/X', function(req, res, next){})
  ```

- post数据解析

  - 安装`body-parser`

  - 引入使用

    ```js
    const express  = require('express');
    var bodyParser = require('body-parser')	//引入中间件
    const app = express();
    
    // 配置解析表单 POST 请求体插件
    // parse application/x-www-form-urlencoded
    app.use(bodyParser.urlencoded({ extended: false }))
    // parse application/json
    app.use(bodyParser.json())
     
    app.post('/', function(req,res) {
        console.log(req.body)	//req.body为表单数据
    })
    app.listen(3000,()=>{
        console.log('[demo] server is starting at port 3000');
    });
    ```

#### 返回数据方法

- status：给浏览器发送状态码

- send：给浏览器发送信息

- json：接收一个对象作为参数，并会自动把对象转为字符串再发送给浏览器

#### 全局页面

- 404页面

  ```js
  app.use(function(req, res, next){404信息})	//最后匹配
  ```

- error页面

  ```js
  //在其他请求判断err后直接调用next(err)
  app.use(function(err, req, res, next){err信息})	//最后匹配
  ```

  

## 路由

```js
var express = require('express')
var fs = require('fs')
var router = express.Router()
router.get('/', function(req,res) {
    res.send('xxx')
})
...
module.exports = router
```

- 重定向

  ```js
  app.get('/', function(req,res) {
      res.redirect('xxx')
  })
  ```

  - 服务端重定向只对同步请求有效，异步请求无效

## session

- `express`框架默认不支持`Session`和`Cookie`，所以需要`express-session`中间件
- 默认`Session`数据是内存存储的，服务器重启就会丢失，生产坏境会进行持久化存储

- 配置

  ```js
  app.use(session({
      secret: 'itcast',    //随意配置字符串增加安全性
      resave: false,
      saveUninitialized: false    //无论是否使用session都配一把钥匙
  }))
  ```

- 添加`session`数据

  ```
  req.session.键值 = value
  ```

- 获取`session`数据

  ```
  req.session.键值
  ```



## 页面模板

- 安装`art-template`和`express-art-template`模板引擎

  - 配置（渲染以.html结尾的文件时使用模板引擎）

    ```js
    app.engine('html', require('express-art-template'))
    app.get('/', function(req,res) {
        res.render('xxx.html', {模板数据})	//默认会去项目中的views目录查找模板文件
    })
    ```

  - 修改默认的views目录

    ```js
    app.set('views', 目录路径)
    ```

- 模板语法

  - 循环

    ```js
    {{ each 循环数组 }}
    <div>模板{{ $value }}</div>
    {{ /each }}
    ```

  - 继承

    ```js
    //父模板layout.html
    <body>
        {{ include './header.html' }}    //公共部分
        {{ block 'content' }}    //替换部分
            <h1>默认内容</h1>
        {{ /block }}
    </body>
    ```

    ```js
    //子模板index.html
    {{ extend './layout.html' }}
    {{ block 'content' }}
        <div>替换内容</div>
    {{ /block }}
    ```

    - 也可替换header中的css，script中的js

## 公开静态资源

- 公开指定目录

  ```js
  //www.localhost:3000/public/index.html
  app.use('/public/', express.static('./public/'))
  
  //www.localhost:3000/index.html
  app.use(express.static('./public/'))
  ```



## 第三方插件

#### nodemon

- 基于`node.js`开发的第三方命令行工具，解决修改代码重启服务器的问题
- 全局安装后使用`nodemon app.js`启动服务