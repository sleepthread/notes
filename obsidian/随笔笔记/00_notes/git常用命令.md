### 1、[[git]]常用命令

```
git status
git add .
git commit -m '提交信息'
git pull
git push

git checkout .   #放弃工作区中全部的修改
```
### 2、[[git]]分支管理
**创建分支**
```
git branch -a  #查看所有分支
git branch <branch_name>       #创建分支，不会自动切换
git checkout <branch_name>     #切换分支
git checkout -b <branch_name>  #创建分支，并自动切换分支
git branch -d  <branch_name>   #删除本地分支
git push origin -d <branch_name>  # 删除远程分支
git push origin -–delete <branch_name>  # 删除远程分支
git push <remote_name> –delete <branch_name> # 删除远程分支
```


 **删除远程已经删除的分支，但是本地仍有缓存的分支：**

```
git fetch --prune
git remote prune origin
```

这两个命令都会删除那些已经从远程仓库中删除但仍然存在于本地的远程跟踪分支。
使用`git fetch --prune`将同时获取最新的远程仓库数据并删除任何过时的远程跟踪分支。
而`git remote prune origin`只专注于删除过时的分支，不会获取新的远程仓库数据。
在执行上述命令后，再次运行`git branch -a`时，你就不应该再看到`origin/ver_791`分支了。


```
git checkout  .   # 放弃本地文件修改，未提交的
```
  
git 更新指定分支

在 Git 中，可以使用以下命令来更新指定分支：

1. 方法一：使用 git checkout 命令切换到指定分支，然后使用 git pull 命令拉取最新的代码。
    

```
git checkout <branch_name>
git pull origin <branch_name>
```

这种方法适用于已经有本地分支的情况。

2. 方法二：使用 git fetch 命令获取最新的远程分支代码，然后使用 git merge 命令将远程分支合并到当前分支。
    

```
git fetch origin <branch_name>
git merge origin/<branch_name>
```

这种方法适用于没有本地分支，但想要更新指定分支代码的情况。

3. 方法三：使用 git pull 命令指定要拉取的远程分支。
    

```
git pull origin <branch_name>:<local_branch_name>
```

这种方法会将远程分支的代码拉取到指定的本地分支。如果本地分支已经存在，则会合并远程分支的代码；如果本地分支不存在，则会创建一个新的本地分支。

以上是几种常见的更新指定分支的方法，具体使用哪种方法取决于你的需求和项目的状态。