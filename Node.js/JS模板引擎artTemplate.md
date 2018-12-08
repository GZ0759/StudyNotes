# JS模板引擎---腾讯artTemplate的使用

常见的模板插件有 百度开发的(BaiduTemplate) ArtTemplate(腾讯开发) velocity.js(淘宝开发) Handlebars 等。 

我学习了一下ArtTemplate。简单总结一下学习的ArtTemplate的知识。

## 语法

art-template同时支持两种模板语法，标准语法和原始语法。 标准语法可以让模板更容易读写；原始语法具有强大的逻辑处理能力。

**标准语法：**

格式为{{ }}, 输出语法的例子：{{value}}、{{data.key}}、{{data[‘key’]}}、 {{a||b}}

**原始语法：** 

格式为{% %}的形式，输出语法的例子如{{= value}}、{{%= data.key%}}、{{%= data[‘key’]%}}、{{% = a||b%}}

刚才举的例子是输出语法的形式，也就是说art-template还有其他语法的形式，如条件、循环、变量等，具体可以查看[文档](<https://aui.github.io/art-template/docs/syntax.html>)。

## 核心方法

- 基于模板名渲染模板 
  template(filename, data);
- 将模板源代码编译成函数 
  template.compile(source, options);
-  将模板源代码编译成函数并立刻执行 
    template.render(source, data, options);

## 使用方法

用一个例子来实践art-template的使用方式。


**第一步：引入js文件**

```javascript
<script type="text/javascript" src="js/template-native.js"></script>1
```



**第二步：定义模板**

```javascript
<script id="test" type="text/html">
    <h1><%=title%></h1>
    <ul>
        <%for (var i =0;i<list.length;i++){%>
            <li>索引<%=i+1%>:<%=list[i]%></li>
        <% } %>
    </ul>
</script>12345678
```



**第三步：定义数据对象**

```javascript
<script>
        var data ={
    title:"artTemplate",
    isTemplate:"true",
    list:['读书', '听歌', '摄影', '旅行', '跑步', '爬山', '骑行']
};

    </script>12345678
```



**第四步 调用模板引擎提供的方法 ，找到并替换 。** 
注意：这一步骤是写在定义对象的`<script></script>`标签内的

```javascript
//        调用模板引擎提供的方法
     /*   参数1：模板的id
        参数2：对象（注意是  对象）*/
        var html = template('test',data);
        //找到并替换
        document.getElementById('content').innerHTML = html;
```



**具体例子演示：**

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>template使用</title>
    <!--导入引擎模板-->
    <script src="js/template-native.js"></script>
</head>
<body>
<div id="content"></div>
    <!--定义模板-->
     <script id="test" type="text/html">
         <h1><%=title%></h1>
         <ul>
             <%for (var i =0;i<list.length;i++){%>
                 <li>索引<%=i+1%>:<%=list[i]%></li>
             <% } %>
         </ul>
     </script>

  <!--定义对象-->
    <script>
        var data ={
            title:"artTemplate",
            isTemplate:"true",
            list:['读书', '听歌', '摄影', '旅行', '跑步', '爬山', '骑行']
        };
//        调用模板引擎提供的方法
     /*   参数1：模板的id
        参数2：对象（注意是  对象）*/
        var html = template('test',data);
        //找到并替换
        document.getElementById('content').innerHTML = html;
    </script>
```

结果： 

![模板渲染结果](F:\Study\前端资料\学习笔记\Node.js\img\模板渲染.png)

这要要说明一点，使用template()方法的时候，**参数2 一定要传入对象，对象！** 

如果数据是数组的话，就要包装成对象，举个例子。返回的是arrA 数组，可以这样包装

```javascript
var obj={
   data:arrA
};
```

**使用模板引擎对于从后台返回的json数据，显示到html页面中是非常方便的**。举个例子，用jQuery中的ajax发送请求。 关于ajax请求数据，我的博客中也有介绍。点击可查看：[jQuery中的ajax操作](http://blog.csdn.net/diligentkong/article/details/72851443)

```javascript
<!--导入js插件 模板插件-->
<script type="text/javascript" src="js/template-native.js"></script>
<!--导入jQuery-->
<script type="text/javascript" src="js/jquery.min.js"></script>

<!--定义模板-->
<script type="text/html" id="template">
    <%for (var i =1; i<items.length;i++){%>
    <div class="item">
        <a href="#" class="cover"><img src="<%=items[i].path%>"></a>
        <div class="bottom">
            <a href="#"><%=items[i].name%></a>
            <div class="rightBox">
                <span class="icon-heart">阅读：<%=items[i].star%></span>
                <span class="icon-commit">评论：<%=items[i].message%></span>
            </div>
        </div>
    </div>
    <%}%>

</script>
<!--自己的代码-->
<script type="text/javascript">
    $(function () {
        $(".getMore").click(function () {
            // 使用jQuery 发送ajax请求
            $.ajax({
                url:'artTem.php',
                type:'get',
                success:function (data) {
                    console.log(data);
                    // 转化为js对象 数组
                    var jsArr = JSON.parse(data);
                    // 包装为js对象
                    var obj ={
                        items:jsArr
                    };
                    // 调用模板引擎的方法，填充数据
                    var result = template('template',obj);

                    $('.container').append(result);
                }
            });
        });
    });
</script>
```

json数据

```javascript
[
  {
    "path":"images/1.jpg",
    "name":" 那阳光，灿烂到心底",
    "star":"6977",
    "message":"188"
  },{
  "path":"images/2.jpg",
  "name":" 守望者",
  "star":"9012",
  "message":"188"
},{
  "path":"images/3.jpg",
  "name":" 日落黄昏时",
  "star":"9012",
  "message":"188"
}
]
```

php页面

```php
<?php
   //读取json 并返回给浏览器
   echo file_get_contents('data/data.json');
?>
```



## 循环

**标准语法**

```jade
{{each target}}
    {{$index}} {{$value}}
{{/each}}
```

**原始语法**

```jade
<% for(var i = 0; i < target.length; i++){ %>
    <%= i %> <%= target[i] %>
<% } %>
```

1. `target` 支持 `array` 与 `object` 的迭代，其默认值为 `$data`。
2. `$value` 与 `$index` 可以自定义：`{{each target val key}}`。

## 模板继承

**标准语法**

```jade
{{extend './layout.art'}}
{{block 'head'}} ... {{/block}}
```

**原始语法**

```jade
<% extend('./layout.art') %>
<% block('head', function(){ %> ... <% }) %>
```

模板继承允许你构建一个包含你站点共同元素的基本模板“骨架”。范例：

```jade
<!--layout.art-->
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>{{block 'title'}}My Site{{/block}}</title>

    {{block 'head'}}
    <link rel="stylesheet" href="main.css">
    {{/block}}
</head>
<body>
    {{block 'content'}}{{/block}}
</body>
</html>


<!--index.art-->
{{extend './layout.art'}}

{{block 'title'}}{{title}}{{/block}}

{{block 'head'}}
    <link rel="stylesheet" href="custom.css">
{{/block}}

{{block 'content'}}
<p>This is just an awesome page.</p>
{{/block}}
```

渲染 index.art 后，将自动应用布局骨架。

## 子模板

**标准语法**

```jade
{{include './header.art'}}
{{include './header.art' data}}
```

**原始语法**

```jade
<% include('./header.art') %>
<% include('./header.art', data) %>
```

1. `data` 数默认值为 `$data`；标准语法不支持声明 `object` 与 `array`，只支持引用变量，而原始语法不受限制。
2. art-template 内建 HTML 压缩器，请避免书写 HTML 非正常闭合的子模板，否则开启压缩后标签可能会被意外“优化。