# Webpack

## 基本概念

### webpack 作用

你知道 webpack 的作用是什么吗？

webpack 的作用其实有以下几点：

1. 模块打包。可以将不同模块的文件打包整合在一起，并且保证它们之间的引用正确，执行有序。利用打包我们就可以在开发的时候根据我们自己的业务自由划分文件模块，保证项目结构的清晰和可读性。

2. 编译兼容。通过 webpack 的 Loader 机制，不仅仅可以帮助我们对代码做 polyfill，还可以编译转换诸如 `.less`、`.vue` 和 `.jsx` 这类在浏览器无法识别的格式文件，让我们在开发的时候可以使用新特性和新语法做开发，提高开发效率。

3. 能力扩展。通过 webpack 的 Plugin 机制，我们在实现模块化打包和编译兼容的基础上，可以进一步实现诸如按需加载，代码压缩等一系列功能，帮助我们进一步提高自动化程度，工程效率以及打包输出的质量。

### webpack 比对

webpack 与 grunt、gulp 的不同？

- gulp 和 grunt 需要开发者将整个前端构建过程拆分成多个`Task`，并合理控制所有`Task`的调用关系；而 webpack 需要开发者找到入口，并需要清楚对于不同的资源应该使用什么 Loader 做何种解析和加工

- gulp 更像后端开发者的思路，需要对于整个流程了如指掌；webpack 更倾向于前端开发者的思路，webpack 适用于大型复杂的前端站点构建

### webpack 优点

webpack 有哪些优点

- 专注于处理模块化的项目，能做到开箱即用，一步到位
- 可通过 plugin 扩展，完整好用又不失灵活
- 使用场景不局限于 web 开发
- 社区庞大活跃，经常引入紧跟时代发展的新特性，能为大多数场景找到已有的开源扩展
- 良好的开发体验

## 基本实践

### loader 和 plugin 比较

Loader 和 Plugin 的不同？

Loader 直译为"加载器"，本质就是一个函数。

- 对其他类型的资源进行转译的预处理工作。webpack 原生是只能解析 js 文件，loader 可以将其他文件打包。
- 在 `module.rules` 中配置，作为模块的解析规则。类型为数组，每一项都是 Object，描述了对什么类型的文loader件（test），使用什么加载（loder）和使用的参数（options）。

Plugin 直译为"插件"，是一个具有 apply 属性的 JavaScript 对象。

- 基于 Tapable 事件流框架，插件可以扩展 webpack 的功能，让 webpack 具有更多的灵活性。在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。
- Plugin 在 plugins 中单独配置。类型为数组，每一项是一个 plugin 的实例，参数都通过构造函数传入。

### 常见的 loader 和 plugin

有哪些常见的 Loader 和 Plugin？他们是解决什么问题的？

Loader 主要有

- image-loader：加载并且压缩图片文件
- babel-loader：把 ES6 转换成 ES5
- css-loader：加载 CSS，支持模块化、压缩、文件导入等特性
- style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
- eslint-loader：通过 ESLint 检查 JavaScript 代码

Plugin 主要有

- define-plugin：定义环境变量（Webpack4 之后指定 mode 会自动配置）
- commons-chunk-plugin：提取公共代码
- uglifyjs-webpack-plugin：通过 UglifyES 压缩 ES6 代码
- html-webpack-plugin 为 html 文件中引入的外部资源，可以生成创建 html 入口文件
- terser-webpack-plugin：通过 TerserPlugin 压缩 ES6 代码
- mini-css-extract-plugin：分离 css 文件
- clean-webpack-plugin：删除打包文件
- happypack：实现多线程加速编译

webpack 的构建流程是什么?从读取配置到输出文件这个过程尽量说全
是否写过 Loader 和 Plugin？描述一下编写 loader 或 plugin 的思路？
webpack 的热更新是如何做到的？说明其原理？

### 优化前端性能

如何利用 webpack 来优化前端性能？（提高性能和体验）

- 利用 CDN 加速。在构建过程中，将引用的静态资源路径修改为 CDN 上对应的路径。可以利用 webpack 对于 output 参数和各 loader 的 publicPath 参数来修改资源路径
- 删除死代码（Tree Shaking）。将代码中永远不会走到的片段删除掉。可以通过在启动 webpack 时追加参数`--optimize-minimize` 来实现
- 提取公共代码。多入口情况下，使用 CommonsChunkPlugin 来提取公共代码

