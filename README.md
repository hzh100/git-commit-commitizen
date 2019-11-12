# git-commit-commitizen

##### A vue project

## 采用 [Google Angularjs commit规范](https://github.com/angular/angular/blob/master/CONTRIBUTING.md#-commit-message-guidelines) 

### commit 工具流 [commitizen](https://github.com/commitizen/cz-cli)

### 安装 commitizen,安装cz-conventional-changelog

#### 项目内安装
```bash

  npm i commitizen cz-conventional-changelog --save-dev
  or yarn add commitizen cz-conventional-changelog --dev

```
##### 在package.json内手动配置
```bash

  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
  }

```
#### 全局安装 commitizen  项目内安装 cz-conventional-changelog 
###### 自动生成package.json 上面config配置

```bash

  npm i -g commitizen
  commitizen init cz-conventional-changelog --save --save-exact

```

#### 可添加script脚本commit命令 （ 通过 npm run commit命令进行提交commit信息了 ）

```bash

  "commit": "git-cz",  
  or  "commit": "git cz",

```

#### 以上操作安装配置完，可在项目中使用git cz 进行 commit

## 配置 commit message 验证， 验证是否符合规范
  1. 配置gitHooks
  ```
      // package.json

      {
        "gitHooks": {
          "pre-commit": "npm run lint",
          "commit-msg": "node scripts/verify-commit-msg.js"
        }
      }

  ```
  2. 添加验证msg格式的verify-commit-msg.js（参考vue作者尤大大在vue中的）
  ```
    const chalk = require('chalk')
    const msgPath = process.env.GIT_PARAMS
    const msg = require('fs').readFileSync(msgPath, 'utf-8').trim()

    const commitRE = /^(revert: )?(feat|fix|docs|style|refactor|perf|test|workflow|ci|chore|types)(\(.+\))?: .{1,50}/

    if (!commitRE.test(msg)) {
      console.log()
      console.error(
        `  ${chalk.bgRed.white(' ERROR ')} ${chalk.red(`invalid commit message format.`)}\n\n` +
        chalk.red(`  Proper commit message format is required for automated changelog generation. Examples:\n\n`) +
        `    ${chalk.green(`feat(compiler): add 'comments' option`)}\n` +
        `    ${chalk.green(`fix(v-model): handle events on blur (close #28)`)}\n\n` +
        chalk.red(`  See .github/COMMIT_CONVENTION.md for more details.\n`) +
        chalk.red(`  You can also use ${chalk.cyan(`npm run commit`)} to interactively generate a commit message.\n`)
      )
      process.exit(1)
    }

  ```

  #### 以上验证方式的好处是自由定制信息

  ### 当然，也可以通过已有的包` commitlint `进行开发（注意，老的推荐库validate-commit-msg已经弃用），这个包的使用很简单，[github仓库](https://github.com/conventional-changelog/commitlint) [官网](https://commitlint.js.org/#/)上有清晰的描述.

  ## 生成 change log

  #### 如果你的提交信息都符合上述的规范，那么这些信息就会出现在 change log 里面。

  #### 只有 `type` 为 `feat` 和 `fix` 的 commit 会出现在 change log 中，其他的不会出现，当然你也可以自己自定义。

  (```)
    function () {

    }
  (```)

  ### 安装依赖 conventional-changelog

  #### 网上很多资料都是
  ```
   项目中安装  npm i conventional-changelog -S
    或则 全局安装  npm install -g conventional-changelog

  ```
  #### 但是这种方法报错 command not found ,以为是conventional-changelog没有安装，通过命令：

  ` npm ls -g -depth=0 `

  #### 打印出
  （```）

      /Users/master/.nvm/versions/node/v10.16.0/lib
      ├── cnpm@6.1.0
      ├── commitizen@4.0.3
      ├── conventional-changelog@3.1.14
      ├── http-server@0.11.1
      └── npm@6.13.0

  (```)

  #### conventional-changelog 是存在的， 在这篇文章[Git 提交记录和分支模型](https://cattail.me/tech/2016/06/06/git-commit-message-and-branching-model.html)中发现Commitizen就依据conventional message，创建起一个生态：

     + [conventional-changelog-cli](https://github.com/conventional-changelog-archived-repos/conventional-changelog-cli)：通过提交记录生成 CHANGELOG.md
     + [conventional-github-releaser](https://github.com/conventional-changelog/releaser-tools)：通过提交记录生成 github release 中的变更描述
     + [conventional-recommended-bump](https://github.com/conventional-changelog-archived-repos/conventional-recommended-bump)：根据提交记录判断需要升级 Semantic Versioning 哪一位版本号
     + [validate-commit-msg](https://github.com/conventional-changelog-archived-repos/validate-commit-msg)：检查提交记录是否符合约定


  ## 正确的打开方式（生成 change log）安装 ` conventional-changelog-cli `

  ```
    项目中安装  npm i conventional-changelog-cli -S
    或则 全局安装  npm install -g conventional-changelog-cli

  ```

  #### 安装成功后 在项目目录下执行
  ` conventional-changelog -p angular -i CHANGELOG.md -w `
  或
  ` conventional-changelog -p angular -i CHANGELOG.md -w -r 0 `

  #### 为了方便使用，可以将其写入` package.json `的`scripts`字段

  ```
    {
      "scripts": {
        "changelog": "conventional-changelog -p angular -i CHANGELOG.md -w -r 0"
      }
    }

  ```
  #### 运行

  ` npm run changelog `











