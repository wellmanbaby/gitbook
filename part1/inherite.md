# 继承的多种方式和优缺点
## 原型链继承

```
function SuperType() {
            this.property = true;
        }

        SuperType.prototype.getSuperValue = function() {
            return this.property;
        }

        function SubType() {
            this.subproperty = false;
        }

        SubType.prototype = new SuperType();  //继承
        SubType.prototype.getSubValue = function() {
            return this.subproperty;
        };

        var instance = new SubType();
        console.log(instance.getSuperValue()); // true
```
SubType继承了SuperType，是通过创建这个SuperType的实例，并将该实例赋值给SubType.property实现的，实现的本质是重写原型对象，代之以一个新类型的实例。

### 原型链继承的缺点
1. 引用类型的属性被所有实例共享，举个例子：

```
function SuperType() {
            this.colors = ["red", "blue", "green"];
        }
        function SubType() {
            
        }
        SubType.prototype = new SuperType();

        var instance1 = new SubType();

        var instance2 = new SubType();
        console.log(instance1.colors === instance2.colors);  //true
```
2. 在创建 Child 的实例时，不能向Parent传参

**实践中很少会单独使用原型链**

## 借用构造函数
利用call方法和构造函数实现继承
```
function SuperType() {
            this.colors = ["red", "blue", "green"];
        }

        function SubType() {
            //继承
            SuperType.call(this);
        }

        var instance1 = new SubType();
        var instance2 = new SubType();
        console.log(instance1.colors === instance2.colors); //false
        console.log(instance1 instanceof SubType);  //true
        console.log(instance1 instanceof SuperType);  //false
```
实现方式：通过在子类型构造函数的内部调父类型构造函数来实现继承
### 优点
1. 避免了引用类型的属性被所有实例共享

2. 可以在 Child 中向 Parent 传参

```
function SuperType(name) {
            this.name = name;
        }

        function SubType() {
            //继承了 SuperType，同时还传递了参数 
            SuperType.call(this, "Nicholas");
            //实例属性 
            this.age = 29;
        }
        var instance = new SubType();
        console.log(instance.name); //"Nicholas";
        console.log(instance.age); //29
```
### 缺点
方法都在构造函数中定义，每次创建实例都会创建一遍方法。

```
function SuperType(name) {
            this.name = name;
            this.sayName = function () {
                console.log(this.name);

            };
        }

        function SubType() {
            //继承了 SuperType，同时还传递了参数 
            SuperType.call(this, "Nicholas");
            //实例属性 
            this.age = 29;
        }
        var instance1 = new SubType();
        var instance2 = new SubType();
        console.log(instance1.sayName === instance2.sayName);  //false
```
## 组合继承

```
function SuperType(name) {
            this.name = name;
            this.colors = ["red", "blue", "green"];
        }

        SuperType.prototype.sayName = function () {
            console.log(this.name);
        }
        function SubType(name, age) {
            //继承属性
            SuperType.call(this, name);
            this.age = age
        }
        //继承方法
        SubType.prototype = new SuperType();
        SubType.prototype.constructor = SubType;
        SubType.prototype.sayAge = function() {
            console.log(this.age);
        };

        var instance1 = new SubType("Nicholas", 29);
        instance1.colors.push("black");
        console.log(instance1.colors);
        instance1.sayAge();
        instance1.sayName();
        
        var instance2 = new SubType("Greg", 27);
        console.log(instance2.colors);
        instance2.sayName();
        instance2.sayAge();
```
实现方式: 通过借用构造函数模式来继承属性，通过原型链模式来继承方法

优点：融合原型链继承和构造函数的优点，是 JavaScript 中最常用的继承模式。
## 原型式继承

```
function object(o) {
            function F() {}
            F.prototype = o;
            return new F();
        }        

        var person = {
            name: "Nicholas",
            friends: ["Shelby", "Court", "Van"]
        };

        var anotherPerson = object(person);
        var yetAnotherPerson = object(person)
        console.log(anotherPerson.friends === yetAnotherPerson.friends);
```
实现方式:即创建一个用于封装继承过程的函数，在函数内部将传入的对象作为创建的对象的原型(就是 ES5 Object.create 的模拟实现)。

缺点：包含引用类型的属性值始终都会共享相应的值，这点跟原型链继承一样。
## 寄生式继承

```
function object(o) {
            function F() {}
            F.prototype = o;
            return new F();
        }

        function createAnother(original) {
            var clone = object(original); //通过调用函数创建一个新独享
            clone.sayHi = function () {  //以某种方式来增强这个对象
                console.log("hi");

            };
            return clone;  //返回这个对象
        }

        var person = {
            name: "Nicholas",
            friends: ["red", "Court", "van"]
        };

        var anotherPerson = createAnother(person);
        var yetanotherPerson = createAnother(person);
        console.log(anotherPerson.sayHi === yetanotherPerson.sayHi);  //false
```
优点：在原型式继承的基础上，增强了对象

缺点：跟借用构造函数模式一样，每次创建对象都会创建一遍方法。
## 寄生组合式继承
再来看下组合继承的例子：

```
function SuperType(name) {
            this.name = name;
            this.colors = ["red", "blue", "green"];
        }
        SuperType.prototype.sayName = function () {
            alert(this.name);
        };

        function SubType(name, age) {
            SuperType.call(this, name); //第二次调用 SuperType()
            this.age = age;
        }
        SubType.prototype = new SuperType(); //第一次调用 SuperType()
        SubType.prototype.constructor = SubType;
        SubType.prototype.sayAge = function () {
            alert(this.age);
        };
```
**组合继承最大的缺点是会调用两次父构造函数**。在第一次调用 SuperType 构造函数时，SubType.prototype 会得到两个属性： name 和 colors ；它们都是 SuperType 的实例属性，只不过现在位于 SubType 的原型中。当调用 SubType 构造函数时，又会调用一次 SuperType 构造函数，这一次又在新对象上创建了实例属性 name 和 colors 。于是，这两个属性就屏蔽了原型中的两个同名属性。

使用寄生组合式继承可以解决这个问题，如下：

```
function object(o) {
            function F() {}
            F.prototype = o;
            return new F();
        }

        function inheritPrototype(subType, superType) {
            var prototype = object(superType.prototype);  //创建对象
            prototype.constructor = subType;  //增强对象
            subType.prototype = prototype;  //指定对象
        }

        function SuperType(name) {
            this.name = name;
            this.colors = ["red", "blue", "green"];
        }
        SuperType.prototype.sayName = function() {
            console.log(this.name);
        };

        function SubType(name, age) {
            SuperType.call(this, name);
            this.age = age;
        }
        inheritPrototype(SubType, SuperType);  //解决组合继承缺点
        SubType.prototype.sayAge = function() {
            console.log(this.age);
        };
```
