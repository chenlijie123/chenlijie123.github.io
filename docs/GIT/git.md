## git

#### 基础提交指令

```
  git pull  同步远程分支合到本地

  git status 查看当前状态

  git add . / 文件名  添加修改到暂存区

  git commit -a "注释"  将暂存区内容添加到本地仓库中

  git push origin 分支名 推远程仓库

```

#### 分支

```
  git clone 地址 // 克隆项目

  git branch 查看本地分支

  git branch -a 查看远程分支

  git branch 分支名  // 新建

  git checkout 分支名  // 切换

  git branch -b 分支名 // 创建并切换分支

  git branch -d 分支名 // 删除本地分支

  git push origin --delete 远程分支名  //删除远程分支

```

#### 合并
```
git checkout 目标分支名 // 切换到目标分支
git pull // 同步数据
git merge dev  // 把改动的dev分支合并到目标分支

```

#### 回退
```
git log  // 查看提交日志

git reset -- head commit_id // 回退到指定commit_id版本

git reset HEAD^ 回退上个版本

git reset HEAD^ hello.js 回退hello.js文件的版本到上一个版本

git reset --head origin/master 将本地回退到与远程master一样

```
#### 误删恢复
```
git reflog  //  复制要恢复操作前的hash值

git reset --head hash 

```

#### 远程分支更新到本地

```
  git remote update origin --prune

```

#### 远程分支与本地

`git fetch`与 `git remote update origin --prune`区别

- git fetch 拉取分支，远程被删去的分支不会同步删除本地的origin/xxx分支

      例如本地有dev分支、有origin/dev，现在远程新加test分支，删除了dev分支，git fetch后  
      本地新增origin/test(并不会有test分支，需要checkout test)，但不会删除本地的origin/dev
- git remote update origin --prune

      与上面相同情况下，执行命令后本地新增origin/test分支(没有test需checkout)，且会删除掉本地  
      的origin/dev分支，但不会删除本地的test分支

`git fetch`与`git pull`区别

      git pull包含git fetch与git merge，例如test分支，git pull之后，会把本地的origin/test同步  
      到最新，然后merge到本地的test分支，类似于git merge origin/test

#### 同步远程分支和本地分支

- 本地有新分支dev远程没有

      直接推送到远程
      git checkout -b dev 新建dev，类似 git branch dev和git checkout dev缩写
      git push -u origin dev 推送到远程仓库
      git branch -a 查看远程分支是否有dev

- 远程有dev 本地没有

      远程仓库同步本地
      git fetch 将远程主句的更新全部取回本地  
      git branch -a 查看远程分支  
      git branch 查看本地分支  
      git checkout -b dev 创建并切换到本地dev

- 本地删除了dev 远程仓库也想删除dev

      git branch -d 分支名 删除本地分支  
      git push origin -d 分支名 删除远程分支  

- 远程删除了分支，本地也想删除

      git remote show origin 查看远程分支与本地分支对应关系  
      git remote prune origin 删除远程已经删除过的分支  

- git fetch 同步远程本地分支
      git branch -a 查看远程与本地分支区别
      git remote prune origin --dry-run 列出所有本地可以删除的分支
      git remote prune origin 删除

####  tag

- 查看、筛选 tag标签 

      git tag 所有标签
      git tag -l xxx 筛选标签名为xxx的标签
      git show 标签名 查看标签信息
      git log --oneline --graph 在提交历史中查看标签

- 创建 tag
      git tag 标签名 给当前的提交版本创建一个(轻量标签)
      git tag 标签名 提交版本号(commitID) 给指定版本创建一个(轻量标签)

      git tag -a 标签名称 -m 附注信息 给当前提交版本创建(附注标签)
      // 例如 git tag -a v4.0 -m "里程碑版本 4.0 发布"
      git tag -a 标签名 commitID -m "附注信息" 给指定的commit提交版本创建(附注标签)

- 删除 tag

      git tag -d 标签名 删除指定标签 （本地）

      git push origin :regs/tags/标签名称(远程仓库)
      or
      git push origin --delete 标签名称(远程仓库)

- 推送远程仓库
      git push origin 标签名 单个推送
      or
      git push origin --tags 全部推送

- 以tag标签版本为基础 创建新的分支
      git checkout -b 分支名称 标签名称