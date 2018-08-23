# 实现水平居中和垂直居中

## 行内元素的水平居中 

要实现行内元素（<span>、<a>等）的水平居中，只需把行内元素包裹在块级父层元素（<div>、<li>、<p>等）中，并且在父层元素CSS设置如下：

```
#container{
    text-align:center;
}
```
并且适用于文字，链接，及其inline或者inline-block、inline-table和inline-flex。

## 块状元素的水平居中    
要实现块状元素（display:block）的水平居中，我们只需要将它的左右外边距margin-left和margin-right设置为auto，即可实现块状元素的居中，要水平居中的块状元素CSS设置如下：

```
#center{
    margin:0 auto;
}
```
## 多个块状元素的水平居中    

要实现多个水平排列的块状元素的水平居中，传统的方法是将要水平排列的块状元素设为display:inline-block，然后在父级元素上设置text-align:center，达到与上面的行内元素的水平居中一样的效果。

```
#container{
    text-align:center;
}
 
#center{
    display:inline-block;
}
```

## 使用flexbox实现多个块状元素的水平居中

Flexbox布局（Flexible Box)模块旨在提供一个更加有效的方式制定、调整和分布一个容器里的项目布局，即使他们的大小是未知或者是动态的。是CSS3 中一个新的布局模式，为了现代网络中更为复杂的网页需求而设计。

### 学会使用flexbox
要为元素设置flexbox布局，只需将display属性值设置为flex。

```
#container {
    display: flex;
}
```
flexbox的默认为一个块级元素，如果需要定义为一个行内级的元素，同理：

```
#container {
    display: inline-flex;
}
```
flexbox由伸缩容器和伸缩项目组成。通过设置元素的display属性为flex或者inline-flex可以得到一个伸缩容器。设置为flex的容器被渲染为一个块级元素，而设置为inline-flex的容器则渲染为一个行内元素。而每一个被设置为flex的容器，它的内部元素都将变成一个flex项目，即是一个伸缩项目。简单的说，flex 定义了伸缩容器内伸缩项目该如何布局。

回到正题，利用flexbox实现多块状元素的水平居中，只需要将父级容器的Css设置如下：

```
#container{
    justify-content:center;
    display:flex;
}
```
[参考](https://www.cnblogs.com/coco1s/p/4444383.html)