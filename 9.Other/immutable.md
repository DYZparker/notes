## 简介

-  Immutable Data 就是一旦创建，就不能再被更改的数据  **（持久化数据结构）** 
-  对 Immutable 对象的任何修改或添加删除操作都会返回一个新的 Immutable 对象 
-  Immutable 使用了[Structural Sharing（结构共享）](https://link.jianshu.com/?t=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F27133830%3Fgroup_id%3D851585269567213568)，即如果对象树中一个节点发生变化，只修改这个节点和受它影响的父节点，其它节点则进行共享 
-  旧数据创建新数据时，要保证旧数据同时可用且不变，同时为了避免 deepCopy 把所有节点都复制一遍带来的性能损耗 



## 优点

-  **降低 Mutable 带来的复杂度** 

  对象的引用被改变赋值时的混乱，用浅拷贝或深拷贝又增加了内存消耗

-  **节省内存空间** 

  immutable的结构共享会尽量复用内存

  ```js
  import { Map } from 'immutable';
  let a = Map({
    select: 'users',
    filter: Map({ name: 'Cam' })
  })
  let b = a.set('select', 'people');
  
  a === b; // false
  a.get('filter') === b.get('filter'); // true
  ```

-  **Undo/Redo，Copy/Paste，随意穿越** 

   因为每次数据都是不一样的，只要把这些数据放到一个数组里储存起来，想回退到哪里就拿出对应数据即可，很容易开发出撤销重做这种功能 

-  **拥抱函数式编程** 

   函数式编程关心数据的映射，命令式编程关心解决问题的步骤，纯函数式编程比面向对象更适用于前端开发。因为只要输入一致，输出必然一致，这样开发的组件更易于调试和组装。 



## 缺点

 Immutable的API设计的和原生对象类似，容易混淆操作 



## 数据类型

- List: 有序索引集，类似JavaScript中的Array。
- Map: 无序索引集，类似JavaScript中的Object。
- OrderedMap: 有序的Map，根据数据的set()进行排序。
- Set: 没有重复值的集合。
- OrderedSet: 有序的Set，根据数据的add进行排序。
- Stack: 有序集合，支持使用unshift()和shift()添加和删除。
- Record: 一个用于生成Record实例的类。类似于JavaScript的Object，但是只接收特定字符串为key，具有默认值。
- Seq: 序列，但是可能不能由具体的数据结构支持。
- Collection: 是构建所有数据结构的基类，不可以直接构建



## 常用API

#### 数据转换

###### fromJS()

作用：将一个js数据转换为Immutable类型的数据
用法：`fromJS(value, converter)`
简介：value是要转变的数据，converter是要做的操作。第二个参数可不填，默认情况会将数组准换为List类型，将对象转换为Map类型，其余不做操作

代码实现：

```csharp
    const obj = Immutable.fromJS({a:'123',b:'234'},function (key, value, path) {
        console.log(key, value, path)
        return isIndexed(value) ? value.toList() : value.toOrderedMap())
    })
```

###### toJS()

作用：将一个Immutable数据转换为JS类型的数据
用法：`value.toJS()`

#### 数据创建

###### List() 和 Map()

作用：用来创建一个新的List/Map对象
用法:

```php
//List
Immutable.List(); // 空List
Immutable.List([1, 2]);

//Map
Immutable.Map(); // 空Map
Immutable.Map({ a: '1', b: '2' });
```

###### size()

作用：属性，获取List/Map的长度，等同于ImmutableData.count();

#### 数据判断

###### is()

作用：对两个对象进行比较
用法：`is(map1,map2)`
简介：和js中对象的比较不同，在js中比较两个对象比较的是地址，但是在Immutable中比较的是这个对象hashCode和valueOf，只要两个对象的hashCode相等，值就是相同的，避免了深度遍历，提高了性能

代码实现：

```jsx
import { Map, is } from 'immutable'
const map1 = Map({ a: 1, b: 1, c: 1 })
const map2 = Map({ a: 1, b: 1, c: 1 })
map1 === map2   //false
Object.is(map1, map2) // false
is(map1, map2) // true
```

###### List.isList() 和 Map.isMap()

作用：判断一个数据结构是不是List/Map类型
用法：

```jsx
List.isList([]); // false
List.isList(List()); // true

Map.isMap({}) // false
Map.isMap(Map()) // true
```

###### has() 、 hasIn()

作用：判断是否存在某一个key
用法：

```bash
Immutable.fromJS([1,2,3,{a:4,b:5}]).has('0'); //true
Immutable.fromJS([1,2,3,{a:4,b:5}]).has('0'); //true
Immutable.fromJS([1,2,3,{a:4,b:5}]).hasIn([3,'b']) //true
```

###### includes()

作用：判断是否存在某一个value
用法：

```bash
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes(2); //true
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes('2'); //false 不包含字符2
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes(5); //false 
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes({a:4,b:5}) //false
Immutable.fromJS([1,2,3,{a:4,b:5}]).includes(Immutable.fromJS({a:4,b:5})) //true
```

#### 数据获取

###### get() 、 getIn()

作用：获取数据结构中的数据

```csharp
//获取List索引的元素
ImmutableData.get(0);

// 获取Map对应key的value
ImmutableData.get('a');

// 获取嵌套数组中的数据
ImmutableData.getIn([1, 2]);

// 获取嵌套map的数据
ImmutableData.getIn(['a', 'b']);
```

###### first() 、 last()

作用：用来获取第一个元素或者最后一个元素，若没有则返回undefined
代码：

```cpp
Immutable.fromJS([1,2,3,{a:4,b:5}]).first()//1
Immutable.fromJS([1,2,3,{a:4,b:5}]).last()//{a:4,b:5}

Immutable.fromJS({a:1,b:2,c:{d:3,e:4}}).first() //1
Immutable.fromJS({a:1,b:2,c:{d:3,e:4}}).first() //{d:3,e:4}
```

#### 数据修改

注：这里对于数据的修改，是对原数据进行操作后的值赋值给一个新的数据，并不会对原数据进行修改，因为Immutable是不可变的数据类型。

###### set()

作用：设置第一层key、index的值
用法：

```csharp
const originalList = List([ 0 ]);
// List [ 0 ]
originalList.set(1, 1);
// List [ 0, 1 ]
originalList.set(0, 'overwritten');
// List [ "overwritten" ]
originalList.set(2, 2);
// List [ 0, undefined, 2 ]

List().set(50000, 'value').size;
// 50001

const originalMap = Map()
const newerMap = originalMap.set('key', 'value')
const newestMap = newerMap.set('key', 'newer value')

originalMap
// Map {}
newerMap
// Map { "key": "value" }
newestMap
// Map { "key": "newer value" }
```

List在使用的时候，将index为number值设置为value。Map在使用的时候，将key的值设置为value。

在List中使用时，若传入的number为负数，则将index为size+index的值设置为value，例，若传入-1，则将size-1的值设为value。若传入的number的值超过了List的长度，则将List自动补全为传入的number的值，将number设置为value，其余用undefined补全。**注：跟js中不同，List中不存在空位，[,,,],List中若没有值，则为undefined。**

###### setIn()

作用：设置深层结构中某属性的值
用法：

```jsx
const originalMap = Map({
  subObject: Map({
    subKey: 'subvalue',
    subSubObject: Map({
      subSubKey: 'subSubValue'
    })
  })
})

const newMap = originalMap.setIn(['subObject', 'subKey'], 'ha ha!')
// Map {
//   "subObject": Map {
//     "subKey": "ha ha!",
//     "subSubObject": Map { "subSubKey": "subSubValue" }
//   }
// }

const newerMap = originalMap.setIn(
  ['subObject', 'subSubObject', 'subSubKey'],
  'ha ha ha!'
)
// Map {
//   "subObject": Map {
//     "subKey": "subvalue",
//     "subSubObject": Map { "subSubKey": "ha ha ha!" }
//   }
// }
```

用法与set()一样，只是第一个参数是一个数组，代表要设置的属性所在的位置

#### 数据删除

###### delete()

作用：用来删除第一层结构中的属性
用法：

```go
// List
List([ 0, 1, 2, 3, 4 ]).delete(0);
// List [ 1, 2, 3, 4 ]

// Map
const originalMap = Map({
  key: 'value',
  otherKey: 'other value'
})
// Map { "key": "value", "otherKey": "other value" }
originalMap.delete('otherKey')
// Map { "key": "value" }
```

###### deleteIn()

用来删除深层数据，用法参考setIn

###### deleteAll() 

**(Map独有，List没有)**

作用：用来删除Map中的多个key
用法：deleteAll(keys: Iterable<K>): this
代码示例：

```jsx
const names = Map({ a: "Aaron", b: "Barry", c: "Connor" })
names.deleteAll([ 'a', 'c' ])
// Map { "b": "Barry" }
```

#### 数据更新

###### update()

作用：对对象中的某个属性进行更新，可对原数据进行相关操作
用法：

```php
////List
const list = List([ 'a', 'b', 'c' ])
const result = list.update(2, val => val.toUpperCase())

///Map
const aMap = Map({ key: 'value' })
const newMap = aMap.update('key', value => value + value)
```

###### updateIn()

用法参考setIn

###### clear()

作用：清除所有数据
用法：`clear(): this`
代码示例：

```php
Map({ key: 'value' }).clear()  //Map
List([ 1, 2, 3, 4 ]).clear()   // List
List中的各种删除与插入
List对应的数据结构是js中的数组，所以数组的一些方法在Immutable中也是通用的，比如push，pop,shift，
unshift，insert。
```

###### push()

在List末尾插入一个元素

###### pop()

在List末尾删除一个元素

###### unshift()

在List首部插入一个元素

###### shift()

在List首部删除一个元素

###### insert()

在List的index处插入元素
代码实现：

```php
List([ 0, 1, 2, 3, 4 ]).insert(6, 5) 
//List [ 0, 1, 2, 3, 4, 5 ]
List([ 1, 2, 3, 4 ]).push(5)
// List [ 1, 2, 3, 4, 5 ]
List([ 1, 2, 3, 4 ]).pop()
// List[ 1, 2, 3 ]
List([ 2, 3, 4]).unshift(1);
// List [ 1, 2, 3, 4 ]
List([ 0, 1, 2, 3, 4 ]).shift();
// List [ 1, 2, 3, 4 ]
```

List中还有一个特有的方法用法设置List的长度，setSize()

```php
List([]).setSize(2).toJS() //[undefined,undefined]
```



#### 关于merge

###### merge

作用：浅合并，新数据与旧数据对比，旧数据中不存在的属性直接添加，就数据中已存在的属性用新数据中的覆盖

###### mergrWith

作用：自定义浅合并，可自行设置某些属性的值

###### mergeIn

作用：对深层数据进行浅合并

###### mergeDeep

作用：深合并，新旧数据中同时存在的的属性为新旧数据合并之后的数据

###### mergeDeepIn

作用：对深层数据进行深合并

###### mergrDeepWith

作用：自定义深合并，可自行设置某些属性的值

这里用一段示例彻底搞懂merge，此示例为Map结构，List与Map原理相同

```jsx
 const Map1 = Immutable.fromJS({a:111,b:222,c:{d:333,e:444}});
 const Map2 = Immutable.fromJS({a:111,b:222,c:{e:444,f:555}});

 const Map3 = Map1.merge(Map2);
  //Map {a:111,b:222,c:{e:444,f:555}}
 const Map4 = Map1.mergeDeep(Map2);
  //Map {a:111,b:222,c:{d:333,e:444,f:555}}
 const Map5 = Map1.mergeWith((oldData,newData,key)=>{
      if(key === 'a'){
        return 666;
      }else{
        return newData
      }
    },Map2);
  //Map {a:666,b:222,c:{e:444,f:555}}
```

#### 序列算法

###### concat()

作用：对象的拼接，用法与js数组中的concat()相同，返回一个新的对象。
用法：`const List = list1.concat(list2)`

###### map()

作用：遍历整个对象，对Map/List元素进行操作，返回一个新的对象。
用法：

```jsx
Map({a:1,b:2}).map(val=>10*val)
//Map{a:10,b:20}
```

###### mapKey()

**Map特有的**

作用：遍历整个对象，对Map元素的key进行操作，返回一个新的对象。
用法：

```jsx
Map({a:1,b:2}).mapKey(val=>val+'l')
//Map{al:10,bl:20}
```

###### mapEntries()

**Map特有的**

作用：遍历整个对象，对Map元素的key和value同时进行操作，返回一个新的对象。Map的map()也可实现此功能。
用法：

```jsx
Map({a:1,b:2}).map((key,val)=>{
  return [key+'l',val*10]
})
//Map{al:10,bl:20}
```

###### 过滤 filter

作用：返回一个新的对象，包括所有满足过滤条件的元素
用法：

```jsx
Map({a:1,b:2}).filter((key,val)=>{
  return val == 2
})
//Map{b:2}
```

还有一个filterNot()方法，与此方法正好相反。

###### 反转 reverse

作用：将数据的结构进行反转
代码示例：

```cpp
Immutable.fromJS([1, 2, 3, 4, 5]).reverse();
// List [5,4,3,2,1]
Immutable.fromJS({a:1,b:{c:2,d:3},e:4}).recerse();
//Map {e:4,b:{c:2,d:3},a:1}
```

###### 排序 sort & sortBy

作用：对数据结构进行排序
代码示例：

```tsx
///List
Immutable.fromJS([4,3,5,2,6,1]).sort()
// List [1,2,3,4,5,6]
Immutable.fromJS([4,3,5,2,6,1]).sort((a,b)=>{
  if (a < b) { return -1; }
  if (a > b) { return 1; }
  if (a === b) { return 0; }
})
// List [1,2,3,4,5,6]
Immutable.fromJS([{a:3},{a:2},{a:4},{a:1}]).sortBy((val,index,obj)=>{
  return val.get('a')
},(a,b)=>{
  if (a < b) { return -1; }
  if (a > b) { return 1; }
  if (a === b) { return 0; }
})
//List  [ {a:3}, {a:2}, {a:4}, {a:1} ]

//Map

Immutable.fromJS( {b:1, a: 3, c: 2, d:5} ).sort()
//Map {b: 1, c: 2, a: 3, d: 5}
Immutable.fromJS( {b:1, a: 3, c: 2, d:5} ).sort((a,b)=>{
  if (a < b) { return -1; }
  if (a > b) { return 1; }
  if (a === b) { return 0; }
})
//Map {b: 1, c: 2, a: 3, d: 5}
Immutable.fromJS( {b:1, a: 3, c: 2, d:5} ).sortBy((value, key, obj)=> {
  return value
})
//Map {b: 1, c: 2, a: 3, d: 5}
```

###### 分组 groupBy

作用：对数据进行分组

```jsx
const listOfMaps = List([
  Map({ v: 0 }),
  Map({ v: 1 }),
  Map({ v: 1 }),
  Map({ v: 0 }),
  Map({ v: 2 })
])
const groupsOfMaps = listOfMaps.groupBy(x => x.get('v'))
// Map {
//   0: List [ Map{ "v": 0 }, Map { "v": 0 } ],
//   1: List [ Map{ "v": 1 }, Map { "v": 1 } ],
//   2: List [ Map{ "v": 2 } ],
// }
```

#### 查找数据

###### indexOf() 、 lastIndexOf 

**Map不存在此方法**
作用：和js数组中的方法相同，查找第一个或者最后一个value的index值，找不到则返回-1
用法：

```cpp
Immutable.fromJS([1,2,3,4]).indexof(3) //2
Immutable.fromJS([1,2,3,4]).lastIndexof(3) //2
```

###### findIndex() 、 findLastIndex() 

**Map不存在此方法**

作用：查找满足要求的元素的index值
用法：

```jsx
Immutable.fromJS([1,2,3,4]).findIndex((value,index,array)=>{
  return value%2 === 0;
})   // 1
Immutable.fromJS([1,2,3,4]).findLastIndex((value,index,array)=>{
  return index%2 === 0;
})  // 3
```

###### find() 、 findLast()

作用：查找满足条件的元素的value值
用法：

```csharp
Immutable.fromJS([1,2,3,4]).find((value,index,array)=>{
  return value%2 === 0;
})  // 2

Immutable.fromJS([1,2,3,4]).findLast((value,index,array)=>{
  return value%2 === 0;
})  // 4
```

###### findKey() 、 findLastKey()

作用：查找满足条件的元素的key值
用法：

```csharp
Immutable.fromJS([1,2,3,4]).findKey((value,index,array)=>{
  return value%2 === 0;
})  // 1

Immutable.fromJS([1,2,3,4]).findLastKey((value,index,array)=>{
  return value%2 === 0;
})  // 3
```

###### findEntry() 、 findLastEntry()

作用：查找满足条件的元素的键值对 key:value
用法：

```csharp
Immutable.fromJS([1,2,3,4]).findEntry((value,index,array)=>{
  return value%2 === 0;
})  // [1,2]

Immutable.fromJS([1,2,3,4]).findLastEntry((value,index,array)=>{
  return value%2 === 0;
})  // [3,4]
```

###### keyOf() lastKeyOf()

作用：查找某一个value对应的key值
用法：

```cpp
Immutable.fromJS([1,2,3,4]).keyOf(2) //1
Immutable.fromJS([1,2,3,4]).lastKeyOf(2) //1
```

###### max() 、 maxBy()

作用：查找最大值
用法:

```csharp
Immutable.fromJS([1, 2, 3, 4]).max() //4

Immutable.fromJS([{a;1},{a:2},{a: 3},{a:4}]).maxBy((value,index,array)=>{
  return value.get('a')
})  //{a:4}
```

###### min() 、 minBy()

作用：查找最小值
用法:

```csharp
Immutable.fromJS([1, 2, 3, 4]).min() //1

Immutable.fromJS([{a;1},{a:2},{a: 3},{a:4}]).minBy((value,index,array)=>{
  return value.get('a')
})  //{a:1}
```

#### 创建子集

###### slice()

作用： 和原生js中数组的slice数组一样，包含两个参数，start和end，start代表开始截取的位置，end代表结束的位置，不包括第end的元素。若不包括end，则返回整个对象，若end为负数，则返回（start，length-end）对应的数据。若start只有一个并且为负数，则返回最后的end个元素。
用法：

```cpp
Immutable.fromJS([1, 2, 3, 4]).slice(0); //[1,2,3,4]
Immutable.fromJS([1, 2, 3, 4]).slice(0,2); //[1,2]
Immutable.fromJS([1, 2, 3, 4]).slice(-2); //[3,4]
Immutable.fromJS([1, 2, 3, 4]).slice(0,-2); //[1,2]
```

###### rest()

作用：返回除第一个元素之外的所有元素
用法:

```cpp
Immutable.fromJS([1, 2, 3, 4]).rest()//[2,3,4]
```

###### butLast()

作用：返回除最后一个元素之外的所有元素
用法:

```cpp
Immutable.fromJS([1, 2, 3, 4]).rest()//[1,2,3]
```

###### skip()

作用：有一个参数n, 返回截掉前n个元素之后剩下的所有元素
用法:

```cpp
Immutable.fromJS([1, 2, 3, 4]).skip(1)//[2,3,4]\
```

###### skipLast()

作用：有一个参数n, 返回截掉最后n个元素之后剩下的所有元素
用法:

```cpp
Immutable.fromJS([1, 2, 3, 4]).skip(1)//[1,2,3]
```

###### skipWhile()

作用：返回从第一次返回false之后的所有元素

```php
Immutable.fromJS([1, 2, 3, 4]).skipWhile(list.skipWhile((value,index,list)=>{
  return value > 2;
}))// [1,2,3,4]
skipUntil()
```

作用：返回从第一次返回true之后的所有元素

```php
Immutable.fromJS([1, 2, 3, 4]).skipUntil(list.skipWhile((value,index,list)=>{
  return value > 2;
}))// [3,4]
```

###### take()

作用：有一个参数n, 返回前n个元素
用法：

```cpp
Immutable.fromJS([1, 2, 3, 4]).take(2)//[1,2]
```

###### takeLast()

作用：有一个参数n, 返回最后n个元素
用法：

```cpp
Immutable.fromJS([1, 2, 3, 4]).takeLast(2)//[3,4]
```

###### takeWhile()

作用：返回从第一次返回false之前的所有元素

```php
Immutable.fromJS([1, 2, 3, 4]).skipWhile(list.takeWhile((value,index,list)=>{
  return value > 2;
}))// []
```

###### takeUntil()

作用：返回从第一次返回true之前的所有元素

```php
Immutable.fromJS([1, 2, 3, 4]).skipUntil(list.takeUntil((value,index,list)=>{
  return value > 2;
}))// [1,2]
```

#### 处理数据

###### reduce()

作用：和js中数组中的reduce相同,按索引升序的顺序处理元素
用法：

```jsx
Immutable.fromJS([1,2,3,4]).reduce((pre,next,index,arr)=>{
  console.log(pre+next)
  return pre+next; 
})
// 3 6 10
```

###### reduceRight()

作用：和js中数组中的reduce相同,按索引降序的顺序处理元素
用法：

```jsx
Immutable.fromJS([1,2,3,4]).reduceRight((pre,next,index,arr)=>{
  console.log(pre+next)
  return pre+next; 
})
// 7 9 10
```

###### every()

作用：判断整个对象总中所有的元素是不是都满足某一个条件，都满足返回true，反之返回false。

代码：

```csharp
Immutable.fromJS([1,2,3,4]).every((value,index,arr)=>{
  return value > 2
}) // false
```

###### some()

作用：判断整个对象总中所有的元素是不是存在满足某一个条件的元素，若存在返回true，反之返回false。
代码：

```csharp
Immutable.fromJS([1,2,3,4]).some((value,index,arr)=>{
  return value > 2
}) // true
```

###### join()

作用：同js中数组的join方法。把准换为字符串
用法：

```csharp
Immutable.fromJS([1,2,3,4]).join(',') //1,2,3,4
```

###### isEmpty()

作用：判断是否为空
用法:

```ruby
Immutable.fromJS([]).isEmpty(); // true
Immutable.fromJS({}).isEmpty(); // true
```

###### count()

作用：返回元素个数，可自定义条件，返回满足条件的个数
用法：

```cpp
const list = Immutable.fromJS([1,2,3,4]);
const map = Immutable.fromJS({a:1,b:2,c:3,d:4});

list.count((value,index,list)=>{
  return value > 2;
})    //2

map.count((value,index,list)=>{
  return value > 2;
})    //2
```

###### countBy()

作用：与count不同的是，countBy返回一个对象
用法：

```cpp
const list = Immutable.fromJS([1,2,3,4]);
const map = Immutable.fromJS({a:1,b:2,c:3,d:4});

list.countBy((value,index,list)=>{
  return value > 2;
} //{false: 2, true: 2}

map.countBy((value,index,list)=>{
  return value > 2;
} //{false: 2, true: 2}
```