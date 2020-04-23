# git简单使用



#### git基本操作

https://wanggw.gitbook.io/chnote/gitguide/git-ji-ben-cao-zuo



#### 常用的 Git 命令

```shell
# 从远程将源码克隆到本地
git clone {$remote_url}

# 切换一个分支（已存在的本地分支，包括把远程分支拉到本地）
git checkout {$branch_name}

# 在当前分支下，创建一个新的分支并切换到该分支
git checkout -b {$new_branch_name}

# 添加当前目录下所有文件至版本库中
git add .

# 提交当前目录下所有文件至（本地）版本库
git commit -m "提交备注"

# 将 master 分支最新的代码 合并到当前分支 {$current_branche_name}
git checkout master && 
git pull && 
git checkout {$current_branche_name} && 
git merge master

# 将当前本地分支下已提交过的文件，推送至远程的master 分支(不建议操作)
git push -u origin master

# 将当前本地分支下已提交过的文件，推送至远程的这个当前分支
git push

# 打版本号 1.0.0 的 tag
git tag -a 1.0.0 -m "提交 tag 的备注"

# 将版本号1.0.0的tag推送至远程服务器
git push origin 1.0.0
```



