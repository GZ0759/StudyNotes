> [React 全家桶](https://www.bilibili.com/video/BV1wy4y1D7JT)
> 尚硅谷

# 第 1 章：React 入门

## 1.1. React 简介

React 框架由 Facebook 开源。用于动态构建用户界面的 JavaScript 库。

React 的特点

1. 声明式编码
2. 组件化编码
3. React Native 编写原生应用
4. 高效（优秀的 Diffing 算法）

React 高效的原因。使用虚拟 DOM, 不总是直接操作页面真实 DOM。借助 DOM Diffing 算法, 最小化页面重绘。

## 1.2. 基本使用

创建虚拟 DOM 的两种方式有两种，一是纯 JS 方式，二是 JSX 方式。需要引入下面的库

1. react.js：React 核心库。
2. react-dom.js：提供操作 DOM 的 react 扩展库。
3. babel.min.js：解析 JSX 语法代码转为 JS 代码的库。

虚拟 DOM 元素

1. React 提供了一些 API 来创建一种特殊 js 对象，即虚拟 DOM 对象
2. 虚拟 DOM 对象最终都会被 React 转换为真实的 DOM
3. 只需要操作 react 的虚拟 DOM 相关数据, react 会转换为真实 DOM 变化而更新界面
4. 语法为 `ReactDOM.render(virtualDOM,?containerDOM)`

## 1.3. React JSX

react 定义的一种类似于 XML（全称: JavaScript XML） 的 JS 扩展语法，本质是渲染虚拟 DOM 方法的语法糖，用来简化创建虚拟 DOM。

基本语法规则如下：

1. 遇到 `<` 开头的代码, 以标签的语法解析:

- html 同名标签转换为 html 同名元素
- 其它标签需要特别解析

2. 遇到以 `{` 开头的代码，以 JS 语法解析: 标签中的 js 表达式必须用`{}`包含

babel.js 的作用

- 浏览器不能直接解析 JSX 代码, 需要 babel 转译为纯 JS 的代码才能运行
- 只要用了 JSX，都要加上 `type="text/babel"`, 声明需要 babel 来处理

## 1.4. 模块与组件

1. 模块：向外提供特定功能的 js 程序, 一般就是一个 js 文件。随着业务逻辑增加，代码越来越多且复杂。因此模块的作用是复用 js, 简化 js 的编写, 提高 js 运行效率。
2. 组件：用来实现局部功能效果的代码和资源的集合。一个界面的功能更复杂。组件的作用是复用编码, 简化项目编码, 提高运行效率
3. 模块化：当应用的 js 都以模块来编写的, 这个应用就是一个模块化的应用
4. 组件化：当应用是以多组件的方式实现, 这个应用就是一个组件化的应用

# 第 2 章：React 面向组件编程

## 2.1. 基本理解和使用

2.1.1. 使用 React 开发者工具调试

2.1.2. 组件类型

1. 函数式组件。接收唯一带有数据的 “props”（代表属性）对象与并返回一个 React 元素。
2. 类式组件。通过 state 机制组件可以动态更新视图内容，还可以使用声明周期函数。

2.1.3. 注意事项

1. 组件名必须首字母大写
2. 虚拟 DOM 元素只能有一个根元素
3. 虚拟 DOM 元素必须有结束标签

2.1.4. 渲染类组件标签的基本流程

1. React 内部会创建组件实例对象
2. 调用 `render()` 得到虚拟 DOM, 并解析为真实 DOM
3. 插入到指定的页面元素内部

## 2.2. 组件三大核心属性 1: state

2.2.1. 效果

需求: 定义一个展示天气信息的组件

1. 默认展示天气“炎热”或“凉爽”
2. 点击文字切换天气

2.2.2. 理解

1. state 是组件对象最重要的属性, 值是对象（可以包含多个 key-value 的组合）
2. 组件被称为"状态机", 通过更新组件的 state 来更新对应的页面显示（重新渲染组件）

2.2.3. 注意事项

1. 组件中 render 方法中的 this 为组件实例对象
2. 组件自定义的方法中 this 为 undefined，如何解决？

- 强制绑定 this: 通过函数对象的 `bind()`
- 箭头函数

3. 状态数据，不能直接修改或更新

## 2.3. 组件三大核心属性 2: props

2.3.1. 效果

需求: 自定义用来显示一个人员信息的组件

1. 姓名必须指定，且为字符串类型；
2. 性别为字符串类型，如果性别没有指定，默认为男
3. 年龄为字符串类型，且为数字类型，默认值为 18

2.3.2. 理解

1. 每个组件对象都会有 props（properties 的简写）属性
2. 组件标签的所有属性都保存在 props 中

2.3.3. 作用

1. 通过标签属性从组件外向组件内传递变化的数据
2. 注意: 组件内部不要修改 props 数据

2.3.4. 编码操作

1. 内部读取某个属性值

```js
this.props.name;
```

2. 对 props 中的属性值进行类型限制和必要性限制

- 第一种方式（React v15.5 开始已弃用）：

```js
Person.propTypes = {
  name: React.PropTypes.string.isRequired,
  age: React.PropTypes.number,
};
```

- 第二种方式（新）：使用 prop-types 库进限制（需要引入 prop-types 库）

```js
Person.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.
}
```

3. 扩展属性: 将对象的所有属性通过 props 传递

```jsx
<Person {...person} />
```

4. 默认属性值：

```js
Person.defaultProps = {
  age: 18,
  sex: '男',
};
```

5. 组件类的构造函数

```js
constructor(props){
  super(props)
  console.log(props)//打印所有属性
}
```

## 2.4. 组件三大核心属性 3: refs 与事件处理

2.4.1. 效果

需求: 自定义组件, 功能说明如下:

1. 点击按钮, 提示第一个输入框中的值
2. 当第 2 个输入框失去焦点时, 提示这个输入框中的值

2.4.2. 理解

组件内的标签可以定义 ref 属性来标识自己

2.4.3. 编码

1. 字符串形式的 ref
2. 回调形式的 ref
3. createRef 创建 ref 容器

2.4.4. 事件处理

1. 通过 onXxx 属性指定事件处理函数（注意大小写）

- React 使用的是自定义（合成）事件, 而不是使用的原生 DOM 事件
- React 中的事件是通过事件委托方式处理的（委托给组件最外层的元素）

2. 通过 `event.target` 得到发生事件的 DOM 元素对象

## 2.5. 收集表单数据

2.5.1. 效果

需求: 定义一个包含表单的组件，输入用户名密码后, 点击登录提示输入信息

2.5.2. 理解

包含表单的组件分类

1. 非受控组件
2. 受控组件

## 2.6. 组件的生命周期

2.6.1. 效果

需求:定义组件实现以下功能：

1. 让指定的文本做显示或隐藏的渐变动画
2. 从完全可见，到彻底消失，耗时 2S
3. 点击“不活了”按钮从界面中卸载组件

2.6.2. 理解

1. 组件从创建到死亡它会经历一些特定的阶段。
2. React 组件中包含一系列钩子函数（生命周期回调函数）, 会在特定的时刻调用。
3. 我们在定义组件时，会在特定的生命周期回调函数中，做特定的工作。

2.6.3. 生命周期流程图（旧）

生命周期的三个阶段（旧）

初始化阶段: 由`ReactDOM.render()`触发---初次渲染

1. `constructor()`
2. `componentWillMount()`
3. `render()`
4. `componentDidMount()`

更新阶段: 由组件内部`this.setSate()`或父组件重新 render 触发

1. `shouldComponentUpdate()`
2. `componentWillUpdate()`
3. `render()`
4. `componentDidUpdate()`

卸载组件: 由`ReactDOM.unmountComponentAtNode()`触发

1. `componentWillUnmount()`

2.6.4. 生命周期流程图（新）

生命周期的三个阶段（新）

初始化阶段: 由`ReactDOM.render()`触发---初次渲染

1. `constructor()`
2. `getDerivedStateFromProps`
3. `render()`
4. `componentDidMount()`

更新阶段: 由组件内部`this.setSate()`或父组件重新 render 触发

1. `getDerivedStateFromProps`
2. `shouldComponentUpdate()`
3. `render()`
4. `getSnapshotBeforeUpdate`
5. `componentDidUpdate()`

卸载组件: 由`ReactDOM.unmountComponentAtNode()`触发

1. `componentWillUnmount()`

2.6.5. 重要的钩子

1. render：初始化渲染或更新渲染调用
2. componentDidMount：开启监听, 发送 ajax 请求
3. componentWillUnmount：做一些收尾工作, 如: 清理定时器

2.6.6. 即将废弃的钩子

1. componentWillMount
2. componentWillReceiveProps
3. componentWillUpdate

现在使用会出现警告，下一个大版本需要加上 `UNSAFE_` 前缀才能使用，以后可能会被彻底废弃，不建议使用。

## 2.7. 虚拟 DOM 与 DOM Diffing 算法

2.7.1. 效果

需求：验证虚拟 DOM Diffing 算法的存在

2.7.2. 基本原理图

# 第 3 章：React 应用

## 3.1. 使用 create-react-app 创建 react 应用

3.1.1. react 脚手架

1. xxx 脚手架: 用来帮助程序员快速创建一个基于 xxx 库的模板项目

- 包含了所有需要的配置（语法检查、jsx 编译、devServer 等）
- 下载好了所有相关的依赖
- 可以直接运行一个简单效果

2. react 提供了一个用于创建 react 项目的脚手架库: create-react-app
3. 项目的整体技术架构为: react + webpack + es6 + eslint
4. 使用脚手架开发的项目的特点: 模块化，组件化，工程化

3.1.2. 创建项目并启动

第一步，全局安装：`npm i -g create-react-app`
第二步，切换到想创项目的目录，使用命令：`create-react-app hello-react`
第三步，进入项目文件夹：`cd hello-react`
第四步，启动项目：`npm start`

3.1.3. react 脚手架项目结构

```
public ---- 静态资源文件夹
  favicon.icon ------ 网站页签图标
  index.html -------- 主页面
  logo192.png ------- logo图
  logo512.png ------- logo图
  manifest.json ----- 应用加壳的配置文件
  robots.txt -------- 爬虫协议文件
src ---- 源码文件夹
  App.css -------- App 组件的样式
  App.js --------- App 组件
  App.test.js ---- 用于给 App 做测试
  index.css ------ 样式
  index.js ------- 入口文件
  logo.svg ------- logo 图
  reportWebVitals.js --- 页面性能分析文件
  setupTests.js ---- 组件单元测试的文件
```

3.1.4. 功能界面的组件化编码流程

1. 拆分组件: 拆分界面，抽取组件
2. 实现静态组件: 使用组件实现静态页面效果
3. 实现动态组件
   - 动态显示初始化数据
   - 数据类型
   - 数据名称
   - 保存在哪个组件?
   - 交互（从绑定事件监听开始）

## 3.2. 组件的组合使用-TodoList

功能: 组件化实现此功能

1. 显示所有 todo 列表
2. 输入文本，点击按钮显示到列表的首位，并清除输入的文本

# 第 4 章：React ajax

## 4.1. 理解

4.1.1. 前置说明

1. React 本身只关注于界面，并不包含发送 ajax 请求的代码
2. 前端应用需要通过 ajax 请求与后台进行交互（json 数据）
3. react 应用中需要集成第三方 ajax 库

4.1.2. 常用的 ajax 请求库

1. jQuery: 比较重, 如果需要另外引入不建议使用
2. axios: 轻量级, 建议使用

- 封装 XmlHttpRequest 对象的 ajax
- promise 风格
- 可以用在浏览器端和 node 服务器端

## 4.2. axios

4.2.1. 文档

https://github.com/axios/axios

## 4.3. 案例—github 用户搜索

4.3.1. 效果

请求地址: https://api.github.com/search/users?q=xxxxxx

## 4.4. 消息订阅-发布机制

1. 工具库: PubSubJS
2. 下载: `npm install pubsub-js --save`
3. 使用:

```js
import PubSub from 'pubsub-js'; //引入
PubSub.subscribe('delete', function (data) {}); //订阅
PubSub.publish('delete', data); //发布消息
```

## 4.5. 扩展：Fetch

4.5.1. 文档

1. https://github.github.io/fetch/
2. https://segmentfault.com/a/1190000003810652

4.5.2. 特点

1. fetch: 原生函数，不再使用 XmlHttpRequest 对象提交 ajax 请求
2. 老版本浏览器可能不支持

4.5.3. 相关 API

1. GET 请求

```js
fetch(url)
  .then(function (response) {
    return response.json();
  })
  .then(function (data) {
    console.log(data);
  })
  .catch(function (e) {
    console.log(e);
  });
```

2. POST 请求

```js
fetch(url, {
  method: 'POST',
  body: JSON.stringify(data),
})
  .then(function (data) {
    console.log(data);
  })
  .catch(function (e) {
    console.log(e);
  });
```

# 第 5 章：React 路由

## 5.1. 相关理解

5.1.1. SPA 的理解

1. 单页 Web 应用（single page web application，SPA）。
2. 整个应用只有一个完整的页面。
3. 点击页面中的链接不会刷新页面，只会做页面的局部更新。
4. 数据都需要通过 ajax 请求获取, 并在前端异步展现。

5.1.2. 路由的理解

1. 什么是路由?

- 一个路由就是一个映射关系
- key 为路径, value 可能是 function 或 component

2. 路由分类

后端路由：

- value 是 function, 用来处理客户端提交的请求。
- 注册路由：`router.get(path, function(req, res))`
- 工作过程：当 node 接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据

前端路由：

- 浏览器端路由，value 是 component，用于展示页面内容。
- 注册路由: `<Route path="/test" component={Test}>`
- 工作过程：当浏览器的 path 变为 `/test` 时, 当前路由组件就会变为 Test 组件

  5.1.3. react-router-dom 的理解

1. react 的一个插件库。
2. 专门用来实现一个 SPA 应用。
3. 基于 react 的项目基本都会用到此库。

## 5.2. react-router-dom 相关 API

5.2.1. 内置组件

1. BrowserRouter
2. HashRouter
3. Route
4. Redirect
5. Link
6. NavLink
7. Switch

5.2.2. 其它

1. history 对象
2. match 对象
3. withRouter 函数

## 5.3. 基本路由使用

5.3.1. 效果

5.3.2. 准备

1. 下载 react-router-dom: `npm install --save react-router-dom`
2. 引入 bootstrap.css: `<link rel="stylesheet" href="/css/bootstrap.css">`

## 5.4. 嵌套路由使用

1. 注册子路由时要写上父路由的 path 值
2. 路由的匹配是按照注册路由的顺序进行的

## 5.5. 向路由组件传递参数数据

1. params 参数

路由链接(携带参数): `<Link to='{/demo/test/tom/18'}>详情</Link>`
注册路由(声明接收): `<Route path=" /demo/test/ :name/ :age" component={Test}/>`
接收参数: `this.props.match.params`

2. search 参数

路由链接(携带参数): `<Link to= '{/demo/test?name=tom&age=18' }>详情</Link>`
注册路由(无需声明，正常注册即可): `<Route path=" /demo/test" component={Test}/>`
接收参数: `this.props.location.search`
备注:获取到的 search 是 urlencoded 编码字符串，需要借助 querystring 解析

3. state 参数

路由链接(携带参数): `<Link to={{path:'/demo/test',state: {name: 'tom' ,age:18}}}>详情</Link>`
注册路由(无需声明，正常注册即可): `<Route path=" /demo/test" component={Test}/>`
接收参数: `this.props.location.state`
备注:刷新也可以保留住参数

## 5.6. 多种路由跳转方式

1. push
2. replace

BrowserRouter 与 HashRouter 的区别

1. 底层原理不一样:

- BrowserRouter 使用的是 H5 的 history API，不兼容 IE9 及以下版本。
- HashRouter 使用的是 URL 的哈希值。

2. url 表现形式不一样
   BrowserRouter 的路径中没有#,例如: `localhost:3000/demo/test`
   HashRouter 的路径包含#,例如:`localhost:3000/#/demo/test`

3. 刷新后对路由 state 参数的影响

- BrowserRouter 没有任何影响，因为 state 保存在 history 对象中。
- HashRouter 刷新后会导致路由 state 参数的丢失。

4. 备注: HashRouter 可以用于解决一些路径错误相关的问题。

# 第 6 章：React UI 组件库

## 6.1.流行的开源 React UI 组件库

[material-ui](http://www.material-ui.com/#/)
[ant-design](https://ant.design/index-cn)

# 第 7 章：redux

## 7.1. redux 理解

7.1.1. 学习文档

[英文文档](https://redux.js.org/)
[中文文档](http://www.redux.org.cn/)
[Github](https://github.com/reactjs/redux)

7.1.2. redux 是什么

1. redux 是一个专门用于做状态管理的 JS 库（不是 react 插件库）。
2. 它可以用在 react/angular/vue 等项目中，但基本与 react 配合使用。
3. 作用: 集中式管理 react 应用中多个组件共享的状态。

7.1.3. 什么情况下需要使用 redux

1. 某个组件的状态，需要让其他组件可以随时拿到（共享）。
2. 一个组件需要改变另一个组件的状态（通信）。
3. 总体原则：能不用就不用, 如果不用比较吃力才考虑使用。

7.1.4. redux 工作流程

## 7.2. redux 的三个核心概念

7.2.1. action

1. 动作的对象
2. 包含 2 个属性

- type：标识属性，值为字符串，唯一，必要属性
- data：数据属性，值类型任意，可选属性

```js
{ type: 'ADD_STUDENT',
  data: {
    name: 'tom',
    age:18
  }
}
```

7.2.2. reducer

1. 用于初始化状态、加工状态。
2. 加工时，根据旧的 state 和 action， 产生新的 state 的纯函数。

7.2.3. store

1. 将 state、action、reducer 联系在一起的对象
2. 如何得到此对象?

```js
import { createStore } from 'redux';
import reducer from './reducers';
const store = createStore(reducer);
```

## 7.3. redux 的核心 API

7.3.1. createstore()

作用：创建包含指定 reducer 的 store 对象

7.3.2. store 对象

1. 作用: redux 库最核心的管理对象
2. 它内部维护着:

- state
- reducer

3. 核心方法:

- `getState()`
- `dispatch(action)`
- `subscribe(listener)`

4. 具体编码:

- `store.getState()`
- `store.dispatch({type:'INCREMENT', number})`
- `store.subscribe(render)`

  7.3.3. applyMiddleware()

作用：应用上基于 redux 的中间件（插件库）

7.3.4. combineReducers()

作用：合并多个 reducer 函数

## 7.4. 使用 redux 编写应用

效果

## 7.5. redux 异步编程

7.5.1 理解：

1. redux 默认是不能进行异步处理的
2. 某些时候应用中需要在 redux 中执行异步任务，例如 ajax 或定时器

7.5.2. 使用异步中间件

```
npm install --save redux-thunk
```

## 7.6. react-redux

7.6.1. 理解

1. 一个 react 插件库
2. 专门用来简化 react 应用中使用 redux

7.6.2. react-Redux 将所有组件分成两大类

1. UI 组件

- 只负责 UI 的呈现，不带有任何业务逻辑
- 通过 props 接收数据（一般数据和函数）
- 不使用任何 Redux 的 API
- 一般保存在 components 文件夹下

2. 容器组件

- 负责管理数据和业务逻辑，不负责 UI 的呈现
- 使用 Redux 的 API
- 一般保存在 containers 文件夹下

  7.6.3. 相关 API

1. Provider：让所有组件都可以得到 state 数据
2. connect：用于包装 UI 组件生成容器组件
3. mapStateToprops：将外部的数据（即 state 对象）转换为 UI 组件的标签属性
4. mapDispatchToProps：将分发 action 的函数转换为 UI 组件的标签属性

## 7.7. 使用上 redux 调试工具

7.7.1. 安装 chrome 浏览器插件

7.7.2. 下载工具依赖包

```
npm install --save-dev redux-devtools-extension
```

## 7.8. 纯函数和高阶函数

7.8.1. 纯函数

1. 一类特别的函数: 只要是同样的输入（实参），必定得到同样的输出（返回）
2. 必须遵守以下一些约束??

- 不得改写参数数据
- 不会产生任何副作用，例如网络请求，输入和输出设备
- 不能调用 `Date.now()` 或者 `Math.random()` 等不纯的方法??

3. redux 的 reducer 函数必须是一个纯函数

7.8.2. 高阶函数

1. 理解: 一类特别的函数

- 情况 1: 参数是函数
- 情况 2: 返回是函数

2. 常见的高阶函数:

- 定时器设置函数
- 数组的 forEach/map/filter/reduce/find/bind
- promise
- react-redux 中的 connect 函数

3. 作用: 能实现更加动态, 更加可扩展的功能

# React 扩展

## 1. setState

### setState 更新状态的 2 种写法

```
(1). setState(stateChange, [callback])------对象式的setState
  1.stateChange为状态改变对象(该对象可以体现出状态的更改)
  2.callback是可选的回调函数, 它在状态更新完毕、界面也更新后(render调用后)才被调用

(2). setState(updater, [callback])------函数式的setState
  1.updater为返回stateChange对象的函数。
  2.updater可以接收到state和props。
  4.callback是可选的回调函数, 它在状态更新、界面也更新后(render调用后)才被调用。
```

总结:

1. 对象式的 setState 是函数式的 setState 的简写方式(语法糖)
2. 使用原则：
   (1).如果新状态不依赖于原状态 ===> 使用对象方式
   (2).如果新状态依赖于原状态 ===> 使用函数方式
   (3).如果需要在 setState()执行后获取最新的状态数据,
   要在第二个 callback 函数中读取

---

## 2. lazyLoad

### 路由组件的 lazyLoad

```js
	//1.通过React的lazy函数配合import()函数动态加载路由组件 ===> 路由组件代码会被分开打包
	const Login = lazy(()=>import('@/pages/Login'))

	//2.通过<Suspense>指定在加载得到路由打包文件前显示一个自定义loading界面
	<Suspense fallback={<h1>loading.....</h1>}>
        <Switch>
            <Route path="/xxx" component={Xxxx}/>
            <Redirect to="/login"/>
        </Switch>
    </Suspense>
```

---

## 3. Hooks

#### 1. React Hook/Hooks 是什么?

```
(1). Hook是React 16.8.0版本增加的新特性/新语法
(2). 可以让你在函数组件中使用 state 以及其他的 React 特性
```

#### 2. 三个常用的 Hook

```
(1). State Hook: React.useState()
(2). Effect Hook: React.useEffect()
(3). Ref Hook: React.useRef()
```

#### 3. State Hook

```
(1). State Hook让函数组件也可以有state状态, 并进行状态数据的读写操作
(2). 语法: const [xxx, setXxx] = React.useState(initValue)
(3). useState()说明:
        参数: 第一次初始化指定的值在内部作缓存
        返回值: 包含2个元素的数组, 第1个为内部当前状态值, 第2个为更新状态值的函数
(4). setXxx()2种写法:
        setXxx(newValue): 参数为非函数值, 直接指定新的状态值, 内部用其覆盖原来的状态值
        setXxx(value => newValue): 参数为函数, 接收原本的状态值, 返回新的状态值, 内部用其覆盖原来的状态值
```

#### 4. Effect Hook

```
(1). Effect Hook 可以让你在函数组件中执行副作用操作(用于模拟类组件中的生命周期钩子)
(2). React中的副作用操作:
        发ajax请求数据获取
        设置订阅 / 启动定时器
        手动更改真实DOM
(3). 语法和说明:
        useEffect(() => {
          // 在此可以执行任何带副作用操作
          return () => { // 在组件卸载前执行
            // 在此做一些收尾工作, 比如清除定时器/取消订阅等
          }
        }, [stateValue]) // 如果指定的是[], 回调函数只会在第一次render()后执行

(4). 可以把 useEffect Hook 看做如下三个函数的组合
        componentDidMount()
        componentDidUpdate()
    	componentWillUnmount()
```

#### 5. Ref Hook

```
(1). Ref Hook可以在函数组件中存储/查找组件内的标签或任意其它数据
(2). 语法: const refContainer = useRef()
(3). 作用:保存标签对象,功能与React.createRef()一样
```

## 4. Fragment

### 使用

```html
<Fragment><Fragment> <></Fragment></Fragment>
```

### 作用

> 可以不用必须有一个真实的 DOM 根标签了

## 5. Context

### 理解

> 一种组件间通信方式, 常用于【祖组件】与【后代组件】间通信

### 使用

```js
1) 创建Context容器对象：
	const XxxContext = React.createContext()

2) 渲染子组时，外面包裹xxxContext.Provider, 通过value属性给后代组件传递数据：
	<xxxContext.Provider value={数据}>
		子组件
    </xxxContext.Provider>

3) 后代组件读取数据：

	//第一种方式:仅适用于类组件
	  static contextType = xxxContext  // 声明接收context
	  this.context // 读取context中的value数据

	//第二种方式: 函数组件与类组件都可以
	  <xxxContext.Consumer>
	    {
	      value => ( // value就是context中的value数据
	        要显示的内容
	      )
	    }
	  </xxxContext.Consumer>
```

### 注意

    在应用开发中一般不用context, 一般都用它的封装react插件

## 6. 组件优化

### Component 的 2 个问题

> 1. 只要执行 setState(),即使不改变状态数据, 组件也会重新 render() ==> 效率低
>
> 2. 只当前组件重新 render(), 就会自动重新 render 子组件，纵使子组件没有用到父组件的任何数据 ==> 效率低

### 效率高的做法

> 只有当组件的 state 或 props 数据发生改变时才重新 render()

### 原因

> Component 中的 shouldComponentUpdate()总是返回 true

### 解决

    办法1:
    	重写shouldComponentUpdate()方法
    	比较新旧state或props数据, 如果有变化才返回true, 如果没有返回false
    办法2:
    	使用PureComponent
    	PureComponent重写了shouldComponentUpdate(), 只有state或props数据有变化才返回true
    	注意:
    		只是进行state和props数据的浅比较, 如果只是数据对象内部数据变了, 返回false
    		不要直接修改state数据, 而是要产生新数据
    项目中一般使用PureComponent来优化

## 7. render props

### 如何向组件内部动态传入带内容的结构(标签)?

    Vue中:
    	使用slot技术, 也就是通过组件标签体传入结构  <A><B/></A>
    React中:
    	使用children props: 通过组件标签体传入结构
    	使用render props: 通过组件标签属性传入结构,而且可以携带数据，一般用render函数属性

### children props

    <A>
      <B>xxxx</B>
    </A>
    {this.props.children}
    问题: 如果B组件需要A组件内的数据, ==> 做不到

### render props

    <A render={(data) => <C data={data}></C>}></A>
    A组件: {this.props.render(内部state数据)}
    C组件: 读取A组件传入的数据显示 {this.props.data}

## 8. 错误边界

#### 理解：

错误边界(Error boundary)：用来捕获后代组件错误，渲染出备用页面

#### 特点：

只能捕获后代组件生命周期产生的错误，不能捕获自己组件产生的错误和其他组件在合成事件、定时器中产生的错误

##### 使用方式：

getDerivedStateFromError 配合 componentDidCatch

```js
// 生命周期函数，一旦后台组件报错，就会触发
static getDerivedStateFromError(error) {
    console.log(error);
    // 在render之前触发
    // 返回新的state
    return {
        hasError: true,
    };
}

componentDidCatch(error, info) {
    // 统计页面的错误。发送请求发送到后台去
    console.log(error, info);
}
```

## 9. 组件通信方式总结

#### 组件间的关系：

- 父子组件
- 兄弟组件（非嵌套组件）
- 祖孙组件（跨级组件）

#### 几种通信方式：

1.props：
(1).children props
(2).render props 2.消息订阅-发布：
pubs-sub、event 等等 3.集中式管理：
redux、dva 等等
4.conText:
生产者-消费者模式

#### 比较好的搭配方式：

父子组件：props
兄弟组件：消息订阅-发布、集中式管理
祖孙组件(跨级组件)：消息订阅-发布、集中式管理、conText(开发用的少，封装插件用的多)
