# Webpack

## 基本概念

### webpack 作用

你知道 webpack 的作用是什么吗？

从官网上的描述我们其实不难理解，webpack 的作用其实有以下几点：

1. 模块打包。可以将不同模块的文件打包整合在一起，并且保证它们之间的引用正确，执行有序。利用打包我们就可以在开发的时候根据我们自己的业务自由划分文件模块，保证项目结构的清晰和可读性。

2. 编译兼容。通过 webpack 的 Loader 机制，不仅仅可以帮助我们对代码做 polyfill，还可以编译转换诸如`.less`、`.vue` 和 `.jsx`这类在浏览器无法识别的格式文件，让我们在开发的时候可以使用新特性和新语法做开发，提高开发效率。

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

作用上

- Loader 直译为"加载器"。Webpack 将一切文件视为模块，但是 webpack 原生是只能解析 js 文件，如果想将其他文件也打包的话，就会用到 loader。 所以 Loader 的作用是让 webpack 拥有了加载和解析非 JavaScript 文件的能力。
- Plugin 直译为"插件"。Plugin 可以扩展 webpack 的功能，让 webpack 具有更多的灵活性。 在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。

用法上

- Loader 在 `module.rules` 中配置，也就是说他作为模块的解析规则而存在。 类型为数组，每一项都是一个 Object，里面描述了对于什么类型的文件（test），使用什么加载（loader 和使用的参数（options）
- Plugin 在 plugins 中单独配置。 类型为数组，每一项是一个 plugin 的实例，参数都通过构造函数传入。

### 常见的 loader 和 plugin

有哪些常见的 Loader 和 Plugin？他们是解决什么问题的？

Loader 主要有

- image-loader：加载并且压缩图片文件
- babel-loader：把 ES6 转换成 ES5
- css-loader：加载 CSS，支持模块化、压缩、文件导入等特性
- style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
- eslint-loader：通过 ESLint 检查 JavaScript 代码

Plugin 主要有

- define-plugin：定义环境变量
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

- 压缩代码。删除多余的代码、注释、简化代码的写法等等方式。可以利用 webpack 的 UglifyJsPlugin 和 ParallelUglifyPlugin 来压缩 JS 文件， 利用 cssnano（css-loader?minimize）来压缩 css
- 利用 CDN 加速。在构建过程中，将引用的静态资源路径修改为 CDN 上对应的路径。可以利用 webpack 对于 output 参数和各 loader 的 publicPath 参数来修改资源路径
- 删除死代码（Tree Shaking）。将代码中永远不会走到的片段删除掉。可以通过在启动 webpack 时追加参数`--optimize-minimize` 来实现
- 提取公共代码。多入口情况下，使用 CommonsChunkPlugin 来提取公共代码

如何提高 webpack 的构建速度？
怎么配置单页应用？怎么配置多页应用？CommonsChunkPlugin
npm 打包时需要注意哪些？如何利用 webpack 来更好的构建？

### 按需加载

如何在 vue 项目中实现按需加载？

- webpack 中提供了 `require.ensure()` 来实现页面按需加载

### tree shaking

tree shaking

- tree-shaking 可以用来剔除 javascript 中不用的死代码，它依赖静态的 es6 模块化语法，例如通过 import 和 export 导入导出，Tree-shaking 最先在 rollup 中出现，webpack 在 2.0 中将其引入，css 中使用 Tree-shaking 需要引入 Purify-CSS

## 实现原理

### 模块打包运行原理

说一下模块打包运行原理？Webpack 是如何把这些模块合并到一起，并且保证其正常工作的，你是否了解呢？

首先我们应该简单了解一下 webpack 的整个打包流程：

1. 读取 webpack 的配置参数；
2. 启动 webpack，创建 Compiler 对象并开始解析项目；
3. 从入口文件（entry）开始解析，并且找到其导入的依赖模块，递归遍历分析，形成依赖关系树；
4. 对不同文件类型的依赖模块文件使用对应的 Loader 进行编译，最终转为 Javascript 文件；
5. 整个过程中 webpack 会通过发布订阅模式，向外抛出一些 hooks，而 webpack 的插件即可通过监听这些关键的事件节点，执行插件任务进而达到干预输出结果的目的。

