##   核心概念

- DOM：浏览器中的概念，用`JS`对象来表示页面上的元素，并提供了操作DOM对象的API
- 虚拟DOM：
  - 虚拟DOM是框架中的概念，用`JS`对象来模拟页面上的DOM和DOM嵌套
  - 目的的为了实现页面中的DOM元素高效更新

- `Diff`算法
  - `tree diff`
  - `component diff`
  - `element diff`



## 创建项目

#### 自己搭建

1. 运行`npm init -y`快速初始化项目
2. 在项目根目录创建`src`源代码目录和`dist`产品目录
3. 在`src`下创建`index.html`
4. 运行`npm i webpack webpack-cli -D`
5. 运行`npm i webpack-dev-server -D`
   - 在`package.js`的`scripts`中添加`"dev": "webpack-dev-server"`
   - 可配置参数`--open --port 3000 --hot --progress --compress --host 127.0.0.1`
   - 打包好的`main.js`是托管到了内存中所以在项目根目录中看不到

6. 运行`npm i html-webpack-pulgin -D`在内存中自动生成`index.html`的插件
7. 运行`npm i react react-dom -S`
   - `react`创建组件和虚拟DOM的，同时组件的生命周期也在这个包中
   - `react-dom`进行DOM操作的，主要应用场景就是`ReactDOM.render()`

8. 在`index.html`页面中创建容器

9. 在`index.js`中

   ```js
   import React from 'react'
   import ReactDOM from 'react-dom'
   React.createElement()
   ReactDOM.render()
   ```

   - `React.createElement()`
     - 参数1：创建元素的类型，字符串，表示元素的名称
     - 参数2：是一个对象或null，表示当前这个DOM元素的属性
     - 参数3：子节点（包括其他虚拟DOM或文本子节点）
     - 参数n：其他子节点

   - `ReactDOM.render()`
     - 参数1：要渲染的那个虚拟DOM元素
     - 参数2：指定页面上一个容器

##### `JSX`语法

- 符合XML规范的`JS`，在`JS`中混合写入类似于HTML的语法

- 本质还是在运行的时候被转换成了`React.createElement`形式来执行

- 安装`babel`插件
  - 运行`npm i babel-croe babel-loader babel-plugin-transform-runtime -D`
  - 运行`npm i babel-preset-env babel-preset-stage-0 -D`

- 安装能够识别转换`jsx`语法的包
  
- `npm i babel-preset-react -D`
  
- 添加`.babelrc`配置文件

  ```
  {
      "presets": ["env", "stage-0", "react"],
      "plugins": ["transform-runtime"]
  }
  ```

  

- 在`webpack.config.js`中添加配置项

  ```
  module: { //所有第三方模块的配置规则
          rules:[
              {test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/}
          ]
      }
  ```

  

- 在`JSX`中变量、数组和对象用{}包裹（数组和对象里面是标签）

- 用`forEach/map/for`循环的元素要加上`key`属性

- 注释推荐使用`{/**/}`

- `JSX`中的元素添加类名需要用`className`来代替`class；htmlFor`来代替`label`标签的`for`属性

- 在标签的内容中不转译

  ```
  <li dangerouslySetInnerHtml={__html:item}></li>
  ```

- 当`JSX`编译时，遇到`<`就把它当做HTML代码编译，遇到`{}`就把当中的代码当做`JS`编译

##### `css`配置

- 在`JSX`中写行间样式，要用`style={{键值对}}`
- 处理`CSS`文件要安装`npm i style-loader css-loader -D`
- `import`的`css`文件是全局的空对象
- `webpack.config.js`配置
  - `css-loader?modules`会让`css`文件模块化并且对象中有值，类选择器和ID选择器自动分配值，标签无效
    - `:global(类名){...}`不被模块化，即全局
    - `:local(类名){...}`模块化的类名，默认不写
  - `css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]`
    - `[path]`表示样式表相对于根目录所在的路径
    - `[name]`表示样式表名称
    - `[local]`表示样式表的类名定义名称
    - `[hash:length]`表示32位的hash值

- 一个元素包含模块化类名和全局类名
  - `className = {cssObj.模块化类名+' 全局类名'}`
  - 字符串拼接，全局类名前有空格
- 第三方样式模块
  - `npm i url-loader -D`
  - `{test: /\.ttf|woff|wofff2|eot|svg$/, use: 'url-loder'}`
