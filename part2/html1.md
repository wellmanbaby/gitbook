# HTML5新特性

**HTML5的新特性非常的多，可是其实用到的也就那些吧，我大致地整理一些：**

## 1. 语义化标签

**感觉这个就好多好多！**

### 什么是语义化标签？
 
用最恰当的HTML元素标记内容。

### 优点是啥？

1. 提升可访问性
2. 有利于搜索引擎优化SEO
3. 结构清晰，便于维护

### 标签罗列

**<title></title>：** 简短、描述性、唯一（提升搜索引擎排名）。

搜索引擎会将title作为判断页面主要内容的指标，有效的title应该包含几个与页面内容密切相关的关键字，建议将title核心内容放在前60个字符中。

**<header></header>：** 页眉通常包括网站标志、主导航、全站链接以及搜索框。

**<nav></nav>：** 标记导航，仅对文档中重要的链接群使用。

**<main></main>:** 页面主要内容，一个页面只能使用一次。如果是web应用，则包围其主要功能。

**<article></article>：** 表示文档、页面、应用或一个独立的容器。

**<aside></aside>：**  指定附注栏，包括引述、侧栏、指向文章的一组链接、广告、友情链接、相关产品列表等。

**<footer></footer>：** 页脚，只有当父级是body时，才是整个页面的页脚。
***
## 新的文档类型（New Doctype）

**新的文档类型带来了便捷的申明方式**

**目前许多网页还在使用XHTML 1.0 并且要在第一行像这样声明文档类型：**

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```
**在HTML5中，上面那种声明方式将失效。下面是HTML5中的声明方式：**

```
<!DOCTYPE html>
```
**是不是非常非常简洁！感谢HTML5！感谢主！**
***
## 链接脚本文件再也不需要type属性

**在HTML4或XHTML中，你需要用下面的几行代码来给你的网页添加CSS和JavaScript文件。**

```
<link rel="stylesheet" href="style/stylesheet.css" type="text/css" />
 <script type="text/javascript" src="js/script.js"></script>
```
**而在HTML5中，你不再需要指定类型属性。因此，代码可以简化如下：**

```
<link rel="stylesheet" href="style/stylesheet.css" />
<script src="js/script.js"></script> 
```
**再一次感谢H5！感谢主！**
***
## Hgroup

**在HTML5中，有许多新引入的元素，hgroup就是其中之一。假设我的网站名下面紧跟着一个子标题，我可以用<h1>和<h2>标签来分别定义。然而，这种定义没有说明这两者之间的关系。而且，h2标签的使用会带来更多问题，比如该页面上还有其他标题的时候。**

**在HTML5中，我们可以用hgroup元素来将它们分组，这样就不会影响文件的大纲。**

```
<header>
    <hgroup>
      <h1> Recall Fan Page </h1>
      <h2> Only for people who want the memory of a lifetime. </h2>
    </hgroup>
</header>
```
***
## 标记元素（Mark Element）

**你可以把它当做高亮标签。被这个标签修饰的字符串应当和用户当前的行动相关。比如说，当我在某博客中搜索“Open your Mind”时，我可以利用一些JavaScript将出现的词组用<mark>修饰一下。**

```
<h3> Search Results </h3>
<p> They were interrupted, just after Quato said, <mark>"Open your Mind"</mark> </p>
```
## 图形元素（Figure Element）

**在HTML4或XHTML中，下面的这些代码被用来修饰图片的注释。**

```
<img src="image/image" alt="About image" />
<p>Image of Mars </p>
```
**然而，上述代码没有将文字和图片内在联系起来。因此，HTML5引入了<figure>元素。当和<figcaption>结合起来后，我们可以语义化地将注释和相应的图片联系起来。**

```
<figure>
    <img src="path/to/image" alt="About image" />
    <figcaption>
        <p>This is an image of something interesting.</p>
    </figcaption>
</figure>
```
[HTML5新特性](https://segmentfault.com/a/1190000007215988)
