







## 创建项目

1. 创建项目文件并npm init
2. 安装express

#### index.js

```js
const express = require('express')
const app = express()
app.get('/', function(req,res) {
    res.send('xxx')
})
app.listen(3000)
```



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