- 为了避免第三方`css`文件被模块化，建议自己写的`css`文件用`.scss`或`.less`结尾
  - `npm i sass-loader node-sass -D`
  - `{test: /\.scss$/, use: ['style-loder', 'css-loder', 'sass-loder?modules&localIdentName=[path][name]-[local]-[hash:5]']}`
  - `jsx`中需要`import cssobj from '@/css/XXX.scss'`
  - 然后普通`.css`文件就不用模块化了



#### 脚手架创建

1. 全局安装脚手架`create-react-app`
2. 创建：`create-react-app 项目名`
   - `Development Server`轻量级的开发服务器
   - `Webpack`打包代码
   - `Babel`转译器

3. `cd项目`，并启动`npm run start`

4. 样式管理第三方包：`styled-components`

   - 将`css`文件改为`js`文件

   - 创建自定义带有样式的标签

   - 全局样式

     ```javascript
     import { injectGlobal } from 'styled-components'
     injectGlobal`
         css样式
     `
     ```

   - 局部样式

     ```javascript
     import styled from 'styled-components'
     export const HeaderWrapper = styled.div`
         css样式
     `
     ```

     ```jsx
     import { HeaderWrapper } from './style'  //在应用的组件内引入
     <HeaderWrapper>Header</HeaderWrapper>
     ```

   - 引入图片

     ```javascript
     import img from '相对地址'
     url(${img})
     ```

   - 标签属性

     ```javascript
     export const NavInput= styled.input.attrs({
         placeholder: '搜索'
     })`
         css样式
     `
     ```

   - 相同标签不同类

     ```js
     export const NavItem= styled.div`
         &.left{...};
         &.right{...};
     `
     ```

5. `package.json`跨域配置：

   `"proxy": "http://xxxxxx"`



## 路由

1. 安装`react-router-dom`

2. 在最外层组件中

   ```jsx
   import { BrowserRouter, Route, Switch, Redirect } from 'react-router-dom'
   <BrowserRouter>
       <Switch>
           <Route path='' exact component={组件名1}></Route>
           <Route path='' exact component={组件名2}></Route>
       </Switch>
   </BrowserRouter>
   ```

   - `exact`精确匹配

   - `Switch`只匹配组件1和2其中的一个

   - 单击跳转

     ```jsx
     import { Link } from 'react-router-dom'
     <Link to='/'>
         组件/标签
     </Link>
     ```

   
   - 标签式重定向
   
     ```js
     <Redirect to='/' />
     ```
   
   - 编程式重定向
   
     ```
     this.props.history.push('/')
     ```
   
3. 获取路由信息

   - `this.props.location`匹配``
   - `this.props.match.params.id`匹配`/:id`



## 组件

```jsx
import React, { Component } from 'react'
import ReactDom from 'react-dom'

class App extends Component {
    constructor(props){
        super(props)
        this.state = {}
    }
    render() {
        return(
        	<div></div>
        )
    }
}

export default App
```

- 用构造函数（首字母大写）来创建组件
- 外界传递的数据需要在构造函数的参数中使用`props`来接收
- 必须要向外`return`一个合法的`JSX`创建的虚拟DOM
- 当组件的`state`或`props`发生改变的时候，`render`函数会重新执行
- 当父组件的`render`重新运行时，他的子组件的`render`都将重新执行一次
- `<Fragment>`可以代替`<div>`作为最外层的标签，且不会显示
- 外界传来的`props`参数不需要接收，直接通过`this.props.xxx`访问
- 除了`props`外还可有自己的私有数据`state`和生命周期（有状态组件）
- 数据只有`props`没有私有数据`state`和生命周期（无状态组件），但运行效率高一些
- 在`class`内部`this`指向当前组件的实例对象

#### 父子组件通讯

- 父传子：子组件标签中用属性传递，子组件内部用`this.props.属性`接收
- 子传父：
  - 首先父组件中有一个操作自己date的方法函数
  - 然后在子组件标签中用属性传递父组件的方法并绑定this指向（bind(this)）
  - 子组件内事件函数内再调用父组件传来的方法函数，并可以传参

- 子组件属性：

  - `propTypes`:
    - 是一个对象，可以规定父组件传来的值的类型
    - 引入：`import PropTypes from 'prop-types'`
    - 使用：`组件.propTypes = {propsname: PropTypes.string}`
    - 类型：`array, bool, number, string, func, object, symbol`
    - 后面还可继续添加 `isRequired`

  - `defaultProps`:
    - 是一个对象，给父组件传的值定一个默认值
    - 使用：`组件.defaultProps = {propsname:'Stranger'}`

