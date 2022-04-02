 Next.js 是一个轻量级的 React 服务端渲染应用框架 

## 区别

- 前端框架的`SPA`（单页应用），首屏加载过慢，不能`SEO`（搜索引擎搜索）
- 服务端框架的`SSR`（服务端渲染）



## 创建项目

#### 手动搭建

1. 创建项目文件并`npm init -y`

2. 安装`react`和`react dom`和`next`

3. `package.json`中配置

   ```
   "scripts": {
   	"dev": "next",
   	"build": "next build",
   	"start": "bext start"
   }
   ```

4. 新建`pages`文件夹

#### 脚手架搭建

1. 全局安装`create-next-app`
2. `npx create-next-app 项目名称`

#### pages

- 此文件夹目录即路由路径

- `index.js`

  ```js
  import React from 'react'
  import Link from 'next/link'
  export default () => {
  	<>
      	<div>    
      </>
  }
  ```

  

- `Link`标签里必须包含a标签

  ```js
  <Link href='/'><a>首页</a></Link>
  ```


#### component

```js
export default ({children})=><button>{children}</button>
```



## 路由

#### 标签式导航

```js
import Link from 'next/link'
export default ()=>(
    <>
        <div>Jspang-B page .  </div>
        <Link href="/"><a>返回首页</a></Link>
    </>
)
```

#### 编程式导航

```js
import Router from 'next/router'
export default ()=>(
    <>
         <div>
        	 <button onClick={()=>{Router.push('/jspangA')}}>去JspangA页面</button>
    	 </div>
    </>
)
```

#### 只能用query传递参数

- 标签导航页`index.js`

  ```js
  import React from 'react'
  import Link from 'next/link'
  import Router from 'next/router'
  const Home = () => {
    return(
      <>
        <div>
          <Link href="/Zujian?name=标签名"><a>标签</a></Link>
        </div>
      </>
    )
  }
  export default Home
  ```

- 组件页`zujian.js`

  ```js
  import { withRouter} from 'next/router'
  import Link from 'next/link'
  const Zujian = ({router})=>{
      return (
          <>
              <div>{router.query.name},跳转了</div>
              <Link href="/"><a>返回首页</a></Link>
          </>
      )
  }
  export default withRouter(Zujian)
  ```

  - 将函数组件转变为Router组件，就可以使用router

- 编程式跳转传参

  ```js
   function gotoZujian(){
      Router.push({
        pathname:'/Zujian',
        query:{
          name:'标签名'
        }
      })
    }
   const Home = () => {
    return(
      <>
         <div>
    		   <button onClick={gotoZujian}>标签</button>
  	   </div>
      </>
    )
  }
  export default Home
  ```

#### 路由钩子事件

- history模式(`/xxx`)
  - `routeChangeStart`
  - `routeChangeComplete`
  - `beforeHistoryChange`
  - `routeChangeError`（不包含404错误）
- hash模式(`#xxx`)
  - `hashChangeStart`
  - `hashChangeComplete`

- 监听：

  ```js
  Router.events.on('routeChangeStart', (...args) => {
  	console.log()
  })
  ```

  

## 获取远端数据

- 在`getInitialProps`中用`Axios`获取

-  `getInitialProps`不能使用在子组件中。只能使用在`pages`页面中 

  ```js
  import withRouter from 'next/router'
  import Axios from 'axios'
  const 组件 = ({router}) => {
  	return (<div>)
  }
  组件.getInitialProps = async() => {
      const promise = new Promise((resolve) => {
          axios('http://...').then((res) => {
              resolve(res.data.data)
          })
      })
      return await promise
  }
  export default withRouter(组件)
  ```

  

## CSS样式

```js
function 组件() {
	return(
		<>
			<div>title</div>
			<style jsx>
				{`
					div {样式}
				`}
			</style>
		</>
	)
}
export default 组件
```

- `next.js`不支持`import 'xxx.css'`引入

- 安装插件`@zeit/next-css`并新建`next.config.js`才可以用import引入

  ```js
  const withCss = require('@zeit/next-css')
  
  if(typeof require !== 'undefined'){
      require.extensions['.css']=file=>{}
  }
  
  module.exports = withCss({})
  ```

  

- 按需加载`antd`

  - 安装`antd`和`babel-plugin-import`

  - 配置`.babelrc`

    ```js
    {
        "presets":["next/babel"],  //Next.js的总配置文件，相当于继承了它本身的所有配置
        "plugins":[     //增加新的插件，这个插件就是让antd可以按需引入，包括CSS
            [
                "import",
                {
                    "libraryName":"antd",
                    "style":"css"
                }
            ]
        ]
    }
    ```

  - 按需加载`antd`后`build`打包不成功，需要更改为全局引入



## 异步加载/懒加载

- 第三方包

  ```js
  function Time() {
  	const [nowTime, setTime] = useState(Date.now())
      const changeTime = async() => {
          const moment = await import('moment')	//需要的时候再引入
          setTime(moment.default(Date.now()).format())
      }
      return (
      	<>
          	<div>显示时间为：{nowTime}</div>
  			<div><button onClick={changeTime}>改变时间格式</button></div>
          </>
      )
  }
  export default Time
  ```

- 自己写的组件

  ```js
  import dynamic from 'next/dynamic'
  const One = dynamic(import('../components/one'))	//包装引入的组件
  
  ...
  	<One />
  ...
  ```

  

## SEO

- 搜索引擎最先搜索的是页面title

- 全局定义再单页引入

  ```js
  import Head from 'next/head'
  const MyHeader = () => {
  	return (
      	<>
          	<Head>
          		<title>标题</title>
          	</Head>
          </>
      )
  }
  export default MyHead
  ```

- 页面单独添加

  ```
  import Head from 'next/head'
  ...
  	<Head>
  		<title>标题</title>
  		<meta charSet='utf-8' />
  	</Head>
  ...
  ```

  

