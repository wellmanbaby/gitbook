# 流式布局的使用

**流式布局，又称等比缩放布局**

## 等比缩放布局
创建等比缩放布局就是将网页分成几栏，然后用比例而非像素设定它们的宽度。以下面两栏布局为例：

```
<!doctype html>
<html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>hangge.com</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
        }
 
        .leftColumn {
            width: 33.3%;
            float: left;
            background-color:yellow;
            height:300px;
        }
 
        .rightColumn {
            width: 66.7%;
            float: left;
            background-color:#7FFF9B;
            height:300px;
        }
    </style>
</head>
<body>
    <div class="leftColumn">
        left
    </div>
    <div class="rightColumn">
        right
    </div>
</body>
</html>
```
## 外边距的宽度设置
使用流式布局时，除了栏宽要使用百分比设置，外边距也必须使用百分比（不能使用固定像素值），确保栏宽+外边距=100%。
下面在左侧、右侧以及栏目间各添加2%的外边距：

```
.leftColumn {
    width: 31.3%;
    margin-left: 2%;
    margin-right: 2%;
    float: left;
    background-color:yellow;
    height:300px;
}
 
.rightColumn {
    width: 62.7%;
    margin-right: 2%;
    float: left;
    background-color:#7FFF9B;
    height:300px;
}
```
## 边框的设置
由于边框是添加在元素的外围，而且边框宽度不接受百分比值，直接在栏上设置固定宽度的边框会破坏流式布局。
解决办法是在等比缩放的栏里额外增加一个<div>元素，把边框设定到这个<div>元素上。

```
<!doctype html>
<html lang="en">
    <head>
    <meta charset="UTF-8">
    <title>hangge.com</title>
    <style>
        * {
            margin: 0px;
            padding: 0px;
        }
 
        body{
            background-color:#EFEFEF;
        }
 
        .leftColumn {
            width: 31.3%;
            margin-left: 2%;
            margin-right: 2%;
            float: left;
            background-color:yellow;   
        }
 
        .rightColumn {
            width: 62.7%;
            margin-right: 2%;
            float: left;
            background-color:#7FFF9B;
        }
 
        .colomnContent {
            border: 1px solid gray;
            height:130px;
        }
    </style>
</head>
<body>
    <div class="leftColumn">
        <div class="colomnContent">
            left
        </div>       
    </div>
    <div class="rightColumn">
        <div class="colomnContent">
            right
        </div>           
    </div>
</body>
</html>
```
