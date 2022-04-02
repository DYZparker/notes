# 1. JavaScript简介

## 1.1 JavaScript是什么？

- HTML是网页的结构，CSS是网页的外观，而JavaScript是页面的行为。

- HTML页面是静态的（只供浏览），平常我们所见到的各种网页特效就是使用JavaScript实现的。

## 1.2 JavaScript的特点

- 动态改变页面内容
  HTML页面是静态的，一旦编写，内容是无法改变的。JavaScript可以弥补这个不足，可以将内容动态地显示在网页中。

- 动态改变网页的外观
  JavaScript通过修改网页元素的CSS样式，达到动态地改变网页的外观。

- 验证表单数据
  我们常见的在各大网站中的注册中的验证功能，就是JavaScript实现的。

- 响应事件
  JavaScript是基于事件的语言。例如点击一个按钮弹出一个对话框，就是鼠标点击触发的事件，例如绿叶学习网教程文章中的点赞效果：

> 对于JavaScript的理解，就一句话：如果没有使用JavaScript，网页就是静态的，唯一的功能就是给用户浏览。加入了JavaScript，网页变得绚丽多彩起来。

## 1.3 JavaScript在HTML的引用

### 1.3.1 script标签

- 属性（都为可选属性）

  | 属性    | 值              | 说明                                                         |
  | ------- | --------------- | ------------------------------------------------------------ |
  | type    | text/javascript | 编写代码使用的脚本语言的类型                                 |
  | charset |                 | 通过src属性指定的代码的字符集                                |
  | src     | 字符串          | 外部脚本文件地址                                             |
  | async   | async           | 异步加载在onload执行前被触发，加载完就触发，无顺序执行，只对外部脚本有效 |
  | defer   | defer           | 延迟加载在onload执行前被触发，等同于写在body底部，按顺序执行，只对外部脚本有效 |

- 使用方式

  - 直接嵌入代码，只须指定type属性

  - 引用外部脚本文件，必须加入src属性

    > 如在引用外部脚本的```<script>```标签中嵌入代码，则该代码会被忽略

### 1.3.2 引用方式

- 页头引入（head标签内）；

  > 在body之前执行JS可能会导致页面留白，可添加defer属性延迟加载


- 页中引入（body标签内）；

  > 放在body底部，IE7不支持defer

- 元素事件中引入（标签属性中引入）；

- 放在一个URL里，使用特殊的“javascript:”协议；

## 1.4 基本语法

- 执行顺序

  JavaScript程序按照在HTML文档中出现的顺序逐行执行。如果需要在整个HTML文件中执行，最好将其放在HTML文件的标签中。某些代码，如函数体内的代码，不会被立即执行，只有当所在的函数被其他程序调用时，该代码才会被执行。

- 区分大小写

  JavaScript是严格区分大小写的。例如str和Str这是两个完全不同的变量。

- 分号和空格

  在JavaScript中，语句的分号“;”是可有可无的。但是我们强烈要求大家在每一句语句后面加一个分号“;”，这是一个非常重要的代码编写习惯。

  另外，JavaScript会忽略多余的空格，用户可以向脚本添加空格，来提高代码的可读性，说白了就是让代码“漂亮点”，读得舒服一点。

  ```js
  var str="JavaScript教程";
  var str = "JavaScript教程";  //这一行代码读起来舒服一点
  ```

## 1.5 注释

在编写JavaScript代码时，我们经常要在一些关键代码旁做一下注释，这样做的好处很多。

```js
//单行注释内容
/*多行注释内容*/
```

“//”是单行注释方式，如果你的注释内容只占一行就应该使用这种注释方式。

“/**/”是多行注释方式，如果你的注释内容占多行建议使用这种注释方式。



# 2. 数据

## 2.1 数据结构

JavaScript的数据结构包括：标识符、关键字、常量、变量等。

### 2.1.1 标识符

标识符，说白了，就是一个名字。在JavaScript中，变量和函数等都需要定义一个名字，这个名字就可以称为“标识符”。

JavaScript语言中标识符最重要的3点就是：

- 第一个字符必须是字母、下划线（_）或美元符号这3种其中之一，其后的字符可以是字母、数字或下划线、美元符号；

- 变量名不能包含空格、加号、减号等符号；

- 标识符不能和JavaScript中用于其他目的的关键字同名；

### 2.1.2 关键字

JavaScript关键字是指在JavaScript语言中有特定含义，成为JavaScript语法中一部分的那些字。

### 2.1.3 常量

常量，顾名思义就是指不能改变的量。常量的指从定义开始就是固定的，一直到程序结束。

常量主要用于为程序提供固定和精确的值，包括数值和字符串，如数字、逻辑值真（true）、逻辑值假（false）等都是常量。

### 2.1.4 变量

变量，顾名思义，就是指在程序运行过程中，其值是可以改变的。

## 2.2 数据类型

JavaScript数据类型有两大分类：一是“基本类型”，二是“引用类型”。

- 基本类型包括以下五种：
  - 空值（null型）；
  - 未定义值（undefined型）；
  - 字符串型（String型）；
  - 数字型（Number型）：
    - 整型
    - 浮点型
    - NaN
  - 布尔型（Boolean型）：
    - true：非0数字、非空字符串、函数、能找到的元素、[]、{}
    - false：0、空字符串、NaN、不能找到的元素、null、undefined
- 引用类型有一种：
  - 对象（Object型）；

## 2.3 类型检测

### 2.3.1 基本类型检测

```js
typeof XXX
```

检测结果为六种：

- undefined
- string
- number
- boolean
- object（包含检测null的结果）
- function

### 2.3.2 引用类型检测

- ```js
  XXX instanceof Object/Array/RegExp
  ```

  - 用原型链来检测引用类型，返回true/false
  - 检测到基本类型也返回false

- ```js
  Object.prototype.toString.call(arr) == '[object Array]'
  ```

  - 用原型方法判断

## 2.4 类型转换

### 2.4.1 显式转换

- Boolean(XXX)
- Number(XXX)
  - 可用于任何数据类型
  - true为1false为0
  - " "或[ ]或null为0
  - { }或undefined为NaN
  - 数组：包含一个数字可以转，多个为NaN
- parseInt(XXX, [进制])
- parseFloat(XXX)
- String(XXX)
  - 值是null或undefined则返回null或undefined
  - 其他值则调用XXX.toString()
- XXX.toString()
  - 不能用于null和undefined
  - 数值进制转换：num.toString(16)
  - 类型判断：Object.prototype.toString.call(arr) == '[object Array]'
- XXX.toFixed()
  - 把数字转为字符串，结果的小数点后指定位数的数字按四舍五入取值

### 2.4.2 隐式转换

- ```+```：只要一边为字符串即为拼接操作
- ```++ --```：前置自增++num先加1再返回，后置自增num++先返回原值参与表达式计算再加1，单独使用前后都一样
- ```- * / %```：有字符串也转为数字计算
- ```> <```：如有字符串则只比较第一位
- ```!```：取反，转为布尔值
- ```==```：基本类型是值的比较，引用类型是地址的比较；null == undefined为true；[ ] == [ ]为false；{ } == { }为false
- ```===```：在==的基础上加入类型比较

## 2.5 运算符

### 2.5.1 逻辑运算符

- ```&&```：与；

  ```js
  var a = 120>100 && 20  //a=20
  ```

- ```||```：或；

  ```js
  var b = 100>120 || 20  //b=20
  ```

- ```!```：非；

> 优先级：先```&&```后```||```

### 2.5.2 三元运算符

```js
条件判断 ? true执行代码1 ：false执行代码2
```

## 2.6 流程控制

JavaScript对程序流程的控制跟其他编程语言是一样的，主要有3种：

### 2.6.1 条件语句

- if语句;

  ```js
  if(condition1){
  	statement1;
  }else if(condition2){
  	statement2;
  }else{
  	statement3;
  }
  ```

- if语句的嵌套;

- switch语句;

  ```js
  switch(expression){
  	case value1:
  	statwment1;
  	break;
  	...
  	default:(可选)
  	statwmentX;
  }
  ```

### 2.6.2 循环语句

- for语句；

  ```js
  //适合已知循环次数
  for(语句1；语句2；语句3){
  	被执行的代码块；
  }
  //语句1：在循环开始前执行
  //语句2：定义循环执行的条件
  //语句3：在循环后执行
  ```

- for……in语句；

  ```js
  for(var key in object){...};  //把对象的所有属性依次循环出来
  for(var i in array){...};  //把数组的所有索引依次循环出来（但得到的是string不是number）
  ```

- for......of语句；

  ```js
  for(let item of array){...};  //直接把数组元素依次循环出来（ES2015新增，更好的循环数组）
  ```

- while语句；

  ```js
  //适合未知循环次数（条件满足才执行）
  while(条件){
  	需要执行的代码；
  }
  ```

