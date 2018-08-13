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
        console.log("吃屎");
    };
}
```
### 调用系统的构造函数
``` 
var per2 = new Object();
per2.name = "西门庆";
per2.age = 30;
per2.eat = function(){
    console.log("吃金瓶梅子");
};
per2.play = function(){
    console.log("玩潘金莲");
}
```
### 自定义构造函数
```
function Person(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.play = function(){
        console.log("玩潘金莲");
    }
}
var per = new Person("小明",18,"男")
console.log(per instanceof Person)//true
```