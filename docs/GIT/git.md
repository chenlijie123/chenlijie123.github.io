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

#### 远程分支更新到本地

```
  git remote update origin --prune

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