- do……while语句；

  ```js
  //适合未知循环次数（执行一次才判断）
  do{
  	需要执行的代码；
  }while(条件)
  ```

### 2.6.3 跳转语句

- break语句：立即退出当前循环

- continue语句：结束当前循环进行下一次循环



# 3. 函数

## 3.1 函数是什么？

函数，就是一个一系列JavaScript语句的集合，这是为了完成某一个会重复使用的特定功能。在需要该功能的时候，直接调用函数即可，而不必每次都编写一大堆重复的代码。并且在需要修改该功能的时候，也只要修改和维护这一个函数即可。

总之，将语句集合成函数，好处就是方便代码重用。并且，一个好的函数名，可以让人一眼就知道这个函数实现的是什么功能，方便维护。

## 3.2 函数的定义

### 3.2.1 函数声明

> 会提升函数声明

```js
function fnName (参数1,参数2,….,参数n) {
    //函数体语句
}
```

### 3.2.2 函数表达式

> 不会提升函数声明

- 匿名函数表达式；

  ```js
  var fn1 = function (参数1,参数2,….,参数n) {
      //函数体语句
  }
  ```
  
- 具名函数表达式；

  ```js
  var fn2 = function fnName (参数1,参数2,….,参数n) {  //外部访问不到fnName，它只作为fn2.name的属性
      //函数体语句
  }
  ```

说明：

定义函数必须使用function关键字来定义。

函数名必须是唯一的，尽量通俗易懂，并且跟你定义的代码有关。

函数可以使用return语句将某个值返回，也可以没有返回值。

参数是可选的，可以不带参数，也可以带多个参数。如果是多个参数的话，参数之间要用英文逗号隔开。

## 3.3 函数的属性

### 3.3.1 name

### 3.3.2 length

- 表示函数希望接收的命名参数个数
- 不包括剩余参数，仅包括“第一个具有默认值之前的参数个数”

### 3.3.3 prototype

- 指向对象的原型对象的引用
- 属性不可枚举

## 3.4 函数的方法

### 3.4.1 call()

```js
fn.call([thisFn[,arg1[,arg2[,[,argN]]]]]) 
```

>参数为确定的

### 3.4.2 apply()

```js
fn.apply([thisFn[,argArray]]) 
```

> 参数为数组或arguments对象

### 3.4.3 bind()

```js
newFn = fn.bind(thisFn)
```

> 返回一个新函数，不会立即执行

### 3.4.4 toString()

```js
fn.toString()
```

> 返回函数的完整代码

### 3.4.5 Getter

```js
get todo () {}
```

> 读取该属性时调用get后的属性方法

### 3.4.6 Setter

```js
set todo () {}
```

> 设置该属性时调用set后的属性方法

## 3.5 函数的作用域

- 预解析
  - 找var、function、函数参数（本质就是局部变量）；
  - var声明的变量都赋予undefined；
  - function声明的函数都赋予整个函数块；
  - 如果变量和函数重名则只留下函数
- 逐行执行代码

  - 表达式可以修改预解析的值
  - 执行顺序自上而下由里到外
  - if和for没有域
  - this始终指向当前对象

## 3.6 函数的参数

### 3.6.1 arguments

```js
function example(x){
    alert(x); //1，多个参数只能传入第一个给x
    alert(arguments.length); //3，arguments包含所有传入参数
    for(var i=0; i<arguments.length; i++){
        alert(arguments[i]);  //1,2,3   
    }      
}
example(1,2,3);
```

- argument是JavaScript中的一个关键字，用于指向调用者传入的所有参数。
- argument并不是数组而是类数组，有数组的length方法和argument[0]
- argument.callee：是一个指针，指向拥有这个arguments对象的函数

### 3.6.2 rest

　由于JavaScript函数允许接收任意个参数，所以不得不用arguments来获取函数定义a以外的参数。

```js
function exm(a) {
    var rest = [];
    if (arguments.length > 1) {
        for (var i = 1; i<arguments.length; i++) {
            rest.push(arguments[i]);
        }
    }
}
```


　其实ES6给了新的rest参数，用在函数最后，多余的参数以数组的形式交给变量rest，如果传入的参数未填满函数定义的参数，rest会是一个空数组。

```js
function exm(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

exm(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

exm(1);
// 结果:
// a = 1
// b = undefined
// Array []
```




```html
<script>
    function say() {
		console.log('Hello' + arguments[0] + arguments[1]);
		console.log(arguments.length);
	}
	say('World！', 'ByeBye！');
</script>
```



## 3.7 特殊函数

### 3.7.1 嵌套

嵌套函数，顾名思义，就是在一个函数的内部定义另外一个函数。不过在内部定义的函数只能在内部调用，如果在外部调用，就会出错。

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <script type="text/javascript">
        //定义阶乘函数
         function fun(a) {
             //嵌套函数定义，计算平方值的函数
             function multi (x) {
                 return x*x;
             }
             var m=1;
             for(var i=1;i<=multi(a);i++) {
                 m=m*i;
             }
             return m;
         }
         var sum =fun(2)+fun(3);
         document.write(sum);
    </script>
</head>
<body>
</body>
</html>
```

### 3.7.2 递归

递归函数用于让一个函数从其内部调用其本身。不过需要注意的是，如果递归函数处理不当，就会使程序陷入“死循环”。为了防止“死循环”的出现，可以设计一个做自加运算的变量，用于记录函数自身调用的次数，如果次数太多就让它自动退出循环。

```js
function 递归函数名(参数1) {
    递归函数名(参数2)
}
```

说明：

在定义递归函数时，需要2个必要条件：

- 首先包括一个结束递归的条件；

- 其次包括一个递归调用的语句；

举例：

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <script type="text/javascript">
         var msg="\n函数的递归调用：\n\n";
         //响应按钮的点击事件
         function Test() {
             var result;
             msg+="调用语句：\n";
             msg+="    result=sum(20);\n";
             msg+="调用步骤：\n";
             result=sum(20);
             msg+="计算结果：\n";
             msg+="    result="+result+"\n";
             alert(msg);
         }
         //计算当前步骤加和值
         function sum(m) {
             if(m==0) {
                 return 0;
             } else {
                 msg+="    result="+m+"+sum("+(m-2)+ ");\n";
                 result=m+sum(m-2);
             }
             return result;
         }
    </script>
</head>
<body>
    <input type="button" value="测试" onclick="Test()"/>
</body>
</html>
```

分析：

在上述代码中，为了求取20以内的偶数和，定义了递归函数sum(m)，而函数Test()对其进行调用，并使用alert()方法弹出相应的提示信息。

### 3.7.3 闭包

- 闭包就是携带状态的函数，并且它的状态可以完全对外隐藏起来
- 有权访问另一个函数作用域中变量的函数，并且让这些变量的值始终保存在内存中
- 返回函数不要引用任何循环变量或者后续会发生变化的变量
- 函数内部有局部变量外部不能访问，且局部变量作为结果返回



## 3.8 箭头函数

### 3.8.1 特点

- 不能使用call/apply/bind改变其内部的this指向
- 没有arguments对象，可以用剩余参数代替
- 不可以当作构造函数，不可以使用new命令
- 返回对象要用（）括起来，否则会把值当做函数体，键当做它的标签
- 函数体内的this始终指向定义时的外部作用域的this



## 3.9 内置函数

### 3.9.1 eval()

在JavaScript中，eval()函数可以把一个字符串当做一个JavaScript表达式一样去执行它。例如：

```js
eval("document.write('<strong>JavaScript入门教程</strong> ')");
```

上面语句说白了就是执行“document.write('JavaScript入门教程 ')”,eval()函数用了等于没用一样。这是这种“多此一举”的做法，在实际开发很少用到eval()函数。

### 3.9.2 isFinite()

在JavaScript中，isFinite()函数用来确定某一个数是否是一个有限数值。

```js
isFinite(number)
```

说明：

number参数是必选的，可以是任意的数值，例如整型、浮点型数据。

如果该参数为非数字、正无穷数和负无穷数，则返回false；否则的话，返回true。如果是字符串类型的数字，就会自动转化为数字型。

### 3.9.3 isNaN()

```js
isNaN(参数)
```

说明：

这里的参数可以是任何类型的数据，例如数字型、字符串型、日期时间型等。不过得注意一点，当参数是“字符串类型的数字”，就会自动转换为数字型。

例如：

```js
123 //这不是NaN值
"123"  //这也不是NaN值，因为“字符串类型的数字”会被自动转换为数字型
"abc123"  //这是NaN值
```

### 3.9.4 parseInt()和parseFloat()

在JavaScript中，将字符串型数据转换为数值型数据有parseInt()和parseFloat()这2种方法。

```js
parseInt()  //将字符串型转换为整型
parseFloat()  //将字符串型转换为浮点型
```

说明：

