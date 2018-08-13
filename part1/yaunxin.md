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