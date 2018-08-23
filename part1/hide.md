# 用 CSS 隐藏页面元素的 5 种方法

## 1. Opacity

opacity 属性的意思是设置一个元素的透明度。它不是为改变元素的边界框（bounding box）而设计的。这意味着将 opacity 设为 0 只能从视觉上隐藏元素。而元素本身依然占据它自己的位置并对网页的布局起作用。它也将响应用户交互。

```
.hide {
  opacity: 0;
}
```
如果你打算使用 opacity 属性在读屏软件中隐藏元素，很不幸，你并不能如愿。元素和它所有的内容会被读屏软件阅读，就像网页上的其他元素那样。换句话说，元素的行为就和它们不透明时一致。

## 2. Visibility

第二个要说的属性是 visibility。将它的值设为 hidden 将隐藏我们的元素。如同 opacity 属性，被隐藏的元素依然会对我们的网页布局起作用。与 opacity 唯一不同的是它不会响应任何用户交互。此外，元素在读屏软件中也会被隐藏。

```
.hide {
   visibility: hidden;
}
```
## 3. Display

display 属性依照词义真正隐藏元素。将 display 属性设为 none 确保元素不可见并且连盒模型也不生成。使用这个属性，被隐藏的元素不占据任何空间。不仅如此，一旦 display 设为 none 任何对该元素直接打用户交互操作都不可能生效。此外，读屏软件也不会读到元素的内容。这种方式产生的效果就像元素完全不存在。

任何这个元素的子孙元素也会被同时隐藏。为这个属性添加过渡动画是无效的，它的任何不同状态值之间的切换总是会立即生效。

不过请注意，通过 DOM 依然可以访问到这个元素。因此你可以通过 DOM 来操作它，就像操作其他的元素。

```
.hide {
   display: none;
}
```

## 4. position

假设有一个元素你想要与它交互，但是你又不想让它影响你的网页布局，没有合适的属性可以处理这种情况（opacity 和 visibility 影响布局， display 不影响布局但又无法直接交互——译者注）。在这种情况下，你只能考虑将元素移出可视区域。这个办法既不会影响布局，有能让元素保持可以操作。下面是采用这种办法的 CSS：

```
.hide {
   position: absolute;
   top: -9999px;
   left: -9999px;
}
```
### 具体案例：

HTML：

```
<div>Hover!</div>
<div class="o-hide"><p>0</p></div>
<div>0</div>
```
CSS：

```
div {
  height: 60px;
  padding: 60px 0;
  width: 180px;
  font-size: 2em;
  line-height: 60px;
  background: pink;
  text-align: center;
  margin: 1%;
  display: block;
  float: left;
  cursor: pointer;
  font-family: 'Lato';
}

.o-hide {
  position: absolute;
  top: -9999px;
  left: -9999px;
}


```
JS:

```
var count = 0;
var oHide = document.querySelector(".o-hide");
var firstDiv = document.querySelector("div:nth-child(1)");

firstDiv.addEventListener("mouseover", function(){
    count++;
    oHide.innerHTML = count;
});

firstDiv.addEventListener("click", function(){
    oHide.style.position = "static";
});
```
这种方法的主要原理是通过将元素的 top 和 left 设置成足够大的负数，使它在屏幕上不可见。采用这个技术的一个好处（或者潜在的缺点）是用它隐藏的元素的内容可以被读屏软件读取。这完全可以理解，是因为你只是将元素移到可视区域外面让用户无法看到它。

## 5. Clip-path
隐藏元素的另一种方法是通过剪裁它们来实现。在以前，这可以通过 clip 属性来实现，但是这个属性被废弃了，换成一个更好的属性叫做 clip-path。Nitish Kumar 最近在 SitePoint 发表了“介绍 clicp-path 属性”这篇文章，通过阅读它可以了解这个属性的更多高级用法。

记住，clip-path 属性还没有在 IE 或者 Edge 下被完全支持。如果要在你的 clip-path 中使用外部的 SVG 文件，浏览器支持度还要更低。使用 clip-path 属性来隐藏元素的代码看起来如下：

```
.hide {
  clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);
}
```
[大牛讲解](https://75team.com/post/five-ways-to-hide-elements-in-css.html)