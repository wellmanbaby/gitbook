# Array

****

## 数组属性


**length:数组的实例属性，设置或者返回数组元素的个数**

**prototype:数组的原型，允许你向数组添加属性和方法**

***
## 聊聊有趣地length实例属性

**描述：length属性的值是一个0到2^32-1 的整数**


```
var namelistA = new Array(4294967296); // 2的32次方 = 4294967296 
var namelistC = new Array(-100) // 负号

console.log(namelistA.length); // RangeError: 无效数组长度 
console.log(namelistC.length); // RangeError: 无效数组长度 



var namelistB = []; 
namelistB.length = Math.pow(2,32)-1; //set array length less than 2 to the 32nd power 
console.log(namelistB.length); 

// 4294967295
```

**你可以设置 length 属性的值来截断任何数组。当通过改变length属性值来扩展数组时，实际元素的数目将会增加。例如：将一个拥有 2 个元素的数组的 length 属性值设为 3 时，那么这个数组将会包含3个元素，并且，第三个元素的值将会是 undefined 。**


```
var arr = [1, 2, 3];
printEntries(arr);

arr.length = 5; // set array length to 5 while currently 3.
printEntries(arr);

function printEntries(arr) {
  var goNext = true;
  var entries = arr.entries();
  while (goNext) {
    var result = entries.next();
    if (result.done !== true) {
      console.log(result.value[1]);
      goNext = true;
    } else
      goNext = false;
  }
  console.log('=== printed ===');
}

// 1
// 2
// 3
// === printed ===
// 1
// 2
// 3
// undefined
// undefined
// === printed ===
```
**入门小白看这个可能比较吃力，跟我一样，关键是printEntries函数！**

**entries()方法返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对**

```
var array1 = ['a', 'b', 'c'];

var iterator1 = array1.entries();

console.log(iterator1.next().value);
// expected output: Array [0, "a"]

console.log(iterator1.next().value);
// expected output: Array [1, "b"]
```
**实际上arr.entries()返回一个新的 Array 迭代器对象：Array Iterator，它的原型（__proto__:Array Iterator）上有一个next方法，可用用于遍历迭代器取得原数组的[key,value]。**

## entries()方法拓展介绍

**Array Iterator**
```
var arr = ["a", "b", "c"];
var iterator = arr.entries();
console.log(iterator);

/*Array Iterator {}
         __proto__:Array Iterator
         next:ƒ next()
         Symbol(Symbol.toStringTag):"Array Iterator"
         __proto__:Object
*/
```
**iterator.next()**

```
var arr = ["a", "b", "c"]; 
var iterator = arr.entries();
console.log(iterator.next());

/*{value: Array(2), done: false}
          done:false
          value:(2) [0, "a"]
           __proto__: Object
*/
// iterator.next()返回一个对象，对于有元素的数组，
// 是next{ value: Array(2), done: false }；
// next.done 用于指示迭代器是否完成：在每次迭代时进行更新而且都是false，
// 直到迭代器结束done才是true。
// next.value是一个["key":"value"]的数组，是返回的迭代器中的元素值。
```
**iterator.next方法进行数组遍历**

```
var arr = ["a", "b", "c"];
var iter = arr.entries();
var a = [];

// for(var i=0; i< arr.length; i++){   // 实际使用的是这个 
for(var i=0; i< arr.length+1; i++){    // 注意，是length+1，比数组的长度大
    var tem = iter.next();             // 每次迭代时更新next
    console.log(tem.done);             // 这里可以看到更新后的done都是false
    if(tem.done !== true){             // 遍历迭代器结束done才是true
        console.log(tem.value);
        a[i]=tem.value;
    }
}
    
console.log(a);   
```
**二维数组按行排序**

```
function sortArr(arr) {
    var goNext = true;
    var entries = arr.entries();
    while (goNext) {
        var result = entries.next();//next()每次只处理一次，返回一个value:(2) [0, [1,34]]
        if (result.done !== true) {
            result.value[1].sort((a, b) => a - b);//以a-b的结果做返回值判断，利用升降序排序
            goNext = true;
        } else {
            goNext = false;
        }
    }
    return arr;
}

var arr = [[1,34],[456,2,3,44,234],[4567,1,4,5,6],[34,78,23,1]];
sortArr(arr);

/*(4) [Array(2), Array(5), Array(5), Array(4)]
    0:(2) [1, 34]
    1:(5) [2, 3, 44, 234, 456]
    2:(5) [1, 4, 5, 6, 4567]
    3:(4) [1, 23, 34, 78]
    length:4
    __proto__:Array(0)
*/
```
**使用for…of 循环**
```
var arr = ["a", "b", "c"];
var iterator = arr.entries();
// undefined

for (let e of iterator) {
    console.log(e);
}

// [0, "a"] 
// [1, "b"] 
// [2, "c"]
```
## 回到length功能示例

**最简单的遍历数组**


```
下面的例子中，通过数组下标遍历数组元素，并把每个元素的值修改为原值的2倍。
var numbers = [1, 2, 3, 4, 5];
var length = numbers.length;
for (var i = 0; i < length; i++) {
  numbers[i] *= 2;
}
// 遍历后的结果 [2, 4, 6, 8, 10]
```
**截断数组**


```
下面的例子中，如果数组长度大于 3，则把该数组的长度截断为 3 。

var numbers = [1, 2, 3, 4, 5];

if (numbers.length > 3) {
  numbers.length = 3;
}

console.log(numbers); // [1, 2, 3]
console.log(numbers.length); // 3
```

## 数组方法
## prototype就没这么简单喽！

**Array.prototype  属性表示 Array 构造函数的原型，并允许您向所有Array对象添加新的属性和方法。**

```
/*
如果JavaScript本身不提供 first() 方法，
添加一个返回数组的第一个元素的新方法。
*/ 

if(!Array.prototype.first) {
    Array.prototype.first = function() {
        console.log(`如果JavaScript本身不提供 first() 方法，
添加一个返回数组的第一个元素的新方法。`);
        return this[0];
    }
}
```
**鲜为人知的事实：Array.prototype 本身也是一个 Array。**

```
Array.isArray(Array.prototype); 
// true
```
***
## 数组方法

**会改变自身的方法**

**Array.prototype.copyWithin()** 

**在数组内部，将一段元素序列拷贝到另一段元素序列上，覆盖原有的值。**

**Array.prototype.fill()**

**将数组中指定区间的所有元素的值，都替换成某个固定的值。**

**Array.prototype.pop()**

**删除数组的最后一个元素，并返回这个元素。**

**Array.prototype.push()**

**在数组的末尾增加一个或多个元素，并返回数组的新长度。**

**Array.prototype.reverse()**

**颠倒数组中元素的排列顺序，即原先的第一个变为最后一个，原先的最后一个变为第一个。**

**Array.prototype.shift()**

**删除数组的第一个元素，并返回这个元素。**

**Array.prototype.sort()**

**对数组元素进行排序，并返回当前数组。**

**Array.prototype.splice()**

**在任意的位置给数组添加或删除任意个元素。**

**Array.prototype.unshift()**

**在数组的开头增加一个或多个元素，并返回数组的新长度。**
***