> Node.JS-7天-黑马程序员  
> [在线视频](https://www.bilibili.com/video/BV1Ns411N7HU?t=1681)


<!-- TOC -->

- [一、Node.js介绍](#一nodejs介绍)
- [二、Node中的JavaScript](#二node中的javascript)
- [三、Web服务器开发](#三web服务器开发)
- [四、Node中的模块系统](#四node中的模块系统)
- [五、包管理器npm](#五包管理器npm)
- [六、开发框架Express](#六开发框架express)
- [七、异步编程](#七异步编程)
- [八、MongoDB](#八mongodb)
- [九、服务器启动工具nodemon](#九服务器启动工具nodemon)
- [十、path路径操作模块](#十path路径操作模块)
- [十一、全局成员](#十一全局成员)
- [十二、中间件](#十二中间件)
- [十三、服务器渲染与客户端渲染](#十三服务器渲染与客户端渲染)

<!-- /TOC -->

# 一、Node.js介绍

## 是什么？

Node.js是一个 JavaScript 运行时环境，使用谷歌V8渲染引擎构建的。意思就是说，JavaScript可以完全脱离浏览器运行，node.js可以解析和执行JavaScript代码。Node.js以 ECMAScript 为基本语法，但没有BOM和DOM操作，只是提供一些服务器级别的操作API，例如文件读写、网络服务构建、网络通信、http服务器等处理。

特点有事件驱动、非阻塞IO模型（异步）、轻量和高效。

拥有世界上最大的开源库生态系统npm，绝大多数JavaScript相关的包都存放在了npm上，这样做的目的是为了让那个开发人员更方便地区找到、下载和使用。

## 能做什么

主要功能是Web服务器后台、命令行工具。学习node.js的目的就是帮助大家打开服务器这个黑盒子。

命令行工具
- npm（node）
- git（C语言）
- hexo（node）

## 得到什么

学习到B/S编程模型，B/S是指基于browser（浏览器）与server（服务器）模式的应用。Node是学习改编程模型的一个比较好的工具。

学习到模块化编程、Node常用API、异步编程（回调函数）、Express开发框架、ECMAScript 6应用等等知识。

## 学习资料

1. [node.js官方网站](https://nodejs.org/)
2. [node.js中文网](http://nodejs.cn/)
3. [node.js 中文社区 CNODE](https://cnodejs.org/)

## Hello World

验证Node是否安装成功，可以打开shell或者通过执行cmd.exe命令行工具并输入`$ node --version`或`$ node -v`进行操作。

1. 创建编写JavaScript脚本文件
2. 打开终端，定位到脚本文件所属目录
3. 输入`node 文件名`执行对应的文件。

注意：文件名不要使用`node.js`来命名，文件中存储的都是二进制数据，可以通过toString方法将其转为正常的字符。

# 二、Node中的JavaScript

## ECMAScript

由于Node使用了V8，其实现很接近标准，通过还提供了一些标准之外的实用的附加功能。Node中没有BOM、DOM一说。Javascript类型可以简单分为基本类型和复杂类型两种，前者访问的是值，后者访问的是对值的引用，基本类型包括number、boolean、string、null和undefined，复杂类型包括array、function和object。

## 核心模块

Node为JavaScript提供了很多服务器级别的API，这些API绝大多数都被包装到了一个具名的核心模块中。例如文件操作的fs核心模块，http服务构建的http模块、path路径操作模块、os操作系统信息模块等等。核心模块在导入时无需添加路径名。

`var fs = require('fs')`

## 第三方模块

必须通过 npm 来下载才可以使用。

## 自定义模块

require是一个方法，它的作用有两个，一是用来加载文件模块并执行里面的代码，二是取得被加载文件模块导出的接口对象。用户自己编写的文件模块，相对路径必须加`./`，可以省略后缀名。在Node中，没有全局作用域，只有模块作用域。

要让模块暴露一个API成为require调用的返回值，就要依靠module和exports这两个全局变量。在默认情况下，每个模块都会暴露出一个空对象：exports。第一步，将需要被外部访问的成员挂载到这个exports中；第二步，取得挂载文件对象module并且通过它的exports对象访问内容。

## 事件

Node.js中的基础API之一就是EventEmitter。无论是在Node中还是在浏览器中，大量代码都依赖于所监听或者分发的事件。在这个API上定义了on、emit和removeListener方法，它以`process.EventEmitter`形式暴露出来。

> 所有能触发事件的对象都是 `EventEmitter` 类的实例。 这些对象开放了一个 `eventEmitter.on()` 函数，允许将一个或多个函数绑定到会被对象触发的命名事件上。 事件名称通常是驼峰式的字符串，但也可以使用任何有效的 JavaScript 属性名。

## Buffer

JavaScript语言没有读取或操作二进制数据流的机制，Node.js 中引入了 Buffer 类型使我们可以操作 TCP 流或文件流。Buffer 是全局的，所以使用的时候无需 `require()` 的方式来加载。

Buffer是一个表示固定内存分配的全局对象，也就是说，任何要放到缓存区中的字节数需要提前定下，它就好比是一个由八位字节元素组成的数组，可以有效地在JavaScript中表示二进制数据。该功能一部分作用是可以对数据进行编码转换，比如，base64就是一种仅用ASCAII字符书写二进制数据的方式。在Node中，绝大部分进行数据IO操作的API都用buffer来接收和返回数据。

# 三、Web服务器开发

## ip地址和端口号

ip地址是用来定位计算机的，端口号是用来定位具体的应用程序，一切需要联网通讯的软件都会占用一个端口号，端口号的范围从0~65536之间。在计算机中有一些默认的端口号，我们最好不要去使用，例如http服务的80端口，所以我们在开发过程中使用一些简单好记的就可以，例如3000、5000端口。我们可以同时开启多个服务，但一定要确保不同服务占用的端口号不一致才可以。意思是说，在一台计算机中，同一个端口号同一时间只能被一个程序占用。

## 服务器与客户端的连接

1. 请求，客户端发起请求。
2. 处理，服务器处理请求。
3. 响应，服务器将处理结果发送给客户端

## 请求头Content-type

服务器将每次响应的数据内容类型告诉客户端，不同的资源对应的 Content-Type 是不一样的，具体参照这个[网址](http://tool.oschina.net/commons)。对于文本类型的数据，最好都加上编码，目的是为了防止中文解析乱码问题。通过网络发送文件，发送的并不是文件，本质上来讲发送的是文件的内容，当浏览器收到服务器响应内容之后，就会根据 Content-Type 进行对应的解析处理。

## 处理网站中的静态资源

浏览器收到 HTML 响应的内容之后，就要开始从上到下依次解析，当在解析的过程中，如果发现 link 、 script 、img 、iframe 、video 、audio 等带有 src 或者 href （ link ）属性标签，即具有外链的资源时，浏览器会自动对这些资源发送新的请求。为了方便的统一处理这些静态资源，所以我们约定把所有的静态资源都存在在 public 目录中。可以通过代码灵活控制资源是否可以被用户访问到，从而完整静态资源的统一加载。统一处理方式：如果请求路径是以 `/public/` 开头的，则可以将请求路径当作文件路径进行直接读取。

## 获取表单提交数据

表单中需要提交的表单控件元素必须具有 name 属性，表单提交分为默认的提交行为和表单异步提交两种方式。 action 就是表单提交的地址，说白了就是请求的 url 地址；metho请求方法有 get 和 post 方法。一般请求包含着复杂的查询字符串，这时候可以通过 node 的 `url.parse` 方法将路径解析为一个方便操作的对象，第二个参数为 true 表示直接 查询字符串转为对象，通过 query 属性来访问即可。

## 软件版本号

1. 软件版本阶段说明

- Base版: 此版本表示该软件仅仅是一个假页面链接，通常包括所有的功能和页面布局，但是页面中的功能都没有做完整的实现，只是做为整体网站的一个基础架构。
- Alpha版: 此版本表示该软件在此阶段主要是以实现软件功能为主，通常只在软件开发者内部交流，一般而言，该版本软件的Bug较多，需要继续修改。
- Beta版: 该版本相对于α版已有了很大的改进，消除了严重的错误，但还是存在着一些缺陷，需要经过多次测试来进一步消除，此版本主要的修改对像是软件的UI。
- RC版: 该版本已经相当成熟了，基本上不存在导致错误的BUG，与即将发行的正式版相差无几。
- Release版: 该版本意味“最终版本”，在前面版本的一系列测试版之后，终归会有一个正式版本，是最终交付用户使用的一个版本。该版本有时也称为标准版。一般情况下，Release不会以单词形式出现在软件封面上，取而代之的是符号（Ｒ）。

2.  版本命名规范

软件版本号由四部分组成，第一个1为主版本号，第二个1为子版本号，第三个1为阶段版本号，第四部分为日期版本号加希腊字母版本号，希腊字母版本号共有5种，分别为：base、alpha、beta、RC、release。例如：1.1.1.051021_beta。版本号定修改规则如下

- 主版本号（1）：当功能模块有较大的变动，比如增加多个模块或者整体架构发生变化。此版本号由项目决定是否修改。
- 子版本号（1）：当功能有一定的增加或变化，比如增加了对权限控制、增加自定义视图等功能。此版本号由项目决定是否修改。
- 阶段版本号（1）：一般是 Bug 修复或是一些小的变动，要经常发布修订版，时间间隔不限，修复一个严重的bug即可发布一个修订版。此版本号由项目经理决定是否修改。
- 日期版本号（051021）:用于记录修改项目的当前日期，每天对项目的修改都需要更改日期版本号。此版本号由开发人员决定是否修改。
- 希腊字母版本号（beta）:此版本号用于标注当前版本的软件处于哪个开发阶段，当软件进入到另一个阶段时需要修改此版本号。此版本号由项目决定是否修改。

## Node.js重定向

重定向的准则;

- 给客户发送301响应代码，告诉客户：资源已经移到另一个位置。其中 301 是永久重定向， 302 是临时重定向。
- 发送一个位置头（Location Header）告诉客户重定向到哪里。

```javascript
var http = require('http');

http.createServer(function (req, res) {
  res.writeHead(301, {
    'Location': 'http://www.homestarrunner.com/sbsite/'
  });
  res.end();
  // 其它方法
  // res.statusCode = 302 
  // res.setHeader('location','/')
  // res.end()
}).listen(3000, "127.0.0.1");
console.log('Server running at http://127.0.0.1:3000/');
```

# 四、Node中的模块系统

## 什么是模块化

我们把每一个 `.js` 文件都视为一个模块，模块内部有自己的作用域，不会影响到全局，防止出现命名冲突的情况。并且，我们约定一些关键词来进行依赖声明和 API 暴露，解决繁琐的文件依赖问题。JavaScript本身不支持模块化。在js中有两种用于实现模块的方法：对象字面量表示法、 Module 模式。有几种用于实现模块的规范，括号内为对应的脚本加载器： CMD（SeaJS） 、AMD（RequireJS）、 CommonJS（NodeJS）、 ES6 Module （ECMAScript 2015）。

## CommonJS模块规范

CommonJS对模块的定义十分简单，主要分为模块的引用、模块定义和模块标识三个部分。

- 模块引用的示例代码是：`var math = require('math');`  
- 在模块中，上下文提供 `require()` 来引入外部模块。对应引入的功能，上下文提供了 exports 对象用于导出当前模块的方法或者变量，并且它是唯一导出的出口。在模块中，还存在一个 module 对象，它代表模块自身，而 exports 是 module 的属性，上下文提供的 exports 对象实际上是 module.exports 的引用。在 Node 中，一个文件就是一个模块，将方法挂载在 exports 对象上作为属性即可定义导出的方式。
- 模块标识就是传递给 `require()` 方法的参数，它必须是符合小驼峰命名的字符串，或者 "./" 或 "../" 开头的相对路径，或者绝对路径。它可以没有文件名后缀 .js 。

Node的模块实现。在Node中引入模块，需要大概经历如下三个步骤：路径分析、文件定位和编译执行。

优先从缓存加载。和浏览器会缓存静态js文件一样，Node也会对引入的模块进行缓存，不同的是浏览器缓存的是文件，Node缓存的是编译执行之后的对象。简言之，已经加载过的模块不会重复加载，如果再次加载一般还是只是取得接口对象。这样避免重复加载会提高加载效率。另外，不论是核心模块还是文件模块， `require()` 对相同模块的二次加载一律采用缓存优先的方式，这是第一优先级的，核心模块缓存检查先于文件模块的缓存检查。
 
模块标识符分析与文件定位。模块标识符在Node中主要分为以下几类：
 
- 核心模块。核心模块优先级仅次于缓存加载，因此无法加载一个和核心模块标识符相同的自定义模块。
- 相对路径文件模块。以 "./" 、 "../" 开头的标识符，分别表示当前目录和上一级目录，不可以省略。读取文件可以直接用文件名作为相对路径的开头，但是读取文件模块不行。
- 绝对路径文件模块。以 "/" 开始或直接使用 "D:/Baidu/BaiduPinyin/a.js" 的标识符，前者表示当前文件模块所属的磁盘根目录。另外，无论是绝对路径还是相对路径的文件模块， `require()` 方法会将路径转为真实路径，并以真实路径作为索引，并将编译执行后的结果存放到缓存中。
- 非路径形式的文件模块，又称作第三方模块或者自定义模块。第三方模块是指非核心模块，也不是路径形式的标识符。它是一种特殊的文件模块，可能是一个文件或者包的形式，如自定义的 connect 模块。

> 注意，因为第三方模块也是通过直接引用包名进行引入，所以第三方模块一定不能与核心模块重名。路径查找规律一般是先找到当前文件所处目录的 node_modules 目录，然后查找该包名文件下的 package.json 文件， 通过该文件里面的 main 属性找到入口模块，然后加载使用这个第三方包，实际上最终加载的还是文件。如果 package.json 文件不存在或者没有 main 指定的入口模块或者 main 属性指定文件名错误， Node 会将 index 当作默认文件名，然后一次查找 index.js 、index.json 、index.node 。如果在目录分析的过程中没有定位成功任何文件，则自定义模块进入下一个模块路径进行查找，即进入其上一级目录的 node_modules 目录查找，如果直到当前磁盘根目录还没找到，则抛出查找失败的异常。当前文件的目录越深，模块查找耗时越多。
 
模块编译。每一个编译成功的模块都会将其文件路径作为索引缓存在 Module._cache 对象上。对于不同扩展名，其载入方法也有所不同：
 
- `.js` 通过fs模块同步读取文件后编译执行。
- `.node` 这是C/C++编写的扩展文件，通过`dlopen()`方法加载最后编译生成的文件
- `.json` 同过fs模块同步读取文件后，用`JSON.pares()`解析返回结果
- 其他 当作.js

# 五、包管理器npm

## npm是什么

NPM的全称是Node Package Manager，是随同NodeJS一起安装的包管理和分发工具，它很方便让JavaScript开发者下载、安装、上传以及管理已经安装的包。pm 由三个独立的部分组成：网站、注册表（registry）、命令行工具 （CLI） 。网站是开发者查找包（package）、设置参数以及管理 npm 使用体验的主要途径。注册表是一个巨大的数据库，保存了每个包（package）的信息。 CLI 通过命令行或终端运行。开发者通过 CLI 与 npm 打交道。

## npm 5 变化

- 使用`npm install xxx`命令安装模块时，不再需要 `--save` 选项，会自动将模块依赖信息保存到 package.json 文件；
- 安装模块操作（改变 node_modules 文件夹内容）会生成或更新 package-lock.json 文件
- 发布的模块不会包含 package-lock.json 文件
- 如果手动修改了 package.json 文件中已有模块的版本，直接执行`npm install`不会安装新指定的版本，只能通过`npm install xxx@yy`更新

重新安装模块之所以快，是因为 package-lock.json 文件中已经记录了整个 node_modules 文件夹的树状结构，甚至连模块的下载地址都记录了，再重新安装的时候只需要直接下载文件即可。

## 命令行常用命令

`npm install` 安装模块

```shell
alias: npm i
common options: [-S|--save|-D|--save-dev|-O|--save-optional] [-E|--save-exact] [--dry-run]

# -S, --save 安装包信息将加入到dependencies（生产阶段的依赖）
# -D, --save-dev 安装包信息将加入到devDependencies（开发阶段的依赖），所以开发阶段一般使用它。
# -O, --save-optional 安装包信息将加入到optionalDependencies（可选阶段的依赖）
# -E, --save-exact 精确安装指定模块版本
```

`npm uninstall` 卸载模块 

`npm update` 更新模块

`npm outdated` 检查模块是否已经过时

`npm ls` 查看安装的模块

`npm init` 在项目中引导创建一个 package.json 文件，`-Y` 表示跳过向导

`npm help` 查看某条命令的详细帮助。系统在默认的浏览器或者默认的编辑器中打开本地nodejs安装包的网页文件，如果是 `--help` 则是在命令行显示。

`npm root` 查看包的安装路径

`npm config` 管理npm的配置路径

`npm cache` 管理模块的缓存。最常用命令无非清除 npm 本地缓存`npm cache clean `

`npm start` 启动模块。该命令写在package.json文件scripts的start字段中，可以自定义命令来配置一个服务器环境和安装一系列的必要程序

`npm stop` 停止模块

`npm restart` 重新启动模块

`npm test` 测试模块。该命令写在package.json文件scripts的test字段中，可以自定义该命令来执行一些操作

`npm version` 查看模块版本

`npm view` 查看模块的注册信息

`npm adduser` 用户登录

`npm publish` 发布模块

`npm access` 在发布的包上设置访问级别

## package.json的语法

npm会根据包内容设置一些默认值。

- `"scripts": {"start": "node server.js"}`
如果包的根目录有`server.js`文件，npm会默认将`start`命令设置为`node server.js`。

- `"scripts":{"preinstall": "node-waf clean || true; node-waf configure build"}`
如果包的根目录有`wscript`文件，npm会默认将`preinstall`命令用node-waf进行编译。

- `"scripts":{"preinstall": "node-gyp rebuild"}`
如果包的根目录有`binding.gyp`文件，npm会默认将`preinstall`命令用node-gyp进行编译。

- `"contributors": [...]`
如果包的根目录有`AUTHORS`文件，npm会默认逐行按`Name <email> (url)`格式处理，邮箱和url是可选的。#号和空格开头的行会被忽略。

package.json 文件至少要有两部分内容：“name” 、“version” 。其他内容：

- description：描述信息，有助于搜索；
- main: 入口文件，一般都是 index.js；
- scripts：支持的脚本，默认是一个空的 test；
- keywords：关键字，有助于在人们使用 npm search 搜索时发现你的项目；
- author：作者信息；
- license：默认是 MIT；
- bugs：当前项目的一些错误信息，如果有的话；我们需要在 package.json 文件中指定项目依赖的包，这样别人在拿到这个项目时才可以使用 npm install 下载。
- 包有两种依赖方式：dependencies：在生产环境中需要用到的依赖；devDependencies：在开发、测试环境中用到的依赖。

**name**

在package.json中最重要的就是name和version字段。他们都是必须的，如果没有就无法install。name和version一起组成的标识在假设中是唯一的。改变包应该同时改变version。

name是这个东西的名字。注意：

- 不要把node或者js放在名字中。因为你写了package.json它就被假定成为了js，不过你可以用"engine"字段指定一个引擎（见后文）。
- 这个名字会作为在URL的一部分、命令行的参数或者文件夹的名字。任何non-url-safe的字符都是不能用的。
- 这个名字可能会作为参数被传入`require()`，所以它应该比较短，但也要意义清晰。
- 在你爱上你的名字之前，你可能要去npm registry查看一下这个名字是否已经被使用了。

**version**

version必须能被node-semver解析，它被包在npm的依赖中。（要自己用可以执行npm install semver）

**description**

放简介，字符串，方便在`npm search`中搜索

**keywords**

关键字，数组、字符串，方便在`npm search`中搜索

**bugs**

你项目的提交问题的url和（或）邮件地址

```
{
"url" : "http://github.com/owner/project/issues", 
"email" : "project@hostname.com"
}
```

**license**

你应该要指定一个许可证，让人知道使用的权利和限制的。

最简单的方法是，假如你用一个像BSD或者MIT这样通用的许可证，就只需要指定一个许可证的名字，像这样：

```
{ "license" : "BSD" }
```

如果你又更复杂的许可条件，或者想要提供给更多地细节，可以这样:

```
"licenses" : [
  { "type" : "MyLicense"
  , "url" : "http://github.com/owner/project/path/to/license"
  }
]
```

**repository**

指定你的代码存放的地方。这个对希望贡献的人有帮助。如果git仓库在github上，那么`npm docs`命令能找到你。

这样做：

```
"repository" :
  { "type" : "git"
  , "url" : "http://github.com/isaacs/npm.git"
  }

"repository" :
  { "type" : "svn"
  , "url" : "http://v8.googlecode.com/svn/trunk/"
  }
```



URL应该是公开的（即便是只读的）能直接被未经过修改的版本控制程序处理的url。不应该是一个html的项目页面。因为它是给计算机看的。

**scripts**

“scripts”是一个由脚本命令组成的hash对象，他们在包不同的生命周期中被执行。key是生命周期事件，value是要运行的命令。

**config**

"config" hash可以用来配置用于包脚本中的跨版本参数。在实例中，如果一个包有下面的配置：

```
{
"name" : "foo",
"config" : { "port" : "8080" } 
}
```

然后有一个“start”命令引用了`npm_package_config_port`环境变量，用户可以通过`npm config set foo:port 8001`来重写他。

**dependencies**

依赖是给一组包名指定版本范围的一个hash。这个版本范围是一个由一个或多个空格分隔的字符串。依赖还可以用tarball或者`git URL`。

请不要将测试或过渡性的依赖放在`dependencies`hash中。见下文的`devDependencies`

- `version` 必须完全和`version`一致
- `>version` 必须比`version`大
- `>=version` 同上
- `<version` 同上
- `<=version` 同上
- `~version` 大约一样
- `1.2.x` 1.2.0, 1.2.1, 等，但不包括1.3.0
- `http://...` 见下文'依赖URL'
- `*` 所有
- `""` 空，同`*`
- `version1 - version2` 同 `>=version1 <=version2`.
- `range1 || range2` 二选一。
- `git...` 见下文'依赖Git URL'
- `user/repo` 见下文'GitHub URLs'

比如下面都是合法的：

```json
{ "dependencies" :
  { "foo" : "1.0.0 - 2.9999.9999"
  , "bar" : ">=1.0.2 <2.1.2"
  , "baz" : ">1.0.2 <=2.3.4"
  , "boo" : "2.0.1"
  , "qux" : "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0"
  , "asd" : "http://asdf.com/asdf.tar.gz"
  , "til" : "~1.2"
  , "elf" : "~1.2.3"
  , "two" : "2.x"
  , "thr" : "3.3.x"
  }
}
```

**devDependencies**

如果有人要使用你的模块，那么他们可能不需要你开发使用的外部测试或者文档框架。

在这种情况下，最好将这些附属的项目列在`devDependencies`中。

这些东西会在执行`npm link`或者`npm install`的时候初始化，并可以像其他npm配置参数一样管理。

对于非特定平台的构建步骤，比如需要编译CoffeeScript，可以用`prepublish`脚本去实现，并把它依赖的包放在devDependency中。（译者注：prepublish定义了在执行`npm publish`的时候先行执行的脚本）

比如：

```json
{
  "name": "ethopia-waza",
  "description": "a delightfully fruity coffee varietal",
  "version": "1.2.3",
  "devDependencies": {
    "coffee-script": "~1.6.3"
  },
  "scripts": {
    "prepublish": "coffee -o lib/ -c src/waza.coffee"
  },
  "main": "lib/waza.js"
}
```

`prepublish`脚本会在publishing前运行，这样用户就不用自己去require来编译就能使用。并且在开发模式中（比如本地运行`npm install`）会运行这个脚本以便更好地测试。

# 六、开发框架Express

## Express 简介

Express 是一个简洁而灵活的 node.js Web应用框架，提供了一系列强大特性帮助你创建各种 Web 应用，和丰富的 HTTP 工具。使用 Express 可以快速地搭建一个完整功能的网站。Express 框架核心特性：

- 可以设置中间件来响应 HTTP 请求。
- 定义了路由表用于执行不同的 HTTP 请求动作。
- 可以通过向模板传递参数来动态渲染 HTML 页面。

## 安装 Express

安装 Express 并将其保存到依赖列表中：

```shell
npm install express --save
```

以上命令会将 Express 框架安装在当前目录的 node_modules 目录中， node_modules 目录下会自动创建 express 目录。以下几个重要的模块是需要与 express 框架一起安装的：

- body-parser - node.js 中间件，用于处理 JSON, Raw, Text 和 URL 编码的数据。
- cookie-parser - 这就是一个解析Cookie的工具。通过req.cookies可以取到传过来的cookie，并把它们转成对象。
- multer - node.js 中间件，用于处理 enctype="multipart/form-data"（设置表单的MIME编码）的表单数据。

## 第一个 Express 框架实例

接下来我们使用 Express 框架来输出 "Hello World"。以下实例中我们引入了 express 模块，并在客户端发起请求后，响应 "Hello World" 字符串。创建 express_demo.js 文件，代码如下所示：

```javascript
//express_demo.js 文件
var express = require('express');
var app = express();
app.get('/', function (req, res) {
  res.send('Hello World');
})
var server = app.listen(8081, function () {
  var host = server.address().address
  var port = server.address().port
  console.log("应用实例，访问地址为 http://%s:%s", host, port)
})
```

执行以下代码：

```shell
# 应用实例，访问地址为 http://0.0.0.0:8081
node express_demo.js 
```

## 请求和响应

Express 应用使用回调函数的参数（ request 对象和 response 对象）来处理请求和响应的数据。

```javascript
app.get('/', function (req, res) {
   // --
})
```

- request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。
- response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。

## 基本路由

路由是指如何定义应用的端点（URIs）以及如何响应客户端的请求。路由是由一个 URI、HTTP 请求（GET、POST等）和若干个句柄组成，它的结构如下： `app.METHOD(path, [callback...], callback)`， app 是 express对象的一个实例， METHOD 是一个 HTTP 请求方法， path 是服务器上的路径， callback 是当路由匹配时要执行的函数。

```javascript
//  GET 请求
//  GET - 从指定的资源请求数据。
app.get('/', function (req, res) {
   console.log("主页 GET 请求");
   res.send('Hello GET');
})
 
//  POST 请求
//  POST - 向指定的资源提交要被处理的数据
app.post('/', function (req, res) {
   console.log("主页 POST 请求");
   res.send('Hello POST');
})
```

## 托管静态文件

通过 Express 内置的 `express.static` 可以方便地托管静态文件，例如图片、CSS、JavaScript 文件等。将静态资源文件所在的目录作为参数传递给 `express.static` 中间件就可以提供静态资源文件的访问了。例如，假设在 `public` 目录放置了图片、CSS 和 JavaScript 文件，你就可以：

```javascript
app.use(express.static('public'));

//  现在，`public` 目录下面的文件就可以访问了。
//  http://localhost:3000/images/kitten.jpg
//  http://localhost:3000/css/style.css
```

所有文件的路径都是相对于存放目录的，因此，存放静态文件的目录名不会出现在 URL 中。如果你的静态资源存放在多个目录下面，你可以多次调用 `express.static` 中间件。访问静态资源文件时，`express.static` 中间件会根据目录添加的顺序查找所需的文件。

如果你希望所有通过 `express.static` 访问的文件都存放在一个“虚拟（virtual）”目录（即目录根本不存在）下面，可以通过为静态资源目录指定一个挂载路径的方式来实现，如下所示：

```javascript
app.use('/static', express.static('public'));

//  现在，你就爱可以通过带有 “/static” 前缀的地址来访问 `public` 目录下面的文件了。
//  http://localhost:3000/static/images/kitten.jpg
//  http://localhost:3000/static/css/style.css
```

## 在 Express 中使用模板引擎

需要在应用中进行如下设置才能让 Express 渲染模板文件：

- views, 放模板文件的目录，比如：`app.set('views', './views')`
- view engine, 模板引擎，比如：`app.set('view engine', 'jade')`

然后安装相应的模板引擎 npm 软件包。

```sh
# 安装 jade 模板引擎
$ npm install jade --save

# 也可以安装 art-template 模板引擎
npm install --save art-template
npm install --save express-art-template
```

和 Express 兼容的模板引擎，比如 Jade，通过 `res.render()` 调用其导出方法 `__express(filePath, options, callback)` 渲染模板。有一些模板引擎不遵循这种约定，Consolidate.js 能将 Node 中所有流行的模板引擎映射为这种约定，这样就可以和 Express 无缝衔接。一旦 `view engine` 设置成功，就不需要显式指定引擎，或者在应用中加载模板引擎模块，Express 已经在内部加载，如下所示。

```javascript
app.set('view engine', 'jade');
```

在 `views` 目录下生成名为 `index.jade` 的 Jade 模板文件，内容如下：

```jade
html
  head
    title!= title
  body
    h1!= message
```

然后创建一个路由渲染 `index.jade` 文件。如果没有设置 `view engine`，您需要指明视图文件的后缀，否则就会遗漏它。

```javascript
app.get('/', function (req, res) {
  res.render('index', { title: 'Hey', message: 'Hello there!'});
});
```

此时向主页发送请求，“index.jade” 会被渲染为 HTML。

## 重定向

```
res.redirect（[status，] path）
```

path使用指定的 HTTP 状态代码重定向到指定的URL status。如果未指定 status ，则状态代码默认为“302”Found“。

```javascript
// res.statusCode = 302 ;
// res.setHeader('Location', '/foo/bar')
res.redirect('/foo/bar');

res.redirect('http://example.com');
res.redirect(301, 'http://example.com');
res.redirect('../login');
```

## 获取表单GET/POST数据

Express内置了一个API，可以直接通过 `req.query` 来获取。但没有内置获取 POST 请求体的 API ，需要使用第三方包： body-parser 。

安装

```shell
$ npm install body-parser
```

配置和使用

```JavaScript
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

// 配置 body-parser ，完成后在 req 请求中多一个 body 属性，表示请求体数据。
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())

app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
```

## 路由模块的提取

路由模块 router.js 的作用是处理路由，根据不同的请求方法和请求路径设置处理的请求处理函数。模块职责要单一，划分模块是为了增强项目代码可维护性，提高开发效率。一般路由容器的挂载要在配置之后。

第一种方法，但是不建议用，因为将执行主代码变成 router.js 文件了。

```javascript
// app.js 主要代码
var express = require('express')
var app = express()
moudule.exports = app
app.listen(3000)

// router.js 主要代码
var app = require('./app')
app.get('/', function (req,res){
  res.send('hello world')
})
```

第二种方法，通过在 router.js 中导出一个接受参数的函数。

```js
// app.js 主要代码
var express = require('express')
var app = express()
var router = require('./router')
router(app)
app.listen(3000)
// router.js 主要代码
moudule.exports = function (app) {
    app.get('/', function (req,res){
    res.send('hello world')
	})
}
```

第三种方法，在 express 中有更好的方式，不用封装函数。

```js
// app.js 主要代码
var express = require('express')
var router = require('./router')  // 4.把 router 路由容器导入
var app = express()
app.use(router)  // 5.把路由容器挂载到 app 服务中
app.listen(3000)

// router.js 主要代码
var express = require('express')
var router = express.Router()  // 1.创建一个路由容器
router.get('/', function (req,res){  // 2.把路由都挂载到 router 路由容器中
  res.send('hello world')
})
module.exports = router  // 3.把 router 路由容器导出
```

## 数据操作文件API模块

文件 student.js 的职责是操作文件中的数据，只处理数据，不关心业务。

1. 获取所有学生列表

```javascript
// students.js
var fs = require('fs')
exports.find = function (callback) {
  fs.readFile(dbPath,'utf-8',function (err,data) {
    if (err){
      return callback(err)
    }
    callback(null,JSON.parse(data).students)
  })
}
// router.js
var Student = require('./student')
router.get('/students',function (req,res) {
  Student.find(function (err,students) {
    if (err) {
      return res.status(500).send('Server error')
    }
    res.render('index.html',{
      students:students
    })
	})
})
```

2. 根据 id 获取学生的信息

```js
// students.js
exports.findById = function (id, callback) {
  fs.readFile(dbPath,'utf-8',function (err,data) {
    if (err){
      return callback(err)
    }
    var students = JSON.parse(data).students
    var ret = students.find(function (item) {
      return item.id === parseInt(id)
    })
    callback(null, ret)
  })
}
// router.js
Student.findById(parseInt(req.query.id),function(err,student)) {
  if (err) {
    return res.status(500).send('Server error')
  }
	res.render('edit.html', {
    student:student
	})
}
```

3. 添加保存学生

```js
// students.js
var fs = require('fs')
exports.save = function (student,callback) {
  fs.readFile(dbPath,'utf-8',function (err,data) {
    if (err){
      return callback(err)
    }
    var students = JSON.parse(data).students
    student.id = students[students.length - 1].id + 1  // 处理学生 id 问题
    students.push(student)
    var fileData = JSON.stringfy({  // 先把数组传递进去变成对象，再把对象数据转换为字符串
      students:students
    })
    fs.writeFile(dbPath,fileData,function(err){  // 把字符串保存到文件中
      if (err) {
        return callback(err)
      }
      callback(null)
    })
  })
}
// router.js
var Student = require('./student')
router.post('/students/new', fucntion (req,res){
  Student.save(req.body,function (err,students) {
    if (err) {
      return res.status(500).send('Server error')
    }
    res.redirect('/students')
  })	
})
```

4. 更新学生

```js
// students.js
exports.update = function (student, callback){
  fs.readFile(dbPath, 'utf-8', function(err,data){
    if (err) {
      return callback(err)
    }
    var students = JSON.parse(data).students
    student.id = parseInt(student.id)
    var stu = students.find(function(item){  // 遍历数组，找到 id 符合的数组成员（对象） 
      return item.id === student.id
    })
    for (var key in student){  // 遍历拷贝对象
      stu[key] = student[key]   // 将拷贝对象的属性值传递给符合要求的 id 符合的数组成员（对象）
    }
    var fileData = JSON.stringify({
      students:students
    })
    fs.writeFile(dbPath,fileData,function(err){
      if (err){
        return callback(err) 
      }
      callback(null)
    })
  })
}
// router.js
var Student = require('./student')
router.post('/students/edit', fucntion (req,res){
  Student.update(req.body,function (err) {
    if (err) {
      return res.status(500).send('Server error')
    }
    res.redirect('/students')
  })	
})
```

5. 删除学生

```js
// students.js
exports.delete = function (id, callback) {
  fs.readFile(dbPath,'utf-8',function (err,data) {
    if (err){
      return callback(err)
    }
    var students = JSON.parse(data).students
    var deleteId = students.findIndex(function (item) {
      return item.id === parseInt(id)
    })
    students.splice(deleteId, 1)
    var fileData = JSON.stringify({
      students:students
    })
    fs.writeFile(dbPath, fileData, function(err) {
      if (err) {
        return callback(err)
      }
      callback(null)
    })
  })
}
// router.js
var Student = require('./student')
Student.delete(id, function (err) {
  if (err) {
    return res.status(500).send('Server error')
  }
  res.redirect('/students')
})
```

# 七、异步编程

## 回调函数

Node.js 通过普及回调函数来改进异步编程模型，回调模式与事件模型类似，异步代码都会在未来的某个时间点执行，二者的区别是回调模式中被调用的函数是作为参数传入的。回调函数在 Javascript 中非常常见，一般是需要在一个耗时操作之后执行某个操作时可以使用回调函数。

```javascript
// 一个定时器
function timer(time, callback){
  setTimeout(function(){
    callback();
  }, time);
}

timer(3000, function(){
  // 可以执行自己的操作
  console.log(123);
})
```

基于原生 XMLHTTPRequest 封装 get 方法

```javascript
function get(url, callback) {
  var oReq = new XMLHttpRequest()
  // 当请求加载成功之后要调用指定的函数
  oReq.onload = function () {
    // 我现在需要得到这里的 oReq.responseText
    callback(oReq.responseText)
  }
  oReq.open("get", url, true)
  oReq.send()
}
get('data.json', function (data) {
  console.log(data)
})
```

## Promise

Promise 相当于异步操作结果的占位符，它不会去订阅一个事件，也不会传递一个回调函数给目标函数，而是让函数返回一个表示异步读取操作的 Promise 对象，未来对这个对象的操作完全取决于 Promise 的声明周期。注意：Promise 本身不是异步的，内部封装的才是异步任务。

每个 Promise 都会经历一个短暂的声明周期：先是处于进行中（pending）的状态，此时操作尚未完成，一旦异步操作结束，就会进入 Fulfilled（ 异步操作完成）或 Rejected （操作失败）两个状态中的一个。内部属性 `[[PromiseState]]` 被用来表示 Promise 的 3 种状态 ：“pending” 、“fulfilled”及“rejected” 。 这个属性不暴露在 Promise 对象上 ， 所以不能以编程的方式检测 Promise 的状态 ， 只有当 Promise 的状态改变时， 通过 `then()` 方法来采取特定的行动 。 

> 一旦状态改变就不会再变，任何时候都可以得到这个结果。 Promise 对象的状态改变只有两种可能：从 Pending 变为 Fulfilled 和从 Pending 变为 Rejected。只要这两种情况发生，状态就凝固了，不会再变，而是一直保持这个结果，这时就称为 Resolved （己定型） 。 就算改变己经发生，再对 Promise 对象添加回调函数，也会立即得到这个结果。这与事件 （event）完全不同。 事件的特点是，如果错过了它，再去监昕是得不到结果的。为了行文方便，本章后面的 Resolved 统一指 Fulfilled 状态，不包含 Rejected 状态 。  

ES6 规定， Promise 对象是一个构造函数，用来生成 Promise 实例，所以可以给某个变量赋予 Promise 实例对象。但是如果想要某个函数拥有 promise 功能，只需让其返回一个 promise 即可。

```javascript
const myFirstPromise = new Promise((resolve, reject) => {
  // 做一些异步操作，最终会调用下面两者之一:
  // resolve(someValue); // fulfilled
  // reject("failure reason"); // rejected
});

function myAsyncFunction(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
};
```

Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject 。 它们是两个函数，由 JavaScript 引擎提供，不用自己部署。 resolve 函数的作用是，将 Promise 对象的状态从“未完成”变为“成功”（即从 Pending 变为 Resolved ），在异步操作成功时调用，并将异步操作的结果作为参数传递出去： reject 函数的作用是，将 Promise 对象的状态从“未完成”变为“失败”（即从 Pending 变为 Rejected）, 在异步操作失败时调用，并将异步操作报出的错误作为参数传递出去 。  

所有 Promise 都有 `then()` 方法。`then()` 方法可以接受两个回调函数作为参数。第一个回调函数是 Promise 对象的状态变为 Resolved 时调用， 第二个回调函数是 Promise 对象的状态变为 Rejected 时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受 Promise 对象传出的值作为参数。`then(null, handleRejection)` 调用的简写形式是 `catch(handleRejection)`。  

```javascript
// Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject 
let p1 = new Promise(function(resolve, reject) {
  resolve("Success!");
  // or
  // reject ("Error!");
});

// then () 方法可以接受两个回调函数作为参数 
p1.then(function(value) {
  console.log(value); // Success! 
}, function(reason) {
  console.log(reason); // Error! 
});
```

串联 Promise 。每次调用 `then()` 方法或 `catch()` 方法时实际上创建并返回了另 一个 Promise，只有当第一个 Promise 完成或被拒绝后 ， 第二个才会被解决。Promise 链的另 一个重要特性是可以给下游 Promise 传递数据，我们己经看到了从执行器 `resolve()` 处理程序到 Promise 完成处理程序的数据传递过程，如果在完成处理程序中指定一个返回值，则可以沿着这条链继续传递数据 。   

```javascript
let p1 = new Promise(function(resolve, reject) {
    resolve(42); 
});

p1.then(function(value) {
    console.log(value);         // "42"
    return value + 1;
}).then(function(value) {
    console.log(value);         // "43"
});
```

如果返回的是 Promise 对象，会通过一个额外的步骤来确定下一步怎么走。如果返回的对象是 resolve ，那么接下来调用 `then()` 方法的第一个函数执行（完成处理函数），如果返回的对象是 reject ，那么接下来调用的 `then()` 方法的第二个函数执行（拒绝处理函数）。

```javascript
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});

p1.then(function(value) {
    console.log(value);     // 42

    // create a new promise
    let p2 = new Promise(function(resolve, reject) {
        resolve(43);
    });

    return p2
}).then(function(value) {
    console.log(value);     // 43
});
```

封装 Promise 版本的 readFile ，解决回调地狱问题。

```javascript
var fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./data/a.txt')
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/b.txt')
  })
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/c.txt')
  })
  .then(function (data) {
    console.log(data)
  })

```

封装 Promise 版本的 Ajax 方法，实现对两个有联系的接口的数据获取。相当于jQuery的`$.get()`异步请求方法。

```javascript
function pGet(url, callback) {
    return new Promise(function (resolve, rejuect)){
      var oReq = new XMLHttpRequest()
      oReq.onload = function () {
        callback && callback(JSON.parse(oReq.responseText))
        resolve(JSON.parse(oReq.responseText))
      }
      oReq.onerror = function (err) {
          reject(err)
      }
      oReq.open("get",url,true)
      oReq.send()
    }
}

var data = {}
pGet('http://127.0.0.1:3000/users/4')
    .then(function (user) {
    	data.user = user
    	return pGet('http://127.0.0.1:3000/jobs')
	})
	.then(function (jobs) {
    	data.jobs = jobs
    	var htmlStr = template('tpl', data)
        document.querySelector('#user_form').innerHTML = htmlStr
	})
```

# 八、MongoDB

## MongoDB 简介

MongoDB 是一个文档数据库，对于需要的查询性和索引内容，具有伸缩性和灵活性。在 node.js 中也有官方的 MongoDB 驱动引擎，为终端用户提供 mongodb 核心之上的高级 API。MongoDB 是长得最像关系型数据库的非关系数据库，它的数据表就是集合（数组），表记录就是文档对象。

- 关系型数据库通过外键关联来建立表与表之间的关系，酥油关系型数据库都需要通过 sql 语言来操作，都需要在操作之前设计结构，数据表支持约束。
- 非关系型数据库通常指数据以对象的形式存储在数据库中，而对象之间的关系通过每个对象自身的属性来决定。非关系数据库非常灵活，有的非关系数据库就是 key-value 对儿。

## 启动和关闭数据库

MongoDB 默认使用执行 mongodb 命令所处盘符目录下的 /data/db 作为自己的数据存储目录，所以在第一次执行该命令之前先自己手动创建一个这样的目录。如果想要修改默认的数据储存目录，可以使用`mongodb --dbpath=数据储存目录路径`的方法。关闭命令行即可停止。

```shell
# 启动数据库
mongodb
# 连接数据库，连接本机的 MongoDB 服务。
mongo
# 在连接状态下退出连接
exit
```

## 基本命令

`show dbs`查看显示所有数据库

`db`查看当前操作的数据库

`use 数据库名称`切换到指定的数据库，如果没有会新建这样的数据库

`db.students.inserOne({"name":"Javk"})`插入数据

## 在 Node 中操作 MongoDB 数据

可以使用官方的 mongodb 包来操作，也可以使用第三方 mongoose 来操作 MongoDB 数据库。该包基于 MongoDB 官方的 mongodb 包再一次做了封装。

```javascript
var mongoose = require("mongoose");

// 连接数据库
var db = mongoose.connect("mongodb://localhost/test",{ useMongoClient: true }); 

db.connection.on("error", function (error) {  
  console.log("数据库连接失败：" + error); 
}); 

db.connection.on("open", function () {  
  console.log("数据库连接成功"); 
});

mongoose.Promise = global.Promise;

// 创建一个模型（设计数据库）
var Cat = mongoose.model('Cat',{ name:String });

// 实例化一个 Cat
var kitty = new Cat ({ name: 'Zildjian' });

// 持久化保存 kitty 实例
kitty.save(function (err) {
  if (err) {
    console.log(err);
  }else {
    console.log('meow');
  }
})

```

设计集合结构（表结构），字段名称就是表结构中的属性名称，约束的目的是为了保证数据的完整性，不要有脏数据。将文档结构发布为模型的方法是`mongoose.model`，第一个参数是大写名词数字字符串的数据库名称，其会自动转换成小写复数的集合名称。

```javascript
// 设计集合结构
var userSchema = new Schema({
  username: {
    type: String,
    required:true
  },
  password: {
    type: String,
    required:true
  },
})

// 将文档结构发布为模型，返回值是模型构造函数
var User = mongoose.model('User', userSchema)
```

添加数据

```javascript
var admin = new User({
  username: 'admin',
  password: '123456'
})

admin.save(function (err,ret) {
  if (err) {
    consolo.log('保存失败')
  }else {
    consolo.log('保存成功')
    console.log(ret)
  }
})
```

查询数据使用`User.find`，删除数据使用`User.remove`，更新使用`User.update`。同时，如果需要根据 id 进行相应的操作，只需要使用`User.findOneAndremove`、`User.findOneAndUpdate`这些命令替代。

```javascript
// 查询所有
User.find(function () {})

// 条件查询
User.find {
  //条件
}，(function () {})
```

## 使用 Node 操作 MySQL 数据库

```javascript
var mysql = require('mysql');

// 创建数据库
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
// 连接数据库
connection.connect();
 
// 执行数据操作
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
 
// 关闭连接
connection.end();
```

# 九、服务器启动工具nodemon

## nodemon 简介

nodemon 是一种工具，通过在检测到目录中的文件更改时自动重新启动节点应用程序，从而来帮助开发者开发基于 node.js 的应用程序。 nodemon 并没有要求任何对你的代码或开发的方法中的额外变化。 nodemon 是一个替换包装器`node`的工具，用于在执行脚本时使用`nodemon`命令替换`node`命令。

## nodemon 安装

通过使用 git 克隆或使用 npm （推荐的方式）， nodemon 将全局安装到您的系统路径。

```shell
npm install -g nodemon
```

## nodemon 用法

安装完 nodemon 后，就可以用 nodemon 来代替 node 来启动应用：

```shell
# 相当于 node [your node app]
nodemon [your node app]
```

如果没有在应用中指定端口，可以在命令中指定：

```shell
nodemon ./server.js localhost 8080
```

可以运行 debug 模式：

```shell
nodemon --debug ./server.js 80
```

查看帮助，帮助里面有很多选项都是一目了然：

```shell
nodemon -h 或者 nodemon -help
```

只要是通过这个方式启动的服务，就会随时监控文件变化，当变化产生时自动重启服务器。

# 十、path路径操作模块

`path` 模块提供了一些工具函数，用于处理文件与目录的路径。可以通过以下方式使用：

```js
const path = require('path');
```

## path.basename()

path.basename(path[, ext]) 获取路径中的文件名。

path.basename() 方法返回一个 path 的最后一部分，类似于 Unix 中的 basename 命令。 没有尾部文件分隔符。后缀是可选的，如果加，请使用'.ext'方式来匹配，则返回值中不包括后缀名。如果 path 不是一个字符串或提供了 ext 但不是一个字符串，则抛出 TypeError。

```js
例子：

path.basename('/foo/bar/baz/asdf/quux.html');
// 返回: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html');
// 返回: 'quux'
```

## path.dirname() 

path.dirname(path) 获取路径中目录名。

path.dirname() 方法返回一个 path 的目录名，类似于 Unix 中的 dirname 命令。如果 path 不是一个字符串，则抛出 TypeError。 

```js
path.dirname('/foo/bar/baz/asdf/quux');
// 返回: '/foo/bar/baz/asdf'
```

## path.extname() 

path.extname(path) 获取路径中的扩展名。

path.extname() 方法返回 path 的扩展名，即从 path 的最后一部分中的最后一个 .（句号）字符到字符串结束。 如果 path 的最后一部分没有 `.` 或 path 的文件名的第一个字符是 `.` ，则返回一个空字符串。如果 path 不是一个字符串，则抛出 TypeError。

```js
path.extname('index.html');
// 返回: '.html'

path.extname('index.coffee.md');
// 返回: '.md'

path.extname('index.');
// 返回: '.'

path.extname('index');
// 返回: ''

path.extname('.index');
// 返回: ''
```

## path.format() 

`path.format(pathObject)` 返回字符串。

`path.format()` 方法会从一个对象返回一个路径字符串。 与 `path.parse()` 相反。当 pathObject 提供的属性有组合时，有些属性的优先级比其他的高：如果提供了 pathObject.dir，则 pathObject.root 会被忽略；如果提供了 pathObject.base 存在，则 pathObject.ext 和 pathObject.name 会被忽略

```js
path.format({
  dir: 'C:\\path\\dir',
  base: 'file.txt'
});
// 返回: 'C:\\path\\dir\\file.txt'
```

## path.isAbsolute() 

path.isAbsolute(path) 判断绝对路径。

path.isAbsolute() 方法会判定 path 是否为一个绝对路径。如果给定的 path 是一个长度为零的字符串，则返回 false。如果 path 不是一个字符串，则抛出 TypeError。

```js
path.isAbsolute('//server');    // true
path.isAbsolute('\\\\server');  // true
path.isAbsolute('C:/foo/..');   // true
path.isAbsolute('C:\\foo\\..'); // true
path.isAbsolute('bar\\baz');    // false
path.isAbsolute('bar/baz');     // false
path.isAbsolute('.');           // false
```

## path.join() 

path.join([...paths]) 获取路径合并结果。

path.join() 方法使用平台特定的分隔符把全部给定的 path 片段连接到一起，并规范化生成的路径。长度为零的 path 片段会被忽略。 如果连接后的路径字符串是一个长度为零的字符串，则返回 '.'，表示当前工作目录。如果任一路径片段不是一个字符串，则抛出 TypeError。

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// 返回: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// 抛出 'TypeError: Path must be a string. Received {}'
```

## path.normalize() 

`path.normalize(path)` 获得规范化路径。


`path.normalize()` 方法会规范化给定的 path，并解析 '..' 和 '.' 片段。当发现多个连续的路径分隔符时（如 POSIX 上的 / 与 Windows 上的 \ 或 /），它们会被单个的路径分隔符（POSIX 上是 /，Windows 上是 \）替换。 末尾的多个分隔符会被保留。如果 path 是一个长度为零的字符串，则返回 '.'，表示当前工作目录。如果 path 不是一个字符串，则抛出 TypeError。

```js
path.normalize('C:\\temp\\\\foo\\bar\\..\\');
// 返回: 'C:\\temp\\foo\\'
// 尽管Windows会识别多种文件路径分隔符，但是两种分隔符在Window上会被(\)分隔符取代：

path.win32.normalize('C:////temp\\\\/\\/\\/foo/bar');
// Returns: 'C:\\temp\\foo\\bar'
```

## path.parse(path)

`path.parse()` 方法返回一个对象，对象的属性表示 `path` 的元素。 尾部文件分隔符会被忽略。如果 path 不是一个字符串，则抛出 TypeError。

```js
path.parse('C:\\path\\dir\\file.txt');
// 返回:
// { root: 'C:\\',
//   dir: 'C:\\path\\dir',
//   base: 'file.txt',
//   ext: '.txt',
//   name: 'file' }
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
" C:\      path\dir   \ file  .txt "
└──────┴──────────────┴──────┴─────┘
// (请无视以上字符串中的空格，它们只是为了布局)
```

## path.relative()

path.relative(from, to) 获取相对路径。


path.relative() 方法返回从 from 到 to 的相对路径（基于当前工作目录）。 如果 from 和 to 各自解析到同一路径（调用 path.resolve()），则返回一个长度为零的字符串。如果 from 或 to 传入了一个长度为零的字符串，则当前工作目录会被用于代替长度为零的字符串。如果 from 或 to 不是一个字符串，则抛出 TypeError。

```js
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb');
// 返回: '..\\..\\impl\\bbb'
```

## path.resolve() 

path.resolve([...paths]) 获取绝对路径。

path.resolve() 方法会把一个路径或路径片段的序列解析为一个绝对路径。给定的路径的序列是从右往左被处理的，后面每个 path 被依次解析，直到构造完成一个绝对路径。 例如，给定的路径片段的序列为：/foo、/bar、baz，则调用 path.resolve('/foo', '/bar', 'baz') 会返回 /bar/baz。如果处理完全部给定的 path 片段后还未生成一个绝对路径，则当前工作目录会被用上。生成的路径是规范化后的，且末尾的斜杠会被删除，除非路径被解析为根目录。长度为零的 path 片段会被忽略。如果没有传入 path 片段，则 path.resolve() 会返回当前工作目录的绝对路径。如果任何参数不是一个字符串，则抛出 TypeError。

```js
path.resolve('/foo/bar', './baz');
// 返回: '/foo/bar/baz'

path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录为 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
```

# 十一、全局成员

## global

在浏览器的平台环境当中，全局对象为window，即任何一个定义在全局环境当中的变量都可以用window这个对象获取到。node环境当中的全局对象为global,它类似于客户端javascript运行环境当中的window。

```javascript
var a = 10
console.log(global.a)  // 10
```

## process

该对象用于获取当前Node进程的信息，一般用于获取环境变量之类的信息。

## 伪全局成员

全局变量在所有模块中均可使用。 以下变量虽然看起来像全局变量，但实际上不是。 它们的作用域只在模块内。

1.  `__dirname`

该成员用于获取当前这个js文件所在目录（所在文件夹）的完成的绝对物理路径。该成员只在模块内部有效，在REPL环境当中失效。输出为当前模块的文件夹名称。等同于 path.dirname( __filename ) 的值。

```js
// 示例：运行位于 `/Users/mjr`目录下的example.js文件：`node example.js`
console.log(__dirname);
// Prints: /Users/mjr
console.log(path.dirname(__filename));
// Prints: /Users/mjr
```

2. `__filename`

该成员用于获取当前这个js文件的完成的绝对物理路径。该成员只在模块内部有效，在REPL环境当中失效。输出为当前模块的文件名称（解析后的绝对路径）。在主程序中这不一定要跟命令行中使用的名称一致。注意：在 Node 文件操作中路径是相对于执行 node 命令所处的路径。

```js
// 在 `/Users/mjr` 目录下执行 `node example.js`
console.log(__filename);
// Prints: /Users/mjr/example.js
```

3. exports

这是一个对于 module.exports 的更简短的引用形式。

4. module


对当前模块的引用。 module.exports 用于指定一个模块所导出的内容，即可以通过 require() 访问的内容。

4. require()

引入模块。

# 十二、中间件

## **前言**

“中间件”在软件领域是一个非常广的概念，除操作系统的软件都可以称为中间件，比如，消息中间件，ESB中间件，日志中间件，数据库中间件等等。 Connect 被定义为 Node 平台的中间件框架，从定位上看 Connect 一定是出众的，广泛兼容的，稳定的，基础的平台性框架。如果攻克Connect，会有助于我们更了解Node的世界。Express就是基于Connect开发的。

## Connect介绍

Connect 是一个 node 中间件（middleware）框架。如果把一个 http 处理过程比作是污水处理，中间件就像是一层层的过滤网。每个中间件在 http 处理过程中通过改写 request 或（和）response 的数据、状态，实现了特定的功能。这些功能非常广泛。将中间件大致分为3类：

1. Pre-Request 通常用来改写request的原始数据
2. Request/Response 大部分中间件都在这里，功能各异
3. Post-Response 全局异常处理，改写response数据等

```js
/*
 * 使用connect实现的静态文件处理
 */
var connect = require('connect');
connect(connect.static(__dirname + '/public')).listen(//监听
    3000,
    function() {
        console.log('Connect started on port 3000');
    }
);
/*
 * 使用node原生api实现
 */
var http = require('http');
http.createServer(
    function(req, res) {
        var url = require('url');
        var fs = require('fs');
        var pathname = __dirname + '/public' + url.parse(req.url).pathname;
        //读取本地文件
        fs.readFile(
            pathname,
            function(err, data) {
                //异常处理
                if (err) {
                    res.writeHead(500);
                    res.end('500');
                }
                else {
                    res.end(data);
                }
            }
        );
    }
).listen(//监听
    3001,
    function() {
        console.log('http.Server started on port 3001');
    }
);
```

## express中间件

Express 是一个自身功能极简，完全是由路由和中间件构成一个的 web 开发框架：从本质上来说，一个 Express 应用就是在调用各种中间件。

中间件（Middleware） 是一个函数，它可以访问请求对象（request object (req)）, 响应对象（response object (res)）, 和 web 应用中处于请求-响应循环流程中的中间件，一般被命名为 next 的变量。

中间件的功能包括：

- 执行任何代码。
- 修改请求和响应对象。
- 终结请求-响应循环。
- 调用堆栈中的下一个中间件。

如果当前中间件没有终结请求-响应循环，则必须调用 `next()` 方法将控制权交给下一个中间件，否则请求就会挂起。

使用可选则挂载路径，可在应用级别或路由级别装载中间件。另外，你还可以同时装在一系列中间件函数，从而在一个挂载点上创建一个子中间件栈。

## express应用级中间件

应用级中间件绑定到 app 对象 使用 app.use() 和 app.METHOD()， 其中， METHOD 是需要处理的 HTTP 请求的方法，例如 GET, PUT, POST 等等，全部小写。

```javascript
var app = express();

// 没有挂载路径的中间件，应用的每个请求都会执行该中间件
app.use(function (req, res, next) {
  console.log('Time:', Date.now());
  next();
});

// 挂载至 /user/:id 的中间件，任何指向 /user/:id 的请求都会执行它
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method);
  next();
});

// 路由和句柄函数(中间件系统)，处理指向 /user/:id 的 GET 请求
app.get('/user/:id', function (req, res, next) {
  res.send('USER');
});

// 在一个挂载点装载一组中间件。一个中间件栈，对任何指向 /user/:id 的 HTTP 请求打印出相关信息
app.use('/user/:id', function(req, res, next) {
  console.log('Request URL:', req.originalUrl);
  next();
}, function (req, res, next) {
  console.log('Request Type:', req.method);
  next();
});

```

如果需要在中间件栈中跳过剩余中间件，调用 `next('route')` 方法将控制权交给下一个路由。 注意： `next('route')` 只对使用 `app.VERB()` 或 `router.VERB()` 加载的中间件有效。

```javascript
// 一个中间件栈，处理指向 /user/:id 的 GET 请求
app.get('/user/:id', function (req, res, next) {
  // 如果 user id 为 0, 跳到下一个路由
  if (req.params.id == 0) next('route');
  // 否则将控制权交给栈中下一个中间件
  else next(); //
}, function (req, res, next) {
  // 渲染常规页面
  res.render('regular');
});

// 处理 /user/:id， 渲染一个特殊页面
app.get('/user/:id', function (req, res, next) {
  res.render('special');
});
```

## express路由级中间件。

路由级中间件和应用级中间件一样，只是它绑定的对象为 `express.Router()`。路由级使用 `router.use()` 或 `router.VERB()` 加载。上述在应用级创建的中间件系统，可通过如下代码改写为路由级：

```javascript
var app = express();
var router = express.Router();

// 没有挂载路径的中间件，通过该路由的每个请求都会执行该中间件
router.use(function (req, res, next) {
  console.log('Time:', Date.now());
  next();
});

// 一个中间件栈，显示任何指向 /user/:id 的 HTTP 请求的信息
router.use('/user/:id', function(req, res, next) {
  console.log('Request URL:', req.originalUrl);
  next();
}, function (req, res, next) {
  console.log('Request Type:', req.method);
  next();
});

// 一个中间件栈，处理指向 /user/:id 的 GET 请求
router.get('/user/:id', function (req, res, next) {
  // 如果 user id 为 0, 跳到下一个路由
  if (req.params.id == 0) next('route');
  // 负责将控制权交给栈中下一个中间件
  else next(); //
}, function (req, res, next) {
  // 渲染常规页面
  res.render('regular');
});

// 处理 /user/:id， 渲染一个特殊页面
router.get('/user/:id', function (req, res, next) {
  console.log(req.params.id);
  res.render('special');
});

// 将路由挂载至应用
app.use('/', router);
```

## express错误处理中间件。

错误处理中间件和其他中间件定义类似，只是要使用 4 个参数，而不是 3 个，其签名如下：`(err, req, res, next)`。

错误处理中间件有 *4* 个参数，定义错误处理中间件时必须使用这 4 个参数。即使不需要 `next` 对象，也必须在签名中声明它，否则中间件会被识别为一个常规中间件，不能处理错误。

```javascript
app.use(function(err, req, res, next) {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

## express内置中间件。

express.static 是 Express 唯一内置的中间件。它基于 serve-static，负责在 Express 应用中提托管静态资源。参数 root 指提供静态资源的根目录。

下面的例子使用了 `express.static` 中间件，其中的 `options` 对象经过了精心的设计。

```javascript
var options = {
  dotfiles: 'ignore',
  etag: false,
  extensions: ['htm', 'html'],
  index: false,
  maxAge: '1d',
  redirect: false,
  setHeaders: function (res, path, stat) {
    res.set('x-timestamp', Date.now());
  }
}

app.use(express.static('public', options));
```

每个应用可有多个静态目录。

```javascript
app.use(express.static('public'));
app.use(express.static('uploads'));
app.use(express.static('files'));
```

## express第三方中间件。

通过使用第三方中间件从而为 Express 应用增加更多功能。安装所需功能的 node 模块，并在应用中加载，可以在应用级加载，也可以在路由级加载。

下面的例子安装并加载了一个解析 cookie 的中间件： `cookie-parser`

```js
// 在命令行输入 npm install cookie-parser
var express = require('express');
var app = express();
var cookieParser = require('cookie-parser');

// 加载用于解析 cookie 的中间件
app.use(cookieParser());
```

# 十三、服务器渲染与客户端渲染

## 什么是服务器端渲染和客户端渲染？

互联网早期，用户使用浏览器浏览的都是一些没有复杂逻辑的、简单的页面，这些页面都是在后端将html拼接好的然后将之返回给前端完整的html文件，浏览器拿到这个html文件之后就可以直接解析展示了，而这也就是所谓的服务器端渲染了。

而随着前端页面的复杂性提高，前端就不仅仅是普通的页面展示了，而可能添加了更多功能性的组件，复杂性更大，另外，彼时ajax的兴起，使得业界就开始推崇前后端分离的开发模式，即后端不提供完整的html页面，而是提供一些api使得前端可以获取到json数据，然后前端拿到json数据之后再在前端进行html页面的拼接，然后展示在浏览器上，这就是所谓的客户端渲染了，这样前端就可以专注UI的开发，后端专注于逻辑的开发。

## 两者本质的区别是什么？

客户端渲染和服务器端渲染的最重要的区别就是究竟是谁来完成html文件的完整拼接，如果是在服务器端完成的，然后返回给客户端，就是服务器端渲染，而如果是前端做了更多的工作完成了html的拼接，则就是客户端渲染。

## 服务器端渲染的优缺点

优点：

1. 前端耗时少。因为后端拼接完了html，浏览器只需要直接渲染出来。
2. 有利于SEO。因为在后端有完整的html页面，所以爬虫更容易爬取获得信息，更有利于seo。
3. 无需占用客户端资源。即解析模板的工作完全交由后端来做，客户端只要解析标准的html页面即可，这样对于客户端的资源占用更少，尤其是移动端，也可以更省电。
4. 后端生成静态化文件。即生成缓存片段，这样就可以减少数据库查询浪费的时间了，且对于数据变化不大的页面非常高效 。

缺点：

1. 不利于前后端分离，开发效率低。使用服务器端渲染，则无法进行分工合作，则对于前端复杂度高的项目，不利于项目高效开发。另外，如果是服务器端渲染，则前端一般就是写一个静态html文件，然后后端再修改为模板，这样是非常低效的，并且还常常需要前后端共同完成修改的动作；或者是前端直接完成html模板，然后交由后端。另外，如果后端改了模板，前端还需要根据改动的模板再调节css，这样使得前后端联调的时间增加。
2. 占用服务器端资源。即服务器端完成html模板的解析，如果请求较多，会对服务器造成一定的访问压力。而如果使用前端渲染，就是把这些解析的压力分摊了前端，而这里确实完全交给了一个服务器。

## 客户端渲染的优缺点

优点：　　

1. 前后端分离。前端专注于前端UI，后端专注于api开发，且前端有更多的选择性，而不需要遵循后端特定的模板。
2. 体验更好。比如，我们将网站做成SPA或者部分内容做成SPA，这样，尤其是移动端，可以使体验更接近于原生app。

缺点：

1. 前端响应较慢。如果是客户端渲染，前端还要进行拼接字符串的过程，需要耗费额外的时间，不如服务器端渲染速度快。
2. 不利于SEO。目前比如百度、谷歌的爬虫对于SPA都是不认的，只是记录了一个页面，所以SEO很差。因为服务器端可能没有保存完整的html，而是前端通过js进行dom的拼接，那么爬虫无法爬取信息。 除非搜索引擎的seo可以增加对于JavaScript的爬取能力，这才能保证seo。

## 使用服务器端渲染还是客户端渲染？

不谈业务场景而盲目选择使用何种渲染方式都是耍流氓。比如企业级网站，主要功能是展示而没有复杂的交互，并且需要良好的SEO，则这时我们就需要使用服务器端渲染；而类似后台管理页面，交互性比较强，不需要seo的考虑，那么就可以使用客户端渲染。

另外，具体使用何种渲染方法并不是绝对的，比如现在一些网站采用了首屏服务器端渲染，即对于用户最开始打开的那个页面采用的是服务器端渲染，这样就保证了渲染速度，而其他的页面采用客户端渲染，这样就完成了前后端分离。

## 对于前后端分离，如果进行seo优化？

如果进行了前后端分离，那么前端就是通过js来修改dom使得html拼接完全，然后再显示，或者是使用SPA，这样，seo几乎没有。那么这种情况下如何做seo优化呢？

我们可以自行提交sitemap，让蜘蛛主动去爬取，但是遇到了sitemap中的url，达到指定页面之后只有元js怎么办呢？这是我们可以使用`<noscript>`标签来进行简单的优化，比如打印出当前页面信息的一些关键的信息点，但是正常用户并不需要这些，会造成额外的负担，且前端可以判断是否支持JavaScript，而后段不行，只好根据百度的spider做UA判断，使用phantomjs或者nginx代理，来对spider访问的页面进行特殊的处理，达到被收录的效果。但这种效果还是不好。

而目前的react和vue都提供了SSR，即服务器端渲染，这也就是提供seo不好的解决方式了。

## 究竟如何理解前后端分离？

实际上，时至今日，前后端分离一定是必然或者趋势，因为早期在web1.0时代的网页就是简单的网页，而如今的网页越来越朝向app前进，而前后端分离就是实现app的必然的结果。

所以，我们可以认为html、css、JavaScript组成了这个app，然后浏览器作为虚拟机来运行这些程序，即浏览器成为了app的运行环境，成了客户端，总的来说就是当前的前端越来越朝向桌面应用或者说是手机上的app发展了，而比如说电脑上的qq可以服务器端渲染吗？肯定不能！所以前后端分离也就成了必然。而我们目前接触额前端工程化、编译（转译）、各种MVC/MVVM框架、依赖工具、npm、bable、webpack等等看似很新鲜、创新的东西实际上都是传动桌面开发所形成的概念，只是近年来前端发展较快而借鉴过来的，本质上就是开源社区东平西凑做出来的一个visual studio。