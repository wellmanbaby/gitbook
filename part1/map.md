# map()

**map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。**

**上面那句话拗口吧，一开始我也没看懂**

**其实map就是遍历数组元素再执行map中的函数最后返回结果数组**


***
## JavaScript Demo: Array.map()

```
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]

```
***

## 语法

```
var new_array = arr.map(function callback(currentValue, index, array) {
  Return element for new_array }[thisArg])
```
***
### 参数

**callback:** 

生成新数组元素的函数，使用三个参数：

**currentValue:** 

callback 数组中正在处理的当前元素。

**index(可选):**

callback 数组中正在处理的当前元素的索引。

**array(可选):**

callback  map 方法被调用的数组。

**thisArg（可选）:**

执行 callback 函数时使用的this 值。
***
### 返回值

一个新数组，每个元素都是回调函数的结果。
***
## 描述

map 方法会给原数组中的每个元素都按顺序调用一次  callback 函数。callback 每次执行后的返回值（包括 undefined）组合起来形成一个新数组。 callback 函数只会在有值的索引上被调用；那些从来没被赋过值或者使用 delete 删除的索引则不会被调用。

callback 函数会被自动传入三个参数：数组元素，元素索引，原数组本身。

如果 thisArg 参数有值，则每次 callback 函数被调用的时候，this 都会指向 thisArg 参数上的这个对象。如果省略了 thisArg 参数,或者赋值为 null 或 undefined，则 this 指向全局对象 。

map 不修改调用它的原数组本身（当然可以在 callback 执行时改变原数组）。

使用 map 方法处理数组时，数组元素的范围是在 callback 方法第一次调用之前就已经确定了。在 map 方法执行的过程中：原数组中新增加的元素将不会被 callback 访问到；若已经存在的元素被改变或删除了，则它们的传递到 callback 的值是 map 方法遍历到它们的那一时刻的值；而被删除的元素将不会被访问到。


## 式例

### 求数组中每个元素的平方根
下面的代码创建了一个新数组，值为原数组中对应数字的平方根。

```
var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
// roots的值为[1, 2, 3], numbers的值仍为[1, 4, 9]
```


### 使用 map 重新格式化数组中的对象
以下代码将一个包含对象的数组用map方法创建一个包含新重新格式化对象的新数组。

```
var kvArray = [{key: 1, value: 10}, 
               {key: 2, value: 20}, 
               {key: 3, value: 30}];

var reformattedArray = kvArray.map(function(obj) { 
   var rObj = {};
   rObj[obj.key] = obj.value;
   return rObj;
});

// reformattedArray 数组为： [{1: 10}, {2: 20}, {3: 30}], 

// kvArray 数组未被修改: 
// [{key: 1, value: 10}, 
//  {key: 2, value: 20}, 
//  {key: 3, value: 30}]
```
### 一般的map 方法
下面的例子演示如何在一个 String  上使用 map 方法获取字符串中每个字符所对应的 ASCII 码组成的数组：
```
function updateVegetablesCollection (veggies, veggie) {
    if (veggies.indexOf(veggie) === -1) {
        veggies.push(veggie);
        console.log('New veggies collection is : ' + veggies);
    } else if (veggies.indexOf(veggie) > -1) {
        console.log(veggie + ' already exists in the veggies collection.');
    }
}

var veggies = ['potato', 'tomato', 'chillies', 'green-pepper'];

// New veggies collection is : potato,tomato,chillies,green-papper,spinach
updateVegetablesCollection(veggies, 'spinach'); 
// spinach already exists in the veggies collection.
updateVegetablesCollection(veggies, 'spinach');
```
### 特殊的map案例
通常情况下，map 方法中的 callback 函数只需要接受一个参数，就是正在被遍历的数组元素本身。但这并不意味着 map 只给 callback 传了一个参数。这个思维惯性可能会让我们犯一个很容易犯的错误。

```
// 下面的语句返回什么呢:
["1", "2", "3"].map(parseInt);
// 你可能觉的会是[1, 2, 3]
// 但实际的结果是 [1, NaN, NaN]

// 通常使用parseInt时,只需要传递一个参数.
// 但实际上,parseInt可以有两个参数.第二个参数是进制数.
// 可以通过语句"alert(parseInt.length)===2"来验证.
// map方法在调用callback函数时,会给它传递三个参数:当前正在遍历的元素, 
// 元素索引, 原数组本身.
// 第三个参数parseInt会忽视, 但第二个参数不会,也就是说,
// parseInt把传过来的索引值当成进制数来使用.从而返回了NaN.

function returnInt(element) {
  return parseInt(element, 10);
}

['1', '2', '3'].map(returnInt); // [1, 2, 3]
// 意料之中的结果

// 也可以使用简单的箭头函数，结果同上
['1', '2', '3'].map( str => parseInt(str) );

// 一个更简单的方式:
['1', '2', '3'].map(Number); // [1, 2, 3]
// 与`parseInt` 不同，下面的结果会返回浮点数或指数:
['1.1', '2.2e2', '3e300'].map(Number); // [1.1, 220, 3e+300]
```