将字符串型转换为整型，前提是字符串一定要是数值字符串。那什么叫数值字符串呢？“123”、“3.1415”这些只有数字的字符串就是数值字符串，而“hao123”、“360cn”等就不是数值字符串。

### 3.9.5 escape()和unescape()

- escape()

  escape()函数主要作用就是对字符串进行编码，以便它们能在所有计算机上可读。

  ```js
  escape(charString)
  ```

  说明：

  charString是必选参数，表示要进行编码的字符串或文字。escape()函数返回一个包含charString内容的字符串值（Unicode格式）。除了个别如“*@”之类的符号外，其余所有空格、标点符号以及其他非ASCII字符均可用“%xx”这种形式的编码代替，其中xx等于表示该字符的十六进制数。

  举例：

  ```html
  <!DOCTYPE html>
  <html xmlns="http://www.w3.org/1999/xhtml">
  <head>
      <title></title>
      <script type="text/javascript">
          document.write(escape("hello lvye!"))
      </script>
  </head>
  <body>
  </body>
  </html>
  ```

  分析：

  空格符对应的编码是“%20”，感叹号对应的编码是“%21”，因此执行escape("hello lvye!")后结果为“hello%20lvye%21”。

- unescape()

  escape()函数和unescape()函数是刚好反过来的，前者是编码，后者是解码。

  ```js
  unescape(charString)
  ```

  说明：

  charString是必选参数，表示要进行解码的字符串。unescape()函数返回指定值的ASCII字符串。与escape()函数相反，unescape()函数返回一个包含charString内容的字符串值，所有以“%xx”十六进制形式编码的字符都用ASCII字符集中等价的字符代替。

  举例：

  ```html
  <!DOCTYPE html>
  <html xmlns="http://www.w3.org/1999/xhtml">
  <head>
      <title></title>
      <script type="text/javascript">
          document.write(unescape("hello%20lvye%21"))
      </script>
  </head>
  <body>
  </body>
  </html>
  ```

  分析：

  空格符对应的编码是“%20”，感叹号对应的编码是“%21”，因此执行unescape("hello%20lvye%21")后结果为“hello lvye!”。



# 4. 对象

## 4.1 对象的定义

无序属性的集合，其属性值可以包含基本值、对象或者函数

## 4.2 对象的创建

### 4.2.1 普通创建对象

- **对象字面量**

  ```js
  var obj = {}
  ```

- **new操作符**

  ```js
  var obj = new Object()
  ```

- **Object.create()**

  ```js
  var obj = Object.create(原型对象, [属性的描述]);
  var obj1 = Object.create(null);		//没有原型的对象，不继承任何属性和方法，比如toString()
  var obj2 = Object.create(Object.prototype);		//和{}和new Object()创建的一样
  ```

### 4.2.2 函数创建对象

- **工厂函数模式**

  ```js
  function createPerson (name, age, job) {
  	var o = new Object();
  	o.name = name;
  	o.age = age;
  	o.job = job;
  	o.sayName = function () {
  		alert(this.name);
  	}
  	return o;
  }
  var person1 = createPerson("Parker", 36, "Software Engineer")
  var person2 = createPerson("Greg", 26, "Doctorr")
  ```

  - 函数名用驼峰形式
  - 以函数来封装以特定接口创建对象的细节

- **构造函数模式**

  ```js
  function Person (name, age, job) {
  	this.name = name;
  	this.age = age;
  	this.job = job;
  	this.sayName = function () {
  		alert(this.name);
  	}
  }
  var person1 = new Person("Parker", 36, "Software Engineer")
  var person2 = new Person("Greg", 26, "Doctorr")
  ```

  - 函数名首字母大写
  - 没有显式地创建对象
  - 将属性和方法直接赋给了this对象
  - 没有return语句
  - 创建实例必须使用new操作符

  缺点：因为sayName方法是function函数定义的，每定义一个函数就实例化了一个对象，所以两个person1和person2的sayName方法不是同一个Function的实例

  解决办法：

  ```js
  function Person (name, age, job) {
  	this.name = name;
  	this.age = age;
  	this.job = job;
  	this.sayName = sayName;	//将this.sayName方法的指针指向一个全局函数
  }
  function sayName () {
  	alert(this.name);
  }
  var person1 = new Person("Parker", 36, "Software Engineer")
  var person2 = new Person("Greg", 26, "Doctorr")
  ```

  解决后的缺点：不利于函数的封装

- **原型模式**

  ```js
  function Person () {
  }
  Person.prototype = {	//Person.prototype指向了新建的对象字面量，constructor属性也指向了Object构造函数
  	constructor : Person;	//共享属性，用于重新定向构造函数，但constructor属性变为可枚举了
  	name : "Parker";	//共享属性的值为基本类型，实例的同名属性的值将会屏蔽原型链的值，但不影响其他实例
  	age : 26;
  	job : "Software Engineer";
  	this.friends = ["Shelby", "Court"];		//共享属性的值为引用类型，所有实例的此属性都将指向同一地址
  	sayName : function () {
  		alert(this.name);
  	}
  }
  Object.defineProperty(Person.prototype, "constructor", {	//重设构造函数
  	enumerable: false;	//不可枚举
  	value: Person;
  })
  var person1 = new Person();
  var person2 = new Person();
  person1.name = "Nicholas";
  person1.friends.push("Van");
  
  alert(person1.name);		//"Nicholas"
  alert(person2.name);		//"Parker"
  alert(person1.friends);		//"Shelby, Court, Van"
  alert(person2.friends);		//"Shelby, Court, Van"
  alert(person1.friends === person2.friends);		//true
  ```

  缺点：不能传参，共享属性的值为引用类型时，一个实例更改其值会影响所有实例

- **组合使用构造函数模式和原型模式**

  ```js
  function Person (name, age, job) {
  	this.name = name;
  	this.age = age;
  	this.job = job;
  	this.friends = ["Shelby", "Court"];
  }
  Person.prototype = {	//Person.prototype指向了新建的对象字面量，constructor属性也指向了Object构造函数
  	constructor : Person;	//共享属性，用于重新定向构造函数，但constructor属性变为可枚举了
  	sayName : function () {		//共享方法
  		alert(this.name);
  	}
  }
  Object.defineProperty(Person.prototype, "constructor", {	//重设构造函数
  	enumerable: false;	//不可枚举
  	value: Person;
  })
  //如没有其他的共享属性挂载，只有共享方法的话，可以简写为
  Person.prototype.sayName = function () {
  	alert(this.name);
  }
  var person1 = new Person("Parker", 36, "Software Engineer")
  var person2 = new Person("Greg", 26, "Doctorr")
  ```

  - 构造函数模式用于定义实例属性
  - 原型模式用于定义方法和共享的属性

## 4.3 对象的原型和原型链

**任何函数（包括构造函数）创建时都会自动获得prototype属性，指向这个函数的原型对象（用途是包含可以由特定类型的所有实例共享的属性和方法），而这个原型对象也自动获得constructor属性指向prototype属性所在的函数，构造函数创建的实例自动获得```__proto__```属性指向构造函数的原型对象**

- 原型对象的方法isPrototypeOf()

  ```js
  //判断实例对象的原型对象是否是构造函数的原型对象，换句话说实例对象是否在构造函数的原型链上
  var person1 = new Person();
  Person.prototype.isPrototypeOf(person1);	//true
  ```

- 普通对象的方法hasOwnProperty()

  ```js
  //判断对象的属性是否是自身属性，而非继承自原型链
  //原型与in操作符：判断属性是否属于该对象，无论是属于自身还是继承自原型链
  function Person () {}
  Person.prototype.name = "Parker";
  var person1 = new Person;
  person.age = 26;
  
  alert(person.hasOwnProperty("name"));	//false
  alert(person.hasOwnProperty("age"));	//true
  alert("name" in person1);	//true
  alert("age" in person1);	//true
  ```



## 4.4 对象的继承

### 4.4.1 属性的继承

父类构造函数.call(this，传参1，传参2)

### 4.4.2 方法的继承

- 浅拷贝继承

  ```js
  //普通方法：
  function extend (obj1, obj2){
  	for(var attr in obj2){
  		obj1[attr] = obj2[attr]
  	}
  }
  extend(子对象.prototype, 父对象.prototype)
  
  //ES6方法: 
  Object.assign(拷贝对象，被拷贝对象)
  ```

- 类式继承

  ```js
  var F = function(参数){父对象.call(this, 参数)}	//中间过渡函数
  F.prototype = 父对象.prototype
  子对象.prototype = new F()
  子对象.prototype.constructor = 子对象	//修正指向
  ```

- 原型继承

  ```js
  var 子对象 = cloneObj(父对象)
  function cloneObj(obj){
  	var F = function(){}
  	F.prototype = obj
  	return new F()
  }
  ```

  

## 4.5 Object对象

### 4.5.1 构造函数属性

- **Object.length**

  值为1