#### 绑定事件

```jsx
<button onClick={()=>this.show(传参)}>按钮</button>
//事件处理函数需要定义为箭头函数并赋值给函数名称
show = (arg) => {....}

<button onClick={this.show.bind(this,传参)}>按钮</button>
//或者绑定普通事件函数并绑定this指向
show (arg) {....}
```

- React提供了自己的事件名，用驼峰形式表示，如`onClick = {function}`
- 修改`state`数据用`this.setState({键值对}, callback)`
  - `setState`只会把对应的state状态更新不会覆盖其他的state状态
  - `setState`是异步的，如想立即拿到更新后的状态值就在callback中拿
  - 常用：`this.setState( {}, (prevState) => {...} ) //prevState表示this.state`

- 文本框的`value`值绑定到`state`不提供`onChagne`处理函数的话，将会是一个只读的文本框
  - 两种方法拿到文本框的值
    - `e.target.value	//需要传参事件参数e`
    - `this.refs.txt.value`

#### `ref`

- 在组件中定义

  ```js
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      this.myRef = React.createRef();
    }
    render() {
      return <div ref={this.myRef} />
    }
  }
  ```

  - `this.myRef.current`
  - 然后使用`current`属性，即可获得当前元素
  - 自定义组件接口是`innerRef`而不是`ref`

- 在标签中定义

  ```
  <input ref={(input) => {this.input = input}}
  ```

  - 使用`this.input`引用

#### 生命周期函数

- 组件创建阶段：（只执行一次）
  - `componentWillMount`
    - 组件即将被挂载到页面的时候执行（只有第一次挂载）
  - `render`
    - 组件创建到内存中还未挂载到页面
  - `componentDidMount`
    - 组件被挂载到页面之后执行（只有第一次挂载）
    - 常用于发送`Ajax`请求

- 组件运行阶段：
  - `componentWillReceiveProps`
    - 子组件要从父组件接受`props`，并且父组件的`render`重新执行的时候执行
  - `shouldComponentUpdate(nextProps,nextState)`
    - 组件被更新之前执行，必须返回一个布尔值
  - `componentWillUpdate`
    - 组件更新之前并且`shouldComponentUpdate`返回`true`后执行
  - `render`
  - `componentDidUpdate`
    - 组件更新完成之后执行

- 组件销毁阶段：
  - `componentWillUnmount`
    - 当组件即将从页面中剔除时执行

#### 渲染优化

问题：当父组件重新渲染时，子组件数据变不变化都要跟着重新渲染

解决：利用生命周期函数判断props变没变化来决定子组件渲染与否

```js
shouldComponentUpdate(nextProps, nextState) {
	if(nextProps.content !== this.props.content) {
		return true
	}else {
	 	return false
	}
}
```

#### 异步组件

- 安装`react-loadable`

- 访问一个页面才加载该页面的`JS`，而不是点击首页就把整个网站`JS`加载完

- 在组建文件夹下新建`loadable.js`

  ```js
  import React from 'react';
  import Loadable from 'react-loadable';
  const LoadableComponent = Loadable({
      loader: () => import('./'),
      loading () {
          return <div>正在加载</div>
      }
  });
  export default () => <LoadableComponent />
  ```


- 在调用组件的app.js里更改调用异步组件

  ```js
  import Xxxx from './xxx/loadable.js'
  ```

- 包装后原组件从`router`引用组件信息会报错，需从`react-router-dom`引入`withRouter`方法，并在导出时`withRouter(组件)`

## 过渡动画

- 通过`CSS`类标签实现

  ```CSS
  .show {
      opacity: 1;
      transition: all  1s  ease-in
  }
  .hide {
      opacity: 0;
      transition: all  1s  ease-in
  }
  ```

  ```CSS
  .show {
      animation: show-item  1s  ease-in  forwards  //forwards参数让动画完后保持最后一帧的状态
  }
  @keyframes  show-item {
      0% {...}
      50% {...}
      100% {...}
  }
  .hide {
      animation: hide-item  1s  ease-in  forwards  //forwards参数让动画完后保持最后一帧的状态
  }
  @keyframes  hide-item {
      0% {...}
      50% {...}
      100% {...}
  }
  ```

