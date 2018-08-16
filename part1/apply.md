# apply

**apply() 方法调用一个函数, 其具有一个指定的this值，以及作为一个数组（或类似数组的对象）提供的参数。**

**注意：call()方法的作用和 apply() 方法类似，只有一个区别，就是 call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组。**
***
## 语法

```
func.apply(thisArg, [argsArray])
```
### 参数

**thisArg：**
可选的。在 func 函数运行时使用的 this 值。需要注意的是，使用的 this 值并不一定是该函数执行时真正的 this 值，如果这个函数处于非严格模式下，则指定为 null 或 undefined 时会自动替换为指向全局对象（浏览器中就是window对象），同时值为原始值（数字，字符串，布尔值）的 this 会指向该原始值的包装对象。

**argsArray：**
可选的。一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 func 函数。如果该参数的值为null 或 undefined，则表示不需要传入任何参数。从ECMAScript 5 开始可以使用类数组对象。浏览器兼容性请参阅本文底部内容。

### 返回值

**调用有指定this值和参数的函数的结果。**
***
## 描述

在调用一个存在的函数时，你可以为其指定一个 this 对象。 this 指当前对象，也就是正在调用这个函数的对象。 使用 apply， 你可以只写一次这个方法然后在另一个对象中继承它，而不用在新对象中重复写该方法。

apply 与 call() 非常相似，不同之处在于提供参数的方式。apply 使用参数数组而不是一组参数列表（原文：a named set of parameters）。apply 可以使用数组字面量（array literal），如 fun.apply(this, ['eat', 'bananas'])，或数组对象， 如  fun.apply(this, new Array('eat', 'bananas'))。

你也可以使用 arguments  对象作为 argsArray 参数。 arguments 是一个函数的局部变量。 它可以被用作被调用对象的所有未指定的参数。 这样，你在使用apply函数的时候就不需要知道被调用对象的所有参数。 你可以使用arguments来把所有的参数传递给被调用对象。 被调用对象接下来就负责处理这些参数。

从 ECMAScript 第5版开始，可以使用任何种类的类数组对象，就是说只要有一个 length 属性和[0...length) 范围的整数属性。例如现在可以使用 NodeList 或一个自己定义的类似 {'length': 2, '0': 'eat', '1': 'bananas'} 形式的对象。

需要注意：Chrome 14 以及 Internet Explorer 9 仍然不接受类数组对象。如果传入类数组对象，它们会抛出异常。

***
## 式例

**调用函数，传递参数**

```
//定义一个add 方法
    function add(x, y) {
        return x + y;
    }

    //用call 来调用 add 方法
    function myAddCall(x, y) {
        //调用 add 方法 的 call 方法
        return add.call(this, x, y);
    }

    //apply 来调用 add 方法
    function myAddApply(x, y) {
        //调用 add 方法 的 applly 方法
        return add.apply(this, [x, y]);
    }

    console.log(myAddCall(10, 20));    //输出结果30
  
    console.log(myAddApply(20, 20));  //输出结果40
```
我们看到通过方法本身的call 和 apply 执行了该函数。
***
**改变函数作用域**

```
    var name = '小白';

    var obj = {name:'小红'};

    function sayName() {
        return this.name;
    }

    console.log(sayName.call(this));    //输出小白

    console.log(sayName. call(obj));    //输入小红
```
我们改变了函数运行的作用域， 通过绑定不同的对象，函数内部 this 也不同。最终输入结果才会这样。
***
**高级用法，实现 js 继承**

```
  //父类 Person
    function Person() {
        this.sayName = function() {
            return this.name;
        }
    }

    //子类 Chinese
    function Chinese(name) {
        //借助 call 实现继承
        Person.call(this);
        this.name = name;

        this.ch = function() {
            alert('我是中国人');
        }
    }

    //子类 America
    function America(name) {
        //借助 call 实现继承
        Person.call(this);
        this.name = name;

        this.am = function() {
            alert('我是美国人');
        }
    }


    //测试
    var chinese = new Chinese('成龙');
    //调用 父类方法
    console.log(chinese.sayName());   //输出 成龙

    var america = new America('America');
    //调用 父类方法
    console.log(america.sayName());   //输出 America
```
