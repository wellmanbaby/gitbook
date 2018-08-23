# 圣杯布局

**一种经典的CSS布局模式**
## 圣杯的由来
**圣杯布局是讨论「三栏液态布局」的实现，它最早出自于谁或许不得而查了，但最早的完美实现是来自于 Matthew Levine 于2006年在「A LIST APART」上写的一篇文章，它主要讲述了网页中关于最佳圣杯的实现方法。**

**所谓液态布局是相对固态布局而言的，固态布局就是固定值不变的布局，液态就好比在容器里到了一杯水，它可以随着容器宽度的变化而自适应宽度。**

## 实现方式

### 建立框架
先写 header, footer 和 container 三个 div

```
<div id="header">#header</div>

<div id="container"></div>

<div id="footer">#footer</div>
```
我们将 container 的内边距设置为左右两边各自的宽度。它看起来就像这样：

![image](https://alistapart.com/d/holygrail/diagram_01.gif)

### 加入三栏
此时我们有了基本框架，可以把三栏塞进去了。

```
<div id="header">#header</div>

<div id="container">
  <div id="center" class="column">#center</div>
  <div id="left" class="column">#left</div>
  <div id="right" class="column">#right</div>
</div>

<div id="footer">#footer</div>
```

接着我们给每一栏配上合适的宽度，并将它们设为浮动。同时我们需要清除 footer 的上下环境，以免遭跟上面三栏一起浮动。

```
#container .column {
  float: left;
}
#center {
  width: 100%;
}
#left {
  width: 200px;  /* LC width */
}
#right {
  width: 150px;  /* RC width */
}
#footer {
  clear: both;
}
```
注意这里中间一栏的 100% 宽是基于它的父容器 container 的宽度而言的，由于 container 设置了内边距，因此中间栏看起来就处在了网页的中间，但左右两栏由于排在中间栏的后面，且因为空间不够被挤到了中间栏的下面，如下图所示：

![image](https://alistapart.com/d/holygrail/diagram_02.gif)
### 把左侧栏放上去
中间栏已经就位，剩下的事情就是把左右两栏放上去了，接下来我们先放左侧栏。

为了详述过程，这里将分为两个小步骤。首先，我们先将它的外边距设置为 -100%，这样一来，由于浮动的关系，左侧栏就能上位，与中间栏交叠在一起，并占据了左边。而右侧栏由于左侧栏的上位，自动向前浮动到了原来左侧栏的位置。

![image](https://alistapart.com/d/holygrail/diagram_03.gif)

接着我们要用到相对定位属性（relative），并设置一个与左侧栏等宽的偏移量：

```
#container .columns {
  float: left;
  position: relative;
}
#left {
  width: 200px;        /* LC width */
  margin-left: -100%;  
  right: 200px;        /* LC width */
}
```
可以看到，它设置的 right 属性就是相对于 container 的右边线向左偏移 200px，如此一来，它就完美地跑到了 container 左内边距的位置，也就是我们希望它呆的地方，如下图所示：
![image](https://alistapart.com/d/holygrail/diagram_04.gif)

### 把右侧栏放上去

最后，我们需要把右侧栏放上去，此时只需利用上面的原理把他放到 container 的右外边距的位置即可，我们需要再一次设置一个负外边距的值，它等于右侧栏的宽度：

```
#right {
  width: 150px;          /* RC width */
  margin-right: -150px;  /* RC width */
}
```
至此，所有的栏目都就位了~
![image](https://alistapart.com/d/holygrail/diagram_05.gif)