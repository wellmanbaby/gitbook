# 请指出document.onload和document.ready两个事件的区别
页面加载完成有两种事件:

1. ready，表示文档结构已经加载完成（不包含图片等非文字媒体文件）

2. onload，指示页面包含图片等文件在内的所有元素都加载完成。

# document load和document DOMContentLoaded两个事件的区别
DOMContentLoaded: DOM解析完成即触发此事件，不等待styles, images等资源的加载

load：依赖的资源也已加载完成

DOMContentLoaded绑定到document，load绑定到window