- 通过模块来实现

  - 安装`react-transition-group`

    ```jsx
    import {CSSTransition} from 'react-transition-group'
    <CSSTransition
    	in={this.state.show}	//动画触发开关，在map渲染中去掉
    	timeout={1000}	//动画时间
    	className='fade'	//css样式前缀
  	appear={true}	//已有的第一次出现也添加动画，可选
    	unmountOnExit	//隐藏时直接从dom删除，可选
    	钩子={函数}	//
    >
        <组件>
    </CSSTransition>
    ```
  
    ```css
    //css中配置
  .fade-enter {}
    .fade-enter-active {}
  .fade-enter-done {}
    .fade-exit {}
    .fade-exit-active {}
    .fade-exit-done {}
    ```
  
  - 一组数据共有的动画
  
    ```JSX
  import {CSSTransition, TransitionGroup} from 'react-transition-group'
    <TransitionGroup>
        <CSSTransition>
            <组件>
        </CSSTransition>
    </TransitionGroup>
    ```
  
    

## `Redux`

#### 工作流程

1. 组件中dispatch一个action给store
2. store自动将action转发给reducer
3. recucer先判断事件type是否存在，再拷贝一份新的仓库state，用action去改变拷贝，再将拷贝返回给store
4. store将reducer返回的拷贝更新到仓库state
5. 组件监听到store的改变执行改变函数替换自己的state

```JSX
//组件文件
class MyComponent extends Component {
    constructor(props) {
        super(props)
        this.state = store.getState()
        this.storechange = this.storechange.bind(this)
        store.subscribe(storechange)    //只要store发生改变就会执行改变函数
    }
    render (){
        return <div onClick={事件函数}></div>
    }
    事件函数(){
        const action = 函数名(参数)    //函数在actionCreators.js里
        store.dispatch(action)
        }
    storechange(){
        this.setState(store.getState())    //将store中的改变更新到组件的state
    }
}
```

#### `store`文件夹

- `index.js`

  ```js
  import {createStore} from 'redux';
  import reducer from './reducer';
  const store = createStore(reducer)
  export default store
  ```

- `reducer.js`

  ```js
  const defaultState = {}
  export default (state = defaultState, action) => {
      if (action.type === 变量类型) => {
          const newState = JSON.parse(JSON.stringify(state));
          newState.xxx = action.xxx;
          return newState;
      }
      return state;
  }
  ```

  - reducer可以接受state但不能改变state

  - reducer里面只能有纯函数（有固定的输入就有固定的输出）

  - import {大写的变量类型} from './actionType'

  - reducer拆分与组合

    ```js
    impoert { combineReducers } from 'redux'
    import herderReducer from '../common/header/store/reducer'
    export default combineReducers({
        header: headerReducer
    })
    ```

- `actionTypes.js`

  - 对action的type的拆分，赋予变量，写错时才会报错

    ```js
    export const 大写的变量类型 = ‘小写的变量’类型‘
    ```

- `actionCreators.js`

  - 对action进行统一管理

    ```js
    import {大写的变量类型} from './actionType'
    import 
    export const 函数名 =  (参数) => {
            type:  大写的变量类型    //变量的值在actionType.js里
            参数 ： 值
        }
    ```

#### `immutable`模块

*详情见Other文件夹immutable扩展*

```js
import { fromJS } from 'immutable'
const defaultState = fromJS({
    键值对
})
export default (state = defaultState, action) => {
    if (action.type === XXX) {
        return state.set('键'，值);
        return state.merge({键值对，键值对， ...})
        //设置值，并没有改变原来，而是返回新对象
    }
}
```

- 使`state`变为不可改变的`immutable`对象
- 获取`state`：
  
- `xxx: state.get('键')`
  
- 取出的对象需要`const newobj = obj.toJS()`才能使用

- 存入对象前需要 `const newobj : fromJS(obj)`

- 使用此模块可配合使用纯组件

  ```JS
  import React, { PureComponent } from 'react'
  class 组件 extends PureComponent {...}
  ```

  - 纯组件使`store`中的数据更新时，没有关联的组件不重新渲染

#### `redux-immutable`模块

- 更改全局state为`imuutable`对象

  ```JS
  impoert { combineReducers } from 'redux'变为
  impoert { combineReducers } from 'redux-immutable'
  xxx: state.header.get('xxx')变为
  xxx: state.get('header').get('xxx')或者xxx: state.getIn(['header', 'xxx'])
  ```

  

