







## 创建项目

1. 创建项目文件并npm init
2. 安装koa

#### index.js

```js
const Koa = require('koa')
const app = new Koa()
app.use(async(ctx) => {
	ctx.body = ''
})
app.listen(3000)
```



## 请求的接收

#### GET请求

- 通过request接收

  ```js
  const Koa = require('koa');
  const app = new Koa();
  app.use(async(ctx)=>{
      let url =ctx.url;	//"/?user=xxx&age=18"
      let request =ctx.request;
      let req_query = request.query;	//格式化好的参数对象{"user":"xxx","age":"18"}
      let req_querystring = request.querystring;	//请求字符串"user=xxx&age=18"
  });
  app.listen(3000,()=>{
      console.log('[demo] server is starting at port 3000');
  });
  ```

-  从ctx接收

  ```js
  const Koa = require('koa');
  const app = new Koa();
  app.use(async(ctx)=>{
      let url =ctx.url;
      let ctx_query = ctx.query;	//等同于ctx.request.query
      let ctx_querystring = ctx.querystring;	//等同于ctx.request.querystring
  });
  app.listen(3000,()=>{
      console.log('[demo] server is starting at port 3000');
  });
  ```

#### POST请求

- 原生解析

  - 解析node原生post参数

    ```js
    function parsePostData(ctx){
        return new Promise((resolve,reject)=>{
            try{
                let postdata="";
                ctx.req.on('data',(data)=>{
                    postdata += data
                })
                ctx.req.addListener("end",function(){
                    resolve(postdata);
                })
            }catch(error){
                reject(error);
            }
        });
    }
    ```

  - post字符串解析为json对象

    ```js
    function parseQueryStr(queryStr){
        let queryData={};
        let queryStrList = queryStr.split('&');
        console.log(queryStrList);
        for( let [index,queryStr] of queryStrList.entries() ){
            let itemList = queryStr.split('=');
            console.log(itemList);
            queryData[itemList[0]] = decodeURIComponent(itemList[1]);
        } 
        return queryData
    }
    ```

- 使用中间件

  - 安装`koa-bodyparser`

  - 引入使用

    ```js
    const Koa  = require('koa');
    const app = new Koa();
    const bodyParser = require('koa-bodyparser');	//引入中间件
     
    app.use(bodyParser());	//注册插件
     
    app.use(async(ctx)=>{
        if(ctx.url==='/' && ctx.method==='GET'){
            ctx.body=html;
        }else if(ctx.url==='/' && ctx.method==='POST'){
            let postData= ctx.request.body;		//直接解析为post参数对象
            ctx.body=postData;
        }else{
            ctx.body='<h1>404!</h1>';
        }
    });
    app.listen(3000,()=>{
        console.log('[demo] server is starting at port 3000');
    });
    ```

    

## 路由

#### 原生路由

```js
const Koa = require('koa');
const fs = require('fs');
const app = new Koa();
//渲染页面
function render(page){
    return  new Promise((resolve,reject)=>{
        let pageUrl = `./page/${page}`;
        fs.readFile(pageUrl,"binary",(err,data)=>{
            if(err){
                reject(err)
            }else{
                resolve(data);
            }
        })
    })
}
//路由：根据路径返回对应页面
async function route(url){
    let page = '404.html';
    switch(url){
        case '/':
            page ='index.html';
            break;
        case '/index':
            page ='index.html';
            break;
        default:
            break; 
    }
    let html = await render(page);
    return html;
}
 
app.use(async(ctx)=>{
    let url = ctx.request.url;	//获取路径
    let html = await route(url);	//根据路径渲染页面
    ctx.body=html;
})
app.listen(3000);
```

#### 使用中间件

- 安装` koa-router `

- 引入使用

  ```
  const Koa = require('koa');
  const Router = require('koa-router');	//引入中间件
  const app = new Koa();
  const router = new Router();	//声明实例
   
  router.get('/', function (ctx, next) {		//使用实例方法
      ctx.body="Hello JSPang";
  })
  .get('/todo',(ctx,next)=>{		//可串联多请求
      ctx.body="Todo page"
  });
   
  app
    .use(router.routes())
    .use(router.allowedMethods());
    app.listen(3000,()=>{
        console.log('starting at port 3000');
    });
  ```

  

#### 路由嵌套

