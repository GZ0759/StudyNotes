# 合并所有 MD 文件

需求：将当前文件夹下的所有 markdown 文件整合在一个新的 markdown 文件中。

```js
const fs = require('fs');

async function print(path) {
  let dir = await fs.readdirSync(path);
  // 过滤index.md/index.js
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

# 接口爬取

需求：获取接口内容并进行格式化输入

```js
const axios = require('axios');

const baseUrl = 'https://www.baidu.com';
const token = 'xxx';
const CreateNoCache = (noCache) => {
  return Math.random() > 0.5
    ? noCache + 0.000000001
    : noCache - 0.00000000000001;
};
const noCache = CreateNoCache(0.52268533670679);

var config = {
  method: 'get',
  url: `${baseUrl}?noCache=${noCache}&pageNum=1&pageSize=10&productId=11&executorIds=666&createStatus`,
  headers: {
    'x-clouddev-token': token,
  },
};

const handleDataPrint = (response) => {
  const { taskList = [] } = response.data.data;
  const res = taskList
    .filter((item) => item.taskProgress < 100)
    .map((item) => {
      const { taskProgress, taskTitle, taskId } = item;
      return [taskId, taskProgress + '%', taskTitle];
    });
  console.log('content for you is\n', res);
};

axios(config)
  .then(function (response) {
    handleDataPrint(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```
