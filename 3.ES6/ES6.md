## ES6开发环境

1. 初始化项目`npm init -y`

2. 全局安装`babel-cli`

3. 本地安装`babel-preset-es2015`和`babel-cli`

4. 新建`.babel`文件

   ```
   {
       "presets":[
           "es2015"
       ],
       "plugins":[]
   }
   ```

5. 在 `package.json`添加命令

   ```
   "scripts": {
       "build": "babel src/index.js -o dist/index.js"
     }
   ```

6.  可以使用 `npm run build` 来进行转换 

## 声明

#### `var`

- 可以重复声明同一个变量且后面覆盖前面
- 提升层级，在声明前可使用（undefined）
- 作用域以函数区域划分

#### `let`

- 声明变量
- for循环：在循环语句之内是一个父作用域，再循环体之中是一个子作用域

#### `const`

- 声明常量
- 声明的时候必须赋值
- 储存简单的数据类型时候不可改变其值
- 储存的是对象，只要引用不改变，对象里面的数据可以变化

**`let/const`共同特点：**

- 只在命令所在的代码块内有效，作用域为{}
- 在预解析的时候不会被提升
- 不允许在同一个作用域下声明已经存在的变量

## 解构赋值

- 本质上的一种匹配模式，只要等号两边的模式相同，那么左边的变量就可以被赋予对应的值

#### 数组

```
let [a, b, c, ...r] = [1, 2, 3, 4, 5]
```

```
let arr = ['aaaa','bbbb','ccc'];
function fun(a,b,c){
    console.log(a,b,c);
}
fun(...arr);
```

#### 对象

```
const obj = {a:'', b:'', c:''}
const {a, b, c} = obj
const {a:m, b:n, c:q} = obj		//别名
```

#### 函数

```
let json = {
    a:'aaa',
    b:'bbb'
}
function fun({a,b='ccc'}){	//b有默认值
    console.log(a,b);
}
fun(json);
```

#### 基本类型

```
let [a, b, c] = '123'
let {length: len} = 'changdu'
```



## 扩展运算符

#### 数组

```
const first = [1, 2, 3]
const second = [5, 6, 7]
//合并添加
const combined = [...first, 4, ...second, 8]
```

#### 对象

```
const first ={a:1, b:2}
const second = {d:4, e:5}
//合并添加
const combined = {...first, c:3, ...second, f:6}
```

- 不确定个数用`(...arg)`



## 数据类型

#### 字符串

- 模板字符串
  - 反引号包裹空格换行的字符串
  - ${变量/三元运算/函数}

- `str.trim()`：去掉字符串前后空格
- `str.repeat(n)`：将字符串重复n次(返回新值，不改变原值)
- `str.includes('x')`：字符串里是否包含x，包含返回true
- `str.startsWith('x')`：字符串开头里是否是x，是返回true
- `str.endsWith('x')`：字符串结尾里是否是x，是返回true
- `str.padStart(maxLength,fillString='')`：在字符串前面添加字符
- `str.padEndt(maxLength,fillString='')`：在字符串后面添加字符

#### 数字

- 二进制声明

  -  二进制的开始是0（零），然后第二个位置是b（注意这里大小写都可以实现） ， 然后跟上二进制的值 

  ```
  let binary = 0B010101;	//21
  ```

- 八进制声明

  -  八进制是以0（零）开始的，然后第二个位置是O（欧），然后跟上八进制的值 

  ```
  let b=0o666;	//438
  ```

- 数字判断

  -  使用`Number.isFinite( )`来进行数字验证，不论是浮点型还是整形都会返回true，其他返回false 

    ```
    let a= 11/4;
    console.log(Number.isFinite(a));//true
    console.log(Number.isFinite('zifuchuan'));//false
    console.log(Number.isFinite(NaN));//false
    console.log(Number.isFinite(undefined));//false
    ```

  -  使用`Number.isNaN()`来进行验证是否为数字

  - 使用`Number.isInteger()`来判断是否为整数

    ```text
    let a=123.1;
    console.log(Number.isInteger(a)); //false
    ```

- 整数转换

  ```
  let a='9.18';
  console.log(Number.parseInt(a)); 
  ```

- 浮点数转换

  ```
  let a='9.18';
  console.log(Number.parseFloat(a));
  ```

- 整数取值范围

  ```
  let a = Math.pow(2,53)-1;
  console.log(a);  //9007199254740991
  ```

- 最大安全整数

  ```
  consolec .log(Number.MAX_SAFE_INTEGER);
  ```

- 最小安全整数

  ```
  console.log(Number.MIN_SAFE_INTEGER);
  ```

- 安全整数判断

  ```
  console.log(Number.isSafeInteger(a));
  ```

#### 数组

- in

  ```
  let arr=[,,,,,];
  console.log(0 in arr); //返回false，判断数组空项
   
  let arr1=['aaa','bbb'];
  console.log(0 in arr1);  //返回true
  ```

- 数组方法

  - `Array.of()`：创建一个数组（括号中一个数不再代表数组长度）
  - `Array.from(类数组)`：把一个类数组转换成真正的数组
  - `Array.isArray(arr)`：判断是否是数组，返回true/false

