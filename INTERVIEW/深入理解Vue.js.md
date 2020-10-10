# 源码实践

## 文本模板解析

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
