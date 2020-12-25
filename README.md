# git-commit-standardization

## 规范 git 提交内容和自动生成 change log

### 规范 git commit 提交内容

- 安装 commitizen 和 cz-conventional-changelog：`npm install -D commitizen cz-conventional-changelog`；规范 git commit 提交的内容。**此时执行 `git commit - m "message"` 依然可以跳过规范提交代码。**
- package.json 加入下面内容：

  ```package.json
  "config":{
    "commitizen":{
      "path":"node_modules/cz-conventional-changelog"
    }
  }
  "scripts":{
    commit:"git-cz"
  }
  ```

- 安装 @commitlint/config-conventional 和 @commitlint/cli：`npm install -D @commitlint/config-conventional @commitlint/cli`；**此时只能按照规范提交代码。**
- 在项目根目录新建 commitlint.config.js 或者 .commitlintrc.js 文件，配置如下内容：

  ```commitlint.config.js
  module.exports = {
    extents:[
     "@commitlint/config-conventional"
    ],
    rules:{}
   }
  ```

- 执行提交：`git add.` 然后 `npm run commit` 触发 `git-cz`

### 自动生成 change log

- 安装 conventional-changelog-cli：`npm install -D conventional-changelog-cli`；

  CHANGELOG.md 中的版本号即是从 package.json 中 version 字段来的；

  `conventional-changelog -p angular -i CHANGELOG.md -s`：不会覆盖以前的 Change log，只会在 CHANGELOG.md 的头部加上自从上次发布以来的变动；

  `conventional-changelog -p angular -i CHANGELOG.md -s -r 0`：生成所有发布的 Change log；

- package.json 加入下面配置：

  ```package.json
  "scripts":{
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
  }
  ```

- 生成 CHANGELOG.md：`npm run changelog`
