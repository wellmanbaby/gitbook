# slice()

**slice() 方法返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。**


***
## JavaScript Demo: Array.slice()

```
var animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// expected output: Array ["camel", "duck"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]



```
***

## 语法

```
arr.slice();
// [0, end]

arr.slice(begin);
// [begin, end]

arr.slice(begin, end);
// [begin, end)
```
***
### 参数

**begin:** 从该索引处开始提取原数组中的元素（从0开始）。

如果该参数为负数，则表示从原数组中的倒数第几个元素开始提取，slice(-2)表示提取原数组中的倒数第二个元素到最后一个元素（包含最后一个元素）。其实看到负的，就用数组length加上这个负数就行了。

如果省略 begin，则 slice 从索引 0 开始。：


**end:** 
在该索引处结束提取原数组元素（从0开始）。
slice会提取原数组中索引从 begin 到 end 的所有元素（包含begin，但不包含end）。

slice(1,4) 提取原数组中的第二个元素开始直到第四个元素的所有元素 （索引为 1, 2, 3的元素）。

如果该参数为负数， 则它表示在原数组中的倒数第几个元素结束抽取。 slice(-2,-1)表示抽取了原数组中的倒数第二个元素到最后一个元素（不包含最后一个元素，也就是只有倒数第二个元素）。

如果 end 被省略，则slice 会一直提取到原数组末尾。

如果 end 大于数组长度，slice 也会一直提取到原数组末尾。


***
### 返回值

一个含有提取元素的新数组
***
## 描述

slice 不修改原数组，只会返回一个浅复制了原数组中的元素的一个新数组。原数组的元素会按照下述规则拷贝：

**如果该元素是个对象引用 （不是实际的对象），slice 会拷贝这个对象引用到新的数组里。两个对象引用都引用了同一个对象。如果被引用的对象发生改变，则新的和原来的数组中的这个元素也会发生改变。**

**对于字符串、数字及布尔值来说（不是 String、Number 或者 Boolean 对象），slice 会拷贝这些值到新的数组里。在别的数组里修改这些字符串或数字或是布尔值，将不会影响另一个数组。**

如果向两个数组任一中添加了新元素，则另一个不会受到影响。
## 提示和注释



## 式例

### 返回现有数组的一部分


```
var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
var citrus = fruits.slice(1, 3);

// fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
// citrus contains ['Orange','Lemon']
```


### 使用 slice

在下例中, slice从myCar中创建了一个新数组newCar.两个数组都包含了一个myHonda对象的引用. 当myHonda的color属性改变为purple, 则两个数组中的对应元素都会随之改变.**myHonda才是本尊！**
```
// 使用slice方法从myCar中创建一个newCar.
var myHonda = { color: 'red', wheels: 4, engine: { cylinders: 4, size: 2.2 } };
var myCar = [myHonda, 2, "cherry condition", "purchased 1997"];
var newCar = myCar.slice(0, 2);

// 输出myCar, newCar,以及各自的myHonda对象引用的color属性.
console.log('myCar = ' + JSON.stringify(myCar));//JSON.stringify到底是啥不清楚
console.log('newCar = ' + JSON.stringify(newCar));
console.log('myCar[0].color = ' + JSON.stringify(myCar[0].color));
console.log('newCar[0].color = ' + JSON.stringify(newCar[0].color));

// 改变myHonda对象的color属性.
myHonda.color = 'purple';
console.log('The new color of my Honda is ' + myHonda.color);

//输出myCar, newCar中各自的myHonda对象引用的color属性.
console.log('myCar[0].color = ' + myCar[0].color);
console.log('newCar[0].color = ' + newCar[0].color);
```
上述代码输出:

```
myCar = [{color: 'red', wheels: 4, engine: {cylinders: 4, size: 2.2}}, 2,
       'cherry condition', 'purchased 1997']
newCar = [{color: 'red', wheels: 4, engine: {cylinders: 4, size: 2.2}}, 2]
myCar[0].color = red 
newCar[0].color = red
The new color of my Honda is purple
myCar[0].color = purple
newCar[0].color = purple
```

### 类数组（Array-like）对象
slice 方法可以用来将一个类数组（Array-like）对象/集合转换成一个新数组。你只需将该方法绑定到这个对象上。 一个函数中的 arguments 就是一个类数组对象的例子。
```
function list() {
  return Array.prototype.slice.call(arguments);
}

var list1 = list(1, 2, 3); // [1, 2, 3]
```