- 使用高版本的 Webpack 和 Node.js
- 多线程/多实例构建：HappyPack、thread-loader
- 压缩代码。删除多余的代码、注释、简化代码的写法等等方式
  - UglifyJsPlugin 和 ParallelUglifyPlugin 来压缩 JS 文件
  - 通过 css-loader 的 minimize 选项开启 cssnano 压缩 CSS
- 图片压缩
- 缩小打包作用域
  - exclude/include 确定 loader 规则范围
  - resolve.extensions 尽可能减少后缀尝试的可能性
  - noParse 对完全不需要解析的库进行忽略 
  - IgnorePlugin 完全排除模块
  - 合理使用 alias
- 提取公共代码
  - 利用 CDN 加速，将引用的静态资源路径修改为 CDN 上对应的路径
  - 使用 splitChunksPlugin/CommonsChunkPlugin 进行公共脚本、基础包、页面公共文件分离
- 充分利用缓存提升二次构建速度
- Tree shaking 检测没有引用过的模块并进行标记，在资源压缩时将它们从最终的bundle中去掉
  - 依赖静态的 es6 模块化语法，例如通过 import 和 export 导入导出
- Scope hoisting
- 动态 Polyfill

### 热更新原理

Webpack 的热更新又称热替换（Hot Module Replacement），缩写为 HMR。 这个机制可以做到不用刷新浏览器而将新变更的模块替换掉旧的模块。

HMR的核心就是客户端从服务端拉去更新后的文件，准确的说是 chunk diff，即 chunk 需要更新的部分，实际上 WDS 与浏览器之间维护了一个 Websocket，当本地资源发生变化时，WDS 会向浏览器推送更新，并带上构建时的 hash，让客户端与上一次资源进行对比。客户端对比出差异后会向 WDS 发起 Ajax 请求来获取更改内容（文件列表、hash），这样客户端就可以再借助这些信息继续向 WDS 发起 jsonp 请求获取该chunk的增量更新。

后续的部分（拿到增量更新之后如何处理？哪些状态该保留？哪些又需要更新？）由 HotModulePlugin 来完成，提供了相关 API 以供开发者针对自身场景进行处理，像 react-hot-loader 和 vue-loader 都是借助这些 API 实现 HMR。

### 按需加载

如何在 vue 项目中实现按需加载？

- webpack 中提供了 `require.ensure()` 来实现页面按需加载

## 实现原理

### 模块打包运行原理

说一下模块打包运行原理？

首先我们应该简单了解一下 webpack 的整个打包流程：

1. 读取 webpack 的配置参数，包括配置文件和 Shell 语句中参数；
2. 启动 webpack，创建 Compiler 对象并开始解析项目；
3. 从入口文件 entry 开始解析，并且找到其导入的依赖模块，递归遍历分析，形成依赖关系树；
4. 对不同文件类型的依赖模块文件使用对应的 Loader 进行编译，最终转为 Javascript 文件；
5. 整个过程中 webpack 会通过发布订阅模式，向外抛出一些 hooks，而 webpack 的插件即可通过监听这些关键的事件节点，执行插件任务进而达到干预输出结果的目的。
6. 在确定好输出内容后，根据配置确定的输出路径和文件名，把文件内容写入到文件系统中。

其中文件的解析与构建是一个比较复杂的过程，在 webpack 源码中主要依赖于 compiler 和 compilation 两个核心对象实现。

compiler 对象是一个全局单例，负责把控整个 webpack 打包的构建流程。compilation 对象是每一次构建的上下文对象，它包含了当次构建所需要的所有信息，每次热更新和重新构建，compiler 都会重新生成一个新的 compilation 对象，负责此次更新的构建过程。

而每个模块间的依赖关系，则依赖于 AST 语法树。每个模块文件在通过 Loader 解析完成之后，会通过 acorn 库生成模块代码的 AST 语法树，通过语法树就可以分析这个模块是否还有依赖的模块，进而继续循环执行下一个模块的编译解析。

### sourceMap 原理

你知道 sourceMap 是什么吗？

sourceMap 是一项将编译、打包、压缩后的代码映射回源代码的技术，可以帮助我们快速定位到源代码的位置，提高我们的开发效率。sourceMap 其实并不是 Webpack 特有的功能，而是 Webpack 支持 sourceMap，像 JQuery 也支持 souceMap。map文件只要不打开开发者工具，浏览器是不会加载的。

既然是一种源码的映射，那必然就需要有一份映射的文件，来标记混淆代码里对应的源码的位置，通常这份映射文件以 `.map` 结尾，里边的数据结构大概长这样：

