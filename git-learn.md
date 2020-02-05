# 《廖雪峰Git教程》学习记录

作者：婷婷

摘要：在windows环境下，Git的基本用法记录，具体内容参考廖雪峰老师教程。

## 1.创建版本库

==注：Git跟踪并管理的是修改，而非文件==

工作区：在电脑里可以看到的目录；

暂存区：Git版本库里，称为stage或index的部分；

分支：Git自动创建的master。

![1580871337942](C:\Users\Tingting Wang\AppData\Roaming\Typora\typora-user-images\1580871337942.png)

- 创建版本库

1. 创建空目录

```
$ mkdir learngit
$ cd learngit
```

2. 初始化仓库

```
$ git init
```

在创建的空目录下编写一个`README.md`文件，内容随意。

3. 将文件添加到仓库

```
$ git add README.md
```

4. 将文件提交到仓库

```
$ git commit -m "wrote a readme file"
```

其中，`git add <file>`可反复使用，添加多个文件后，再使用`git commit -m <message>`一次提交所有文件。

## 2. 版本回退

提交了不合适的修改到版本库时，想要撤销本次提交，可使用版本回退。

- 查看提交日志

```
$ git log
```

或者查看简化版，显示的第一部分为`commit id`（版本号）：

```
$ git log --pretty=oneline
```

- 版本回退

 在Git中，用`HEAD`表示当前版本，也就是最新的`commit id`，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100` 。

1. 回退到上一个版本：

```
$ git reset --hard HEAD^
```

2. 回退到指定版本：

```
git reset --hard <commit id的前五个字符>
```

- 查看命令日志

可以看到每一条自己输入的历史命令。

```
$ git reflog
```

## 3. 管理修改

- 查看状态

```
$ git status
```

- 查看工作区与版本库的区别

```
$ git diff HEAD -- <file>
```

## 4. 撤销修改

- 撤销暂存区修改

  暂存区的修改回退到工作区。具体指已经使用`git add <file>`命令的情况。

  命令：`git reset HEAD <file>`  

  或：`git restore --staged <file>`

- 丢弃工作区的修改

  命令：`git checkout -- <file>`

  或：`git restore <file>` 

   `git checkout`是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原” 。

## 5. 删除文件

- 删除工作区文件

```
$ rm <file>
```

- 删除版本库文件

```
$ git rm <file>
$ git commit -m <message>
```

## 6. 远程仓库

### 6.1 创建远程仓库

使用`Github`网站作为自己的远程仓库。注册一个账户，即可获得免费的Git远程仓库。

本地Git仓库与Github仓库之间的传输通过SSH加密，具体设置方法如下：

1. 创建`SSH Key`

在windows下，打开Git Bash，创建SSH Key:

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

注意替换邮件地址为自己的邮件地址，一路回车。 之后可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。 

2. 登陆`GitHub`创建连接

打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。

3. 添加远程库

-  登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库 。
-  在Repository name填入`learngit`，其他保持默认设置，点击“Create repository”按钮，创建一个新的Git仓库。

4.  把本地仓库的内容推送到GitHub仓库 

- 将本地库与远程库关联：

```
$ git remote add origin git@github.com:username/learngit.git
```

注意替换username为自己的Github用户名。 远程库的名字就是`origin`，这是Git默认的叫法 。

 第一次使用Git的`clone`或者`push`命令连接GitHub时，会得到一个警告，选yes即可。

- 将本地库的内容推送到远程：

```
$ git push -u origin master
```

第一次推送master分支时加`-u`， 加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令 。 每次本地提交后，只要有必要，就可以使用命令：

```git push origin master
git push origin master
```

推送最新修改 。

### 6.2 从远程仓库克隆

1. 登陆Github，创建新的仓库。
2. 克隆一个本地库：

```
git clone git@github.com:username/repo-name.git
```

## 7. 管理分支

1. 创建分支`dev`

```
$ git checkout -b dev
```

 `git checkout`命令加上`-b`参数表示创建并切换，等价于：

```
$ git branch dev
$ git checkout dev
```

2. 查看当前分支

```
$ git branch
```

3. 切换回master主分支

```
$ git checkout master
```

也可以使用`switch`语句。

- 切换分支

```
$ git switch -c dev
```

- 切换回master

```
$ git switch master
```

4. 合并分支

```
$ git merge dev
```

5. 删除分支

```
$ git branch -d dev
```

6. 查看分支合并图

```
$ git log --graph --pretty=oneline --abbrev-commit
```

7. 解决冲突的办法

修改冲突部分内容后，重新提交到Git仓库。

8. 合并分支时关闭`Fast Forward`模式

```
$ git merge --no-ff -m "merge with no-ff" dev
```

9. 修复分支bug

- 保存工作现场

```
$ git status
```

- 创建临时分支

 确定要在哪个分支上修复bug，假定需要在`master`分支上修复，就从`master`创建临时分支： 

```
$ git checkout master
$ git checkout -b issue-101
```

在临时分支修复bug，提交内容。

```
$ git add <file>
$ git commit -m "fixed bug 101"
```

切换回master分支，并合并临时分支，然后删除临时分支。

- 恢复工作现场

返回工作分支：

```
$ git switch dev
```

查看工作现场列表：

```
$ git stash list
```

恢复现场：

```
$ git stash pop
```

- 修复工作现场同样的bug

```
$ git cherry-pick <bug fixed id>
```

多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令：

```
$ git stash apply stash@{0}
```

10. 强行删除

 要丢弃一个没有被合并过的分支，可以通过 

```
$ git branch -D <name>
```

强行删除 。

11. 多人协作

- 查看远程库信息

```
$ git remote
```

或者：

```
$ git remote -v
```

- 推送分支

```
$ git push origin <分支name>
```

- 抓取分支

```
$ git clone git@github.com:username/repo-name.git
```

 默认抓取本地的`master`分支。  要在`dev`分支上开发，就必须创建远程`origin`的`dev`分支到本地：

```
$ git checkout -b dev origin/dev
```

推送冲突时：

 先用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，解决冲突 。

```
$ git pull
```

 `git pull`也失败了，原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接，之后再`git pull`： 

```
$ git branch --set-upstream-to=origin/dev dev
$ git pull
```

本地合并冲突时，手动解决，参考<u>7.解决分支冲突的办法</u>部分内容。

12. 分支整理

 把本地未push的分叉提交历史整理成直线 。

```
$ git rebase
```

## 8. 管理标签

标签tag与某个commit绑在一起，易于记忆，比如：commit号是6a5819…的tag是v1.1。

- 创建标签

```
$ git tag <tagname>
```

- 查看标签

```
$ git tag
```

- 对指定commit打标签

```
$ git tag <tagname> <commit id>
```

 标签不是按时间顺序列出，而是按字母排序。

- 查看标签信息

```
$ git show <tagname>
```

-  创建带有说明的标签 

```
$ git tag -a v1.0 -m "version 1.0 released" 1094abd
```

- 删除本地标签

```
$ git tag -d v1.0
```

- 推送标签到远程

```
$ git push origin v1.0
```

或者推送所有本地标签：

```
$ git push origin --tags
```

- 删除已推送的标签

先删除本地标签：

```
$ git tag -d v1.0
```

再删除远程标签：

```
git push origin:refs/tags/v1.0
```