- **Object.prototype**

  - 可以为所有 Object 类型的对象添加属性
  - ```__proto__```是对象的私有属性，而prototype却是只有函数才有的属性

### 4.5.2 构造函数方法

- **Object.create()**

  使用指定的原型对象和属性创建一个新对象

- **Object.assign(目标对象，源对象1，源对象2...)**

  - 将源对象的所有可枚举属性（不包括继承属性）复制到目标对象
  - 参数必须为对象否则会抛出typeError错误
  - 目标对象和源对象有重名属性，后面的覆盖前面
  - 数组会被看做对象：Object.assign([1, 2, 3], [4, 5])结果为[4, 5, 3]

- **Object.defineProperty(obj, prop, descriptor)**

  - 定义对象中新属性或修改原有的属性，并返回此对象

- **Object.freeze()**

  冻结对象：其他代码不能删除或更改任何属性

- **Object.setPrototypeOf()**

  设置对象的原型（即内部 [[Prototype]] 属性）

- **Object.getPrototypeOf()**

  返回指定对象的原型对象

- **Object.is()**

  - 判断两个数据是否长的一样
  - Object.is(NaN, NaN)返回true
  - Object.is([], [])返回false
  - Object.is(+0, -0)返回false
  - Object.is(0, +0)返回true

- **Object.entries()**

  返回给定对象自身可枚举属性的 [key, value] 数组

- **Object.keys()**

  返回一个包含所有给定对象自身可枚举属性名称的数组

- **Object.values()**

  返回给定对象自身可枚举值的数组

### 4.5.3 原型属性

**Object.prototype.constructor**

特定的函数，用于创建一个对象的原型

### 4.5.4 原型方法

- **Object.prototype.isPrototypeOf()**

  返回一个布尔值，表示指定的对象是否在本对象的原型链中

- **Object.prototype.propertyIsEnumerable()**

  判断指定属性是否可枚举

- **Object.prototype.toLocaleString()**

  直接调用 toString()方法，该字符串与执行环境的地区对应

- **Object.prototype.toString()**

  返回对象的字符串表示

- **Object.prototype.valueOf()**

  返回指定对象的原始值

### 4.5.5 实例方法

**obj.hasOwnProperty()**

返回一个布尔值 ，表示某个对象是否含有指定的属性，而且此属性非原型链继承的



## 4.6 字符串对象

### 4.6.1 属性

**str.length**

### 4.6.2 方法

- **str.charAt(index)** 返回下标字符
- **str.charCodeAt(index)** 返回下标字符编码
- **String.fromCharCode(22937)**返回编码对应的字符
- **str.indexOf('字符',[num])** 返回字符的下标，如没有则返回-1。第二个可选参数表示从第num位开始查找
- **str.lastIndexOf(字符)** 从右往左搜索，返回字符的下标，如没有则返回-1
- **str.concat('字符串1', '字符串2', ...)** 连结多个字符串返回一个新字符串
- **str.slice(start,end)**截取字符串：
  - start（必选）开始下标位置，包括
  - end（可选）元素下标值，结束选取，但不包括
  - 如是负数从数组尾部开始算起（最后一个是-1）
- **str.substring(start,end)**截取字符串：
  - start（必选）开始下标位置，包括
  - end（可选）元素下标值，结束选取，但不包括
  - 两个参数位置：会自动将较小的数作为start，较大的数作为end
  - 如是负数自动转为0
- **str.substr(start,len)**截取字符串：
  - start（必选）开始下标位置，包括，如是负数从数组尾部开始算起（最后一个是-1）
  - len（可选）截取字符总数，如是负数返回空字符串
- **str.replace(regexp/substr,replacement)**在字符串中用一些字符替换另一些字符，或替换一个正则表达式匹配的子串
- **str.split(separator)**把一个字符串分隔成字符串数组
- **str.toUpperCase()**把字符串转换为大写
- **str.toLowerCase()**把字符串转换为小写
- **str.match('字符串'/正则表达式)**检索一个字符串是否存在。如果存在的话，返回要检索的字符串；如果不存在的话，返回null。
- **str.search('字符串'/正则表达式)**返回的是子字符串的起始位置，如果没有找到任何匹配的子串，则返回-1。
- **str.repeat(n)**将字符串重复n次(返回新值，不改变原值)
- **str.includes('x')**字符串里是否包含x，包含返回true
- **str.startsWith('x')**字符串开头里是否是x，是返回true
- **str.endsWith('x')**字符串结尾里是否是x，是返回true
- **str.padStart(maxLength,fillString='')**在字符串前面添加字符
- **str.padEndt(maxLength,fillString='')**在字符串后面添加字符
- **str.trim()**去掉字符串前后空格



## 4.7 数组对象

### 4.7.1 定义

- 构造函数：var colors = new Array()
  - 可传递length：var colors = new Array(20)
  - 可传递包含项：var colors = new Array("red", "blue", "green")
- 数组字面量：var colors = ["red", "blue", "green"]

### 4.7.1 属性

**arr.length**

### 4.7.2 方法

- 一般方法
  - **arr.indexOf(searchvalue,startIndex)**
    - searchvalue：要搜寻的元素
    - startIndex：（可选）起始搜寻的位置
    - 如有此值则返回其索引，没有则返回-1
  - **arr.lastIndexOf(searchvalue,startIndex)** 用法同上，区别在于从末尾向前查找
  
- 改变原有数组的方法
  - **arr.push()** 往后添加，返回值为新数组的长度
  
  - **arr.unshift()** 往前添加，返回值为新数组的长度
  
  - **arr.pop()** 删除最后一个，返回值为删除的值
  
  - **arr.shift()** 删除第一个，返回值为删除的值
  
  - **arr.join()** 把数组转换为字符串
  
  - **arr.reverse()** 把数组倒序
  
  - **arr.splice**
  
    - 删除：arr.splice(index,count) 删除从index处开始的count个元素，返回删除值的数组
    - 插入：arr.splice(index,0,item1,...itemX) 从index处开始插入（插入第一个元素下标为index），count为删除个数设置为0，item1,...itemX为插入的元素
    - 替换：arr.splice(index,count,item1,...itemX) 综合删除和插入
    - 必有返回值，即使count为0也要返回[]
  
  - **arr.sort()**排列方法
  
    - 数字：
  
      (1). 从小到大：arr.sort(function(a,b){return a-b;})
  
      (2). 从大到小：arr.sort(function(a,b){return b-a;})
  
      (3). 字符串数字：arr.sort(function(a,b){return parseInt(a)-parseInt(b);})
  
    - 字符串：
  
      (1). 数字：按字符串比较（比较第一位，相同在比较后位）
  
      (2). 字母：按字母顺序
  
    - 随机排序：arr.sort(function(a,b){return Math.random()-0.5;})
  
- 不改变原数组的方法（返回新数组）
  - **arr.concat()** 连接两个或多个数组：
    - var newArr=arr.concat(arr1,arr2...)
    - 参数也可以是字符串
    - 如没有参数则复制数组
  - **arr.slice(start,end)**截取数组：
    - start（必选）开始下标位置，包括
    - end（可选）元素下标值，结束选取，但不包括
    - 如是负数从数组尾部开始算起（最后一个是-1）
  - 迭代方法
    - **arr.every()**：每一项返回true，则返回true
    - **arr.some()**：任何一项返回true，则返回true
    - **arr.filter()**：返回该函数会返回true的项组成的数组
    - **arr.map()**：返回每次函数调用的结果组成的数组
    - **arr.forEach()**：没有返回值
  - 归并方法
    - **arr.reduce(function(previousVal,currentVal,initialVal),[currentIndex],[array])**用来迭代一个数组，并把它累积到一个值中
    - **arr.reduceRight()**同上，不过倒序迭代

- 扩展方法

  - **Array.of()**：创建一个数组（括号中一个数不再代表数组长度）

  - **Array.from(类数组)**：把一个类数组或可遍历对象转换成真正的数组，包括ES6的Set和Map

  - **arr.keys()**：对键名遍历，返回遍历器对象

  - **arr.values()**：对键值遍历，返回遍历器对象

  - **arr.entries()**：对键值对遍历，返回遍历器对象

  - **Arr.find((item, index) => {})**：在数组中查找符合回调函数的第一个元素并返回此元素，没有则返回undefined

  - **Arr.findIndex(回调函数)**：在数组中查找符合回调函数的第一个元素并返回此元素的下标，没有则返回-1

  - **Arr.includes(x)**

    - 表示某个数组是否包含给定的值，返回布尔值

    - 第二个可选参数为起始位置，若为负数表示倒数

    - ```js
      [NaN].indexOf(NaN)    // -1
      [NaN].includes(NaN)    // true
      ```

  - **Arr.fill('x', m, n)**

    - 将数组中m到n之间的每一个元素都替换为x
    - 如没有m和n则全部替换为x



