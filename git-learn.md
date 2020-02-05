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

- 创建远程仓库

使用`Github`网站作为自己的远程仓库。注册一个账户，即可获得免费的Git远程仓库。

本地Git仓库与Github仓库之间的传输通过SSH加密，具体设置方法如下：

1. 创建`SSH Key`

在windows下，打开Git Bash，创建SSH Key:

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

注意替换邮件地址为自己的邮件地址，一路回车。 之后可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。 

2. 登陆GitHub创建连接

打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。

## 7. 管理分支





## 8. 管理标签


