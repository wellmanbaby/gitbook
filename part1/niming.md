# 匿名函数的典型用例
**匿名函数的典型案例就是闭包**

## 使用匿名函数实现局部变量驻留在内存中从而实现累加

```
function box(){
    var age = 100;
    return function(){
        age++;
        return age;
    }
}
var b = box();
alert(b());//101
alert(b());//102
b=null;//解除引用，等待垃圾回收
alert(b());//undefind
```
