### v-show和v-if的区别？

### 为何v-for中要用key？

- 必须用key，且不能是index和random
- diff算法中通过tag和key来判断，是否是sameNode
- 减少渲染次数，提升渲染性能

### 描述Vue组件生命周期（有父子组件的情况）

父子组件：

- 父组件比子组件先创建
- 子组件比父组件先挂载
- 父组件比子组件先before update
- 子组件比父组件先update

单个组件：

- 挂载
- 更新
- 销毁

### Vue组件如何通讯？

- 父子组件props和this.$emit
- 自定义事件event.$no event.$off event.$emit
- vuex

### 描述组件渲染和更新的过程？

### 双向数据绑定v-model的实现原理

- input元素的value=this.name
- 绑定input事件this.name=$event.target.value
- data更新触发re-render

### 如何自己实现v-model?

### 对MVVM的理解

### computed有何特点？

- 缓存，data不变不会重新计算
- 提高性能

### 为和组件data必须是一个函数？

- 组件其实是一个class类，使用类得到的就是一个实例
- data为函数避免了各个实例共享一个data

### ajax请求应该放在那个生命周期？

- mounted
- JS是单线程的，ajax异步获取数据
- 放在mounted之前没有用，只会让逻辑更加混乱

### 如何将组件所有props传递给子组件？

- $props
- <User v-bind = "$props" />

### 多个组件有相同的逻辑，如何抽离？

- mixin

### 何时使用异步组件？

- 加载大组件
- 路由异步加载

### 何时需要使用keep-alive?

- 缓存组件，不需要重复渲染
- 如多个静态tab页的切换
- 优化性能

### 何时需要使用beforeDestory?

- 解绑自定义事件event.$off
- 清除定时器
- 解绑自定义的DOM事件，如window scroll等

### Vuex中action和mutation有何区别？

- action中处理异步，mutation不可以
- mutation做原子操作，一次一个
- action可以整合多个mutation

### 请用vnode描述一个DOM结构？

```
{
	tag: 'div',
	props: {
		className: 'container',
		id: 'div1'
	},
	children: [
		{
			tag: 'p',
			children: 'vdom'
		},
		{
			tag: 'url',
			props: {style: 'font-size: 20px'}
			children: [
				{
					tag: 'li',
					children: 'a'
				}
			]
		}
	]
}
```

### 监听data变化的核心API是什么？

- Object.defineProperty
- 以及深度监听，监听数组
- 有何缺点

### 简述diff算法过程？

- patch(elem, vnode)和patch(vnode, newVnode)
- patchVnode和addVnode和removeVnode
- updateCildren（key的重要性）

### Vue常见性能优化方式？

- 合理使用v-show和v-if
- 合理使用computed
- v-for时加key，以及避免和v-if同时使用
- 自定义事件、DOM事件及时销毁
- 合理使用异步组件
- 合理使用keep-alive
- data层级不要太深
- 使用v-loader在开发环境做模板编译（预编译）
- webpack层面优化
- 前端通用的性能优化，如图片懒加载
- 使用SSR

### Vue3升级内容

- 全部用ts重写（响应式、vdom、模板编译等）
- 性能提升，代码量减少
- 会调整部分API