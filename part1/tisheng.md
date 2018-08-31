# 请解释变量声明提升
在JS里定义的变量，存在于作用域链里，而在函数执行时会先把变量的声明进行提升，仅仅是把声明进行了提升，而其值的定义还在原来位置。示例如下：

```
var test = function() {
    console.log(name); // 输出：undefined
    var name = "jeri";
    console.log(name); // 输出：jeri
}

test();
```
上述代码与下述代码等价:

```
var test = function() {
    var name;
    console.log(name); // 输出：undefined
    name = "jeri";
    console.log(name); // 输出：jeri
}

test();
```
由以上代码可知，在函数执行时，把变量的声明提升到了函数顶部，而其值定义依然在原来位置。