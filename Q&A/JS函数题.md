### 清除字符串前后空格

```
const trimString = function (str) {
	// const reg = new RegExp("^\\s*|\\s*$", "")	//构造函数第一个参数用引号时里面特殊字符需要前面加‘\’转义
	const reg = new RegExp(/^\s*|\s*$/, "")		//也可以第一个参数用‘//’表达式
	if(str && typeof str === "string") {
		return str.replace(reg, "")
	}
}
let a = "   hello "
console.log(trimString(a))
```





### 冒泡排序

```
//自己做的
const a = [3, 2, 6, 1, 5, 4]
const bubbleSort = function (arr) {
	for(var i=0; i<arr.length-1; i++) {
		for(var j=i+1; j<arr.length; j++) {
			if(arr[i]>arr[j]) {
				const store = arr[i]
				arr[i] = arr[j]
				arr[j] = store
			}
			console.log(`j第${j}次`,arr)
		}
		console.log(`i第${i}次`,arr)
	}
}
//结果
j第1次 (6) [2, 3, 6, 1, 5, 4]
j第2次 (6) [2, 3, 6, 1, 5, 4]
j第3次 (6) [1, 3, 6, 2, 5, 4]
j第4次 (6) [1, 3, 6, 2, 5, 4]
j第5次 (6) [1, 3, 6, 2, 5, 4]
i第0次 (6) [1, 3, 6, 2, 5, 4]
j第2次 (6) [1, 3, 6, 2, 5, 4]
j第3次 (6) [1, 2, 6, 3, 5, 4]
j第4次 (6) [1, 2, 6, 3, 5, 4]
j第5次 (6) [1, 2, 6, 3, 5, 4]
i第1次 (6) [1, 2, 6, 3, 5, 4]
j第3次 (6) [1, 2, 3, 6, 5, 4]
j第4次 (6) [1, 2, 3, 6, 5, 4]
j第5次 (6) [1, 2, 3, 6, 5, 4]
i第2次 (6) [1, 2, 3, 6, 5, 4]
j第4次 (6) [1, 2, 3, 5, 6, 4]
j第5次 (6) [1, 2, 3, 4, 6, 5]
i第3次 (6) [1, 2, 3, 4, 6, 5]
j第5次 (6) [1, 2, 3, 4, 5, 6]
i第4次 (6) [1, 2, 3, 4, 5, 6]

//其他答案
var array=[10,20,9,8,79,65,100];
//比较轮数
for ( var i=0;i<array.length-1;i++){
    //每轮比较次数，次数=长度-1-此时的轮数
    for (var j=0;j<array.length-1-i;j++) {
        if (array[j] > array[j + 1]) {
            var temp = array[i];
            array[j] = array[j + 1];
            array[j + 1] = temp;
        } //end if
    }//end for 次数
} //end for 轮数
console.log(array);
```





### ajax 请求或者submit请求时 锁屏功能以及开锁功能





### 获得url参数的值







### 计算1-10000中出现的0 的次数







### 降维数组



### 判断一个字符串中出现次数最多的字符，统计这个次数

```
//自己做的
const s = 'abcabacc'
const maxStr = function (str) {
	const a = {}
	const arr = str.split('')
	for(var i=0; i<arr.length; i++) {
		if(!Object.keys(a).includes(arr[i])) {
			a[arr[i]] = 1
		}else{
			a[arr[i]]++
		}
	}
	const maxNum = Math.max(...Object.values(a))
	const keys = Object.keys(a)
	const res = keys.filter((item) => {
		return a[item] === maxNum
	})
	console.log(`出现最多的字符是${res},出现了${maxNum}次`)
}
maxStr(s)
//结果 ‘出现最多的字符是a,c,出现了3次’
```





### 去掉一个数组的重复元素

```
//自己做的
const a = [3, 2, 1, 6, 1, 3, 5, 2, 4]
const removeRepet = function (arr) {
	const b = []
	for(var i=0; i<arr.length; i++) {
		if(!b.includes(arr[i])) {
			b.push(arr[i])
		}
	}
	console.log(b)
}
removeRepet(a)
//结果[3, 2, 1, 6, 5, 4]
```





### 深度克隆