# values()

**values() 方法返回一个新的 Array Iterator 对象，该对象包含数组每个索引的值**

**乍一看，妈的这不是entries()么！其实，非也非也，entries()返回的是键值对，values返回的只是键值**

**后面还会学到keys方法，它返回的是键名**


***
## JavaScript Demo: Array.values()

```
const array1 = ['a', 'b', 'c'];
const iterator = array1.values();

for (const value of iterator) {
  console.log(value); // expected output: "a" "b" "c"
}
```
***

## 语法

```
arr.values()
```
***
### 参数

无


## 式例

### 使用 for...of 循环进行迭代


```
let arr = ['w', 'y', 'k', 'o', 'p'];
let eArr = arr.values();
// 您的浏览器必须支持 for..of 循环
// 以及 let —— 将变量作用域限定在 for 循环中
for (let letter of eArr) {
  console.log(letter);
}
```


### 另一种迭代方式


```
let arr = ['w', 'y', 'k', 'o', 'p'];
let eArr = arr.values();
console.log(eArr.next().value); // w
console.log(eArr.next().value); // y
console.log(eArr.next().value); // k
console.log(eArr.next().value); // o
console.log(eArr.next().value); // p
```