## 4.8 BOM对象

### 4.8.1 window对象

#### 4.8.1.1 属性

- screenLeft：窗口相对于屏幕左边的位置
- screenTop：窗口相对于屏幕上边的位置

#### 4.8.1.2 方法

| 方法                           | 说明                           |
| ------------------------------ | ------------------------------ |
| open()、close()                | 打开窗口、关闭窗口             |
| resizeBy()、resizeTo()         | 改变窗口大小                   |
| moveBy()、moveTo()             | 移动窗口                       |
| setTimeout()、clearTimeout()   | 设置或取消“一次性”执行的定时器 |
| setInterval()、clearInterval() | 设置或取消“重复性”执行的定时器 |

- **window.open**

  ```html
  window.open(URL, 窗口名称, 参数);
  ```
  
  说明：

  - URL：指的是打开窗口的地址，如果URL为空字符串，则浏览器打开一个空白窗口，并且可以使用document.write()方法动态输出HTML文档。

  - 窗口名称：指的是window对象的名称，可以是a标签或form标签中target属性值。如果指定的名称是一个已经存在的窗口名称，则返回对该窗口的引用，而不会再新打开一个窗口。

  - 参数：对打开的窗口进行属性设置。

    | 参数       | 说明                                     |
    | ---------- | ---------------------------------------- |
    | top        | 窗口顶部距离屏幕顶部的距离，默认单位为px |
    | left       | 窗口左边距离屏幕左边的距离，默认单位为px |
    | width      | 窗口的宽度，默认单位为px                 |
    | height     | 窗口的高度，默认单位为px                 |
    | scrollbars | 是否显示滚动条                           |
    | resizable  | 窗口大小是否固定                         |
    | toolbar    | 浏览器工具条，包括前进或后退按钮         |
    | menubar    | 菜单条，一般包括文件、编辑及其它一些条目 |
    | location   | 地址栏，是可以输入URL的浏览器文本区      |
    | location   | 地址栏，是可以输入URL的浏览器文本区      |
  
- **window.close()**

  - 关闭当前窗口

    在JavaScript中，如果想要关闭当前的窗口，有3种方式：

    ```html
    window.close();
    close();
    this.close();
    ```
  
  - 关闭子窗口

    所谓的“关闭子窗口”就是关闭之前使用window.open()方法动态创建的子窗口。

    ```html
    窗口名.close();
    ```
  
    说明：

    使用window.open()方法动态创建的窗口时，我们可以将窗口以变量形式保存，然后再使用close()方法关闭动态创建的窗口。

- **resizeTo()**

  ```html
  window.resizeTo(x, y)
  ```

  说明：

  x表示改变后的水平宽度，y表示改变后的垂直高度。x和y的单位都是px，浏览器自带单位，我们只需要使用数值即可。

- **resizeBy()**

  ```html
  window.resizeBy(x, y)
  ```

  说明：

  当x、y的值大于0时为扩大，小于0时为缩小。其中x和y的单位都是px。

  x表示窗口水平方向每次扩大或缩小的数值，y表示垂直方向窗口每次扩大或缩小的数值。

> resizeTo(x,y)与resizeBy(x,y)不同在于：resizeTo(x,y)中的x、y是“改变后”的数值，而resizeBy(x,y)中的x、y是“增加或减少”的数值。“to”表示一个结果，“by”表示一个过程，大家好好琢磨“to”和“by”的英文含义就懂了。

### 4.8.2 history对象

#### 4.8.2.1 属性

| 属性     | 说明                                     |
| -------- | ---------------------------------------- |
| current  | 当前窗口的URL                            |
| next     | 历史列表中的下一个URL                    |
| previous | 历史列表中的前一个URL                    |
| length   | 历史列表的长度，用于判断列表中的入口数目 |

#### 4.8.2.2 方法

| 方法      | 说明           |
| --------- | -------------- |
| go()      | 进入指定的网页 |
| back()    | 返回上一页     |
| forward() | 进入下一页     |

```html
<a href="javascript:window.history.forward();">下一页</a>
<a href="javascript:window.history.back();">上一页</a>
```

我们还可以使用hisotry.go()方法指定要访问的历史记录。若参数为正数，则向前移动；若参数为负数，则向后移动，例如：

```html
<a href="javascript:window.history.go(-1);">向后退1次</a>
<a href="javascript:window.history.back(2);">向后前进2次</a>
```

使用history.length属性能够访问history数组的长度，可以很容易地转移到列表的末尾，例如：

```html
<a href="javascript:window.history.length-1;">末尾</a>
```

在JavaScript中，操作窗口历史语法很简单，也不是那么常用。一般情况下，在404页面中，为了用户体验，往往会有一个提供“返回上一页”的选项，这其中就用到了下面这种语法：

```html
<a href="javascript:window.history.go(-1);">返回上一页</a>
```

### 4.8.3 location对象

#### 4.8.3.1 属性

- **href**：返回当前加载页面的完整URL
- **hash**：返回URL中的hash（#锚点），若不包含则返回空字符串
- **host**：返回服务器名称和端口号（如果有）
- **hostname**：返回不带端口号的服务器名称
- **pathname**：返回URL中的目录和（或）文件名
- **port**：返回URL中指定的端口号，没有则返回空字符串
- **protocol**：返回页面使用协议
- **search**：返回URL的查询字符串（以？开头）

#### 4.8.3.2 方法

- **assign(url)**：重定向URL
- **replace(url)**：重定向URL（不会留下历史记录）
- **reload()**：
  - 重新加载当前显示的页面
  - 无参数：从缓存加载
  - true参数：从服务器加载

### 4.8.4 Web储存

#### 4.8.4.1 localStorage

- 保存数据：localStorage.setItem(key,value);
- 读取数据：localStorage.getItem(key);
- 删除单个数据：localStorage.removeItem(key);
- 删除所有数据：localStorage.clear();
- 得到某个索引的key：localStorage.key(index);

#### 4.8.4.2 sessionStorage

- 针对一个 session 的数据存储
- API和localStorage相同

### 4.8.5 定时器

- **setTimeout()和clearTimeout()**

  setTimeout()方法来设置“一次性”调用的函数。clearTimeout()可以用来取消执行setTimeout()方法。

  ```html
  var 变量名 = setTimeout(code , time);
  ```

  说明：

  参数code可以是一段代码，也可以是一个调用的函数名；

  参数time表示时间，表示要过多长时间才执行code中的内容，单位为毫秒。

  举例：

  ```html
  <!DOCTYPE html>
  <html xmlns="http://www.w3.org/1999/xhtml">
  <head>
      <title></title>
      <script type="text/javascript">
          window.onload = function () {
              setTimeout("alert('欢迎来到学习网');", 2000);
          }
      </script>
  </head>
  <body>
      <p>2秒后提示欢迎语。</p>
  </body>
  </html>
  ```

  分析：

  打开页面2秒后，浏览器会弹出欢迎语。由于setTimeout()方法只会执行一次，所以只会弹出一次对话框。弹出对话框如下图：

- **setInterval()和clearInterval()**

  在JavaScript中，我们可以使用setInterval()方法来设置“重复性”调用的函数。其中clearInterval()可以用来取消执行setTimeout()方法。

  ```html
  var 变量名 = setInterval (code , time);
  ```

  说明：

  参数code可以是一段代码，也可以是一个调用的函数名；

  参数time表示时间，表示要过多长时间才执行code中的内容，单位为毫秒。

  > setTimeout()方法与setInterval()方法的语法很相似，实际上这两者在用法方面区别非常大。其中setTimeout()方法内的代码只会执行一次，而setInterval()方法内的代码会重复性执行，除非你使用clearInterval()方法来取消执行。

  举例：

  ```html
  <!DOCTYPE html>
  <html xmlns="http://www.w3.org/1999/xhtml">
  <head>
  <title></title>
      <script type="text/javascript">
          //定义全局变量，用于记录秒数
          var n = 5;
          window.onload = function () {
              //设置定时器，重复执行函数countDown()
              var t = setInterval("countDown()", 1000);
          }
          //定义函数
          function countDown() {
              //判断n是否大于0，因为倒计时不可能有负数
              if (n > 0){
                  n--;
                  document.getElementById("num").innerHTML = n;
              }
          }
      </script>
  </head>
  <body>
      <p>新年倒计时：<span id="num">5</span></p>
  </body>
  </html>
  ```

  分析：

  window.onload表示在页面加载完毕执行，在“JavaScript页面相关事件”我们会详细讲解到。

  setInterval()方法会重复执行某一段代码或函数。如果这个例子使用setTimeout方法就不能实现了，因为setTimeout()方法只会执行一次，而setInterval()会重复执行。

总结：

- 在JavaScript中，关于定时器的实现，我们有2组方法：

  - setTimeout()和clearTimeout()；

  - setInterval()和clearInterval()；

