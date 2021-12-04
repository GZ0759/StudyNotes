# 移动端 vConsole 调试的使用方法

前言：由于手机一般不能打开调试工具，在开发时移动端项目或者 WebView 项目时，遇到问题比较难调试，不能根据控制台内容或者网络请求情况排查问题，因此我们可能需要借助 vConsole 提供了的专为手机网页前端设计的调试面板。下面介绍四种 vConsole 的使用实践。

## 1. 浏览器地址栏注入代码

这段代码主要是引用 vConsole 并在页面时进行初始化，基本只要在待调试页面的地址栏输入该内容，就可以运行这段 JS 代码并成功开启移动端调试工具。同时，可以把这段代码放到收藏夹哦。

```
javascript:(function () { var script = document.createElement('script'); script.src="//unpkg.com/vconsole@latest/dist/vconsole.min.js"; document.body.appendChild(script); script.onload = function () { var vConsole = new window.VConsole(); } })();
```

## 2. 直接在项目中引用插件

这也是官方文档所说的两种简单方式。

方法一：首先安装 NPM 包。然后 Import 并初始化后。

```
$ npm install vconsole
```

```js
import VConsole from 'vconsole';

const vConsole = new VConsole();
const vConsole = new VConsole({ maxLogNumber: 1000 });
console.log('Hello world');
vConsole.destroy();
```

方法二：使用 CDN 直接插入到 HTML

```html
<script src="https://unpkg.com/vconsole@latest/dist/vconsole.min.js"></script>
<script>
  // VConsole 默认会挂载到 `window.VConsole` 上
  var vConsole = new window.VConsole();
</script>
```

## 3. 利用事件驱动开启调试

在页面某个地方埋入过不起眼的操作，从而触发 vConsole 的初始化和页面重载。例如在输入框中输入特定内容，或者连续点击某个头像。

```js
// 触发处
let clickTime = 0;
const openVConsole = (ev) => {
  clickTime++;
  setTimeout(() => {
    clickTime = 0;
  }, 1500);
  if (clickTime >= 6) {
    localStorage.setItem('DEBUG', JSON.stringify(true));
    window.location.reload();
  }
};
```

```js
// 页面重载时
const debug = JSON.parse(localStorage.getItem('DEBUG'));
if (!debug) return;
let script = document.createElement('script');
script.src = '//unpkg.com/vconsole@latest/dist/vconsole.min.js';
document.body.appendChild(script);
script.onload = function () {
  let vConsole = new window.VConsole();
};
```

## 4. 利用地址栏参数开启调试

在项目初始化时，通过获取地址栏的特定参数，进入调试模式。例如在 Vue 项目的 App.vue 文件中写入。

```js
if (URLSearchParams) {
  let { search } = window.location;
  let params = new URLSearchParams(search);
  // debug=true
  let isDebug = params.get('debug') === 'true';
  if (!isDebug) return;
  let script = document.createElement('script');
  script.src = '//unpkg.com/vconsole@latest/dist/vconsole.min.js';
  document.body.appendChild(script);
  script.onload = function () {
    let vConsole = new window.VConsole();
  };
}
```
