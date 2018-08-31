# this
## this的指向问题

### 全局作用域和普通函数
全局作用域和普通函数中this指向全局对象window

```
console.log(this);//window

function bar() {
    console.log(this);//window
}
bar()
```
声明函数赋值给变量

```
var bar = function(){
    console.log(this);
}
bar();//window
```
自执行函数

```
(function(){
console.log(this)
});
();//window
```
### 在构造函数或者构造函数原型对象中this指向构造函数的实例
#### 不使用new

```
function Person(name){
    this.name = name;
    console.log(this);//window
}
Person('papa');
```
#### 使用new

```
function Person(name){
    this.name = name;
    console.log(this)//Person
    self = this;
}
var people = new Person('papa');
console.log(self === people);//true
```
####  prototype 属性

```

function Foo(){
    this.x = 10;
}
Foo.prototype.getX = function () {
    console.log(this);        //Foo {x: 10, getX: function}
    console.log(this.x);      //10
}
var foo = new Foo();

foo.getX();
```
在 Foo.prototype.getX 函数中，this 指向的 foo 对象。不仅仅如此，即便是在整个原型链中，this 代表的也是当前对象的值。

### 方法调用中，谁调用指向谁
#### 对象方法调用

```
var Person = {
    run:function(){
        console.log(this);
    }
}
Person.run()//Person
```
#### 事件监听

```
var btn =document.querySelector("button");
btn.addEventListener('click',function(){
    console.log(this);//btn
})
```
#### 事件绑定

```
var btn =document.querySelector("button");
btn.onclick = function(){
    console.log(this);//btn
}
```
### 函数用 call、apply或者 bind 调用

```

var obj = {
    x: 10
}
function foo(){
    console.log(this);     //{x: 10}
    console.log(this.x);   //10
}
foo.call(obj);
foo.apply(obj);
foo.bind(obj)();
```
当一个函数被 call、apply 或者 bind 调用时，this 的值就取传入的对象的值。
### 箭头函数中的 this
当使用箭头函数的时候，情况就有所不同了：箭头函数内部的 this 是词法作用域，由上下文确定。

```
var obj = {
    x: 10,
    foo: function() {
        var fn = () => {
            return () => {
                return () => {
                    console.log(this);      //Object {x: 10}
                    console.log(this.x);    //10
                }
            }
        }
        fn()()();
    }
}

```
现在，箭头函数完全修复了 this 的指向，this 总是指向词法作用域，也就是外层调用者 obj。

如果使用箭头函数，以前的这种 hack 写法：
```
var self = this;
```
就不再需要了

```

var obj = {
    x: 10,
    foo: function() {
        var fn = () => {
            return () => {
                return () => {
                    console.log(this);    // Object {x: 10}
                    console.log(this.x);  //10
                }
            }
        }
        fn.bind({x: 14})()()();
        fn.call({x: 14})()();
    }
}

```
由于 this 在箭头函数中已经按照词法作用域绑定了，所以，用 call()或者 apply()调用箭头函数时，无法对 this 进行绑定，即传入的第一个参数被忽略。

## 如何改变this的值
### new关键字改变this指向

```
//构造函数版this
function Fn(){
    this.user = "追梦子";
}
var a = new Fn();
console.log(a.user); //追梦子
```
用变量a创建了一个Fn的实例（相当于复制了一份Fn到对象a里面），此时仅仅只是创建，并没有执行，而调用这个函数Fn的是对象a，那么this指向的自然是对象a，那么为什么对象a中会有user，因为你已经复制了一份Fn函数到对象a中，用了new关键字就等同于复制了一份
###  call（）     fun.call(this的值,参数列表）

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user); //追梦子
    }
}
var b = a.fn;
b.call(a);  //若不用call，则b()执行后this指的是Window对象
```
把b添加到第一个参数的环境中，简单来说，this就会指向那个对象。

### apply（）          fun.apply(this的值,参数数组）

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user); //追梦子
    }
}
var b = a.fn;
b.apply(a);
```
### bind（）          fun.bind(this的值,参数列表）
bind方法和call、apply方法有些不同，如下：

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user);
    }
}
var b = a.fn;
b.bind(a);  //代码没有被打印
```
我们发现代码没有被打印，对，这就是bind和call、apply方法的不同，实际上bind方法返回的是一个修改过后的函数供后续调用。

```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user);
    }
}
var b = a.fn;
var c = b.bind(a);
console.log(c); //function() { [native code] }
```
函数c看看，能不能打印出对象a里面的user


```
var a = {
    user:"追梦子",
    fn:function(){
        console.log(this.user); //追梦子
    }
}
var b = a.fn;
var c = b.bind(a);
c();
```
同样bind也可以有多个参数，并且参数可以执行的时候再次添加，但是要注意的是，后续调用新函数时的实参要往已有参数的后面排，参数是按照形参的顺序进行的。

```
var a = {
    user:"追梦子",
    fn:function(e,d,f){
        console.log(this.user); //追梦子
        console.log(e,d,f); //10 1 2
    }
}
var b = a.fn;
var c = b.bind(a,10);
c(1,2);
```

总结： call和apply都是改变上下文中的this并立即执行这个函数，bind方法可以让对应的函数想什么时候调就什么时候调用，并且可以将参数在执行的时候添加，这是它们的区别


