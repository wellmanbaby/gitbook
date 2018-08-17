# unshift()

**unshift() 方法将一个或多个元素添加到数组的开头，并返回新数组的长度。**


***
## JavaScript Demo: Array.unshift()

```
var array1 = [1, 2, 3];

console.log(array1.unshift(4, 5));
// expected output: 5

console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]
```
***

## 语法

```
arr.unshift(element1, ..., elementN)
```
***
### 参数列表

**elementN:** 要添加到数组开头的元素
***
### 返回值
当一个对象调用该方法时，返回其length属性值
***
## 描述

**unshift 方法会在调用它的类数组对象的开始位置插入给定的参数。**

**unshift 特意被设计成具有通用性；这个方法能够通过 call 或 apply 方法作用于类数组对象上。不过对于没有 length 属性（代表从0开始的一系列连续的数字属性的最后一个）的对象，调用该方法可能没有任何意义。**
***
## 式例

```
var arr = [1, 2];

arr.unshift(0); //result of call is 3, the new array length
//arr is [0, 1, 2]

arr.unshift(-2, -1); // = 5
//arr is [-2, -1, 0, 1, 2]

arr.unshift( [-3] );
//arr is [[-3], -2, -1, 0, 1, 2]
```
