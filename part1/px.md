# CSS 实现移动端 1px 线条的绘制
## 1px 线条变胖之谜

iPhone 3GS 和 iPhone 4 的像素分别是 320px 和 640px，但是显示屏的宽度却却都是相同的，所以为了在所有设备上渲染出的显示效果相同，CSS 中的 1px 映射到 iPhone 4 的物理像素上，就会是 2px

同样的道理，在 iPhone 5、6 上 CSS 的 1px 对应物理像素 2px，6plus 则是 3px

所以当我们设置 1px 时，实际的显示效果其实是由两个甚至三个像素点所绘制的。

## 如何让线条恢复苗天身材
**先放大，再缩小**

原理很简单，对于想要加上 1px 边框的元素，我们只需要将它的伪元素设置成一个两倍宽高与其自身的盒子，将这个盒子的边框设置为 1px ，然后再将其缩放到原先的 50%，即可成功绘制出真正的 1px 线条，因为原先对应的 2 物理像素缩放 50% 后，就会变成 1 个物理像素

同样的，在 3 倍分辨率屏幕上也可以通过类似的方式来实现 1px 边框，但是一般情况下不会去特意设置 3 倍分辨率的情况，而是统一使用 2 倍分辨率的解决方案

下面是 CSS 代码

```
.box:before{
    content: "";
    pointer-events: none; /* 防止点击触发 */
    box-sizing: border-box;
    position: absolute;
    width: 200%;
    height: 200%;
    left: 0;
    top: 0;
    border:1px solid #000;
    -webkit-transform(scale(0.5));
    -webkit-transform-origin: 0 0;
    transform(scale(0.5));
    transform-origin: 0 0;
}
```
**缺点**
1. 占据了该元素的伪元素，代码量相对较多

2. input元素没有伪元素

## 采用自适应方案
例如淘宝的移动端适配解决方案 flexible.js ，将设备的视口宽度（viewport）设置为实际的物理像素，那么绘制出来的 1px 就会等于 1 个物理像素，同时也可解决其他的适配问题

缺点：并不能够完美适用于安卓（毕竟安卓坑多）

## 其他方法
上面说了两种普适性较高的方法，但是其他方法也是有的呦，比如直接根据 CSS media query 的 devicePixelRatio 来设置线条的像素，devicePixelRatio=2 时设置 0.5px，devicePixelRatio=3 时设置 0.333333 px，但是这个方法完全不使用与安卓


