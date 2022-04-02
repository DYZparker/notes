**一、typeof**
typeof 是一个一元运算，放在一个运算数之前，运算数可以是任意类型。它返回值是一个字符串，该字符串说明运算数的类型。

```
var a = 'a';
var b = null;
console.log(typeof a); // String
console.log(typeof b); //Object1234
```

**二、instanceof**

判断前者是否为后者的实例，换而言之，是判断后者的原型对象（prototype）是否在前者的原型链之上。

```
function A () {};
var a = new A();
a instanceof A // true123
```

另外要注意的是Object和Function，两者即可为对象，亦可为函数。

```
Object instanceof Function // true
Function instanceof Object// true

Object.__proto__ === Function.prototype //true
Function.prototype.__proto__ === Object.prototype //true
Object.__proto__ === Function.__.proto__ //true123456
```

**三、isPrototypeOf()方法**
判断当前的原型对象（prototype）是否在传入参数的原型链上面。

```
function A () {};
var a = new A();
(A.prototype).isPrototypeOf(a) // true
(Object.prototype).isPrototypeOf(a) // true
(Object.prototype).isPrototypeOf(A.prototype) // true
```





