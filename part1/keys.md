# keys()

**keys() 方法返回一个包含数组中每个索引键的Array Iterator对象。**

**就是返回键值也就是每个元素的索引值**


***
## JavaScript Demo: Array.keys()

```
var array1 = ['a', 'b', 'c'];
var iterator = array1.keys(); 
  
for (let key of iterator) {
  console.log(key); // expected output: 0 1 2
}

```
***

## 语法

```
arr.keys()
```
***
### 参数

无
### 返回值

一个新的 Array 迭代器对象。

## 式例

### 索引迭代器会包含那些没有对应元素的索引


```
var arr = ["a", , "c"];
var sparseKeys = Object.keys(arr);
var denseKeys = [...arr.keys()];
console.log(sparseKeys); // ['0', '2']
console.log(denseKeys);  // [0, 1, 2]
```








