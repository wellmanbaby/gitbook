# 讲讲前端三毒IE6.7.8

**兼容性：页面在不同的浏览器可能会显示不同**

**IE浏览器兼容性测试神器：IE Tester**

**典型1：盒模型计算不精确导致的问题**
```
<body>
  <div id = "box">
    <div class = "left"></div>
    <div class = "right">
      <div class = "cou"></div>
    </div>
 </div>
</body>

<style>
  #box {
      width: 400px;
  }
  .left {
      width: 200px;
      background: red；
      height: 300px;
      float: left;
  }
  .cou {
      width: 180px;
      height: 180px;
      padding: 15px;
      background: blue;
  }
</style>
```
**显然180+30=210px，已经撑破了父级的宽度，在IE6下，父级的宽度会被子级修改，只要将180改为170，问题就可以解决。**

**典型2：父级元素浮动却需要子级内容撑开宽度**


```
<body>
  <div id = "box">
    <div class = "left">
      <h3>左侧</h3>
    </div>
    <div class = "right">
      <h3>右侧</h3>
    </div>
 </div>
</body>

<style>
  #box {
      width: 400px;
  }
  .left {
      background: red；
      float: left;
  }
  .right {
      float: right;
      background: blue;
  }
  h3 {
      margin: 0;
      height: 40px;
      float: left;
  }
</style>
```
**在IE6中，元素浮动，如果宽度要靠内容撑开的话，就需要给里面的block元素都添加浮动**

**典型3：著名的3px的bug**


```
//考虑一种布局设计，为实现两个同级元素并排，
//可以先将第一个设置浮动，将第二个元素的margin-left设置为第一个元素的宽度即可,
//其他浏览器下计划当然是天衣无缝，只是会在IE6.7下两个元素中间会出现3px的缝隙
<body>
  <div id = "box">
    <div class = "left"></div>
    <div class = "right"></div>
 </div>
</body>

<style>
  #box {
      width: 400px;
  }
  .left {
      width: 100px;
      background: red；
      height: 100px;
      float: left;
  }
  .right {
      width: 200px;
      height: 100px;
      margin-left: 100px;
      background: blue;
  }
</style>

```
**解决方法：在IE6.7下，元素要通过浮动排在同一排，就需要给这行元素都加浮动**

**典型4：著名的19px的bug**

```
<body>
 <div class = "box"></div>
<body>

<style>
 .box{
     height: 2px;
     background: red;
     overflow: hidden;
 }
</style>
```
**若不加overflow:hidden， IE6会把2px变成19px，即在IE6下元素的高度如何小于19px的时候，会被当成19px来处理，解决办法： overflow： hidden**

**典型5： 著名的双边距问题**

```
<body>
 <div class = "box"></div>
<body>

<style>
 body {
     margin: 0;
 }
 .box{
     width: 200px;
     height: 200px;
     background: red;
     float: left;
     margin: 100px
 }
</style>
```
**双边距问题：在IE6中，块级元素有浮动且有横向的margin值时，横向的margin的值会扩大两倍**

**解决办法：可以用span等内联标签代替块级标签，或者将块级标签中display设置为inline**