# JS阻止冒泡和阻止浏览器默认行为

## 事件兼容

```
function myfn(e){ var evt = e ? e:window.event; }
```
## js停止冒泡

```
function myfn(e){window.event? window.event.cancelBubble = true : e.stopPropagation();}
```
## js阻止默认行为

```
function myfn(e){window.event? window.event.returnValue = false : e.preventDefault();}
```
