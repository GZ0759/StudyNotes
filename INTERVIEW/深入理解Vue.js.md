# 源码实践

## 数据驱动

### 文本模板解析

将文本的 Mustache 语法进行解析替换，其中嵌套节点采用递归的形式进行 DOM 替换。

```html
<div id="avue">
  <div>
    <p>{{name}}-{{message}}</p>
  </div>
  <p>{{name}}</p>
  <p>{{message}}</p>
</div>
```

```js
let data = {
  name: 'Major',
  message: 'vue code is easy',
};

let oNode = document.querySelector('#avue'),
  uNode = oNode.cloneNode(true);

function complileNode(template, data) {
  let mustache = /\{\{(.+?)\}\}/g;
  for (let node of template.childNodes) {
    let { nodeType, nodeValue } = node;
    if (nodeType === 3) {
      // 未解决嵌套属性问题
      let res = nodeValue.replace(mustache, (_, p) => {
        return data[p.trim()];
      });
      node.nodeValue = res;
    } else if (nodeType === 1) {
      complileNode(node, data);
    }
  }
}

complileNode(uNode, data);

oNode.parentNode.replaceChild(uNode, oNode);
```

### 虚拟节点

```js
class VNode {
  constructor(tag, data, value, type) {
    this.tag = tag && tag.toLowerCase();
    this.data = data; // 标签属性键值对
    this.value = value;
    this.type = type;
    this.children = [];
  }

  appendChild(vnode) {
    this.children.push(vnode);
  }
}

// 转换成虚拟节点
function getVNode(node) {
  let { nodeType, nodeName, nodeValue, attributes, childNodes } = node;
  let _vnode = null;
  // 元素节点
  if (nodeType === 1) {
    let _attrObj = {};
    // 元素属性
    for (let i = 0; i < attributes.length; i++) {
      let { nodeName, nodeValue } = attributes[i];
      _attrObj[nodeName] = nodeValue;
    }
    _vnode = new VNode(nodeName, _attrObj, undefined, nodeType);
    // 元素子节点
    for (let i = 0; i < childNodes.length; i++) {
      let childVnode = getVNode(childNodes[i]);
      _vnode.appendChild(childVnode);
    }
  } else if (nodeType === 3) {
    _vnode = new VNode(undefined, undefined, nodeValue, nodeType);
  }

  return _vnode;
}

let root = document.querySelector('#root');
let vroot = getVNode(root);

// 解析成真实节点
function parseVNode(vnode) {
  let { tag, data, value, type, children } = vnode;
  let _node = null;
  if (type === 1) {
    _node = document.createElement(tag);
    for (const [key, value] of Object.entries(data)) {
      _node.setAttribute(key, value);
    }

    for (const subVnode of children) {
      _node.appendChild(parseVNode(subVnode));
    }

    return _node;
  } else if (type === 3) {
    return document.createTextNode(value);
  }
}

let dom2 = parseVNode(vroot);
```

### 渲染和挂载函数

```js
/** 虚拟 DOM 构造函数 */
class VNode {}
/** 由 HTML DOM -> VNode: 将这个函数当做 compiler 函数 */
function getVNode(node) {}
/** 将虚拟 DOM 转换成真正的 DOM */
function parseVNode(vnode) {}
/** 根据路径 访问对象成员 */
function getValueByPath(obj, path) {}

/** 将 带有 坑的 Vnode 与数据 data 结合, 得到 填充数据的 VNode: 模拟 AST -> VNode */
function combine(vnode, data) {
  let _type = vnode.type;
  let _data = vnode.data;
  let _value = vnode.value;
  let _tag = vnode.tag;
  let _children = vnode.children;

  let _vnode = null;

  if (_type === 3) {
    // 文本节点
    _value = _value.replace(rkuohao, function (_, g) {
      return getValueByPath(data, g.trim());
    });

    _vnode = new VNode(_tag, _data, _value, _type);
  } else if (_type === 1) {
    // 元素节点
    _vnode = new VNode(_tag, _data, _value, _type);
    _children.forEach((_subvnode) =>
      _vnode.appendChild(combine(_subvnode, data))
    );
  }

  return _vnode;
}

function JGVue(options) {
  this._data = options.data;
  let elm = document.querySelector(options.el); // vue 是字符串, 这里是 DOM
  this._template = elm;
  this._parent = elm.parentNode;

  this.mount(); // 挂载
}

JGVue.prototype.mount = function () {
  // 需要提供一个 render 方法: 生成 虚拟 DOM
  this.render = this.createRenderFn(); // 带有缓存 ( Vue 本身是可以带有 render 成员 )

  this.mountComponent();
};

JGVue.prototype.mountComponent = function () {
  // 执行 mountComponent() 函数
  let mount = () => {
    // 这里是一个函数, 函数的 this 默认是全局对象 "函数调用模式"
    this.update(this.render());
  };
  mount.call(this); // 本质应该交给 watcher 来调用, 但是还没有讲到这里

  // this.update( this.render() ); // 使用发布订阅模式. 渲染和计算的行为应该交给 watcher 来完成
};

// 这里是生成 render 函数, 目的是缓存 抽象语法树 ( 我们使用 虚拟 DOM 来模拟 )
JGVue.prototype.createRenderFn = function () {
  let ast = getVNode(this._template);
  // Vue: 将 AST + data => VNode
  // 我们: 带有坑的 VNode + data => 含有数据的 VNode
  return function render() {
    // 将 带有 坑的 VNode 转换为 待数据的 VNode
    let _tmp = combine(ast, this._data);
    return _tmp;
  };
};

// 将虚拟 DOM 渲染到页面中: diff 算法就在里
JGVue.prototype.update = function (vnode) {
  // 简化, 直接生成 HTML DOM replaceChild 到页面中
  // 父元素.replaceChild( 新元素, 旧元素 )
  let realDOM = parseVNode(vnode);

  // 这个算法是不负责任的:
  // 每次会将页面中的 DOM 全部替换
  this._parent.replaceChild(realDOM, document.querySelector('#root'));
};
```

## 响应式原理

### 对象响应式化

```js
function defineReactive(target, key, value, enumerable) {
  if (typeof value === 'object' && value != null && !Array.isArray(value)) {
    // 引用类型
    reactify(value);
  }

  Object.defineProperty(target, key, {
    configurable: true,
    enumerable: !!enumerable,
    get() {
      console.log(`读取 ${key} 属性`);
      return value;
    },
    set(newVal) {
      console.log(`设置 ${key} 属性为: ${newVal}`);
      value = newVal;
    },
  });
}
// 响应式化
function reactify(o) {
  let keys = Object.keys(o);

  for (let i = 0; i < keys.length; i++) {
    let key = keys[i];
    let value = o[key];
    if (Array.isArray(value)) {
      // 数组
      for (let j = 0; j < value.length; j++) {
        reactify(value[j]);
      }
    } else {
      // 对象或值类型
      defineReactive(o, key, value, true);
    }
  }
}
```
