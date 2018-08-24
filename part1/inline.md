# 谈谈block，inline-block和inline
**其实理解这三个displa属性不难，主要是要知道三种标签的类型**
## 标签的类型
标签的类型有三种：

1. 块级标签

2. 内联标签

3. 内联块标签

### 块级标签

#### 特性：

1. 默认是父级100%的宽度

2. 适用于所有css样式
 
3. 块级标签独占一行

#### 常用的块级标签：

div标签，h标签，article标签，ul标签，ol标签，p标签

### 内联标签：

#### 特性：

1. 内容撑开宽度

2. 同属性的标签排在同一排
 
3. 不支持宽高，不支持上下margin和padding
 
4. 代码换行会有间隙，间隙的大小由父级的font-size决定
 
#### 常用的内联标签:

span标签,em标签，strong标签，a标签

### 内联块标签：

##### 特性：

1. 同属性的标签排在同一排

2. 内容撑开宽度

3. 支持css样式包括宽高设置，margin和padding设置

4. 代码换行被解析，间距的大小取决于父级的font-size设计的大小


**终于扯到本章的重点，block，inline，inline-block，利用他们实现标签类型的转换**

**块属性：display:block**

**内联属性：display:inline**

**块属性：display:inline-block**