- setTimeout()方法内的代码只会执行一次，而setInterval()方法内的代码会重复性执行。

 

### 4.8.6 对话框

- **alert()**

  alert()方法来弹出一个提示框。该对话框效果如下：

  ```html
  alert(message)
  ```

  说明：

  该对话框只是用于提示，并不能对JavaScript脚本产生任何影响。message是必选参数，即提示框的信息，这是一个字符串。alert()方法没有返回值。

- **confirm()**
  confirm()方法对话框一般用于确认信息，它只有一个参数，返回值为true或false。该对话框效果如下：

  ```html
  confirm(message)
  ```

  说明：

  message是必选项，表示弹出对话框中的文本，这是一个字符串。如果用户点击“确定”，则confirm()返回true。如果用户点击“取消”按钮，则confirm()返回false。confirm()方法往往都是和按钮结合使用。

- **prompt()**
  prompt()方法对话框用于输入并返回用户输入的字符串。该对话框效果如下：

  ```html
  prompt(message);
  ```

  说明：

  参数message表示对话框提示内容，这是一个字符串。

总结：

- alert()：仅有提示文字，没有返回值；

- confirm()：具有提示文字，返回“布尔值”（true或false）；

- prompt()：具有提示文字，返回“字符串”；



## 4.9 DOM对象

### 4.9.1 Node类型对象

#### 4.9.1.1 特点

JS中所有的节点类型都继承自Node类型

#### 4.9.1.2 属性

| 属性            | 说明                                           |
| :-------------- | ---------------------------------------------- |
| nodeType        | 节点类型值（1，2，3 ...）                      |
| nodeName        |                                                |
| nodeValue       |                                                |
| childNodes      | 获取某个节点下的所有子节点，返回一个类数组     |
| children        | 获取某个节点下的所有元素子节点，返回一个类数组 |
| parentNode      | 查找元素的父节点                               |
| previousSibling | 查找元素的上一个兄弟节点                       |
| nextSibling     | 查找元素的下一个兄弟节点                       |
| firstChild      | 查找元素的第一个子节点                         |
| lastChild       | 查找元素的最后一个子节点                       |
| ownerDocument   | 指向表示整个文档的文档节点                     |

备注：nodeType的几个常用类型值

- 1为element元素节点
- 2为attr属性节点
- 3为text文本节点（文字，换行，空格）
- 8为注释节点
- 9为document文档节点

#### 4.9.1.3 方法

- **父节点.appendChild(子节点)**
  - 向childNodes列表的末尾添加一个节点
  - 返回值为新添的节点
  - 如果添加的是已有节点，则从原位置挪到最后
- **父节点.insertBefore(插入节点，参照节点)**
  - 向childNodes列表的参照节点前插入新节点
  - 返回值为新插入的节点
  - 如参照节点为null，则等于appendChild()
- **父节点.replaceChild(插入节点，替换节点)**
  - 在childNodes列表中用插入节点替换掉替换节点
  - 返回被替换的节点
- **父节点.removeChild(移除节点)**
  - 在childNodes列表中移除要被移除的节点
  - 返回被移除的节点
- **节点.cloneNode(布尔值参数)**
  - 创建调用这个方法的节点的一个完全相同的副本
  - 布尔值参数为是否进行深复制，即也复制整个子节点
- **节点.normalize()**
  - 处理文档树中的文本节点
- **祖先节点.contains(后代节点)**
  - H5新增
  - 检测后代节点是否为祖先节点的后代节点，是则返回true



### 4.9.2 document对象

document对象是window对象中的子对象。

document对象，即文档对象。顾名思义，操作的都是HTML文档。

#### 4.9.2.1 属性

| 属性             | 说明                      |
| ---------------- | ------------------------- |
| title            | 文档标题，即title标签内容 |
| URL              | 文档地址                  |
| fileCreateDate   | 文档创建日期              |
| fileModifiedDate | 文档修改时间（精确到天）  |
| lastModified     | 文档修改时间（精确到秒）  |
| fileSize         | 文档大小                  |
| fgColor          | 定义文档的前景色          |
| bgColor          | 定义文档的背景色          |
| linkColor        | 定义“未访问”的超链接颜色  |
| alinkColor       | 定义“被激活”的超链接颜色  |
| vlinkColor       | 定义“访问过”的超链接颜色  |

#### 4.9.2.2 方法

| 方法                          | 说明                                                    |
| ----------------------------- | ------------------------------------------------------- |
| createElement()               | 创建元素节点                                            |
| createTextNode()              | 创建文本节点                                            |
| write()                       | 输入文本到当前打开的文档                                |
| writeIn()                     | 输入文本到当前打开的文档，并添加换行符“\n”              |
| getElementById()              | 获取某个id值的元素                                      |
| getElementsByName()           | 获取某个name值的元素，用于表单元素                      |
| getElementsByTagName()        | 标签查找元素                                            |
| getElementsByClassName()      | 也可用Element调用，H5新增                               |
| querySelector("CSS选择符")    | 返回与模式匹配的第一个元素，也可用Element调用           |
| querySelectorAll("CSS选择符") | 返回与模式匹配的所有元素，也可用Element调用             |
| matchesSelector("CSS选择符")  | 如果调用元素与该选择符匹配则返回true，也可用Element调用 |
| open()                        |                                                         |
| close()                       |                                                         |
| hasFocus()                    | 用于确定文档是否获得了焦点，H5新增                      |

### 4.9.3 element对象

#### 4.9.3.1 特性

类别：

| 类别名         | 说明                                                |
| -------------- | --------------------------------------------------- |
| id             | 元素在文档中的唯一标识符                            |
| title          | 有关元素的附加说明                                  |
| lang           | 元素内容的语言代码，很少使用                        |
| dir            | 语言的方向，很少使用                                |
| className      | 元素指定的CSS类                                     |
| style          | 读和写元素的样式，样式名都用驼峰格式                |
| H5可自定义特性 | 最好以data-开头，获取属性值方法：div.dataset.属性名 |

操作特性：

- **getAttribute("key")**：可以获取src、href等的相对地址用于判断
- **setAttribute("key"，"value")**：没有则创建，有则覆盖
- **removeAttribute("key")**

#### 4.9.3.2 属性

- **attributes**：获取某个节点下的所有属性节点，返回一个类数组
  - attributes[n].nodeName：返回第n-1个属性的属性名
  - attributes[n].nodeValue：返回第n-1个属性的属性值

- H5新增：

  | 属性                   | 说明                                                         |
  | ---------------------- | ------------------------------------------------------------ |
  | previousElementSibling | 查找元素的上一个兄弟元素节点                                 |
  | nextElementSibling     | 查找元素的下一个兄弟元素节点                                 |
  | firstElementChild      | 查找元素的第一个子元素节点                                   |
  | lastElementChild       | 查找元素的最后一个子元素节点                                 |
  | childElementCount      | 返回子元素（不包括文本和注释）的个数                         |
  | classList              | 类名数组                                                     |
  | innerHTML              | 返回与调用元素的所有子节点（包括元素、注释和文本节点）对应的HTML标记 |
  | outerHTML              | 返回调用它的元素及所有子节点的HTML标签                       |

  备注：classList的属性和方法：

  - length：class的长度
  - add()：添加class方法
  - remove()：删除class方法
  - toggle()：切换class方法（有就删除，没有添加）

#### 4.9.3.3 方法

H5新增：**insertAdjacentHTML(插入位置，要插入的HTML文本)**

- 插入位置
  - beforebegin：在当前元素之前插入一个紧邻的同辈元素
  - afterbegin：在当前元素之下插入一个新的子元素或在第一个子元素之前再插入新的子元素
  - beforeend：在当前元素之下插入一个新的子元素或在最后一个子元素之后再插入新的子元素
  - afterend：在当前元素之后插入一个紧邻的同辈元素
- 第二个参数是一个HTML字符串

### 4.9.4 元素大小

- **offsetParent**
  - 最近的有定位属性的祖先节点，如都没有就是```<body>```
  - 自己要有定位

- **element.getBoundingClientRect()**
  - 获取某个元素相对于浏览器可视范围的信息对象
    - left
    - top
    - right：元素右边距离页面左边的距离
    - bottom：元素下边距离页面上边的距离
  - 获取的值会根据滚动条变化

#### 4.9.4.1 偏移量

- **offsetLeft**：元素左外边框到最近的有定位父级的左内边框的像素距离
- **offsetTop**：元素上外边框到最近的有定位父级的上内边框的像素距离
- **offsetwidth**：元素在水平方向上占用的空间大小，以像素计，包括元素的宽度、（可见的）垂直滚动条的宽度、左边框和右边框的宽度
- **offsetHeight**：元素在垂直方向上占用的空间大小，以像素计，包括元素的高度、（可见的）水平滚动条的高度、上边框和下边框的高度

#### 4.9.4.2 客户区大小

