# splice()

**splice() 方法通过删除现有元素和/或添加新元素来更改一个数组的内容。**


***
## JavaScript Demo: Array.splice()

```
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at 1st index position
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'June']

months.splice(4, 1, 'May');
// replaces 1 element at 4th index
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'May']

```
***

## 语法

```
array.splice(start, deleteCount, item1, item2 ...])
```
***
### 参数

**start:** 指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从-1计数）；如果负数的绝对值大于数组的长度，则表示开始位置为第0位。

**deleteCount(可选):** 整数，表示要移除的数组元素的个数。如果 deleteCount 是 0，则不移除元素。这种情况下，至少应添加一个新元素。如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。

如果deleteCount被省略，则其相当于(arr.length - start)。

**item1, item2, ...（可选）：** 要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。

splice方法使用deleteCount参数来控制是删除还是添加：start参数是必须的，表示开始的位置（从0计数），如：start=0从第一个开始；start>= array.length-1表示从最后一个开始。
1. 从start位置开始删除[start，end]的元素。
array.splice(start)
2. 从start位置开始删除[start，Count]的元素。
array.splice(start, deleteCount)    
3. 从start位置开始添加item1, item2, ...元素。
array.splice(start, 0, item1, item2, ...)   
***
### 返回值
由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。
***
## 描述

如果添加进数组的元素个数不等于被删除的元素个数，数组的长度会发生相应的改变。

## 提示和注释

**注释：请注意，splice() 方法与 slice() 方法的作用是不同的，splice() 方法会直接对数组进行修改。**

## 式例

### 从第2位开始删除0个元素，插入“drum”
```
var myFish = ["angel", "clown", "mandarin", "surgeon"]; 
//从第 2 位开始删除 0 个元素，插入 "drum" 
var removed = myFish.splice(2, 0, "drum"); 
//运算后的 myFish:["angel", "clown", "drum", "mandarin", "surgeon"] 
//被删除元素数组：[]，没有元素被删除
```
### 从第3位开始删除1个元素

```
var myFish = ['angel', 'clown', 'drum', 'sturgeon'];
var removed = myFish.splice(2, 1, "trumpet"); 
//运算后的myFish: ["angel", "clown", "trumpet", "surgeon"] 
//被删除元素数组：["drum"]
```
### 从第0位开始删除2个元素，然后插入"parrot","anemone"和"blue"

```
var myFish = ['angel', 'clown', 'trumpet', 'sturgeon'];
var removed = myFish.splice(0, 2, 'parrot', 'anemone', 'blue');
// 运算后的myFish： ["parrot", "anemone", "blue", "trumpet", "sturgeon"] 
// 被删除元素数组：["angel", "clown"]
```
### 从第2位开始删除2个元素

```
var myFish = ['parrot', 'anemone', 'blue', 'trumpet', 'sturgeon'];
var removed = myFish.splice(myFish.length - 3, 2);
// 运算后的myFish： ["parrot", "anemone", "sturgeon"] 
// 被删除元素数组：["blue", "trumpet"]
```
### 从第2位开始删除所有元素

```
var myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];
var removed = myFish.splice(2);
// 运算后的myFish ：["angel", "clown"] 
// 被删除的元素数组： ["mandarin", "sturgeon"]
```

***