#### 异步操作`store`

##### `redux-thunk`中间件

- 可以使`redux`的`dispatch`不光可以发送对象也可以发送函数

  - 如果`dispatch`是一个对象会直接传给`tore`
  - 如果是一个函数会先执行，如函数中有继续`dispatch`对象则传给`store`

- 可以把生命周期中发送`Ajax`请求转换到`action`中

- 在`store/index.js`内配置

  ```js
  import {createStore, applyMiddleware} from 'redux';
  import thunk from 'redux-thunk'
  const store = createStore(
      reducer,
      applyMiddleware(thunk)
  )
  ```

  如包含多个中间件（redux浏览器插件），就是用增强函数

  ```js
  import {createStore, applyMiddleware, compose} from 'redux';
  import thunk from 'redux-thunk'
  const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose
  const enhancer = composeEnhancers(applyMiddleware(thunk))
  const store = createStore(
      reducer,
      enhancer
  )
  ```

- 在`store/actionCreators.js`内应用

  ```js
  import axios from 'axios'
  export const 函数名 = () => {
      return (dispatch) => {
          axios.get('/list.json').then((res) => {
              const data = res.data;
              const action = initListAction(data);
              dispatch(action);
          })
      }
  }
  ```

  

##### `redux-saga`中间件

- 生命周期发送普通的`action`，而新建的`sagas.js`文件也能接受

- 在`store/index.js`内配置

  ```js
  import {createStore, applyMiddleware} from 'redux';
  import createSagaMiddleware from 'redux-saga';
  import todoSagas from './sagas';
  const sagaMiddleware = createSagaMiddleware()
  const store = createStore(
      reducer,
      applyMiddleware(sagaMiddleware )
  )
  sagaMiddleware.run (todoSagas)
  ```

- 创建`store/sagas.js`文件

  ```js
  import {takeEvery} from 'redux-saga/effects';
  import {大写的变量类型} from './actionTypes';
  import {initListAction} from './actionCreators';
  import axios from 'axios';
  //generator函数
  function* getInitList() {
      try {
          const res = yield axios.get('/list.json');
          const action = initListAction(res.data);
          yield put(action);
      }catch(e) {
          console.log('网络请求失败')
      }
  }
  function* mySaga() {
      yield takeEvery(大写的变量类型, getInitList)
  }
  export default mySaga
  ```

  

#### `react-redux`模块

- 让`react`更好的使用`redux`

- 在`src/index.js`中配置

  ```js
  import {Provider} from 'react-redux';
  import store from './store';	//提供器
  const App = (
      <Provider store={store}>
          <组件>
      </Provider>
  )
  ```

- 在组件中

  ```js
  import {connect} from 'react-redux'		//连接器
  
  class 组件类名 extends Component {
      render(){
          return(
          <div>
              <input value={this.props.inputValue} onChange={this.props.changeInputValue}>
              <button>提交</button>
          </div>
          )
      }
  }
  const mapStateToProps = (state) => {    //将store中的state与组件中的props相连接
      return {
      inputValue: state.inputValue
      }
  } 
  const mapDispatchToProps = (dispatch) => {    //将store中的dispatch映射到props中
      return{
          changeInputValue(){
              const action = {
                  type: 'XXXXX',
                  value
              }
              dispatch(action)
          }
      }
  }
  export default connect(mapStateToProps ,mapDispatchToProps )(组件类名)
  ```



## `antd`

- 全局引入

  ```
  import 'antd/dist/antd.css'
  import {组件} from 'antd'
  ```

- 按需引入

  - 安装`customize-cra`和`react-app-rewired`，前一个安装的前置，后一个是覆盖`package.json`配置

  - 在原`package.json`中修改

    ```
    "scripts": {
    -   "start": "react-scripts start",
    -   "build": "react-scripts build",
    -   "test": "react-scripts test",
    }
    ```

    改为

    ```
    "scripts": {
    +   "start": "react-app-rewired start",
    +   "build": "react-app-rewired build",
    +   "test": "react-app-rewired test",
    }
    ```

    

- 创建`config-overrides.js`修改默认配置

  ```
  module.exports = function override(config, env) {
    // do stuff with the webpack config...
    return config;
  };
  ```

  

