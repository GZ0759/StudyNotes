# 合并所有 MD 文件

```js
const fs = require('fs');

async function print(path) {
  let dir = await fs.readdirSync(path);
//   过滤index.md/index.js
  dir = dir.filter((item) => item.indexOf('index') < 0);
  let content = '';
  for (const dirent of dir) {
    let data = fs.readFileSync('./' + dirent);
    // 将文件名设置一级标题
    let title = dirent.slice(0, dirent.length - 3);
    content = content + `\n# ${title}\n` + data.toString();
  }
  const data = new Uint8Array(Buffer.from(content));
  fs.writeFile('index.md', data, (err) => {
    if (err) throw err;
    console.log('The file has been saved!');
  });
}
print('./').catch(console.error);
```
