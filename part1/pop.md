# 改变自身值得方法之一pop()

**pop()方法从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。**
***
## JavaScript Demo: Array.pop()

```
var plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop());
// expected output: "tomato"

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]

plants.pop();

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage"]
```
***
## 语法

```
arr.pop()
```

### 返回值

**从数组中删除的元素(当数组为空时返回undefined)。**
***
## 描述
**pop** 方法从一个数组中删除并返回最后一个元素，有点儿出栈的意思，最后一个元素推出数组。

**pop** 方法有意具有通用性。该方法和 **call()** 或 **apply()** 一起使用时，可应用在类似数组的对象上。**pop**方法根据 **length**属性来确定最后一个元素的位置。如果不包含**length**属性或**length**属性不能被转成一个数值，会将**length**置为0，并返回**undefined**。

如果你在一个空数组上调用 **pop()**，它返回  **undefined**。
***
## 式例

**例子: 删除掉数组的最后一个元素**

下面的代码首先创建了一个拥有四个元素的数组myFish，然后删除掉它的最后一个元素。

```
let myFish = ["angel", "clown", "mandarin", "surgeon"];

let popped = myFish.pop();

console.log(myFish); 
// ["angel", "clown", "mandarin"]

console.log(popped); 
// surgeon
```