其中文件的解析与构建是一个比较复杂的过程，在 webpack 源码中主要依赖于 compiler 和 compilation 两个核心对象实现。

compiler 对象是一个全局单例，他负责把控整个 webpack 打包的构建流程。 compilation 对象是每一次构建的上下文对象，它包含了当次构建所需要的所有信息，每次热更新和重新构建，compiler 都会重新生成一个新的 compilation 对象，负责此次更新的构建过程。

而每个模块间的依赖关系，则依赖于 AST 语法树。每个模块文件在通过 Loader 解析完成之后，会通过 acorn 库生成模块代码的 AST 语法树，通过语法树就可以分析这个模块是否还有依赖的模块，进而继续循环执行下一个模块的编译解析。

最终 Webpack 打包出来的 bundle 文件是一个 IIFE 的执行函数。

```js
// webpack 5 打包的bundle文件内容

(() => { // webpackBootstrap
    var __webpack_modules__ = ({
        'file-A-path': ((modules) => { // ... })
        'index-file-path': ((__unused_webpack_module, __unused_webpack_exports, __webpack_require__) => { // ... })
    })

    // The module cache
    var __webpack_module_cache__ = {};

    // The require function
    function __webpack_require__(moduleId) {
        // Check if module is in cache
        var cachedModule = __webpack_module_cache__[moduleId];
        if (cachedModule !== undefined) {
                return cachedModule.exports;
        }
        // Create a new module (and put it into the cache)
        var module = __webpack_module_cache__[moduleId] = {
                // no module.id needed
                // no module.loaded needed
                exports: {}
        };

        // Execute the module function
        __webpack_modules__[moduleId](module, module.exports, __webpack_require__);

        // Return the exports of the module
        return module.exports;
    }

    // startup
    // Load entry module and return exports
    // This entry module can't be inlined because the eval devtool is used.
    var __webpack_exports__ = __webpack_require__("./src/index.js");
})
```

和 webpack4 相比，webpack5 打包出来的 bundle 做了相当的精简。在上面的打包 demo 中，整个立即执行函数里边只有三个变量和一个函数方法，`__webpack_modules__`存放了编译后的各个文件模块的 JS 内容，`__webpack_module_cache__` 用来做模块缓存，`__webpack_require__`是 Webpack 内部实现的一套依赖引入函数。最后一句则是代码运行的起点，从入口文件开始，启动整个项目。

其中值得一提的是`__webpack_require__`模块引入函数，我们在模块化开发的时候，通常会使用 ES Module 或者 CommonJS 规范导出/引入依赖模块，webpack 打包编译的时候，会统一替换成自己的`__webpack_require__`来实现模块的引入和导出，从而实现模块缓存机制，以及抹平不同模块规范之间的一些差异性。

### sourceMap 原理

你知道 sourceMap 是什么吗？

提到 sourceMap，很多小伙伴可能会立刻想到 Webpack 配置里边的 devtool 参数，以及对应的 eval，eval-cheap-source-map 等等可选值以及它们的含义。除了知道不同参数之间的区别以及性能上的差异外，我们也可以一起了解一下 sourceMap 的实现方式。

sourceMap 是一项将编译、打包、压缩后的代码映射回源代码的技术，由于打包压缩后的代码并没有阅读性可言，一旦在开发中报错或者遇到问题，直接在混淆代码中 debug 问题会带来非常糟糕的体验，sourceMap 可以帮助我们快速定位到源代码的位置，提高我们的开发效率。sourceMap 其实并不是 Webpack 特有的功能，而是 Webpack 支持 sourceMap，像 JQuery 也支持 souceMap。

既然是一种源码的映射，那必然就需要有一份映射的文件，来标记混淆代码里对应的源码的位置，通常这份映射文件以`.map`结尾，里边的数据结构大概长这样：

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

从上面的打包代码我们其实可以知道，Webpack 最后打包出来的成果是一份 Javascript 代码，实际上在 Webpack 内部默认也只能够处理 JS 模块代码，在打包过程中，会默认把所有遇到的文件都当作 JavaScript 代码进行解析，因此当项目存在非 JS 类型文件时，我们需要先对其进行必要的转换，才能继续执行打包任务，这也是 Loader 机制存在的意义。

