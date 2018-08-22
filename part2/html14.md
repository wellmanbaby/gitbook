# iframe

## 什么是iframe

**iframe即内联框架。不同于frame，frame与frameset综合使用，成为帧，框架集。frame已经不大使用了，说白了，frame是僵硬的叠加，iframe是内联的，不是简单的叠加，而是承前启后，对于外围的页面，iframe是一个普通的元素，对于iframe里面的内容，又是一个五脏俱全的页面。iframe的写法是：**

　　<iframe id="coreIframe" name="coreIframe" src="/blank.html"></iframe>

**可以看出，iframe毫无神秘可言，就是一个普通的元素，与span,div一样。那么，iframe是内联元素还是块元素？第一，iframe可以设置width,height并且有效。第二，iframe像普通文本一样不会换行。**

**由此两点，可以判定：**

　　*iframe是inline-block元素*

　**iframes 提供了一个简单的方式把一个网站的内容嵌入到另一个网站中。**
　
## 慎重使用iframe

1. iframe的创建比其它包括scripts和css的 DOM 元素的创建慢了 1-2 个数量级。

   使用 iframe 的页面一般不会包含太多 iframe，所以创建 DOM 节点所花费的时间不会占很大的比重。
2. onload 事件以及连接池(connection pool)
 
   **Iframes 阻塞页面加载**

   及时触发 window 的 onload 事件是非常重要的。onload 事件触发使浏览器的 “忙” 指示器停止，告诉用户当前网页已经加载完毕。当 onload 事件加载延迟后，它给用户的感觉就是这个网页非常慢。
   
   window 的 onload 事件需要在所有 iframe 加载完毕后(包含里面的元素)才会触发。在 Safari 和 Chrome 里，通过 JavaScript 动态设置 iframe 的 SRC 可以避免这种阻塞情况。
3. 唯一的连接池

   浏览器只能开少量的连接到web服务器。比较老的浏览器，包含 Internet Explorer 6 & 7 和 Firefox 2，只能对一个域名(hostname)同时打开两个连接。这个数量的限制在新版本的浏览器中有所提高。
   
   有人可能希望 iframe 会有自己独立的连接池，但不是这样的。绝大部分浏览器，主页面和其中的 iframe 是共享这些连接的。这意味着 iframe 在加载资源时可能用光了所有的可用连接，从而阻塞了主页面资源的加载。如果 iframe 中的内容比主页面的内容更重要，这当然是很好的。但通常情况下，iframe 里的内容是没有主页面的内容重要的。
   
   美国前 10 大网站都使用了 iframe。大部分情况下，他们用它来加载广告。这是可以理解的，也是一种符合逻辑的解决方案，用一种简单的办法来加载广告服务。但请记住，iframe 会给你的页面性能带来冲击。只要可能，不要使用 iframe。当确实需要时，谨慎的使用他们。