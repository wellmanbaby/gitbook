# 前端知识点总结（HTML篇）

## HTML
1. **ie的某些兼容性问题**
2. **doctype的作用**
3. **HTML中标准模式和怪异模式有什么不同**
4. **写出你常用的HTML标签**
5. **为什么要少用iframe**
6. **HTML语义化的理解**
7. **行内元素和块级元素的异同及img类似的特殊性**
8. **盒模型，及在浏览器兼容方面的异同**

## HTML5  
1. **HTML5的新特性**  
2. **canvas画图**
3. **HTML5中引进`data-`有什么作用**
4. **canvas的性能优化**



## 新增
2018-08-14
1. **HTML5新特性，语义化**

     **语义化**
      **用最恰当的HTML元素标记的内容**
      1. **提升可访问性**
      2. **有利于SEO**
      3. **结构清晰，利于维护**
      
     [HTML5新特性](https://segmentfault.com/a/1190000010504564)
     [HTML5](https://segmentfault.com/a/1190000007215988)


2. **浏览器的标准模式和怪异模式**

      **标准模式和怪异模式的由来？**
      
      在HTML与CSS的标准化未完成之前，各个浏览器对于HTML和CSS的解析有各自不同的实现，而有很多旧的网页都是按照这些非标准的实现去设计的。在HTML与CSS标准确定之后，浏览器一方面要按照标准去实现对HTML与CSS的支持，另一方面又要保证对非标准的旧网页设计的后向兼容性。因此，现代的浏览器一般都有两种渲染模式：标准模式和怪异模式。在标准模式下，浏览器按照HTML与CSS标准对文档进行解析和渲染；而在怪异模式下，浏览器则按照旧有的非标准的实现方式对文档进行解析和渲染。这样的话，对于旧有的网页，浏览器启动怪异模式，就能够使得旧网页正常显示；对于新的网页，则可以启动标准模式，使得新网页能够使用HTML与CSS的标准特性。
      
      **浏览器如何确定使用哪种渲染模式？**
      
     知道了这两种渲染模式的来由，那剩下的问题就是浏览器如何能够确定应该使用哪种模式了。其实归根结底就是，浏览器如何能将旧网页与新网页区分开来。
平常编写网页的时候，一般都会见到HTML文档的头部会有文档类型声明：DOCTYPE。当浏览器遇到正确的文档声明时，浏览器就会启动标准模式，按照制定的文档类型标准解析和渲染文档。而对于旧有的网页，由于网页编写的当时标准还没有确定，所以一般是不会有文档类型声明的。所以，对于没有文档类型声明或者文档类型声明不正确的文档，浏览器就会认为它是一个旧的HTML文档，就会使用怪异模式解析和渲染该文档。关于DOCTYPE的更详细说明，请戳这里 DOCTYPE声明作用及用法详解

      **标准模式与怪异模式的两个常见区别？**
      
      1. 盒模型的处理差异:    标准CSS盒模型的宽度和高度等于内容区的高度和宽度，不包含内边距和边框，而IE6之前的浏览器实现的盒模型的宽高计算方式是包含内边距和边框的。因此，对于IE，怪异模式和标准模式下的盒模型宽高计算方式是不一样的；
      
      2. 行内元素的垂直对齐:    很多早期的浏览器对齐图片至包含它们的盒子的下边框，虽然CSS的规范要求它们被对齐至盒内文本的基线。标准模式下，基于Gecko的浏览器将会对齐至基线，而在quirks模式下它们会对齐至底部。最直接的例子就是图片的显示。在标准模式下，图片并不是与父元素的下边框对齐的，如果仔细观察，你会发现图片与父元素下边框之间存在一点小空隙。那是因为标准模式下，图片是基线对齐的。而怪异模式下，则不存在这个问题


3. **xhtml和html的区别**

      **strict html 4.01 标准**

         1. <html> 必须是root元素
         2. <head>和<body> 是 <html>中一定有且只有的元素
         3. <head> 必须有 <title>， <meta>和<style>可选, 他们只能在<head>里
         4. <body> 里只能有 block元素
         5. block元素不能放在inline元素里
         6. block元素不能放在<p>里
         7. <ul>和<ol>中只能有<li>元素,但<li>里可以放其他，包括block元素
         8. <blockquote>中只能放block元素
         
     **xhtml 1.0 标准**

         1. html元素需要有xml相关属性
         2. 元素名必须是小写字母素
         3. 元素属性用"包围,不能为空值里
         4. 在内容里不能有&, 需要转义，包括其他特殊字符<>
         5. 空元素以 />结尾
         
4. **使用data-的好处**
 
     [HTML5 data-* 自定义属性](https://www.cnblogs.com/dolphinX/p/3348458.html)
     在HTML5中添加了data-的方式来自定义属性，所谓data-实际上就是data-前缀加上自定义的属性名，使用这样的结构可以进行数据存放。使用data-*可以解决自定义属性混乱无管理的现状。
5. **meta标签**

    meta常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页面），搜索引擎和其它网络服务。
    [HTML meta标签总结与属性使用介绍](https://segmentfault.com/a/1190000004279791)

6. **meta viewport原理**

   [这个有些复杂](https://lizhiyao.github.io/2017/04/01/viewport/)


7. **canvas**
 
   HTML5 的标准已经出来好久了，但是似乎其中的 Canvas 现在并没有在太多的地方用到。一个很重要的原因是，Canvas 的标准还没有完全确定，不适合大规模用在生产环境。但是，Canvas 的优点也是很明显的，例如在绘制含有大量元素的图表的时候，SVG 往往因为性能问题而无法胜任，例如我见过的一次技术分享会的抽奖环节，虽然效果比较炫，但因为每个头像都是 DOM，利用 CSS3 控制的动画，导致了性能非常低下。此外，随着硬件性能的提高，视频截图、图像处理等功能也逐渐可以在网页上实现了，大多数网站用的是 Flash，但是 Flash 在 Mac 电脑上性能不高，还需要学一些额外的知识。Canvas 则是直接使用 JavaScript 来进行绘图，对 Mac 友好，所以不失为 Flash 的一个继承者。[使用 Canvas](http://www.techug.com/post/html5-canvas.html)



8. **HTML废弃的标签**
   
   **为什么有些标签被废弃了？**

   因为当前HTML标签只有一个作用，就是用来添加语义，而早期的HTML标签中有一部分是没有语义的。

   有一部分标签是由来修改样式的

    例如：<br>  <hr>  <font>  <b> <u>  <i>  <s>   以上这些标签没有语义，都是用来修改样式的

    b (bold)：加粗文本，没有任何语义。

    u(underline):给文本添加下划线，没有任何语义。

    i(italic):将文本倾斜，没有任何语义。

    s(strikethrough):给文本添加删除线，没有任何语义。

    注意点：以后在企业开发中不到万不得已不要用废弃的html废弃的标签，如果要使用，一般情况下都是用来css的钩子来使用。

   用新标签来替代：

   strong==b                              有语义，定义重要性强调的文字。

   ins==u（inseted）                有语义，定义插入的文字。

   em==i （emphasized）         有语义，定义强调的文字。

   del==s （deleted）               有语义，定义删除的文字。

   [HTML被废弃的标签](https://www.jianshu.com/p/feb5d88f90bf)
9. **IE6 bug，和一些定位写法**
   
    前端三毒IE6.7.8，目前主流框架已经不再做IE6.7.8兼容，不过万一政府，学校单位要做什么系统要用到IE6.7.8也是不无可能，所以看看吧！

    1、双边距Bug,由float所引起，通过使用display解决

    2、3像素问题，由使用float引起，使用display:inline -3px;解决

    3、超链接hover，点击后失效，使用正确的书写顺序：link visited hover active

   4、z-index问题，给父级添加position:relative

   5、png透明，使用js代码进行修改

   6、min-height最小高度，使用!important解决

   7、select在IE6下遮盖，使用iframe嵌套

   8、为什么没有办法定义1px左右宽度的宽度容器
（IE6默认的行高造成的，使用overflow:hidden;zoom:0.08;line-height:1px;解决）

   [IE6兼容性问题及IE6常见bug详细汇总](https://www.jb51.net/css/76894.html)
   
   
   
10. **css js放置位置和原因**
  
    问这个问题之前，我先说一下浏览器的解析方式，浏览器解析html页面首先浏览器先下载html，然后在内存中把html代码转化成Dom Tree，
然后浏览器根据Dom Tree上的Node分析css和Images，当文档下载遇到js时，js独立下载。
那为什么还要将引用的外部js放在下面，外部css放在上面？（浏览器会有自己的解析顺序）
仅仅是一种良好的编码习惯吗？还是的确会对性能有好处？好处体现在哪些方面？
顺便问一下，有些知名网站的首页会把所有的js和css都写在html的head中，这又是一种什么现象？他们的考虑点在哪里？CSS、JS [放置位置与前端性能的关系](https://blog.csdn.net/bigtree_3721/article/details/51006066)


11. **什么是渐进式渲染**

     为什么说渐进式渲染?
     以往基于字符串拼接的模板引擎技术, 性能还可以, 但是前端不方便,
     而现在基于 Virtual DOM 实现的后端渲染, 前端舒服, 后端却变慢,
     原因是 Virtual DOM 难以做静态分析进行预编译, 最终难以提高性能.
     另外组件级别 Caching 方案也不够成熟, 以后比较难确定有效果.

     既然提高性能短期做不到, 那么考虑对服务端渲染的工作进行缩减.
     比如说, 首屏渲染多少内容? 整页渲染性能低, 能不能只渲染部分,
      比如说只渲染第一屏主体内容, 而下方或者更详细数据在客户端抓取.
就是说, 服务端渲染一部分, 客户端加载一部分, 从而做出效果.
当然, 并不是新的东西, 只是说这套方案在 Virtual DOM 上要重新实现一遍.

     再说"渐进式", 上述过程"服务端/客户端"渲染工作分割的比例如何?
比如说定义 Level 0~5 的等级, 服务端渲染的部分可以有多种情况,
最主要的比如说 App Shell 情况, 也就是页面的静态框架部分,
那么渲染过程就是: 服务端渲染局部, 客户端渲染局部,
而且随着服务端性能提高, 可以分配更多工作到服务器上. 这样的"渐进",
[首屏渐进式渲染设想](http://www.voidcn.com/article/p-vakeccfd-c.html)
12. **html模板语言**

模板概述

1. 作为Web框架，Django提供了模板，可以很便利的动态生HTML
2. 模版系统致力于表达外观，而不是程序逻辑。
3. 模板的设计实现了业务逻辑(view)与显示内容（template）的分离，一个视图可以使用任意一个模板，一个模板可以供多个视图使用。
4. 模板包含：
    1.	HTML的静态部分
    2.	动态插入内容部分
5. Django模板语言，简写DTL，定义在django.template包中，由startproject命令生成的settings.py定义关于模板的值：
    1. DIRS定义了一个目录列表，模板引擎按列表顺序搜索这些目录以查找模板源文件
    2. APP_DIRS告诉模板引擎是否应该在每个已安装的应用中查找模板，这种便于发布应用
    3. 常用方式：在项目的根目录下创建templates目录，设置DIRS值
DIRS=[os.path.join(BASE_DIR,"templates")]       注释{# 代码或html #}

注意

当模版引擎遇到点(".")，会按照下列顺序查询：
1.	字典查询，例如：foo["bar"]   {{foo.bar}}
2.	属性或方法查询，例如：foo.bar
3.	数字索引查询，例如：foo[bar]  {{all_students.0}}。如果变量不存在， 模版系统将插入'' (空字符串)。在模板中调用方法时不能传递参数
	
[HTML模板语言](https://blog.csdn.net/xiaoming0018/article/details/80389277)
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


13. **ie的某些兼容性问题**
   [IE的兼容性问题](http://fengzheqi.com/2015/10/18/%E6%B5%8F%E8%A7%88%E5%99%A8%E5%85%BC%E5%AE%B9/)

14. **doctype的作用**  
   答案：doctype告诉浏览器它使用了什么文档类型。它指出阅读程序应该用什么		规则集来解释文档中的标记。XHTML中有三种，包括过度型、严格型、框架型。HTML4严格。随着XML的流行，HTML推出了XHTML标准，其中严格模式严格遵守了XML的规范，例如属性必须有值、标签必须闭合等，同时也抛弃了一些不推荐的标签。而XHTML过度版本，则稍微比严格模式松散些，一些不推荐的标签依然可用外。当页面有框架时，则应该使用框架型。再就是HTML5的版本。使用HTML5的Doctype会默认触发标准模式。

15. **HTML中标准模式和怪异模式有什么不同**  
   答案：由于历史的原因，各个浏览器在对页面的渲染上存在差异，甚至同一浏览器在不同版本中，对页面的渲染也不同。在W3C标准出台以前，浏览器在对页面的渲染上没有统一规范，产生了差异(Quirks mode或者称为Compatibility Mode)；由于W3C标准的推出，浏览器渲染页面有了统一的标准(CSScompat或称为Strict mode也有叫做Standars mode)，这就是二者最简单的区别。  
   W3C标准推出以后，浏览器都开始采纳新标准，但存在一个问题就是如何保证旧的网页还能继续浏览，在标准出来以前，很多页面都是根据旧的渲染方法编写的，如果用的标准来渲染，将导致页面显示异常。为保持浏览器渲染的兼容性，使以前的页面能够正常浏览，浏览器都保留了旧的渲染方法（如：微软的IE）。这样浏览器渲染上就产生了Quircks mode和Standars mode，两种渲染方法共存在一个浏览器上。火狐一直工作在标准模式下，但IE（6，7，8）标准模式与怪异模式差别很大，主要体现在对盒子模型的解释上，这个很重要，下面就重点说这个。    那么浏览器究竟该采用哪种模式渲染呢？这就引出的DTD，既是网页的头部声明，浏览器会通过识别DTD而采用相对应的渲染模式。  
   1.浏览器要使老旧的网页正常工作，但这部分网页是没有doctype声明的，所以浏览器对没有doctype声明的网页采用quirks mode解析。  
   2.对于拥有doctype声明的网页，什么浏览器采用何种模式解析，这里有一张详细列表可参考：[点击这里](http://hsivonen.iki.fi/doctype)。  
   3.对于拥有doctype声明的网页，这里有几条简单的规则可用于判断：对于那些浏览器不能识别的doctype声明，浏览器采用strict mode解析。  
   4.在doctype声明中，没有使用DTD声明或者使用HTML4以下（不包括HTML4）的DTD声明时，基本所有的浏览器都是使用quirks mode呈现，其他的则使用strict mode解析。  
   5.可以这么说，在现有有doctype声明的网页，绝大多数是采用strict mode进行解析的。  
   6.在ie6中，如果在doctype声明前有一个xml声明(比如:<?xml version=”1.0″ encoding=”iso-8859-1″?>)，则采用quirks mode解析。这条规则在ie7中已经移除了。  

16. **写出你常用的HTML标签**  
   答案：根据自己的使用和掌握来写吧。参考http://blog.csdn.net/ithomer/article/details/5277162。

17. **为什么要少用iframe**  
   答案：[为什么应该减少使用iframe](http://www.williamlong.info/archives/3136.html)  
   iframe的创建比其它包括scripts和css的 DOM 元素的创建慢了 1-2 个数量级。  
   Iframes阻塞页面加载:window 的 onload 事件需要在所有 iframe 加载完毕后(包含里面的元素)才会触发。在 Safari 和 Chrome 里，通过 JavaScript 动态设置 iframe 的 SRC 可以避免这种阻塞情况。  
   唯一的连接池:有人可能希望 iframe 会有自己独立的连接池，但不是这样的。绝大部分浏览器，主页面和其中的 iframe 是共享这些连接的。这意味着 iframe 在加载资源时可能用光了所有的可用连接，从而阻塞了主页面资源的加载。如果 iframe 中的内容比主页面的内容更重要，这当然是很好的。但通常情况下，iframe 里的内容是没有主页面的内容重要的。这时 iframe 中用光了可用的连接就是不值得的了。一种解决办法是，在主页面上重要的元素加载完毕后，再动态设置 iframe 的 SRC。

18. **HTML语义化的理解**  
   答案：用正确的标签表达正确的内容，可以增强网页的易用性（如障碍人士访问等）和搜索引擎的爬取和检索。HTML5新增的语义化标签如header\section\article\footer等。

19. **行内元素和块级元素的异同及img类似的特殊性**  
    答案：行内元素和块级元素异同如下：  
    1.行内元素与块级元素直观上的区别，行内元素会在一条直线上排列，都是同一行的，水平方向排列;  
    2.块级元素可以包含行内元素和块级元素。行内元素不能包含块级元素;    
    3.行内元素与块级元素的属性的不同，主要是盒模型属性上(行内元素设置width无效，height无效(可以设置line-height)，margin上下无效)；  
    4.行内元素转换为块级元素,通过设置display:block

    注：img\input\textarea等是特殊的行内元素，确切的说是inline-block元素。

20. **盒模型，及在浏览器兼容方面的异同**  
    答案：浏览器的盒子模型指的是它的盒子宽度需要包括内容区宽度、内外边距和边框大小，高度类似。一般设置宽度默认是对应内容区宽度。  
    兼容性方面：在IE7以前的版本中设置宽度是包括：内边距+边框+内容区的。IE7之后跟其它浏览器一样，都是只对应内容区的宽度。可以通过修改box-sizing:border-box来修改。让设置宽度等于内容区和边框和内边距之和。

## HTML5

1. **HTML5的新特性**  
   答案：HTML5新增的特性与API
   **语义化标签**：提升Web的可用性，利于SEO和屏幕阅读器；一般有header、footer、nav、article、section等。  
   **新的音视频**：HTML中包含audio和video标签，可以播放视频和音评，不过格式有限制。  
   **Geolocation**：提供地理位置的API，获取用户的地理位置信息。  
   **WebSocket**：提供Websock的API，使得web可以实时的接受服务器响应。  
   **Communication**：HTML5中提供了CORS，可以实现跨域资源共享；还有实现了跨文档消息传输，postMessage。  
   **Form API**：增强了form表单，比如增加了input的type类型，number/tel/range等，点击查看[移动端显示](http://www.oschina.net/translate/using-html5-input-types-to-enhance-the-mobile-browsing-experience?cmp)。  
   **Webworkers**：Webworkers使得在浏览器端也可以实现多线程的应用。  
   **WebStorage**：Webstorage是为了减少http请求，在用户客户端实现缓存数据，包括localStorage和sessionStorage，还有indexDB等。  
   **OffineWeb**：浏览器借用WebStorage可以实现一些简单的离线应用，比如读写邮件、编辑文档、创建todo等
   **推荐博客**：  
   [28 HTML5 Features, Tips, and Techniques you Must Know](http://code.tutsplus.com/tutorials/25-html5-features-tips-and-techniques-you-must-know--net-13520)  [中文](http://www.zhangxinxu.com/wordpress/2010/08/%E7%BF%BB%E8%AF%91-%E4%BD%A0%E5%BF%85%E9%A1%BB%E7%9F%A5%E9%81%93%E7%9A%8428%E4%B8%AAhtml5%E7%89%B9%E5%BE%81%E3%80%81%E7%AA%8D%E9%97%A8%E5%92%8C%E6%8A%80%E6%9C%AF/)

2. **canvas画图**  

3. **HTML5中引进`data-`有什么作用**  
   答案：data-是HTML5新增的一个自定义属性。用以方便开发者在HTML中自定义一些属性来存储和操作数据，同时又不违背HTML的规范，不会带来一些副作用。data-自定义属性非常简单，如下例：

   ``` html
   <article  id="electriccars"  data-columns="3"  data-index-number="12314"  data-parent="cars">...</article>。
   ```

   通过JS去获取自定义属性非常简单，可以通过 getAttribute()传递全部名称来获取，也可以使用 dataset 属性集来获取。如：

   ``` javascript
   var article = document.querySelector('#electriccars');
   article.dataset.columns; // "3"  
   article.dataset.indexNumber ;// "12314"  
   article.dataset.parent ;//
   ```

4. **canvas的性能优化**  
   答案：主要有使用缓存、避免浮点运算、尽量减少canvas API的调用、硬件加速。  
   [canvas的性能优化](http://www.cnblogs.com/rubylouvre/p/3570636.html)