Loader 的配置使用我们应该已经非常的熟悉：

```js
// webpack.config.js
module.exports = {
  // ...other config
  module: {
    rules: [
      {
        test: /^your-regExp$/,
        use: [
          {
            loader: 'loader-name-A',
          },
          {
            loader: 'loader-name-B',
          },
        ],
      },
    ],
  },
};
```

通过配置可以看出，针对每个文件类型，loader 是支持以数组的形式配置多个的，因此当 Webpack 在转换该文件类型的时候，会按顺序链式调用每一个 loader，前一个 loader 返回的内容会作为下一个 loader 的入参。因此 loader 的开发需要遵循一些规范，比如返回值必须是标准的 JS 代码字符串，以保证下一个 loader 能够正常工作，同时在开发上需要严格遵循“单一职责”，只关心 loader 的输出以及对应的输出。

loader 函数中的 this 上下文由 webpack 提供，可以通过 this 对象提供的相关属性，获取当前 loader 需要的各种信息数据，事实上，这个 this 指向了一个叫 loaderContext 的 loader-runner 特有对象。有兴趣的小伙伴可以自行阅读源码。

```js
module.exports = function (source) {
  const content = doSomeThing2JsString(source);

  // 如果 loader 配置了 options 对象，那么this.query将指向 options
  const options = this.query;

  // 可以用作解析其他模块路径的上下文
  console.log('this.context');

  /*
   * this.callback 参数：
   * error：Error | null，当 loader 出错时向外抛出一个 error
   * content：String | Buffer，经过 loader 编译后需要导出的内容
   * sourceMap：为方便调试生成的编译后内容的 source map
   * ast：本次编译生成的 AST 静态语法树，之后执行的 loader 可以直接使用这个 AST，进而省去重复生成 AST 的过程
   */
  this.callback(null, content);
  // or return content;
};
```

更详细的开发文档可以直接查看官网的 Loader API。

### plugin 原理

是否写过 Plugin？简单描述一下编写 plugin 的思路？

如果说 Loader 负责文件转换，那么 Plugin 便是负责功能扩展。Loader 和 Plugin 作为 Webpack 的两个重要组成部分，承担着两部分不同的职责。

上文已经说过，webpack 基于发布订阅模式，在运行的生命周期中会广播出许多事件，插件通过监听这些事件，就可以在特定的阶段执行自己的插件任务，从而实现自己想要的功能。

既然基于发布订阅模式，那么知道 Webpack 到底提供了哪些事件钩子供插件开发者使用是非常重要的，上文提到过 compiler 和 compilation 是 Webpack 两个非常核心的对象，其中 compiler 暴露了和 Webpack 整个生命周期相关的钩子（compiler-hooks），而 compilation 则暴露了与模块和依赖有关的粒度更小的事件钩子（Compilation Hooks）。

Webpack 的事件机制基于 webpack 自己实现的一套 Tapable 事件流方案（github）

```js
// Tapable的简单使用
const { SyncHook } = require('tapable');

class Car {
  constructor() {
    // 在this.hooks中定义所有的钩子事件
    this.hooks = {
      accelerate: new SyncHook(['newSpeed']),
      brake: new SyncHook(),
      calculateRoutes: new AsyncParallelHook([
        'source',
        'target',
        'routesList',
      ]),
    };
  }

  /* ... */
}

const myCar = new Car();
// 通过调用tap方法即可增加一个消费者，订阅对应的钩子事件了
myCar.hooks.brake.tap('WarningLampPlugin', () => warningLamp.on());
```

Plugin 的开发和开发 Loader 一样，需要遵循一些开发上的规范和原则：

- 插件必须是一个函数或者是一个包含 apply 方法的对象，这样才能访问 compiler 实例；
- 传给每个插件的 compiler 和 compilation 对象都是同一个引用，若在一个插件中修改了它们身上的属性，会影响后面的插件;
- 异步的事件需要在插件处理完任务时调用回调函数通知 Webpack 进入下一个流程，不然会卡住;

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

更详细的开发文档可以直接查看官网的 Plugin API。
