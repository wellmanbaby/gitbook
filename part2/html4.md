# 认识date-

*在HTML5中添加了data-的方式来自定义属性，所谓data-实际上就是data-前缀加上自定义的属性名，使用这样的结构可以进行数据存放。使用data-*可以解决自定义属性混乱无管理的现状。**

*以前，需要存储含有特定含义的信息通常是通过 class 完成的，但这并不是 class 本来的用途。现在，利用 HTML 5，可以为元素添加data-&属性，从而存储自定义信息。其中&是可以自定义的部分*

*举例：*

```
<article id="tu" data-category="Web Development" data-author="1"> ... </article>
```
## 通过JavaScript访问

通过 JavaScript 访问自定义的信息有两种方式：**getAttribute()** 和**dataset。**

### getAttribute 方法

这就是经典的取得一个元素属性的方式，和以前一样。

```
document.getElementById('tu').getAttribute('data-category'); // "Web Development"
```
### dataset 方法

这是 HTML 5 新增的方法，可以更方便的读取所有的 data 信息。

```
var article = document.getElementById('tu');
var data = article.dataset;
alert(data.category); // "Web Development"
alert(data.author); // 1
```
***
## 通过CSS访问

### 使用attr

```
article::before {
    content: attr(data-category);
}
```
### 使用属性选择器

```
article[data-author='1'] {
    border-width: 1px;
}
```

