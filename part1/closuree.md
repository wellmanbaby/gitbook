# 闭包

**简单的说，闭包最原始的状态就是匿名函数，原始闭包就是可以访问函数作用域里变量的匿名函数，这里引出了闭包的最基本作用：访问函数作用域里的变量。**

**闭包是指有权访问另一个函数作用域中的变量的函数，创建闭包的常用方式，就是在一个函数内部创建另一个函数，通过另一个函数访问这个函数的局部变量**

## 典型闭包

```
function box(){
    return function(){
        return 'Lee';
    }
}
alert(box()())
```
**闭包随着进一步的发展实现了新的作用：设计私有方法和变量。**

**使用闭包有一个优点同时也是他的缺点，就是会使变量驻留在内存，同时也避免了全局变量的污染。**

## 全局污染

全局变量污染导致应用程序不可预测性，每个模块都可以调用的变量，必将引来诸多后果，因此，最佳的是使用私有的、封装的局部变量。


```
function a(){
	var i=0;
	function b(){
		console.log(i++)
	}
	return b;
}
var c=a();//这里执行了函数a，返回函数b，因此c为函数b
c();//0，这里调用了函数b

```
## 案例

### 在循环中直接找到对应元素的索引

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title></title>
    <script type="text/javascript" charset="UTF-8">
        window.onload = function () {
            var aLi = document.getElementsByTagName('li');
            for (var i = 0; i < aLi.length; i++) {
                aLi[i].onclick = function () {        //当点击时for循环已经结束
                    alert(i);
                };
            }
        }
    </script>
</head>

<body>
    <ul>
        <li>a</li>
        <li>b</li>
        <li>c</li>
        <li>d</li>
    </ul>
</body>

</html>
```
执行以上代码发现点击任何一个返回的都是4，这是因为赋值的时候，传的i是对内存地址的引用，循环结束，i指向的就是4.

使用闭包改写上面的代码。

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title>闭包</title>
    <script type="text/javascript" charset="UTF-8">
        window.onload = function () {
            var aLi = document.getElementsByTagName('li');
            for (var i = 0; i < aLi.length; i++) {
                (function (i) {
                    aLi[i].onclick = function () {
                        alert(i);
                    };
                })(i);
            }
        };
    </script>
</head>

<body>
    <ul>
        <li>a</li>
        <li>b</li>
        <li>c</li>
        <li>d</li>
    </ul>
</body>

</html>
```
每一次循环的时候，都把当前的i通过立即执行函数赋值。

### 变量的累加
全局变量的累加

```
<script type="text/javascript" charset="UTF-8">
        var i = 1;
        function text() {
            i++;
            alert(i);
        }
        text();//2
        text();//3
    </script>
```
局部变量的累加

```
<script type="text/javascript" charset="UTF-8">
        function text() {
            var i = 1;
            i++;
            alert(i);
        }
        text();//2
        text();//2
    </script>
```
上述代码没有实现累加，改写代码如下：

```
<script type="text/javascript" charset="UTF-8">
        function text() {
            var i = 1;
            return function () {//函数嵌套
                i++;
                alert(i);
            }
        }
        var a = text();//外部函数赋给a
        a();//2
        a();//3
    </script>
```
### 模块化代码，减少全局变量的污染

```
<script type="text/javascript" charset="UTF-8">
        var g = (function () {
            var i = 1;
            return function () {
                i++;
                alert(i);
            }
        })();
        g();//2 调用一次g函数，其实调用的是里面内部函数的返回值
        g();//3
    </script>
```
### this对象
在闭包中使用this对象可能导致一些问题

```
<script type="text/javascript" charset="UTF-8">
        var name = "The Window";

        var object = {
            name: "My Object",

            getNameFunc: function () {
                return function () {
                    return this.name;
                };

            }

        };

        alert(object.getNameFunc()());//The Window
    </script>
```
代码先创建了一个全局变量name，又创建了一个包含name属性的对象。这个对象还包含一个getNameFunc()方法，返回一个匿名函数，匿名函数又返回一个this.name。调用object.getNameFunc()()返回一个字符串。内部函数搜索的时候只搜索到活动对象。

```
<script type="text/javascript" charset="UTF-8">
        var name = "The Window";

        var object = {
            name: "My Object",

            getNameFunc: function () {
                var that = this;
                return function () {
                    return that.name;
                };

            }

        };

        alert(object.getNameFunc()());//My Object
    </script>
```
在定义匿名函数前，把this对象赋值给that变量，闭包也可以访问这个变量。即使函数返回，仍然引用着object。
## 内存泄漏
由于IE的JavaScript对象和DOM对象使用不同的垃圾回收采集方式，因此闭包在IE中会导致一些问题，即内存泄漏问题，也就是无法销毁驻留在内存的元素。

```
function Box(){
    var oDiv = document.getElementById('oDiv');//oDiv用完后一直驻留在内存中
    oDiv.onclick = function(){
        alert(oDiv.innerHTML);//这里用oDIV导致内存泄漏
    }
};
Box()
```
那么在最后应该将oDiv解除引用来避免内存泄漏。

```
function Box(){
    var oDiv = document.getElementById('oDiv');
    var text = oDiv.innerHTML;
    oDiv.onclick = function(){
        alert(text);
    }
    oDiv = null;//解除引用
};
Box()
```
[闭包](https://segmentfault.com/a/1190000009026788)