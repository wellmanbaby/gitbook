# reverse()

**reverse() 方法将数组中元素的位置颠倒。**

**第一个数组元素成为最后一个数组元素，最后一个数组元素成为第一个。**
***
## JavaScript Demo: Array.reverse()

```
var array1 = ['one', 'two', 'three'];
console.log('array1: ', array1);
// expected output: Array ['one', 'two', 'three']

var reversed = array1.reverse(); 
console.log('reversed: ', reversed);
// expected output: Array ['three', 'two', 'one']

/* Careful: reverse is destructive. It also changes
the original array */ 
console.log('array1: ', array1);
// expected output: Array ['three', 'two', 'one']
```
***
## 语法

```
arr.reverse()
```
***
## 参数

无
***
## 描述

**reverse 方法颠倒数组中元素的位置，并返回该数组的引用，其实就是返回改变位置后的数组。**
***
## 式例

**颠倒数组中的元素**

下例将会创建一个数组 myArray，其包含三个元素，然后颠倒该数组。

```
var myArray = ['one', 'two', 'three'];
myArray.reverse(); 

console.log(myArray) // ['three', 'two', 'one']
```
