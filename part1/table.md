# table布局
## display:table-cell属性简述：

display:table-cell属性指让标签元素以表格单元格的形式呈现，类似于td标签。目前IE8+以及其他现代浏览器都是支持此属性的，但是IE6/7只能对你说sorry了，这一事实也是大大制约了display:table-cell属性在实际项目中的应用（写于2016年8月24日：时代在变，当下，是时候登上舞台了）。

我们都知道，单元格有一些比较特别的属性，例如元素的垂直居中对齐，关联伸缩等，所以display:table-cell还是有不少潜在的使用价值的，虽说IE6/7不支持此属性，但是幸运的是，IE6/7一些乱糟糟的属性与渲染，我们可以其他方法实现同样或是类似的效果。

与其他一些display属性类似，table-cell同样会被其他一些CSS属性破坏，例如float, position:absolute，所以，在使用display:table-cell与float:left或是position:absolute属性尽量不用同用。设置了display:table-cell的元素对宽度高度敏感，对margin值无反应，响应padding属性，基本上就是活脱脱的一个td标签元素了。

## 利用display:table-cell解决大小不固定的图片、多行文字的水平垂直居中
### 多行文字
文字可能一行显示，也有可能多行显示；文字可能是小号字体，也有可能是大号的。这时候如何让其垂直居中显示：

HTML

```
<div class="box_2">
  <span class="word">这里显示多行文字。</span>
</div>
```
CSS

```
box_2 {
 display:table-cell; 
 width:550px; 
 height:200px; 
 padding:10px; 
 border:4px solid #beceeb; 
 color:#069; 
 font-size:2px; 
 vertical-align:middle;
}
.word{
 display:inline-block; 
 font-size:2px; 
 vertical-align:middle
}
```
说白了，就是把文字当图片处理。用一个span标签将所有的文字封装起来，设置文字与图片相同的display属性（inline-block属性），然后用处理图片垂直居中的方式处理文字的垂直居中即可。

图片同理。

## 两栏自适应布局
css

```
  .left{
          width:300px;
          float:left;
          text-align:center;
          background: #333322;;
          height:500px;
          }
      .right{
          display:table-cell;
          width:2000px;
          background:bisque;
          height:800px;
          }
```
HTMl

```
<div class="left">
                <a href="#prettyGirl" class="l mr10">
                    <img border="0" src="//image.zhangxinxu.com/image/study/s/s128/mm2.jpg" />
                </a>
        </div>
 <div class="right">时代时代所多撒多多</div>
```

## 等高布局
table布局有两个特性：

1. 同行等高
2. 宽度自动调节

```
<style type="text/css"> 
   .classtd {
        display:table-cell;
        padding:30px; 
        border:1px solid #ccc;
    }
</style>
<div class="classtd">
   <p>大人。<br />
    其实我觉得大家别问元芳，元芳不是神人，<br />
    也不会武功，也许还是个智障，<br />
    我就不信我在这里黑元芳<br />
    他会突然飞檐走壁来到我身后<br />
    把我的头按在键盘上</p>
</div>
<div class="classtd">
    <p>我和左边等高</p>
</div>

```
设置几个div的样式为table-cell，那么这几个div会被视作类似表单的同一行几个td, 有相同的高度，并且无缝相接。 并且！！！设置了table-cell后的元素，再设置margin是没有用的！！因为margin对table不起作用！！！

## 列表布局

一般这类布局都是使用浮动的。但是浮动布局的不足在于：一是需要清除浮动造成影响；二是不支持不定高列表的浮动。替代浮动布局的方法是有的，如果深究细节以及一些思想，方法还不少。其中有一个方法就是使用display:table-cell。

display:table-cell下的列表布局最适用的场景是：列表个数不固定，但是，无论列表几个，都平分容器空间。什么意思呢？就是如果4个列表，希望每个宽度25%，3个就33.3333%，2个列表希望每个宽度50%。此时，没有比display:table-cell更合适的技术了。

父级设置display:table同时宽度为容器宽度，或者直接width:100%，此时，display:table-cell子元素就会自动等分。