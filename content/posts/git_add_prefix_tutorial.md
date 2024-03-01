---
title: "git commit时如何自动添加前缀"
date: 2024-03-01T17:49:38+08:00
draft: false
categories: ["development"]
featuredImagePreview: "/images/git.jpeg"
featuredImage: "/images/git.jpeg"
---

> # 功能说明

该钩子可用于在`git commit`时自动给`message`添加前缀

> # 使用说明

> ## 1 创建`commit-msg`钩子:

控制台输入:
```shell

npx husky add commit-msg

```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

> ## 2 在`.husky/`下创建`hooks/commit-msg.js`，并写入以下内容

```javascript
function getFileContent(filePath) {
  try {
    var buffer = fs.readFileSync(filePath);
    var hasToString = buffer && typeof buffer.toString === 'function';

    return hasToString && buffer.toString();
  } catch (err) {
    if (err && err.code !== 'ENOENT' && err.code !== 'ENAMETOOLONG') {
      throw err;
    }
  }
}
require('dotenv').config({ path: '.env' });
const path = require('path');
const fs = require('fs');
const dotenv = require('dotenv');
const commitMsgPath = process.argv[2];
const gitMsgPath = path.resolve(__dirname, '../../', commitMsgPath);
const prefix = process.env.prefix;
const commitMsg = prefix + getFileContent(gitMsgPath);
let ret = 0;
console.log('this is the commiting message:@@ ', commitMsg);
if (commitMsg.match(/^--(story|bug)=[0-9]+/)) {
  console.log('提交符合规范！@@');
  fs.writeFileSync(gitMsgPath, commitMsg);
} else {
  ret = 1;
  console.log(`提交不符合规范！`);
}
process.exit(ret);

```

> ## 3 将以下内容覆盖到`.husky/commit-msg`


```shell
#!/bin/sh

commitFiles=$(git diff --name-only --cached)
sudo node  ./.husky/hooks/commit-msg.js $1 $commitFiles
```

> ## 4 在根目录创建`.env`文件，并写入以下内容

```shell
prefix="--story=xxx 你想要添加的前缀"
```

> ## 5 挂载钩子

```shell
npx husky install
```
