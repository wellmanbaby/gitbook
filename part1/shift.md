# shift()

**shift() 方法从数组中删除第一个元素，并返回该元素的值。此方法更改数组的长度。**


***
## JavaScript Demo: Array.shift()

```
var array1 = [1, 2, 3];

var firstElement = array1.shift();

console.log(array1);
// expected output: Array [2, 3]

console.log(firstElement);
// expected output: 1
```
***
## 返回值

**从数组中删除的元素; 如果数组为空则返回undefined 。 **

***
## 语法

```
arr.shift()
```
***
## 参数

无
***
## 描述

**shift 方法移除索引为 0 的元素(即第一个元素)，并返回被移除的元素，其他元素的索引值随之减 1。如果 length 属性的值为 0 (长度为 0)，则返回 undefined。**

**shift 方法并不局限于数组：这个方法能够通过 call 或 apply 方法作用于类似数组的对象上。但是对于没有 length 属性（从0开始的一系列连续的数字属性的最后一个）的对象，调用该方法可能没有任何意义。**
***
## 式例

**移除数组中的一个元素**

以下代码显示了删除其第一个元素之前和之后的myFish数组。它还显示已删除的元素：

```
let myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

console.log('调用 shift 之前: ' + myFish);
// "调用 shift 之前: angel,clown,mandarin,surgeon"

var shifted = myFish.shift(); 

console.log('调用 shift 之后: ' + myFish); 
// "调用 shift 之后: clown,mandarin,surgeon" 

console.log('被删除的元素: ' + shifted); 
// "被删除的元素: angel"
```
