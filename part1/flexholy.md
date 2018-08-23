# Flex布局实现圣杯布局

## Flex主要解决两个问题:

## 1. 元素位置

**元素的位置由6个容器属性和2个项目属性控制**

**6个容器属性**
1. flex-direction: 属性决定主轴的方向（即项目的排列方向）
2. flex-wrap: 如果一条轴线排不下，如何换行。
3. flex-flow: 属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
4. justify-content: 定义了项目在主轴上的对齐方式
5. align-items:属性定义项目在交叉轴上如何对齐。
6. align-content:定义了多根轴线的对齐方式

**2个项目属性**

1. order
2. align-self

## 2. 元素尺寸或自适应能力

**元素尺寸或自适应能力由三个项目属性控制**

1. flex-grow: 定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
2. flex-shrink:定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
3. flex- basis:定义了在分配多余空间之前，项目占据的主轴空间（main size）。

## 使用flex实现圣杯布局
页面从上到下为头部、中部、脚部；头部、脚部定高，不可伸缩；中部高度自适应。

中部三列式布局：左右两列定宽，不可伸缩；中间内容区自适应。

**代码**

css部分

```
<style type="text/css">
    *{
        box-sizing:content-box;/* 伸缩项目自动box-sizing:border-box，所以需调整为content-box */
        margin:0;
        padding:0;
    }

    body{
        display:flex;
        flex-direction:column;// 在flex模型中纵向显示 
    }

    header,footer{
        flex:0 0 50px;/* 头、脚尺寸固定，不放大、不缩小 */
        background:#3f3f3f;
    }

    .main{
        display:flex;

        /* 
        flex:1 == 1 1 auto：剩余空间放大比例(flex-grow)  空间不足缩小比例(flex-shrink)    分配多余空间之前项目占据的主轴空间(flex-basis)
        flex:1指的是：中部区域自由伸缩
        auto指的是项目本来大小，因未给main设置高度,main高度由子元素最高者决定，若子元素高度为0，则main高度为0
        块级元素未主动设置高度或未被子元素撑起高度，浏览器默认为块级元素分配高度为0。
        */
        flex:1;
    }

   .content{
        background:red;
        height:1000px;

        /* 
        横向中间内容区自适应，即使未指定宽度，但会分配宽度 
        块级元素未主动设置宽度或未被子元素撑起宽度，浏览器默认为块级元素分配宽度为可使用的全部宽度，比如全屏宽。
        */
        flex:1;
   }
   .left,.right{
        height:800px;
        background:blue;
        flex:0 0 100px;/* 左右两列固定宽 */
   }

   .left{
        order:-1;/* 让left居于左侧 */
   }

</style>
```
HTML代码

```
<body>
    <header></header>
    <div class="main">
        <div class="content"></div>
        <div class="left"></div>
        <div class="right"></div>
    </div>
    <footer></footer>
</body>
```

