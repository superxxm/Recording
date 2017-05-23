# Git搭建
1.Git配置
首先配置用户名与email

	$ git config --global user.name "example"
	$ git config --global user.email "example"

配置后会在家目录下生成.gitconfig文件，里面是Git全局配置文件，一般【配置方法是git config --global <配置名称> <配置值>。如果想是项目里的某个值与全局配置有区别，可在项目中使用`git config`不带`--global`来设置，会在当前项目目录下创建`.git/config`，生成针对当前项目的配置。
2.获取Git仓库
### Clone一个仓库
要Clone仓库需要知道仓库的地址。Git URL可以以ssh://,http(s)://,git://.协议访问

	$ git clone url

### 初始化新仓库
创建目录，使用`git init`初始化仓库
3.正常的工作流程
>1.创建或修改文件

>2.使用`git add`命令添加新创建或修改的文件到本地的缓存区

>3.使用`git commit`命令提交到本地代码库

>4.使用`git push`命令将本地代码库同步到远端代码库

>tips `git status`查看状态 `git diff --cached`命令查看缓冲区中那些文件被修改了`q`退出
>`$ git commit -m "..."`添加本次修改注释 `$ git commit -a`将没有添加到缓存区的修改也一起提交，但不会添加新建的文件只会提交更改

4.分支与合并

>Git的分支可以让你在主线（master分支）之外进行代码提交，同时又不会影响代码库主线。分支的作用体现在多人协作开发中，比如一个团队开发软件，你负责独立的一个功能需要一个月的时间来完成，你就可以创建一个分支，只把该功能的代码提交到这个分支，而其他同事仍然可以继续使用主线开发，你每天的提交不会对他们造成任何影响。当你完成功能后，测试通过再把你的功能分支合并到主线。

### 分支

创建分支：

	$ git branch branchname

>运行`git branch`命令可以查看当前的分支列表，以及目前开发环境处在那个分支上

>`git checkout branchname`可以切换到其他分支

>`git merge -m '注释' branchname`合并分支到主线分支， 如果没有发生修改冲突，则合并成功，如有冲突，则冲突文件合并失败，并且两个冲突的内容都会到文件中，我们可以手动去解决我们需要哪些

>`git branch -d branchname`删除分支

>`git reset --hare HEAS^`撤销合并

>`git log`查看所有的提交`git log --stat`显示每个提交中那些文件被修改了

- git config : 配置相关信息
- git clone : 复制仓库
- git init : 初始化仓库
- git add : 添加更新内容到索引中
- git diff : 比较内容
- git status : 获取当前项目状况
- git commit : 提交
- git branch : 分支相关
- git checkout : 切换分支
- git merge : 合并分支
- git reset : 恢复版本
- git log : 查看日志

# Git 本地项目上传
## 1.建立远程仓库
### a.设置用户信息(用户名和邮箱)
## 2.配置SSH KEY
### a.检查并删除ssh key
- 配置之前，先检查一下电脑中是否存在.ssh文件，如果有就删除然后重新开始。
### b.创建新的.ssh文件
>mkdir .ssh

### c.切换到.ssh文件下
>cd .ssh

### d.创建公钥和私钥
>ssh-keygen -t rsa -C"your email address"

回车不做任何操作
### e.查看是否存在 id_rsa(私钥) id_rsa.pub(公钥)，存在就成功了
>ls -la

### f.拷贝公钥
>pbcopy <~/.ssh/id_rsa.pub(mac专用命令)

### g.在GitHub上配置公钥
>add ssh key 后钥匙是灰色的

>执行 ssh -T git@github.com 激活公钥(测试使用)

## 3.上传本地项目
### a.建立Git仓库
切换到要上传的目录
>git init

### b.将项目中所有文件添加到仓库中
> git add .

后面有个点哦！！！
### c.将add的文件commit到git仓库
>git commit -m "comments"

### d.本地仓库与github上的仓库进行关联
>git remote add origin 远程仓库地址

### e.上传之前先从git上拉取一下
>git pull origin master

### f.push到远程仓库
>git push -u origin master

# GitHub fork项目后如何与原项目保持同步
## 方法一
>简单粗暴，删除fork的项目，重新fork一份();

## 方法二
>本地建立两个仓库的中介，把两个都拉取到本地，然后拉取原仓库的更新到本地，合并更新，然后在push到github

1. 准备本地目录，将fork的项目clone到本地
2. 进入仓库，列出所有远程仓库，发现只有自己的远程仓库
3. clone原项目到本仓库（git remote add xxx https://github.com/xxx/xxx.git），再次查看远程仓库信息
4. fetch原仓库的更新到本地(git fetch xxx)
5. 查看分支(git branch -av),合并分支(git checkout master,git merge xxx/master)
6. push到github完成更新(git push -u origin master)
