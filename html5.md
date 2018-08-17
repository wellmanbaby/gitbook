# meta标签
**之前学习前端中，对meta标签的了解仅仅只是这一句。**

```
<meta charset="UTF-8">
```
**但是打开任意的网站，其head标签内都有一列的meta标签，但是自己却很不熟悉。**
## 简介
**在查阅w3school中，第一句话中的“元数据”就让我开始了Google之旅。然后很顺利的在英文版的w3school找到了想要的结果。**

```
The <meta> tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.
```
我解释一下，meta标签会给HTML文档提供元数据，元数据将会被计算机解析，不会被展示在网页中。

## 用处

```
Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata.

The metadata can be used by browsers (how to display content or reload page), search engines (keywords), or other web services
```
翻译过来就是：meta常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。其实说白了，这些东西不是给程序员和用户看的，是给浏览器和搜索引擎看的。

## 组成

**meta标签共有两个属性，分别是http-equiv属性和name属性。**

### name属性
name属性主要用于描述网页，比如网页的关键词，叙述等。与之对应的属性值为content，content中的内容是对name填入类型的具体描述，便于搜索引擎抓取。

meta标签中name属性语法格式是：


```
<meta name="参数" content="具体的描述">。
```
**其中name属性共有以下几种参数:**

**A. keywords(关键字):** 用于告诉搜索引擎，你网页的关键字。

```
<meta name="keywords" content="Lxxyx,博客，文科生，前端">
```
**B. description(网站内容的描述):** 用于告诉搜索引擎，你网站的主要内容。

```
<meta name="description" content="文科生，热爱前端与编程。目前大二，这是我的前端博客">
```
**C. viewport(移动端的窗口):** 这个概念较为复杂，
这个属性常用于设计移动端网页。在用bootstrap,AmazeUI等框架时候都有用过viewport。

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```
**E. author(作者)：** 用于标注网页作者

```
<meta name="author" content="Lxxyx,841380530@qq.com">
```
**G. copyright(版权)：** 用于标注版权信息

```
<meta name="copyright" content="Lxxyx"> //代表该网站为Lxxyx个人版权所有
```
**I. renderer(双核浏览器渲染方式)：** renderer是为双核浏览器准备的，用于指定双核浏览器默认以何种方式渲染页面。比如说360浏览器。

```
<meta name="renderer" content="webkit"> //默认webkit内核
<meta name="renderer" content="ie-comp"> //默认IE兼容模式
<meta name="renderer" content="ie-stand"> //默认IE标准模式
```
### http-equiv属性
介绍之前，先说个小插曲。看文档和博客关于http-equiv的介绍时，有这么一句。

```
http-equiv顾名思义，相当于http的文件头作用。
```
一开始看到这句话的时候，我是迷糊的。因为我看各类技术名词，都会习惯性的去记住它的英文全称。equiv的全称是"equivalent"，意思是相等，相当于。然后我脑子里出现了大大的迷惑：“HTTP相等？”

后来还准备去Segmentfault提问来着。结果在写问题的时候，突然反应出equivalent还有相当于的意思。意思就是相当于http的作用。至于文件头是哪儿出来的，估计是从其作用来分析的。我认为顾名思义并不能得出"相当于http的文件头作用"这个论断。

这个我所认为的http-equiv意思的简介，相当于HTTP的作用，比如说定义些HTTP参数啥的。

meta标签中http-equiv属性语法格式是：

```
<meta http-equiv="参数" content="具体的描述">
```
**其中http-equiv属性主要有以下几种参数：**

**A. content-Type(设定网页字符集)(推荐使用HTML5的方式:**

说明：用于设定网页字符集，便于浏览器解析与渲染页面

```
<meta http-equiv="content-Type" content="text/html;charset=utf-8">  //旧的HTML，不推荐

<meta charset="utf-8"> //HTML5设定网页字符集的方式，推荐使用UTF-8
```
**B. X-UA-Compatible(浏览器采取何种版本渲染当前页面):**

说明：用于告知浏览器以何种版本来渲染页面。（一般都设置为最新模式，在各大框架中这个设置也很常见。）

```
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/> //指定IE和Chrome使用最新版本渲染当前页面
```
[大牛](https://segmentfault.com/a/1190000004279791)