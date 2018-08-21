# join()

**join() 方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。**


***
## JavaScript Demo: Array.join()

```
var elements = ['Fire', 'Wind', 'Rain'];

console.log(elements.join());
// expected output: Fire,Wind,Rain

console.log(elements.join(''));
// expected output: FireWindRain

console.log(elements.join('-'));
// expected output: Fire-Wind-Rain
```
***

## 语法

```
str = arr.join()
// 默认为 ","

str = arr.join("")
// 分隔符 === 空字符串 ""

str = arr.join(separator)
// 分隔符

```
***
### 参数

**separator:** 

指定一个字符串来分隔数组的每个元素。

如果需要(separator)，将分隔符转换为字符串。

如果省略()，数组元素用逗号分隔。默认为 ","。

如果separator是空字符串("")，则所有元素之间都没有任何字符。

***
### 返回值

一个所有数组元素连接的字符串。如果 arr.length 为0，则返回空字符串
***
## 描述

所有的数组元素被转换成字符串，再用一个分隔符将这些字符串连接起来。如果元素是undefined 或者null， 则会转化成空字符串。

## 式例

### 使用四种不同的分隔符连接数组元素
下例首先创建了一个数组a，包含有三个元素，然后用四种不同的分隔符连接所有数组元素。首先是默认的分隔符逗号，然后是一个逗号加空格，接下来是一个加号前后加空格，最后是一个空字符串。


```
var a = ['Wind', 'Rain', 'Fire'];
var myVar1 = a.join();      // myVar1的值变为"Wind,Rain,Fire"
var myVar2 = a.join(', ');  // myVar2的值变为"Wind, Rain, Fire"
var myVar3 = a.join(' + '); // myVar3的值变为"Wind + Rain + Fire"
var myVar4 = a.join('');    // myVar4的值变为"WindRainFire"
```


### 连接类数组对象
下面的示例将连接类数组对象（arguments），通过在Array.prototype.join上调用Function.prototype.call.

```
function f(a, b, c) {
  var s = Array.prototype.join.call(arguments);
  console.log(s); // '1,a,true'
}
f(1, 'a', true);
```








