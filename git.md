# Git简单使用



#### Git基本操作

##### 基础流程

- git init			                  #把这个文件夹变成Git可管理的仓库。

- git add .                            #把该目录下的所有文件添加到仓库，注意点是用空格隔开的

- git add index.html          #(只添加一个)把项目添加到仓库

- git status                          #查看状态

- git commit -m "第一次提交"

  #把项目提交到仓库。( -m后面引号里面是本次提交的注释内容，这个可以不写，但最好写上，不然会报错)

- 若提示  请告诉我你是谁 添加邮箱昵称

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

- git remote add origin https://github.com/sxxxzi/sxxxn.git       #Git仓库和本地仓库进行关联

- git push -u origin master                           #将当前本地分支下已提交过的文件，推送至远程的master 分支

  可能提示输入账号密码

  Username for 'https://github.com': sal×××
  Password for 'https://sxxxzi@github.com': xxxxxx

##### 常用操作

- git clone {$remote_url}					    # 从远程将源码克隆到本地
- git branch bug_fix 								# 建立branch，名为bug_fix
- git checkout bug_fix 							 # 切换到bug_fix
- git push                                                   #将当前本地分支下已提交过的文件，推送至远程的这个当前分支

##### 分支管理

- git branch bug_fix 								# 建立branch，名为bug_fix
- git checkout bug_fix 							 # 切换到bug_fix
- git checkout master 							 #切换到主要的repo
- git merge bug_fix 								 #把bug_fix这个branch和现在的branch合并
- git branch -d  Chapater6                      #删除本地分支Chapater6

##### 远程branch

- git branch -r		 				                               # 查看远程branch

- git remote update origin --prune                    #更新远程分支列表

- git push origin --delete Chapater6                  #删除远程分支Chapater6

- git checkout -b bug_fix_local bug_fix_remote 

  #把本地端切换为远程的bug_fix_remote branch并命名为bug_fix_local

##### 查看repo状态的工具

- git log 									#可以查看每次commit的改变
- git diff                                    #可以查看最近一次改变的內容，加上参数可以看其它的改变并互相比较
- git show                                #可以看某次的变更
- git status                              #查看状态

##### 其他

- git tag -a 1.0.0 -m "提交 tag 的备注"      #打版本号 1.0.0 的 tag

- git push origin 1.0.0                                #将版本号1.0.0的tag推送至远程服务器

- 推送本地标签到云仓库          git push origin --tags

- 显示某个标签的详细信息      git show v1.0.0

- 显示标签列表                          git tag

- 删除本地标签                          git tag -d 2.0.0

- 删除远程标签                          git push origin :refs/tags/2.0.0

- 撤销当前的修改                      git reset —hard

- 修改仓库名                              git remote rename  oldname newname  (一般oldname是origin) 

  注：以后推送时执行的命令就不再是 git push origin master  而是 git push newname master 拉取也是一样的



#### Git常用操作

##### 全局配置

- 全局设置用户名：$ git config --global user.name "XXXX"
- 全局设置邮箱：$ git config --global user.email "XXXX@gmail.com"
- 全局设置查看命令：$ git config -l

##### **局部配置**

- 局部设置用户名：$ git config user.name "XXXX"
- 局部设置邮箱：$ git config user.email "XXXX@gmail.com"
- 设置查看命令：$ git config --list

##### 撤销修改和代码回滚

- git reset --hard f8b05d07dc9220e79387b9a183e9ebaab97257cd     回滚代码到某个版本

- git reset –soft f8b05d07dc9220e79387b9a183e9ebaab97257cd       会将之间的修改全部进行revert,然后在进行add commit操作就行了.

- 撤销当前的修改                      git reset —hard

- 回滚到标签

  1. 先 git clone 整个仓库

  2. 然后 git checkout tag_name 就可以取得 tag 对应的代码了

  3. 这时候 git 可能会提示你当前处于一个“detached HEAD" 状态，因为 tag 相当于是一个快照，是不能更改它的代码的，如果要在 tag 代码的基础上做修改，你需要一个分支：git checkout -b branch_name tag_name，这样会从 tag 创建一个分支，然后就和普通的 git 操作一样了。

##### 文件忽略

在git中如果想忽略掉某个文件，不让这个文件提交到版本库中，可以使用修改根目录中 .gitignore 文件的方法（如无，则需自己手工建立此文件）。这个文件每一行保存了一个匹配的规则例如：

```
# 此为注释 – 将被 Git 忽略

*.a       # 忽略所有 .a 结尾的文件

!lib.a    # 但 lib.a 除外

/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO

build/    # 忽略 build/ 目录下的所有文件

doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

将某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，原因是.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。解决方法就是先把本地缓存删除（改变成未track状态），然后再提交：

```
git rm -r --cached .

git add .

git commit -m 'update .gitignore'
```

##### 记住密码

- 带密码形式的添加远程仓库：

  1. git remote add origin http://yourUsername:password@git.oschina.net/name/project.git
  2. git remote add origin http://yourUsername:yourPassword@xxx.com/xxproject.git

- 设置存储密码：

  1. 长期存储：git config --global credential.helper store
  2. 默认15分钟：git config --global credential.helper cache
  3. 自定义保存时长：git config credential.helper 'cache --timeout=3600' （**保存一小时**）

- 添加 SSH Key：

  1. 生成SSH：`ssh-keygen -t rsa -C "XXXX@gmail.com"`
  2. 查看SSH：`cat ~/.ssh/id_rsa.pub`

##### SSH Key：常用命令

1. 生成 SSH Key：`ssh-keygen -t rsa -C "XXXX@gmail.com"`（一路回车，或者设置一个密码）
2. 拷贝 SSH Key：`cat ~/.ssh/id_rsa.pub`
3. 添加 SSH Key：
4. 测试 SSH Key：`ssh -T git@git.oschina.net`
5. 获取 ssh key 方法一：`vim ~/.ssh/id_rsa.pub`
6. 获取 ssh key 方法一：`cat ~/.ssh/id_rsa.pub`