- 实例方法

  - `Arr.find(function(value, index, arr){})`：

    在数组中查找符合回调函数的第一个元素并返回此元素

  - `Arr.findIndex(function(value, index, arr){})`：

    在数组中查找符合回调函数的第一个元素并返回此元素的下标

  - `Arr.fill('x', m, n)`：

    将数组中m到n（不包含n）之间的每一个元素都替换为x，如没有m和n则全部替换为x

  - `for (let item of Arr) { console.log(item) }`：

    循环输出数组中的每一项值

    - `for (let item of Arr.keys()) { console.log(item) }`：

      循环输出数组的index值

    - `for (let item of Arr.entries()) { console.log(item) }`：

      循环输出数组的键值对

    - `for (let [index, value] of Arr.entries()) { console.log(index, value) }`：

      将键值对分离

  - `Arr.entries()`是`ArrayIterator`类型数组（手动输出），每`Arr.entries().next()`一次，按顺序输出一次键值对

#### 对象

- in

  ```
  let obj={
      a:'aaa',
      b:'bbb'
  }
  console.log('a' in obj);  //true
  ```

- `for (let item of Object) { console.log(item) }`：循环输出对象的属性值

- 声明的变量直接赋值给对象

  ```
  let name="parker";
  let skill= 'web';
  var obj= {name,skill};
  console.log(obj);  //Object {name: "parker", skill: "web"}
  ```

- 对象key键构值

  ```
  let key='skill';
  var obj={
      [key]:'web'
  }
  console.log(obj.skill);
  ```

- 对象比较

  ```
  var obj1 = {name:'parker'};
  var obj2 = {name:'parker'};
  console.log(obj1.name === obj2.name);	//true
  console.log(Object.is(obj1.name,obj2.name));	//true
  ```

  区别：

  ```
  console.log(+0 === -0);				//true
  console.log(NaN === NaN ); 			//false
  console.log(Object.is(+0,-0)); 		//false
  console.log(Object.is(NaN,NaN)); 	//true
  ```

- 合并对象 `assgin( )`

  ```
  var a={a:'parker'};
  var b={b:'dyz'};
  var c={c:'web'};
   
  let d=Object.assign(a,b,c)
  console.log(d);		//{a: "parker", b: "dyz", c: "web"}
  ```

#### 函数

- 为函数参数指定默认值

  ```
  function fn(a=10,b=20){...}
  ```

- 函数的简写形式

  ```
  fn(){...}相当于fn = function (){...}
  ```

- 函数的剩余参数

  ```
  function fn(a,b, ...r)	//r是个数组（而函数的arguments是类数组）
  ```

- 箭头函数

  ```
  (a, b) => a + b
  (a, b) => { return a + b }
  ```

  - 不能使用call/apply/bind改变其内部的this指向
  - 没有arguments对象，可以用剩余参数代替
  - 不可以当作构造函数，不可以使用new命令
  - 返回对象要用（）括起来，否则会把值当做函数体，键当做它的标签
  - 函数体内的this始终指向定义时的外部作用域的this

#### Symbol

- `JS`的第七种数据类型，表示独一无二的值

- Symbol函数前不能使用new否则会报错，因为symbol是一个原始类型的值，不是对象

- Symbol函数接受一个字符串作为参数，表示对Symbol的描述

  ```
  let obj = {a:1}
  let a = Symbol("a");
  obj[a] = "sa";
  console.log(obj)=>obj{a:1, Symbol("a"):"sa"}
  ```

- 不能被for...in循环遍历，可以通过`object.getOwnPropertySymbols`方法获得一个对象的所有的Symbol属性

  ```
  let obj={name:'parker',skill:'web'};
  let age=Symbol();
  obj[age]=18;	//年龄用symbol表示
  for (let item in obj){
      console.log(obj[item]);
  } 
  console.log(obj);	////{"parker", "web"}，age不能被遍历
  ```

  

## 数据结构

- `JSON`也是一种数据结构

#### set

- 集合：是由一组无序唯一的项组成，key和value相同，没有重复的value
- 创建：`const s = new Set([1, 2, 3])`
- 属性：`s.size`（类似与`s.length`）
- 方法
  - `s.add(value)`：添加一个数据，返回set结构本身
  - `s.delete(value)`：删除指定数据，返回一个布尔值，表示删除是否成功
  - `s.has(value)`：判断该值是否为set的成员，返回一个布尔值
  - `s.clear()`：清除所有数据，没有返回值
  - `s.keys()`：返回键名的遍历器
  - `s.values()`：返回键值的遍历器
  - `s.entries()`：返回键值对的遍历器
  - `s.next()`：返回按顺序插入的值和是否完成（value: xxx, done: false）
  - `s.forEach(function(value, key, set){...})`：使用回调函数遍历每个成员

#### map

