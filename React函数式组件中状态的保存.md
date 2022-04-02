# 问题概述

函数式组件要比类式组件性能消耗低，并且在hooks出现后更是替代了许多类式组件，但同一个函数式组件作为子组件在不同的父组件之间调用或者切换，其状态是如何改变的呢？

# 实验比较

## 组件声明

### Son组件

```jsx
let a = 0
const Son: FC = () =>{
    let b = 0
    const hand = () => {
        a = 1
        b = 2
    	setC(3)
    }
  	const [c, setC] = useState(0)	//如果没有useState，的点击后不会触发重新渲染

    return (
        <>
            <div>Son组件a:{a}，b:{b}，c:{c}</div>
            <Button onClick = {hand}>点击</Button>
        </>
    )
}

export default Son
```

### Father组件

```jsx
const Father: FC = () =>{
    return (
        <>
            <div>Father组件</div>
            <Son />
        </>
    )
}

export default Father
```

### Mother组件

```jsx
const Mother: FC = () =>{
    return (
        <>
            <div>Mother组件</div>
            <Son />
        </>
    )
}

export default Mother
```

### Stranger组件

```jsx
const Stranger: FC = () =>{
    return (
        <>
            <div>Stranger组件</div>
        </>
    )
}

export default Stranger
```

## 点击实验

1. 在Father组件中点击按钮显示：

   ```Son组件a:1，b:0，c:3```

2. 切换到Mother组件显示：

   ```Son组件a:1，b:0，c:3```

3. 切换到Stranger组件再切回Mother组件显示：

   ```Son组件a:1，b:0，c:0```

4. 点击后显示：

   ```Son组件a:1，b:0，c:3```

## 总结

### 在函数式组件外层声明变量

- a的值一旦被改变在所有父母组件中都会改变
- 不受子组件重新渲染影响

### 在函数式组件内层声明变量

- 函数内b的值会改变，但是useState触发重新渲染后let b = 0将重新覆盖b值，所以页面上b一直为初始值

### 在函数式组件中使用useState

- c的值一旦被改变在所有父母组件中都会改变
- 会受子组件重新渲染影响

## 延申

- 函数外层不要写任何变量
- 函数内层只能写const常量
- 其他变量写在useState中，变量一旦改变就会更新视图
- 子组件创建销毁后需要保存的数据用useReducer和useContext保存（模拟redux）