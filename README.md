# git-commit-commitizen
### A vue project

## git config
```bash

  在git中，我们使用git config 命令用来配置git的配置文件，git配置级别主要有以下3类：

  1、仓库级别 local 【优先级最高】
  2、用户级别 global【优先级次之】
  3、系统级别 system【优先级最低】

  git config -l  等同  git config --list  查看所有的配置信息
  git config --local -l 查看仓库配置
  git config --global -l 查看用户配置
  git config --system -l 查看系统配置

  ```
## git config 设置

```
  git config [--local|--global|--system] user.email "you@example.com"
  git config [--local|--global|--system] user.name "Your Name"

  git config user.name 'Your name'
  等同于 git config --local user.name 'Your name'

```

## git config配置文件（ 增 、删、改、查 ）

### 增
```bash

  git config --global --add configName configValue

```

### 删
```bash

  git config --global --unset configName
  (只针对存在唯一值的情况)
  
```

### 改
```bash

  git config --global configName configValue
  
```

### 改
```bash

  git config --global configName

  或 git config --global --get configName
  
```



