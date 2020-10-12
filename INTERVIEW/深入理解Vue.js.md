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

## 类封装/数据渲染优化

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