- 使用`babel-plugin-import`

  - 用于按需加载组件代码和样式的 `babel` 插件

  ```
  const { override, fixBabelImports } = require('customize-cra');
  
  module.exports = override(
    fixBabelImports('import', {
      libraryName: 'antd',
      libraryDirectory: 'es',
      style: 'css',
    }),
  );
  ```

  - 移除前面在 `src/App.css` 里全量添加的 `@import '~antd/dist/antd.css'`

- 使用自定义主题

  - 安装`less`和`less-loader`

  ```js
  const { override, fixBabelImports, addLessLoader } = require('customize-cra');
  
  module.exports = override(
    fixBabelImports('import', {
      libraryName: 'antd',
      libraryDirectory: 'es',
  -   style: 'css',
  +   style: true,
    }),
  + addLessLoader({
  +   javascriptEnabled: true,
  +   modifyVars: { '@primary-color': '#1DA57A' },
  + }),
  );
  ```

  

## 高阶组件







## React Hooks



#### useState

- 用函数的形式代替原来的继承类的形式，并且使用预函数的形式管理`state`，不再使用类的形式定义组件

- 原始写法：

  ```js
  import React, { Component } from 'react'
  class Example extends Component {
      constructor(props) {
          super(props);
          this.state = { count:0 }
      }
      render() { 
          return (
              <div>
                  <p>You clicked {this.state.count} times</p>
                  <button onClick={this.addCount.bind(this)}>Chlick me</button>
              </div>
          );
      }
      addCount(){
          this.setState({count:this.state.count+1})
      }
  }
  export default Example;
  ```

- React Hooks写法：

  ```js
  import React, { useState } from 'react'
  function Example(){
      const [ count , setCount ] = useState(0);	//数组解构
      return (
          <div>
              <p>You clicked {count} times</p>
              <button onClick={()=>{setCount(count+1)}}>click me</button>
          </div>
      )
  }
  export default Example;
  ```

#### useEffect

- 代替常用生命周期函数

- 代替`componentDidMount`和`componentDidUpdate`

  - 首次渲染和之后的每次渲染都会调用一遍`useEffect`函数 
  -  `useEffect`函数时异步执行的，而`componentDidMonut`和`componentDidUpdate`中的代码都是同步执行

  ```js
  import React, { useEffect } from 'react'
  useEffect(() => {
      console.log(绑定组件一开始要做的事件)	//componentDidMonut/componentDidUpdate
  })
  ```

- 代替`componentWillUnmount`

  ```js
  import React, { useEffect } from 'react'
  useEffect(() => {
      console.log(绑定组件一开始要做的事件)	//componentDidMonut/componentDidUpdate
      return () => {
          console.log(组件销毁时解除绑定的事件)	//componentWillUnmount
      }
  }, [])	//数组中的值变化才解绑，为空表示组件销毁时才解绑
  ```

#### useContext

- 作用是对它所包含的组件树提供全局共享数据的一种技术

- 父组件：

  ```js
  import React, { useState , createContext } from 'react'
  import Child from './Child'
  const CountContext = createContext()
  function Parent(){
      const [ count , setCount ] = useState(0);
      return (
          <div>
              <p>You clicked {count} times</p>
              <button onClick={()=>{setCount(count+1)}}>click me</button>
              <CountContext.Provider value={count}>
                  <Child></Child>
              </CountContext.Provider>
          </div>
      )
  }
  export default Parent
  ```

- 子组件：

  ```js
  import React, { useState , createContext , useContext } from 'react'
  function Child(){
      const count = useContext(CountContext)  //一句话就可以得到count
      return (<h2>{count}</h2>)
  }
  export default Child
  ```

#### useReducer

- daima

  ```js
  import React, { useReducer } from 'react'
  function ReducerDemo(){
      const [ count , dispatch ] =useReducer((state,action)=>{
          switch(action){
              case 'add':
                  return state+1
              case 'sub':
                  return state-1
              default:
                  return state
          }
      },0)
      return (
         <div>
             <h2>现在的分数是{count}</h2>
             <button onClick={()=>dispatch('add')}>Increment</button>
             <button onClick={()=>dispatch('sub')}>Decrement</button>
         </div>
      )
  }
  export default ReducerDemo
  ```

-  使用`useContext`和`useReducer`是可以实现类似`Redux`的效果 



#### useMemo





#### useRef







#### useCallback 





































## 问答

1. react单向数据流
   - 父组件向子组件传值是只读的，子组件不可以改变 
2. react函数式编程
   - 可以清晰地看到函数的结构和方法
   - 方便测试