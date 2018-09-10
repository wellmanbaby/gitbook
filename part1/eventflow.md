# 事件流
**首先我们思考一个很有意思的事情：一张纸上画了两个同心圆，当我们把手指放到圆心上时，手指指向的不是一个圆，而是纸上的两个圆，同理之，当我们单击网页上的一个div块的时候（代码片段一），单击事件会仅仅作用在这个div上面吗？ 在浏览器发展到第四代时，IE和Netscape的开发团队都遇到这个问题，他们都一致认为，除了单击div块，我们也单击了body、 html、甚至是整个document，但不幸的是两个团队针对事件流模型产生了两个完全相反的概念。**

## 事件冒泡（推荐）

IE的事件流称为事件冒泡。

即：事件由最具体的元素接收(div)，逐级向上传播到不具体的节点(document)。

当我们点击代码片段一中id为box的div块时，单击事件会按照如下顺序传播：
div ——> body——> html ——> document

![image](https://image-static.segmentfault.com/160/277/1602772756-5a05abc58fb41)

如上图所示，click首先在div元素上发生，然后沿着Dom树向上传播，每一级节点都会发生直至传播到document对象。

**测试代码**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件流</title>
</head>
<style type="text/css">
    #box1{
        width: 300px;
        height: 300px;
        background-color: red;
    }
    #box2{
        width: 200px;
        height: 200px;
        background-color: yellow;
    }
    #box3{
        height: 100px;
        width: 100px;
        background-color: green;
    }
</style>
<body>
    <div id="box1">
        <div id="box2">
            <div id="box3"></div>
        </div>
    </div>
</body>
<script type="text/javascript">
    document.getElementById('box1').onclick = function () {
        console.log('box1 click')
    }
    document.getElementById('box2').onclick = function () {
        console.log('box2 click')
    }

    document.getElementById('box3').onclick = function () {
        console.log('box3 click')
    }
