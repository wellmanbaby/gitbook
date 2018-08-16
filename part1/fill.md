# ES6新增方法fill()

**fill() 方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。**
***
## JavaScript Demo: Array.fill()

```
var array1 = [1, 2, 3, 4];

// fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0]

// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]

console.log(array1.fill(6));
// expected output: [6, 6, 6, 6]

```
***
## 语法

```
arr.fill(value, start, end)
```
***
### 参数
**value：** 用来填充数组元素的值

**start:** 起始索引，默认为0，可选

**end：** 终止索引，默认值是this.length，可选
***
### 返回值

**修改后的数组**
***
## 描述

**fill** 方法接受三个参数 **value**, **start** 以及 **end**。**start** 和
**end** 参数是可选的, 其默认值分别为 **0** 和 **this** 对象的 **length** 属性值。

如果 **start** 是个负数, 则开始索引会被自动计算成为 **length+start**, 其中 **length** 是 **this** 对象的 **length** 属性值。如果 **end** 是个负数, 则结束索引会被自动计算成为 **length+end**。

**fill** 方法故意被设计成通用方法, 该方法不要求 **this** 是数组对象。

**fill** 方法是个可变方法, 它会改变调用它的 **this** 对象本身, 然后返回它, 而并不是返回一个副本。

当一个对象被传递给 **fill**方法的时候, 填充数组的是这个对象的引用(这句话我看不太懂)。
***
## 式例

```
[1, 2, 3].fill(4);               // [4, 4, 4]
[1, 2, 3].fill(4, 1);            // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2);         // [1, 4, 3]
[1, 2, 3].fill(4, 1, 1);         // [1, 2, 3]
[1, 2, 3].fill(4, 3, 3);         // [1, 2, 3]
[1, 2, 3].fill(4, -3, -2);       // [4, 2, 3]
[1, 2, 3].fill(4, NaN, NaN);     // [1, 2, 3]
[1, 2, 3].fill(4, 3, 5);         // [1, 2, 3]
Array(3).fill(4);                // [4, 4, 4]
[].fill.call({ length: 3 }, 4);  // {0: 4, 1: 4, 2: 4, length: 3}，我还没看到call！

// Objects by reference.
var arr = Array(3).fill({}) // [{}, {}, {}];
arr[0].hi = "hi"; // [{ hi: "hi" }, { hi: "hi" }, { hi: "hi" }]
```
