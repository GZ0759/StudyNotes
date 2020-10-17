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

### 类封装/数据渲染优化

```js
function JGVue(options) {
  this._data = options.data;
  this._el = options.el;
  this._templateDOM = document.querySelector(this._el);
  this._parent = this._templateDOM.parentNode;

  this.render();
}

JGVue.prototype.render = function () {
  this.compiler();
};

JGVue.prototype.compiler = function () {
  let realHTMLDOM = this._templateDOM.cloneNode(true);
  compiler(realHTMLDOM, this._data);
  this.update(realHTMLDOM);
};

JGVue.prototype.update = function (real) {
  this._parent.replaceChild(real, document.querySelector('#root'));
};

// 字符串路径来访问对象的成员
function getValueByPath(obj, path) {
  let paths = path.split('.');
  let res = obj;
  let prop;
  while ((prop = paths.shift())) {
    res = res[prop];
  }
  return res;
}
```

## 虚拟节点

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

//   转换成虚拟节点
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
