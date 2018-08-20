# forEach()

**forEach() 方法对数组的每个元素执行一次提供的函数。**


***
## JavaScript Demo: Array.forEach()

```
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// expected output: "a"
// expected output: "b"
// expected output: "c"


```
***

## 语法

```
array.forEach(callback(currentValue, index, array){
    //do something
}, this)

array.forEach(callback[, thisArg])
```
***
### 参数

**callback:** 为数组中每个元素执行的函数，该函数接收三个参数：

**currentValue:** 数组中正在处理的当前元素。

**index：** 要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。

**array：** forEach()方法正在操作的数组。 

**thisArg：** 可选参数。当执行回调 函数时用作this的值(参考对象)。
***
### 返回值

undefined
***
## 描述

forEach 方法按升序为数组中含有效值的每一项执行一次callback 函数，那些已删除或者未初始化的项将被跳过（例如在稀疏数组上）。

callback 函数会被依次传入三个参数：

**1. 数组当前项的值；**

**2. 数组当前项的引用；**

**3. 数组对象本身**

如果给forEach传递了thisArg参数，当调用时，它将被传给callback 函数，作为它的this值。否则，将会传入 undefined 作为它的this值。callback函数最终可观察到this值，这取决于 函数观察到this的常用规则。

forEach 遍历的范围在第一次调用 callback 前就会确定。调用forEach 后添加到数组中的项不会被 callback 访问到。如果已经存在的值被改变，则传递给 callback 的值是 forEach 遍历到他们那一刻的值。已删除的项不会被遍历到。如果已访问的元素在迭代时被删除了(例如使用 shift()) ，之后的元素将被跳过 - 参见下面的示例。

forEach() 为每个数组元素执行callback函数；不像map() 或者reduce() ，它总是返回 undefined值，并且不可链式调用。典型用例是在一个链的最后执行副作用。
## 提示和注释

**注释：没有办法中止或者跳出 forEach 循环，除了抛出一个异常。如果你需要这样，使用forEach()方法是错误的，你可以用一个简单的循环作为替代。如果您正在测试一个数组里的元素是否符合某条件，且需要返回一个布尔值，那么可使用 Array.every 或 Array.some。如果可用，新方法 find() 或者findIndex() 也可被用于真值测试的提早终止。**

## 式例

### for 循环转换为 forEach

转换前：
```
const items = ['item1', 'item2', 'item3'];
const copy = [];

for (let i=0; i<items.length; i++) {
  copy.push(items[i])
}
```
转换后：

```
const items = ['item1', 'item2', 'item3'];
const copy = [];

items.forEach(function(item){
  copy.push(item)
});
```

### 打印出数组的内容

下面的代码会为每一个数组元素输出一行记录：
```
function logArrayElements(element, index, array) {
    console.log("a[" + index + "] = " + element);
}

// 注意索引2被跳过了，因为在数组的这个位置没有项
[2, 5, ,9].forEach(logArrayElements);

// a[0] = 2
// a[1] = 5
// a[3] = 9

[2, 5,"" ,9].forEach(logArrayElements);
// a[0] = 2
// a[1] = 5
// a[2] = 
// a[3] = 9

[2, 5, undefined ,9].forEach(logArrayElements);
// a[0] = 2
// a[1] = 5
// a[2] = undefined
// a[3] = 9


let xxx;
// undefined

[2, 5, xxx ,9].forEach(logArrayElements);
// a[0] = 2
// a[1] = 5
// a[2] = undefined
// a[3] = 9
```
### 使用thisArg
举个勉强的例子，从每个数组中的元素值中更新一个对象的属性：
```
function Counter() {
    this.sum = 0;
    this.count = 0;
}

Counter.prototype.add = function(array) {
    array.forEach(function(entry) {
        this.sum += entry;
        ++this.count;
    }, this);
    //console.log(this);
};

var obj = new Counter();
obj.add([1, 3, 5, 7]);

obj.count; 
// 4 === (1+1+1+1)
obj.sum;
// 16 === (1+3+5+7)
```
### 如果数组在迭代时被修改了，则其他元素会被跳过。
下面的例子输出"one", "two", "four"。当到达包含值"two"的项时，整个数组的第一个项被移除了，这导致所有剩下的项上移一个位置。因为元素 "four"现在在数组更前的位置，"three"会被跳过。 forEach()不会在迭代之前创建数组的副本。
```
var words = ["one", "two", "three", "four"];
words.forEach(function(word) {
  console.log(word);
  if (word === "two") {
    words.shift();
  }
});
// one
// two
// four
```





