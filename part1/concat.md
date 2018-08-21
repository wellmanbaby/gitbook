# concat()

**concat() 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。**


***
## JavaScript Demo: Array.concat()

```
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];

console.log(array1.concat(array2));
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```
***

## 语法

```
var new_array = old_array.concat(value1, value2, ..., valueN)
```
***
### 参数

**valueN:** 将数组和/或值连接成新数组。

***
### 返回值

新的 Array 实例。
***
## 描述

concat方法创建一个新的数组，它由被调用的对象中的元素组成，每个参数的顺序依次是该参数的元素（如果参数是数组）或参数本身（如果参数不是数组）。它不会递归到嵌套数组参数中。

concat方法不会改变this或任何作为参数提供的数组，而是返回一个浅拷贝，它包含与原始数组相结合的相同元素的副本。 原始数组的元素将复制到新数组中，如下所示：

对象引用（而不是实际对象）：concat将对象引用复制到新数组中。 原始数组和新数组都引用相同的对象。 也就是说，如果引用的对象被修改，则更改对于新数组和原始数组都是可见的。 这包括也是数组的数组参数的元素。

数据类型如字符串，数字和布尔（不是String，Number 和 Boolean 对象）：concat将字符串和数字的值复制到新数组中。

## 式例

### 连接两个数组
以下代码将两个数组合并为一个新数组：


```
var alpha = ['a', 'b', 'c'];
var numeric = [1, 2, 3];

alpha.concat(numeric);
// result in ['a', 'b', 'c', 1, 2, 3]
```


### 连接三个数组
以下代码将三个数组合并为一个新数组：

```
var num1 = [1, 2, 3],
    num2 = [4, 5, 6],
    num3 = [7, 8, 9];

var nums = num1.concat(num2, num3);

console.log(nums); 
// results in [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
### 将值连接到数组
以下代码将三个值连接到数组：
```
var alpha = ['a', 'b', 'c'];

var alphaNumeric = alpha.concat(1, [2, 3]);
//刚开始有些疑虑觉得结果应该是['a', 'b', 'c', 1, [2, 3]],仔细一下自己傻逼了
console.log(alphaNumeric); 
// results in ['a', 'b', 'c', 1, 2, 3]
```
### 合并嵌套数组
以下代码，合并数组并保留引用：

```
var num1 = [[1]];
var num2 = [2, [3]];

var nums = num1.concat(num2);

console.log(nums);
// results in [[1], 2, [3]]

// modify the first element of num1
num1[0].push(4);

console.log(nums);
// results in [[1, 4], 2, [3]]
```
所谓保留引用就是原数组不动