- 字典：是用来储存不重复key的Hash结构，使用[键，值]的形式来储存数据
- 创建：`const m = new Map([['a', 1], ['b', 2]])`
- 属性：`m.size`（类似与`m.length`）
- 方法：
  - `m.set(key, value)`：设置键值对，返回整个map结构（如果key有值则更新，没key则创建）
  - `m.get(key)`：读取key对应的值，如找不到key则返回undefined
  - `m.delete(key)`：删除某个键，返回true，删除失败返回false
  - `m.has(key)`：判断某个键是否在当前map对象之中，返回一个布尔值
  - `m.clear()`：清除所有数据，没有返回值
  - `m.keys()`：返回键名的遍历器
  - `m.values()`：返回键值的遍历器
  - `m.entries()`：返回键值对的遍历器
  - `m.forEach(function(value, key, map){...})`：使用回调函数遍历每个成员

## proxy

- 翻译为“代理”，相当于组件的生命周期钩子函数，不过添加于函数上

- 声明：

  ```js
  var pro = new Proxy（{
  	//函数主体
      add: function (val) {
          return val + 10;
      },
      name: 'I am parker'
  },{
  	//代理处理
  	get:function(target,key){
          console.log('come in Get');
          return target[key];		//'I am parker'
      },
      set:function(target,key,value,receiver){
          console.log(`setting ${key} = ${value}`);
          return target[key] = value;
      }
  }）
  console.log(pro.name)
  ```

  - get属性： 在得到某对象属性值时预处理的方法， 他接受三个参数 

    - target：目标对象
    - key： 目标的key值，相当于对象的属性 
    - property：

    

  - set属性： 要改变Proxy属性值时，进行的预先处理。它接收四个参数 
    - target：目标对象
    - key： 目标的key值
    -  value：要改变的值 
    -  receiver：改变前的原始值 

  -  apply方法：调用内部的方法，它使用在方法体是一个匿名函数时 

    ```js
    get = function () {
        return 'I am parker';
    };
    var handler = {
        apply(target, ctx, args) {
            console.log('do apply');
            return Reflect.apply(...arguments);
        }
    }
     
    var pro = new Proxy(target, handler);
    console.log(pro());
    ```

## promise

- promise函数不是异步，里面的程序才是异步

- 创建对象：

  ```js
  var p = new Promise((res,rej)=>{
      res("成功参数")
      rej("失败参数")
  })
  ```

  

- 实例方法：

  - `p.then((data1)=>{}).then((data2)=>{})`	//`data1`为res中的"成功参数",`data2`为前面then回调函数中成功参数\
  - `p.catch((err)=>{})`	//err为`rej`中的"失败参数"
  - `p.finally(()=>{})`       //无参数，无论成功失败都会执行
  - `p.then((data)=>{},(err)=>{})`        //then和catch合并写法

- 静态方法：

  - `Promise.resolve()`        //直接创建一个成功的promise

  - `Promise.reject()`        //直接创建一个失败的promise

  - ```
    var p = Promise.all([p1,p2,p3])
    p.then((data)=>{})        //data为三个不同的promise成功参数的数组
    ```

  - ```
    var p = Promise.race([p1,p2,p3])
    p.then((data)=>{})        //data为最先完成的promise的成功参数
    ```

    

## async...await

- 作用：简化Promise函数，以同步函数的书写方式表达异步函数
- `async`：写在Promise最近的函数前面
- `await`：写在Promise前面，返回的是成功后的数据
- `try...catch`：抓取Promise错误，将await移至try里，error写在catch里



## class

- 定义在类中的方法都是不可以枚举的（`obj.keys(XXX.prototype)`）

- 声明

  ```
  class 类名{
          constructor(属性) //构造函数
               this.属性 = 属性  //实例属性
          }
          实例方法(){...}
          static.静态属性 = “...”
          static 静态方法(){...}
  }
  ```

  - class的{}内只能写构造器、实例属性/方法或静态属性/方法
  - 类中的方法都挂载在prototype上
  - 类中的静态方法和属性都挂载在constructor上

- 继承

  ```
  class 子类 extends 父类{
        constructor(要继承的父类属性,新增属性){
              super(要继承的父类属性);
              this.新增属性 = 新增属性; //只能放在super后
        }
  }
  ```

  - 为父类指定静态方法，使用static方法名字
  - super:
    - 在构造函数中可以当一个函数来使用，相当于调用父类的构造函数
    - 在原型方法中，可以当一个对象来使用，相当于父类的原型对象，并且会自动绑定this到子类上



## generator

- generator由function*定义（注意多出的*号），并且，除了return语句，还可以用yield返回多次

- 调用generator对象有两个方法

  - next()方法
    - next()方法会执行generator的代码，然后，每次遇到yield x;就返回一个对象{value: x, done: true/false}，然后“暂停”
    - 返回的value就是yield的返回值，done表示generator是否已经执行结束。如果done为true，则value就是return的返回值
  - for ... of循环迭代generator对象

- generator还有另一个巨大的好处，就是把异步回调代码变成“同步”代码

  ```
  try {
      r1 = yield ajax('http://url-1', data1);
      r2 = yield ajax('http://url-2', data2);
      r3 = yield ajax('http://url-3', data3);
      success(r3);
  }
  catch (err) {
      handle(err);
  }
  ```

  

