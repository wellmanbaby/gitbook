# 创建对象的三种方式
  1. 字面量的方式（实例对象）
  2. 调用系统的构造函数
  3. 自定义构造函数方式
  

### 字面量的方式（实例对象）
``` 
var per1 = {
    name:"小明",
    age:"20",
    sex:"男“,
    eat:function(){
        console.log("吃水煮鱼");
    };
}
```
### 调用系统的构造函数
``` 
var per2 = new Object();
per2.name = "西门庆";
per2.age = 30;
per2.eat = function(){
    console.log("吃金瓶梅");
};
per2.play = function(){
    console.log("玩金莲");
}
```
### 自定义构造函数
```
function Person(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.play = function(){
        console.log("玩命");
    }
}
var per = new Person("小明",18,"男")
console.log(per instanceof Person)//true
```
# 自定义构造函数和工厂模式对比

### 自定义构造函数创建对象做的事情
```
function Person(name,age){
    this.name = name;
    this.age = age;
    this.sayHi = function(){
        console.log("您好");
    };
}
//创建对象 --->实例化一个对象的同时对属性进行初始化
var per = new Person("小红",20);
1. 开辟空间，存储对象
2. 把this设置为当前的对象
3. 设置属性和方法的值
4. 把this对象返回
```
### 工厂模式创建对象
```
function createObject(name,age){
//原料
    var obj = new Object();
//加工
    obj.name = name;
    obj.age = age;
    obj.sayHi = function(){
        console.log("您好");
    }
    return obj;
}
//出厂
var per1 = createObject("小明",20);
```
## 工厂模式和自定义构造函数的区别
### 工厂模式          --------------------------------- 自定义构造函数
1. 函数名是小写 ------------------------------------1. 函数名是大写（首字母）
2. 有new -------------------------------------- -----2. 没有new
3. 有返回值-----------------------------------------3. 没有返回值
4. new之后的对象是当前对象----------------------4. this是当前对象
5. 直接调用函数就可以创建对象-------------------5. 通过new的方式来创建对象

# 构造函数和实例对象以及原型对象之间的关系
```
var arr = new Array(10,20,30,40)//通过构造函数实例化对象并初始化
arr.join()//join是方法，实例对象调用的方法
console.dir(arr),//join方法在实例对象_proto_原型中
console.log(arr._proto == Array.prototype),//true
```
1. 构造函数可以实例化对象
2. 构造函数中有一个属性叫prototype，是构造函数的原型对象
3. 构造函数的原型对象（prototype）中有一个constructor构造器，这个构造器指向的就是自己所在的自己所在的原型对象所在的构造函数
4. 实例对象的原型对象（_proto_）指向的是该构造函数的原型对象
5. 构造函数的原型对象（prototype）中的方法是可以被实例对象直接访问的

# 原型的简单语法

```
function Student(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Student.prototype = {
    height: "188",//不必Student.prototype.height="188"
    weight: "55kg",
    study:function(){
        console.log("学习");
    }
}
var stu = new Student("段飞"，20，“男”)；
stu.study();

```
# 进一步研究构造函数和实例对象之间的关系

```
function Student(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    study:function(){
        console.log("学习");
    }；
}
//构造函数实例化对象
var stu = new Student("段飞"，20，“男”)；
//实例对象是通过构造函数来创建
stu.study();
console.log(per instanceof Person);//true
console.log(per.constructor == Person);//true
console.dir(per);//实例
console.dir(Person);//构造函数
console.log(per._proto_.constructor == Person.prototype.constructor);//true
console.log(per._proto_constructor == Person.prototype.constructor);//true
```
## 总结
### 实例对象和构造函数之间的关系：
1. 实例对象是通过构造函数来创建的  --->创建的过程叫实例化
2. 如何判断这个对象是不是这个数据类型？
    1. 通过构造器的方式 实例对象.构造器 == 构造函数的名字
    2. 对象instanceof构造函数名字（尽量用此方）

# 构造函数创建带来的问题 --引出原型的作用
```
function Person(name,age){
    this.name = name;
    this.age = age;
    eat:function(){
        console.log("吃屎");
    }；
}
var per1 = new Person("小白", 20);
var per2 = new Person("小黑", 30);

per1.eat();//不是同一个方法，很浪费空间跟内存
per2.eat();//引出原型的作用之一，数据共享，节省内存空间
console,log(per1.eat == per2.eat);//false

//原型
function Person(name,age){
    this.name = name;
    this.age = age
}//通过原型添加方法，解决数据共享，节省内存空间
Person.prototype.eat:function(){
        console.log("吃屎");
    }；
var per1 = new Person("小白", 20);
var per2 = new Person("小黑", 30);
per1.eat();
per2.eat();
console,log(per1.eat == per2.eat);//true
```

# 体会面向过程和面向对象的编程思想

```
//构造函数
function Person(sex,age){
    this.sex = sex;
    this.age = age
}
//通过原型添加方法
Person.prototype.eat:function(){
        console.log("吃屎");
    }；
var per = new Person("男",20);
console.dir(per);//实例对象
console.dir(Person);//构造函数的名字
```
1. 实例对象中有两个属性(sex,age)，另外还有_proto_这个属性，
2. 构造函数中并没有sex和age这两个属性
3. 实例对象中的属性_proto_也是一个对象，叫原型，不是标准属性，用于浏览器识别；
4. 构造函数中有一个属性prototype，也是一个对象，叫原型，是标准属性，程序员使用；
5. console.log(per._proto_.constructor ==Person.prototype.constructor);//true
6. 原型------------>_proto_或者prototype都是原型对象；
7. 原型的作用，var per2 = new Person("发"，30);console.log(per.eat == per2.eat)//true,即原型的作用为共享数据，节省内存空间；