- **clientWidth**：元素内容区宽度加上左右内边距宽度
- **clientHeight**：元素内容区高度加上上下内边距高度

#### 4.9.4.3 滚动大小

- **scrollLeft**：被隐藏在内容区域左侧的像素数
- **scrollTop**：被隐藏在内容区域上方的像素数
- **scrollWidth**：在没有滚动条的情况下，元素内容的总宽度
- **scrollHeight**：在没有滚动条的情况下，元素内容的总高度

#### 4.9.4.4 页面滚动距离

- 声明了DTD（<!DOCTYPE>），使用**document.documentElement.scrollTop**
- 未声明DTD，使用**document.body.scrollTop**
- IE9以上新方法，**window.pageYoffset**

#### 4.9.4.5 元素居中

- 页面可视区的宽高
  - document.documentElement.clientWidth
  - document.documentElement.clientHeight
- 元素.style.left = （可视区宽 - 元素宽）/2 +'px'
- 元素.style.top = （可视区高 - 元素高）/2 +'px'

### 4.9.5 innerHTML和innerText

innerHTML和innerText这2个属性很方便地获取和设置某一个元素内部子元素或文本。

innerHTML属性被多数浏览器所支持，而innerText只能被IE、chrome等支持而不被Firefox支持。

### 4.9.6 JavaScript操作CSS样式

对于元素的CSS操作，使用的是DOM对象中的style对象来操作。

```html
obj.style.属性名;
```

说明：

obj指的是DOM对象，也就是通过document.getElementById()等获取而来的DOM元素节点。



## 4.10 Math对象

| 方法     | 说明                       |
| -------- | -------------------------- |
| max(x,y) | 返回x和y中的最大值         |
| min(x,y) | 返回x和y中的最小值         |
| pow(x,y) | 返回x的y次幂               |
| abs(x)   | 返回数的绝对值             |
| round(x) | 把数四舍五入为最接近的整数 |
| random() | 返回0~1之间的随机数        |
| ceil(x)  | 对一个数进行上舍入         |
| floor(x) | 对一个数进行下舍入         |

备注：x~y之间的任意值：

- Math.floor(Math.random()*(y-x+1)+x);
- Math.round(Math.random()*(y-x)+x);

## 4.11 Date对象

### 4.11.1 创建日期对象

方法一：

```js
var 日期对象名 = new Date();
```

方法二：

```js
var 日期对象名 = new Date(日期字符串);
```

日期字符串可以是以下几种形式：

- "2015-5-3"

- "May 3,2015"

- "2015/5/3"

举例：

```js
var dt1 = new Date("2015-5-3");
var dt2 = new Date("May 3,2015");
var dt3 = new Date("2015/5/3");
```

### 4.11.2 日期对象方法

日期对象Date的方法主要分为三大组：setXxx、getXxx和toXxx。

setXxx用于设置时间和日期值；getXxx用于获取时间和日期值；toXxxx主要是将日期转换为指定格式。

- 用于获日期时间的getXxx

| 方法          | 说明                                          |
| ------------- | --------------------------------------------- |
| getFullYear() | 返回一个表示年份的4位数字                     |
| getMonth()    | 返回值是0（一月）到11（十二月）之间的一个整数 |
| getDate()     | 返回值是1~31之间的一个整数                    |
| getDay()      | 返回星期，返回值为0~6（0为日）                |
| getHours()    | 返回值是0~23之间的一个整数，来表示小时数      |
| getMinutes()  | 返回值是0~59之间的一个整数，来表示分钟数      |
| getSeconds()  | 返回值是0~59之间的一个整数，来表示秒数        |

- 用于设置日期时间的setXxx

| 方法          | 说明                     |
| ------------- | ------------------------ |
| setFullYear() | 可以设置年、月、日       |
| setMonth()    | 可以设置月、日           |
| setDate()     | 可以设置日数             |
| setHours()    | 可以设置时、分、秒、毫秒 |
| setMinutes()  | 可以设置分、秒、毫秒     |
| setSeconds()  | 可以设置秒、毫秒         |

- 将日期时间转换为字符串的toXxx

| 方法             | 说明                                        |
| ---------------- | ------------------------------------------- |
| toString()       | 将日期时间转换为普通字符串                  |
| toUTCString()    | 将日期时间转换为世界时间（UTC）格式的字符串 |
| toLocaleString() | 将日期时间转换为本地时间格式的字符串        |



## 4.12 事件对象

### 4.12.1 事件绑定

- 第一种形式：
  - 绑定：obj.事件=事件函数
  - 移除：obj.事件=null
  - 缺点：多次绑定同一对象的同一事件，后面的函数会覆盖前面的函数

- 第二种形式：
  - IE
    - 绑定：obj.attachEvent(事件名称，事件函数)
    - 移除：obj.detachEvent(事件名称，事件函数)
    - 事件函数中this指向window
    - 解决方法：事件函数中调用call方法第一个参数重新改变指向```obj.attachEvent(事件名称，function(){ 事件函数.call(obj); })```
  - 标准
    - 绑定：obj.addEventListener(事件名称，事件函数，是否捕获)
    - 移除：obj.removeEventListener(事件名称，事件函数，是否捕获)
    - 事件名称前没有on
    - 事件函数中this指向obj
    - 事件函数如为匿名函数则无法移除
    - 是否捕获?false：冒泡; true：捕获

### 4.12.2 事件对象

#### 4.12.2.1 定义

当一个事件发生的时候，和当前这个对象发生的这个事件有关的一些详细信息都会被临时保存到event对象中，必须在一个事件调用的函数里面使用才有内容

#### 4.12.2.2 标准事件对象

- 属性

  | 属性          | 说明                                                         |
  | ------------- | ------------------------------------------------------------ |
  | bubbles       | 表明事件是否冒泡                                             |
  | cancelable    | 表明是否可以取消事件的默认行为                               |
  | currentTarget | 其事件处理程序当前正在处理事件的那个元素，在事件处理程序内部始终等于this |
  | target        | 包含事件的实际目标                                           |
  | type          | 被触发的事件类型                                             |
  | eventPhase    | 调用事件处理程序的阶段，值为1表示捕获阶段，2表示处于目标，3表示冒泡阶段 |

- 方法

  - preventDefault()：取消事件的默认行为，如果cancelable属性为true可以使用此方法
  - stopPropagation()：取消事件的捕获或冒泡，如果bubbles属性为true可以使用此方法

#### 4.12.2.3 IE事件对象

- 属性

  | 属性                | 说明                               |
  | ------------------- | ---------------------------------- |
  | srcElement          | 事件的目标，等同于标准下的target   |
  | type                | 被触发的事件类型                   |
  | returnValue = false | 取消事件的默认行为                 |
  | cancelBubble = true | 取消事件的冒泡（IE不支持事件捕获） |

- 方法

  （无）

#### 4.12.2.4 兼容事件对象

```js
function fn(ev) {
	var ev = ev || event
}
```

- 标准：事件对象通过事件函数的第一个参数传入
- IE/chrome：event是一个内置全局对象

#### 4.12.2.5 event属性

- e.screenX/Y：返回鼠标相对于电脑屏幕的距离
- e.clientX/Y：返回鼠标相对于浏览器窗口可视区的距离
- e.pageX/Y：返回鼠标相对于文档页面的距离
- keyCode：按键的键值，数字类型

#### 4.12.2.6 event方法

- focus()：给指定的元素设置焦点
- blur()：取消指定元素的焦点
- select()：选择指定元素里面的文本内容

#### 4.12.2.7 事件类型

- 鼠标事件

  | 事件          | 说明                                                         |
  | ------------- | ------------------------------------------------------------ |
  | onclick       | 鼠标单击事件                                                 |
  | ondbclick     | 鼠标双击事件                                                 |
  | onmouseover   | 鼠标移入事件                                                 |
  | onmouseout    | 鼠标移出事件                                                 |
  | onmousemove   | 鼠标移动事件                                                 |
  | onmousedown   | 鼠标按下事件                                                 |
  | onmouseup     | 鼠标松开事件                                                 |
  | onmouseenter  | 在鼠标光标从元素外部首次移动到元素范围之内时触发，不会冒泡，而且光标移动到后代元素上不会触发 |
  | onmouseleave  | 在位于元素上方的鼠标光标移动到元素范围之外时触发，不会冒泡，而且光标移动到后代元素上不会触发 |
  | oncontextmenu | 右键菜单事件                                                 |
  | onmousewheel  | 向上或向下滚动滚轮时触发，会冒泡                             |

- 键盘事件

  | 方法       | 说明                             |
  | ---------- | -------------------------------- |
  | onkeydown  | 按下键事件（包括数字键、功能键） |
  | onkeypress | 按下键事件（只包含数字键）       |
  | onkeyup    | 放开键事件（包括数字键、功能键   |

