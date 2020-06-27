
[css教程](https://www.html.cn/book/css/properties/background/index.htm)
    
#### css语法

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明

    selector {declaration1; declaration2; ... declarationN }
    
#### 如何插入样式表

当读取到一个样式表时，浏览器会根据它来格式化 HTML 文档。插入样式表的方法有以下三种：

外部样式表(External style sheet)

    <head>
    <link rel="stylesheet" type="text/css" href="style.css">
    </head>
        
内部样式表(Internal style sheet)

    <head>
    <style>
    hr{color:sienna;}
    p{margin-left:20px;}
    body{background-image:url("images/back40.gif");}
    </style>
    </head>
        

内联样式(Inline style)

    <p style="color:sienna;margin-left:20px">HTML中文网</p>
    
    
样式继承规则

    如果某些属性在不同的样式表中被同样的选择器定义，那么属性值将从更具体的样式表中被继承过来。 
    
多重样式优先级

一般情况下，优先级如下：

    内联样式 >内部样式 >外部样式> 浏览器默认样式

注意：如果外部样式放在内部样式的后面，则外部样式将覆盖内部样式


#### 嵌套选择器

适用于选择器内部的选择器的样式,例：
    
    p{ }: 为所有的 p 元素指定一个样式
    
    .demo }: 为所有的class="demo" 的元素指定一个样式
    
    .demo p{ }: 为所有 class="demo" 元素内的 p 元素指定一个样式
    
    p.demo{ }: 为所有 class="demo" 的 p 元素指定一个样式