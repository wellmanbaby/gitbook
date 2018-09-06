[雪碧图](https://www.jianshu.com/p/879d190f3fc4)
[雪碧图高级](https://segmentfault.com/a/1190000007686042)
# 雪碧图
## 什么时候用雪碧图
1. 静态图片，不随用户信息的变化而变化

2. 小图片，图片容量较小

3. 加载量比较大

**一些大图不建议拼成雪碧图，一句话，加载量比较大的静态小图片用雪碧图**
## 雪碧图的作用
有效的减少http请求的数量，加速内容显示。

因为每请求一次，就会和服务器连接一次，建立链接是需要额外时间的。

## 雪碧图实现原理

**关键就是background-position**

## 实现方式

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>css盒子模型</title>
</head>
<style>
    *{
        margin: 0;
        padding: 0;
    }
    ul{
        list-style: none;
    };
    li h3{
        font-size: 14px;
        font-weight: 400;
    }
    li{
        display: block;
        height: 31px;
        line-height: 31px;
        overflow: hidden;
        border-bottom:1px solid #dedede
    }
    li i{
        background: url("../sidebar.png");
        width: 30px;
        height: 24px;
        float: left;
        margin: 3px 10px 0 0;
    }
    .cat{
      width: 150px;
      background: #f8f8f8;
      border: 1px solid #bbb;
    }
    .cat-1 i{
        background-position: 0 0;
    }
    .cat-2 i{
        background-position: 0 -24px; 
    }
    .cat-3 i{
        background-position: 0 -48px; 
    }
    .cat-4 i{
        background-position: 0 -72px; 
    }
    .cat-5 i{
        background-position: 0 -96px; 
    }
    .cat-6 i{
        background-position: 0 -120px; 
    }
    .cat-7 i{
        background-position: 0 -144px; 
    }
    .cat-8 i{
        background-position: 0 -168px; 
    }
    .cat-9 i{
        background-position: -40px 0; 
    }
</style>
<body>
   <div class="cat">
       <ul>
           <li class="cat-1">
                <i></i>
                <h3 style="font-size: 14px;font-weight: 400">服装内衣</h3>
           </li>
           <li class="cat-2">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">鞋包配饰</h3>
           </li>
           <li class="cat-3">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">运动户外</h3>
           </li>
          <li class="cat-4">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">珠宝手表</h3>
          </li>
          <li class="cat-5">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">手机数码</h3>
          </li>
          <li class="cat-6">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">办公家电脑</h3>
          </li>
          <li class="cat-7">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">护肤彩妆</h3>
          </li>
          <li class="cat-8">
               <i></i>
               <h3 style="font-size: 14px;font-weight: 400">母婴用品</h3>
         </li>
         <li class="cat-9">
                <i></i>
                <h3 style="font-size: 14px;font-weight: 400">其他分类</h3>
          </li>
       </ul>
   </div>
</body>
</html>
```