- 表单事件

  | 事件       | 说明                         |
  | ---------- | ---------------------------- |
  | onfocus    | 获取焦点事件，不会冒泡       |
  | onfocusin  | 在元素获得焦点时触发，会冒泡 |
  | onfocusout | 在元素失去焦点时触发，会冒泡 |
  | onblur     | 失去焦点事件，不会冒泡       |
  | onchange   | 状态改变事件                 |
  | onselect   | 选中文本事件                 |

- 编辑事件

  | 方法    | 说明     |
  | ------- | -------- |
  | oncopy  | 复制事件 |
  | oncut   | 剪切事件 |
  | onpaste | 粘贴事件 |

- 页面相关事件

  | 方法     | 说明                                               |
  | -------- | -------------------------------------------------- |
  | onload   | 页面加载事件                                       |
  | onunload | 页面卸载事件                                       |
  | onresize | 页面大小事件                                       |
  | onerror  | 页面或图片加载出错事件                             |
  | onselect | 当用户选择文本框中的一个或多个字符时触发           |
  | onscroll | 当用户滚动带滚动条的元素中的内容时在该元素上面触发 |
  
  

## 4.13 JSON对象*



# 5. ES6

## 5.1 声明

### 5.1.1 var

- 可以重复声明同一个变量且后面覆盖前面
- 提升层级，在声明前可使用（undefined）
- 作用域以函数区域划分

### 5.1.2 let

- 声明变量
- 只在命令所在的代码块内有效，作用域为{}
- 在预解析的时候不会被提升
- 暂时性死区：相同变量名不会往块级外查找值
- 不允许在同一个作用域下声明已经存在的变量
- for循环：在循环语句之内是一个父作用域，再循环体之中是一个子作用域

### 5.1.3 const

- 声明常量
- 只在命令所在的代码块内有效，作用域为{}
- 在预解析的时候不会被提升
- 不允许在同一个作用域下声明已经存在的变量
- 声明的时候必须赋值
- 储存简单的数据类型时候不可改变其值
- 储存的是对象，只要引用不改变，对象里面的数据可以变化

## 5.2 Class类

### 5.2.1 xxx

- Class不存在变量提升，必须先定义再调用

- 类和模块的内部默认是严格模式

- ES5的构造函数对应ES6中Class的constructor构造方法

- constructor方法是类的默认方法，constructor中的this指向将要创建的实例，通过new创建实例时自动调用该方法

- 实例的属性通过constructor的this定义在实例自身上，其他都是定义在原型上

  ```js
  class Person {
  	constructor(name, age) {
  		this.name = name;
  		this.age = age;
  	}
  	sayName() {
  		return 'my name is' + this.name;
  	}
  }
  var person1 = new Person("Parker", 26);
  
  person1.hasOwnProperty("name");		//true
  person1.hasOwnProperty("age");		//true
  person1.hasOwnProperty("sayName");		//false
  ```

  

- 类的属性名可以用表达式

- 类中的方法不需要加上function，且定义在类的prototype上，且不可枚举（ES5定义在prototype上的方法可枚举）

- CLass也可以使用表达式的形式定义

  ```js
  const MyClass = class Me {	//类名是MyClass，而Me只在Class的内部代码可用
  	getClassName() {
  		return Me.name
  	}
  }
  let inst = new MyClass();
  inst.getClassName();	//Me
  Me.name;	//报错，Me未定义
  
  //如代码内部没有用到Me，可简写为
  const MyClass = class {...}
  ```


### 5.2.2 类的继承

```js
class 子类 extends 父类{
      constructor(要继承的父类属性,新增属性){
            super(要继承的父类属性);
            this.新增属性 = 新增属性; //只能放在super后
      }
}
```

- 子类通过extends关键字实现继承
- 子类中的super关键字指代父类的实例，即父类的this对象
- 子类的constructor方法必须先调用super方法，因为子类没有自己的this对象，而是继承了父类的this对象。（ES5的继承实际上是先创建子类的实例对象this，然后再将父类的方法添加到this上，Parent.apply(this)）

### 5.2.3 getter

### 5.2.4 setter

## 5.3 解构赋值

本质上的一种匹配模式，只要等号两边的模式相同，那么左边的变量就可以被赋予对应的值

### 5.3.1 数组

```js
let [a, b, c, ...r] = [1, 2, 3, 4, 5]	//r是个数组
```

新创建数组中变量可随意写

### 5.3.1 对象

```js
const obj = {a:'', b:'', c:''}
const {a, b, c} = obj
const {a:m, b:n, c:q} = obj
```

新创建对象中key必须和源对象key一致，但可以取别名

### 5.3.1 基本类型

```js
let [a, b, c] = '123'
let {length: len} = 'miaov'
```

### 5.3.1 综合

```js
var arr = [
   {
   a: 1,
   b: [2, 3, 4]
   },
   {
   c: 5,
   d: 6
   }
]
//取b数组的第一项
var [{b:[x]}] = arr
//结果为x=2
```

## 5.4 展开运算符

### 5.4.1 数组

```js
const first = [1, 2, 3]
const second = [4, 5, 6]
const combined = [...first, 7, 8, ...second, 9]
```

### 5.4.2 对象

```js
const first ={a:1, b:2}
const second = {c:3, d:4}
const combined = {...first, e:5, ...second, g:6}
```

注意：不能直接```...对象```这样展开对象，必须在外包裹```{...对象}```，表示克隆字面量对象

```js
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 };
// 克隆后的对象: { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 };
// 合并后的对象: { foo: "baz", x: 42, y: 13 }

var changeObj = { ...obj1, foo: 'parker'};
// 克隆并修改（也算合并）对象：{ foo: "parker", x: 42 }
```



## 5.5 promise异步对象

### 5.5.1 特点

- 用来传递异步操作的消息
- 对象的状态不受外界干扰
- 一旦状态改变就不会再变
- 每当new一个promise对象就会立即执行
- promise函数不是异步，里面的程序才是异步

### 5.5.2 创建

```js
const p = new Promise((resolve,reject)=>{
    异步函数(() => {
        //此处何时调用resolve还是reject都是人为安排的，并不是异步函数报错才用reject
        resolve("成功参数")	//将promise对象的状态设置为成功
        reject("失败参数")	//将promise对象的状态设置为失败
    })
})
p.then((value) => {
    //执行成功的回调
},(reason) => {
    //执行失败的回调
})
```

### 5.5.3 三种状态

Pending(进行中)===>Resolved(已完成)

Pending(进行中)===>Rejected(已失败)

### 5.5.4 实例方法

- p.then((data1)=>{}).then((data2)=>{})：data1为res中的"成功参数",data2为前面then回调函数中成功参数
- p.catch((err)=>{})：err为rej中的"失败参数"
- p.finally(()=>{})：无参数，无论成功失败都会执行
- then和catch合并写法：p.then((data)=>{},(err)=>{})
- p.done()：写在链式最后，捕捉任何出现的错误并向全局抛出
- p.finally()：不管promise对象最后的状态如何都会执行的操作

### 5.5.5 静态方法

- Promise.resolve()：直接创建一个成功的promise

- Promise.reject()：直接创建一个失败的promise

- ```js
  var p = Promise.all([p1,p2,p3])
  p.then((data)=>{})
  //data为三个不同的promise成功参数的数组
  //返回一个新的promise，只有所有的promise都成功才成功，只要有一个失败了就直接失败
  ```
  
- ```js
  var p = Promise.race([p1,p2,p3])
  p.then((data)=>{})
  //data为最先完成的promise的成功参数
  //返回一个新的promise，第一个完成的promise的结果状态就是最终的结果状态
  ```
  

### 5.5.6 异常穿透

- 当使用promise的then链式调用时，可以在最后指定失败的回调

- 前面任何操作出了异常，都会传到最后失败的回调中处理

  ```js
  const p = new Promise((resolve,reject)=>{
      异步函数(() => {
          resolve("成功参数")
      })
  })
  p.then((value) => {
      console.log('1')
  }.then(value) => {
      console.log('2')
  }).catch(reason => {
      console.warn(reason)
  })
  ```

### 5.5.7 中断promise链

- 当使用promise的then链式调用时，在中间中断，不再调用后面的回调函数

- 办法：在回调函数中返回一个pendding状态的promise对象

  ```js
  const p = new Promise((resolve,reject)=>{
      异步函数(() => {
          resolve("成功参数")
      })
  })
  p.then((value) => {
      console.log('1')
      return new Promise(() => {})	//返回一个pendding状态的promise对象
  }.then(value) => {
      console.log('2')
  })
  ```

  



## 5.6 async和await

- 简化Promise函数，以同步函数的书写方式表达异步函数
- async函数就是Generator函数的语法糖，*替换为async，yield替换为await
- async函数返回promise函数



## 5.7 generator



## 5.8 Symbol



# 6. 正则表达式



# 7. Canvas绘图