</script>
</html>
```
**测试效果**
![image](https://image-static.segmentfault.com/377/126/3771269734-5a05ac7e16308)

note: 几乎现代所有的浏览器都支持事件冒泡，不过有一些细微的差别

IE5.5 和 IE5.5 - 版本的事件冒泡会跳过html元素（body 直接到 document）

IE9、Firefox、Chrome、Safari则一直冒泡到window对象。
## 事件捕获
Netscape提出的事件流模型称为事件捕获。

即：事件从最不具体的节点开始接收（document），传递至最具体的节点<div>，和IE的冒泡刚好相反， 事件捕获的本意是当事件到达预定目标前捕获它。

当我们点击代码片段一中id为box的div块时，单击事件会按照如下顺序传播：

document——> html ——> body ——> div
![image](https://image-static.segmentfault.com/801/904/801904692-5a05ada634d5c)

note: 虽然事件捕获是Netscape唯一支持的事件流模型，但IE9、Firefox、Chrome、Safari目前也都支持这种事件模型，由于老版本的浏览器并不支持，所以我们应该尽量使用事件冒泡，有特殊需求的时候再考虑事件捕获。

## DOM2级事件流

为了能够兼容上述两种事件模型，又提出了一个DOM2级事件模型，它规定了事件流包含三个阶段：

1. 事件捕获阶段：为事件捕获提供机会；

2. 处于目标阶段：事件的目标接收到事件（但并不会做出响应）；

3. 事件冒泡阶段：事件响应阶段；

在DOM2级事件流中，但我们点击代码片段一中的div，在事件捕获阶段从document ->html ->body就停止了（div元素在这个阶段并不会接收到点击事件）。紧接着，事件在div上发生，并把事件真正的处理看成是冒泡阶段的一部分，然后，冒泡阶段发生，事件又回传到document。

**测试代码**

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>DOM2级事件流</title>
</head>
<style type="text/css">
    #box1{
        width: 300px;
        height: 300px;
        background-color: red;
    }
    #box2{
        width: 200px;
        height: 200px;
        background-color: yellow;
    }
    #box3{
        height: 100px;
        width: 100px;
        background-color: green;
    }
</style>
<body>
    <div id="box1">
        <div id="box2">
            <div id="box3"></div>
        </div>
    </div>
</body>
<script type="text/javascript">
    var box1 = document.getElementById('box1');
    var box2 = document.getElementById('box2');
    var box3 = document.getElementById('box3');
    // true表示在捕获阶段处理事件、false表示在冒泡阶段处理
    box1.addEventListener('click',function () {
        console.log('事件捕获阶段触发box1点击事件');
    }, true);
    box1.addEventListener('click',function () {
        console.log('事件冒泡阶段触发box1点击事件');
    }, false);
    box2.addEventListener('click',function () {
        console.log('事件捕获阶段触发box2点击事件');
    }, true);
    box2.addEventListener('click',function () {
        console.log('事件冒泡阶段触发box2点击事件');
    }, false)
    box3.addEventListener('click',function () {
        console.log('事件捕获阶段触发box3点击事件');
    }, true);
    box3.addEventListener('click',function () {
        console.log('事件冒泡阶段触发box3点击事件');
    }, false)
</script>
</html>
```
**测试结果**
![image](https://image-static.segmentfault.com/364/586/364586151-5a05b31005703)
## 事件流的典型应用——事件代理
传统的事件处理中，需要为每个元素添加事件处理器。js事件代理则是一种简单有效的技巧，通过它可以把事件处理器添加到一个父级元素上，从而避免把事件处理器添加到多个子级元素上。

事件代理的原理用到的就是事件冒泡和目标元素，把事件处理器添加到父元素，等待子元素事件冒泡，并且父元素能够通过target（IE为srcElement）判断是哪个子元素，从而做相应处理, 下面举例说明：

**代码**

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>传统的事件绑定</title>
</head>

<body>
    <ul id="color-list">
        <li>red</li>
        <li>orange</li>
        <li>yellow</li>
        <li>green</li>
        <li>blue</li>
        <li>indigo</li>
        <li>purple</li>
    </ul>
</body>
<script>
(function() {
    var colorList = document.getElementById("color-list");
    var colors = colorList.getElementsByTagName("li");
    for (var i = 0; i < colors.length; i++) {
        colors[i].addEventListener('click', showColor, false);
    };

    function showColor(e) {
        e = e || window.event;
        var targetElement = e.target || e.srcElement;
        console.log(targetElement.innerHTML);
    }
})();
</script>
</script>

</html>
```
**事件代理的处理方式**

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>传统的事件绑定</title>
</head>

<body>
    <ul id="color-list">
        <li>red</li>
        <li>orange</li>
        <li>yellow</li>
        <li>green</li>
        <li>blue</li>
        <li>indigo</li>
        <li>purple</li>
    </ul>
    <script>
    (function() {
        var colorList = document.getElementById("color-list");
        colorList.addEventListener('click', showColor, false);

        function showColor(e) {
            e = e || window.event;
            var targetElement = e.target || e.srcElement;
            if (targetElement.nodeName.toLowerCase() === "li") {
                alert(targetElement.innerHTML);
            }
        }
    })();
    </script>
</body>

</html>
```
## 使用事件代理的好处：
1. 将多个事件处理器减少到一个，因为事件处理器要驻留内存，这样就提高了性能。想象如果有一个100行的表格，对比传统的为每个单元格绑定事件处理器的方式和事件代理（即table上添加一个事件处理器），不难得出结论，事件代理确实避免了一些潜在的风险，提高了性能。

2. DOM更新无需重新绑定事件处理器，因为事件代理对不同子元素可采用不同处理方法。如果新增其他子元素（a,span,div等），直接修改事件代理的事件处理函数即可，不需要重新绑定处理器，不需要再次循环遍历。