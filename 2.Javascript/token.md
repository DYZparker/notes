## JWT

`JSON Web Token` (JWT)是一个开放标准(RFC 7519)，它定义了一种紧凑的、自包含的方式，用于作为`JSON`对象在各方之间安全地传输信息。该信息可以被验证和信任，因为它是数字签名的。

本文只讲`Koa2 + jwt`的使用，不了解`JWT`的话请到[这里](https://segmentfault.com/a/1190000019338195#))进行了解。

## koa环境

要使用`koa2+jwt`需要先有个`koa`的空环境，搭环境比较麻烦，我直接使用[koa起手式](https://github.com/Vibing/ts-koa-starter)，这是我使用`koa+typescript`搭建的空环境，如果你也经常用`koa`写写小`demo`,可以点个star，方便~

## 安装koa-jwt

`koa-jwt`主要作用是控制哪些路由需要jwt验证，哪些接口不需要验证：

使用了 `koa-jwt` 中间件后，如果没有token，或者token失效，该中间件会给出对应的错误信息。如果没有自定义中间件的话，会直接将 `koa-jwt` 暴露的错误信息直接返回给用户

```
import  *  as  koaJwt  from  'koa-jwt';

//路由权限控制 除了path里的路径不需要验证token 其他都要
app.use(
    koaJwt({
        secret:  secret.sign
    }).unless({
        path: [/^\/login/, /^\/register/]
    })
);
```

上面代码中，除了登录、注册接口不需要jwt验证，其他请求都需要。

## 使用jsonwebtoken生成、验证token

执行`npm install jsonwebtoken`安装`jsonwebtoken`
相关代码：

```
import  *  as  jwt  from  'jsonwebtoken';

const secret = 'my_app_secret';
const payload = {user_name:'Jack', id:3, email: '1234@gmail.com'};
const token = jwt.sign(payload, secret, { expiresIn:  '1h' });
```

上面代码中通过`jwt.sign`来生成一个token，
参数意义：

- payload：载体，一般把用户信息作为载体来生成token
- secret：秘钥，可以是字符串也可以是文件
- expiresIn：过期时间 1h表示一小时

## 在登录中返回token

```
import * as crypto from 'crypto';
import * as jwt from 'jsonwebtoken';

async login(ctx){

  //从数据库中查找对应用户
  const user = await userRespository.findOne({
    where: {
      name: user.name
    }
  });

  //密码加密
  const psdMd5 = crypto
    .createHash('md5')
    .update(user.password)
    .digest('hex');

  //比较密码的md5值是否一致 若一致则生成token并返回给前端
  if (user.password === psdMd5) {
    //生成token
    token = jwt.sign(user, secret, { expiresIn:  '1h' });
    //响应到前端
    ctx.body = {
      token
    }
  }

}
```

## 前端拦截器

前端通过登录拿到返回过来的`token`，可以将它存在`localStorage`里，然后再以后的请求中把`token`放在请求头的`Authorization`里带给服务端。
这里以`axios`请求为例，在发送请求时，通过请求拦截器把`token`塞到`header`里：

```
//请求拦截器
axios.interceptors.request.use(function(config) {
    //从localStorage里取出token
    const token = localStorage.getItem('tokenName');
    //把token塞入Authorization里
    config.headers.Authorization = `Bearer ${token}`;
    
    return config;
  },
  function(error) {
    // Do something with request error
    return Promise.reject(error);
  }
);
```

## 服务端处理前端发送过来的Token

前端发送请求携带token，后端需要判断以下几点：

1. token是否正确，不正确则返回错误
2. token是否过期，过期则刷新token 或返回401表示需要从新登录

关于上面两点，需要在后端写一个中间件来完成：

```
app.use((ctx, next) => {
  if (ctx.header && ctx.header.authorization) {
    const parts = ctx.header.authorization.split(' ');
    if (parts.length === 2) {
      //取出token
      const scheme = parts[0];
      const token = parts[1];
      
      if (/^Bearer$/i.test(scheme)) {
        try {
          //jwt.verify方法验证token是否有效
          jwt.verify(token, secret.sign, {
            complete: true
          });
        } catch (error) {
          //token过期 生成新的token
          const newToken = getToken(user);
          //将新token放入Authorization中返回给前端
          ctx.res.setHeader('Authorization', newToken);
        }
      }
    }
  }

  return next().catch(err => {
    if (err.status === 401) {
      ctx.status = 401;
      ctx.body =
        'Protected resource, use Authorization header to get access\n';
    } else {
      throw err;
    }});
 });   
```

上面中间件是需要验证token时都需要走这里，可以理解为拦截器，在这个拦截器中处理判断token是否正确及是否过期，并作出相应处理。

## 后端刷新token 前端需要更新token

后端更换新token后，前端也需要获取新token 这样请求才不会报错。
由于后端更新的token是在响应头里，所以前端需要在响应拦截器中获取新token。
依然以`axios`为例：

```
//响应拦截器
axios.interceptors.response.use(function(response) {
    //获取更新的token
    const { authorization } = response.headers;
    //如果token存在则存在localStorage
    authorization && localStorage.setItem('tokenName', authorization);
    return response;
  },
  function(error) {
    if (error.response) {
      const { status } = error.response;
      //如果401或405则到登录页
      if (status == 401 || status == 405) {
        history.push('/login');
      }
    }
    return Promise.reject(error);
  }
);
```

## 注意的几点

1. 错误处理配置要在`app.use(koa-jwt())`前面
2. 上面两配置要在router配置前面
3. 只要使用koa-jwt（配置中login除外），就相当于请求拦截器，有token过，无或错token直接返回401
4. jsonwebtoken只用于生成和验证token