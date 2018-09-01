# 函数的作用域是什么？js 的作用域有几种？
**我是搞不清为什么要把函数和js分开谈作用域，函数不是js里的一个对象吗？只是函数体内是一个封闭的块级作用域而已，ES5没有明确提出块级作用域，因此函数作用域才显得这么特别？**

## 函数作用域
在JavaScript中变量的作用域，并非和C、Java等编程语言似得，在变量声明的代码段之外是不可见的，我们通常称为块级作用域，然而在JavaScript中使用的是函数作用域（变量在声明它们的函数体以及这个函数体嵌套的任意函数体都是有定义的，其实ES6以后也出现了块级作用域了）

JavaScript的函数作用域是指在函数内声明的所有变量在函数体内始终是可见的，可以在整个函数的范围内使用及复用。

## js 的作用域

### ES5中的作用域

#### 全局变量

声明在函数外部的变量，在代码中任何地方都能访问到的对象拥有全局作用域（所有没有var直接赋值的变量都属于全局变量）

1. 最外层函数和在最外层函数外面定义的变量拥有全局作用域，例如：

```

var authorName="山边小溪";
function doSomething(){
    var blogName="梦想天空";
    function innerSay(){
        alert(blogName);
    }
    innerSay();
}
alert(authorName); //山边小溪
alert(blogName); //脚本错误
doSomething(); //梦想天空
innerSay() //脚本错误
```
2. 所有末定义直接赋值的变量自动声明为拥有全局作用域，例如：

```

function doSomething(){
    var authorName="山边小溪";
    blogName="梦想天空";
    alert(authorName);
}
doSomething(); //山边小溪
alert(blogName); //梦想天空
alert(authorName); //脚本错误
```
变量blogName拥有全局作用域，而authorName在函数外部无法访问到。

3. 所有window对象的属性拥有全局作用域

　一般情况下，window对象的内置属性都拥有全局作用域，例如window.name、window.location、window.top等等。
#### 局部变量
　一般情况下，window对象的内置属性都拥有全局作用域，例如window.name、window.location、window.top等等。
　
```

function doSomething(){
    var blogName="梦想天空";
    function innerSay(){
        alert(blogName);
    }
    innerSay();
}
alert(blogName); //脚本错误
innerSay(); //脚本错误
```
代码中的blogName和函数innerSay都只拥有局部作用域。
### ES6中的作用域 
**为什么需要块级作用域**

ES5只有全局作用域和函数作用域，没有块级作用域，会带来以下问题：

1. 变量提升导致内层变量可能会覆盖外层变量

```
var i = 5;  
function func() {  
    console.log(i);  
    if (true) {  
        var i = 6;  
    }  
}  
func(); // undefined
```
2. 用来计数的循环变量泄露为全局变量

```
for (var i = 0; i < 10; i++) {    
        console.log(i);    
}    
console.log(i);  // 10  
```
**块级作用域’通过新增命令let和const来体现。**
#### let
let和var差不多，都是用来声明变量的。区别就在于：

　　1、  let声明的变量只在所处于的块级有效；

　　2、  let没有‘变量提升’的特性，而是‘暂时性死区（temporal dead zone）’特性。
　　
　　
　
**1. let声明的变量只在块级有效**

```
'use strict';
function func(args){
    if(true){
        //let声明i
        let i = 6;
        //在if内打印i值
        console.log('inside: ' + i);//6
    }
    //在if外，再次打印i值
    console.log('outside: ' + i);//i is not defined
};
```
这因为let声明的变量i是属于if内的块级作用域；而不是像var一样。


**2.let没有‘变量提升’的特性，而却有‘暂时性死区（temporal dead zone）’的特性。**

```

'use strict';
function func(){
    //在let声明前，打印i
    console.log(i);//i is not defined
    let i;
};
func();
```
在let声明变量前，使用该变量，它是会报错的，而不是像var那样会‘变量提升’。其实说let没有‘变量提升’的特性，不太对。或者说它提升了，但是ES6规定了在let声明变量前不能使用该变量。

```

'use strict';
var test = 1;
function func(){
    //打印test的值
    console.log(test);//i is not defined
    let test = 2;
};
func();
```
如果let声明的变量没有变量提升，应该打印’1’（func函数外的test）；而他却报错，说明它是提升了的，只是规定了不能在其声明之前使用而已。我们称这特性叫“暂时性死区（temporal dead zone）”。且这一特性，仅对遵循‘块级作用域’的命令有效（let、const）。

**3.可以解决闭包问题**

```

'use strict';
var arr = [];
for(let i = 0; i < 2; i++){
    arr[i] = function(){
        console.log(i);
    };
};
arr[1]();//1
```
#### const
const命令与let命令一样，声明的变量，其作用域都是块级。

所以const遵循的规则与let相差无二，只是，const是用来声明恒定变量的。

且，用const声明恒定变量，声明的同时就必须赋值，否则会报错。

```
'use strict';
function func(){
    const PI;//报错，声明就得赋值
    PI = 3.14;
    console.log(PI);
};
func();
```
