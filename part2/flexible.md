# flexible.js 移动端自适应方案

## 使用方法

建议对于js做内联处理，在所有资源加载之前执行这个js。

执行这个js后，会在html（也就是document.documentElement）上增加一个data-dpr属性，以及font-size样式。

之后页面中的元素，都可以用rem单位来设置。html上的font-size就是rem的基准像素。

## 把视觉稿中的px转换成rem

首先，目前视觉稿大小分为640，750以及，1125这三种。

当前方案会把这3类视觉稿分成100份来看待（为了以后兼容vh，vw单位）。每一份被称为一个单位a。同时，1rem单位认定为10a。拿750的视觉稿举例：

1a = 7.5px

1rem = 75px

因此，对于视觉稿上的元素的尺寸换算，只需要原始px值除以rem基准px值即可。例如240px * 120px的元素，最后转换为3.2rem * 1.6rem。

这个也不会真的让你算

如果你用的是SublimeText3，你可以直接在这个编辑器上安装CSSREM插件。

如果你用的是其他编辑器或者IDE，就可以用CSS的处理器来处理，比如说Sass、LESS以及PostCSS这样的处理器。我们简单来看两个示例。

## 字体不使用rem的方法

工作中做完一个触屏版的页面后，我们会拿iPhone5s、iPhone6、iPhone6s等手机进行测试，他们都是Retina屏，我们当然希望在这些手机型号上看到的文本字号是相同的。也就是说，我们不希望文本在Retina屏幕下变小，另外，我们希望在大屏手机上看到更多文本（例如iPhone7、iPhone7Plus）。另外，现在绝大多数的字体文件都自带一些点阵尺寸，通常是16px和24px，都是偶数，所以我们不希望出现13px和15px这样的奇葩尺寸。

如此一来，就决定了在制作H5的页面中，rem并不适合用到段落文本上。所以在Flexible整个适配方案中，考虑文本还是使用px作为单位。只不过使用[data-dpr]属性来区分不同dpr下的文本字号大小。


字体的大小不推荐用rem作为单位。所以对于字体的设置，仍旧使用px作为单位，并配合用data-dpr属性来区分不同dpr下的的大小。

举例子：

```
div {
    width: 1rem; 
    height: 0.4rem;
    font-size: 12px; // 默认写上dpr为1的fontSize
}

[data-dpr="2"] div {
    font-size: 24px;
}

[data-dpr="3"] div {
    font-size: 36px;
}
```
## 手动配置dpr

引入执行js之前，可以通过输出meta标签方式来手动设置dpr。语法如下：
```
<meta name="flexible" content="initial-dpr=2,maximum-dpr=3" />
```
其中initial-dpr会把dpr强制设置为给定的值，maximum-dpr会比较系统的dpr和给定的dpr，取最小值。**注意：这两个参数只能选其一**。

## viewport的meta标签

该标签主要用来告诉浏览器如何规范的渲染Web页面，而你则需要告诉它视窗有多大。在开发移动端页面，我们需要设置meta标签如下：

```
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```
代码以显示网页的屏幕宽度定义了视窗宽度。网页的比例和最大比例被设置为100%。

而我们在使用flexible.js时候就只需要像下面这样写<meta>标签，或者干脆省略下面的标签：

```
<meta name="viewport" content="width=device-width, user-scalable=no">
```
**有了meta标签之后，就可以动态改写data-dpr和font-size两个属性的值，因此也就达到了适配的效果。**

[参考1](http://570109268.iteye.com/blog/2410021)
[参考2](https://www.jianshu.com/p/04efb4a1d2f8)