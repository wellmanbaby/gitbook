# 复习一下浮动

**开门见山：浮动就是使元素脱离文档流，按照一定的方式排列，遇到相邻的浮动元素或者父级的边界停下来**

## 浮动的特性：

1. 浮动的元素排在同一排

2. 浮动的元素内容撑开宽度

3. 浮动元素支持所有css样式 

4. 浮动的元素脱离文档流

5. 浮动的元素提升层级半径（什么意思？）

## 清除浮动的方式：

**首先什么是清浮动，所谓的清浮动就是解决元素脱离文档流的问题**

### 子级浮动，父级也浮动

这个方法弊端比较大，因为页面嵌套会比较深，而且margin： 0 auto会失效

### 给父级加display：inline-block

这个方法margin： 0 auto也会失效，不过给父级加text-align：center应该可以解决问题

### 给父级加高

这就是一个权宜之策，扩展性太差了，一旦子级增加了，那不得不停地改高呀

### 在子级中用br标签

<br/>标签的作用本来是换行，在子级里加<br clear ="all"/>达到清除浮动的效果

### 在子级中使用clear：both

```
<div id="box1">
  <span class="class1"></span>
  <span class="class2"></span>
  <span class="class3"></span>
  <span class="class4"></span>
  <span class="cla1"></span>
</div>

<style>
.cla1{clear：both}
</style>
```
第4第5种方法不符合w3c规范中结构、行为、样式三者分离原则

### 伪类清标签
**该种为淘宝主流清浮动方法**

```
:after{content:" ";display:block;clear:both}
```
具体实施：

```
<div id="box1">
  <span class="class1"><span>
  <span class="class2"><span>
  
</div>

<style>
  #box1:after{content:" ";display：block;clear:both}
</style>
```
## 提升层级半径

**其实这个不难理解，一个块级标签元素是由属性和内容构成的。**

**不过，当两个本来是各占一排的块级标签浮动时，会脱离文档流，上面的div标签不能占位子了，下面的div标签的属性会顶替原来的div标签属性，但内容并没有跟上。**

### 利用提升层级来实现文字环绕效果

```
<body>
    <div class="box1"></div>
    <div class="box2">你你你你你你你你你你你你您你你你你你你你你你你你您你你你你你您你你你你您您你你你你你年</div>
</body>

<style>
      .box1{
          width: 100px;
          height: 100px;
          background: red;
          float: left;
      }
      .box2{
          width: 200px;
          height: 210px;
          background: yellow;
      }
</style>
```