```js
{
  "version" : 3,                          // Source Map版本
  "file": "out.js",                       // 输出文件（可选）
  "sourceRoot": "",                       // 源文件根目录（可选）
  "sources": ["foo.js", "bar.js"],        // 源文件列表
  "sourcesContent": [null, null],         // 源内容列表（可选，和源文件列表顺序一致）
  "names": ["src", "maps", "are", "fun"], // mappings使用的符号名称列表
  "mappings": "A,AAAB;;ABCDE;"            // 带有编码映射数据的字符串
}
```

其中 mappings 数据有如下规则：

- 生成文件中的一行的每个组用“;”分隔；
- 每一段用“,”分隔；
- 每个段由 1、4 或 5 个可变长度字段组成；

有了这份映射文件，我们只需要在我们的压缩代码的最末端加上这句注释，即可让 sourceMap 生效：

```js
//# sourceURL=/path/to/file.js.map
```

有了这段注释后，浏览器就会通过 sourceURL 去获取这份映射文件，通过解释器解析后，实现源码和混淆代码之间的映射。因此 sourceMap 其实也是一项需要浏览器支持的技术。

如果我们仔细查看 webpack 打包出来的 bundle 文件，就可以发现在默认的 development 开发模式下，每个`_webpack_modules__`文件模块的代码最末端，都会加上`//# sourceURL=webpack://file-path?`，从而实现对 sourceMap 的支持。

### loader 原理

是否写过 Loader？简单描述一下编写 loader 的思路？

在打包过程中，会默认把所有遇到的文件都当作 JavaScript 代码进行解析，因此当项目存在非 JS 类型文件时，我们需要先对其进行必要的转换，才能继续执行打包任务，这也是 Loader 机制存在的意义。

所谓 loader 只是一个导出为函数的 JavaScript 模块。loader runner 会调用这个函数，然后把上一个 loader 产生的结果或者资源文件 resource file 传入进去。函数的 this 上下文将由 webpack 填充，并且 loader runner 具有一些有用方法，可以使 loader 改变为异步调用方式，或者获取 query 参数。

- 按顺序链式调用每一个 loader
- 前一个 loader 返回的内容会作为下一个 loader 的入参
- 函数中的 this 上下文由 webpack 提供，可以通过 this 对象提供的相关属性
- 返回值必须是标准的 JS 代码字符串

如果是单个处理结果，可以在同步模式中直接返回。如果有多个处理结果，则必须调用 `this.callback()`。在异步模式中，必须调用 `this.async()`，来指示 loader runner 等待异步结果，它会返回 `this.callback()` 回调函数，随后 loader 必须返回 undefined 并且调用该回调函数。

更详细的开发文档可以直接查看官网的 [Loader API](https://www.webpackjs.com/api/loaders/)。

### plugin 原理

是否写过 Plugin？简单描述一下编写 plugin 的思路？

插件是 webpack 生态系统的重要组成部分，为社区用户提供了一种强大方式来直接触及 webpack 的编译过程。插件能够 钩入 hook 到在每个编译 compilation 中触发的所有关键事件。在编译的每一步，插件都具备完全访问 compiler 对象的能力，如果情况合适，还可以访问当前 compilation 对象。

- compiler 对象代表了完整的 webpack 环境配置。这个对象在启动 webpack 时被一次性建立，并配置好所有可操作的设置。暴露了和 Webpack 整个生命周期相关的钩子。
- compilation 对象代表了一次资源版本构建。当运行 webpack 开发环境中间件时，每当检测到一个文件变化，就会创建一个新的 compilation，从而生成一组新的编译资源。暴露了与模块和依赖有关的粒度更小的事件钩子。

Webpack 基于发布订阅模式，在运行的生命周期中会广播出许多事件，插件通过监听这些事件，就可以在特定的阶段执行自己的插件任务，从而实现自己想要的功能。事件流方案 webpack 提供了 webpack 插件接口的支柱。

webpack 插件由以下组成：

- 一个 JavaScript 命名函数。
- 在插件函数的 prototype 上定义一个 apply 方法。
- 指定一个绑定到 webpack 自身的事件钩子。
- 处理 webpack 内部实例的特定数据。
- 功能完成后调用 webpack 提供的回调。

了解了以上这些内容，想要开发一个 Webpack Plugin，其实也并不困难。

```js
class MyPlugin {
  apply(compiler) {
    // 找到合适的事件钩子，实现自己的插件功能
    compiler.hooks.emit.tap('MyPlugin', (compilation) => {
      // compilation: 当前打包构建流程的上下文
      console.log(compilation);

      // do something...
    });
  }
}
```

更详细的开发文档可以直接查看官网的 [Plugin API](https://www.webpackjs.com/api/plugins/)。