- 方法一：设置统一前缀

  ```js
  const router = new Router({
        prefix:'/jspang'
  })
  ```

- 方法二：多种层级

  ```js
  const Koa = require('koa');
  const app = new Koa();
  const Router = require('koa-router');
  
  let home = new Router();
  home.get('/jspang',async(ctx)=>{
      ctx.body="Home JSPang";
  }).get('/todo',async(ctx)=>{
      ctx.body ='Home ToDo';
  })
  
  let page = new Router();
  page.get('/jspang',async(ctx)=>{
      ctx.body="Page JSPang";
  }).get('/todo',async(ctx)=>{
      ctx.body ='Page ToDo';
  })
  //装载所有子路由
  let router = new Router();
  router.use('/home',home.routes(),home.allowedMethods());
  router.use('/page',page.routes(),page.allowedMethods());
  //加载路由中间件
  app.use(router.routes()).use(router.allowedMethods());
   
  app.listen(3000,()=>{
      console.log('[demo] server is starting at port 3000');
  });
  ```

## cookie

#### 写入cookie

```js
const Koa  = require('koa');
const app = new Koa();
 
app.use(async(ctx)=>{
    if(ctx.url=== '/index'){
        ctx.cookies.set(
            'MyName','value'
        );
        ctx.body = 'cookie is ok';
    }else{
        ctx.body = 'hello world'
    }
});
 
app.listen(3000,()=>{
    console.log('[demo] server is starting at port 3000');
})
```

#### cookie选项

```js
const Koa  = require('koa');
const app = new Koa();
 
app.use(async(ctx)=>{
    if(ctx.url=== '/index'){
        ctx.cookies.set(
            'MyName','value',{
                domain:'127.0.0.1', // 写cookie所在的域名
                path:'/index',       // 写cookie所在的路径
                maxAge:1000*60*60*24,   // cookie有效时长
                expires:new Date('2018-12-31'), // cookie失效时间
                httpOnly:false,  // 是否只用于http请求中获取
                overwrite:false  // 是否允许重写
            }
        );
        ctx.body = 'cookie is ok';
    }else{
        ctx.body = 'hello world'
    }
});
 
app.listen(3000,()=>{
    console.log('[demo] server is starting at port 3000');
})
```

#### 读取cookie

```js
const Koa  = require('koa');
const app = new Koa();
 
app.use(async(ctx)=>{
    if(ctx.url=== '/index'){
        ctx.cookies.set(
            'MyName','JSPang',{...
            }
        );
        ctx.body = 'cookie is ok';
    }else{
        if( ctx.cookies.get('MyName')){
            ctx.body = ctx.cookies.get('MyName');	//读取cookie
        }else{
            ctx.body = 'Cookie is none';
        }
    }
});
 
app.listen(3000,()=>{
    console.log('[demo] server is starting at port 3000');
})
```

## 页面模板

- 安装 koa-views中间件 

- 安装ejs模板引擎

- 编写inde.ejs模板

  ```ejs
  <!DOCTYPE html>
  <html>
  <head>
      <title><%= title %></title>http://jspang.com/wp-admin/post.php?post=2760&action=edit#
  </head>
  <body>
      <h1><%= title %></h1>
      <p>EJS Welcome to <%= title %></p>
  </body>
  </html>
  ```

- 配置并渲染

  ```js
  const Koa = require('koa')
  const views = require('koa-views')	//引入中间件
  const path = require('path')
  const app = new Koa()
  // 加载模板引擎
  app.use(views(path.join(__dirname, './view'), {
    extension: 'ejs'
  }))
   
  app.use( async ( ctx ) => {
    let title = 'hello koa2'
    await ctx.render('index', {	//传递参数
      title
    })
  })
   
  app.listen(3000,()=>{
      console.log('[demo] server is starting at port 3000');
  })
  ```

## 公开静态资源

- 安装 koa-static中间件 

- 引入使用

  ```js
  const Koa = require('koa')
  const path = require('path')
  const static = require('koa-static')	//引入中间件
   
  const app = new Koa()
   
  const staticPath = './static'
   
  app.use(static(
    path.join( __dirname,  staticPath)
  ))
   
  app.use( async ( ctx ) => {
    ctx.body = 'hello world'
  })
   
  app.listen(3000, () => {
    console.log('[demo] static-use-middleware is starting at port 3000')
  })
  ```