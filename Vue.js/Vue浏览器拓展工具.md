# Vue Devtools

[安装地址](https://devtools.vuejs.org/)

## 生产环境开启

```js
const devtools = window.__VUE_DEVTOOLS_GLOBAL_HOOK__;
const hasRoot = document.querySelector('#app');
if (!hasRoot) return alert('找不到挂在节点');
const Vue = hasRoot.__vue__.__proto__.__proto__.constructor;
Vue.config.devtools = true;
devtools.emit('init', Vue);
```

Bookmarklet

```js
javascript:(function(){const devtools=window.__VUE_DEVTOOLS_GLOBAL_HOOK__;const hasRoot=document.querySelector('#app');if(!hasRoot)return%20alert('%E6%89%BE%E4%B8%8D%E5%88%B0%E6%8C%82%E5%9C%A8%E8%8A%82%E7%82%B9');const%20Vue=hasRoot.__vue__.__proto__.__proto__.constructor;Vue.config.devtools=true;devtools.emit('init',Vue);})();
```

### 代码解析

**/src/core/util/env.js**

```js
// 部分核心源码
// detect devtools
export const devtools = inBrowser && window.__VUE_DEVTOOLS_GLOBAL_HOOK__;
```

**/src/platforms/web/runtime/index.js**

```js
// 部分核心源码
// devtools global hook
if (config.devtools) {
  if (devtools) {
    devtools.emit('init', Vue);
  } else if (
    process.env.NODE_ENV !== 'production' &&
    process.env.NODE_ENV !== 'test'
  ) {
    console[console.info ? 'info' : 'log'](
      'Download the Vue Devtools extension for a better development experience:\n' +
        'https://github.com/vuejs/vue-devtools'
    );
  }
}
```
