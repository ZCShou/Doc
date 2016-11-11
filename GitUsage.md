# Git 使用记录

　　笔者用的是Win10系统，所以以下内容均是以Win10为基础，也因此没能在其他平台上测试。不过，应该不会差很多。

　　当然，网上现在关于GIT的教程数不胜数。不过，以下所有内容均是在笔者亲身实践的基础之上，可以说，下面的内容就是笔者使用的一个记录。

## Git 安装

　　对于Windows上安装，非常简单，直接登录[官网](https://git-scm.com/)或者https://git-for-windows.github.io/，下载安装包安装即可。（自带了 ssh 客户端）

## Git 配置

　　安装好之后，我们还需要稍微配置一下才可以使用。首先，Git是分布式版本控制系统，必须要能区别每个成员，所以，每个机器都必须自报家门：你的名字和Email地址。
``` bash
$ git config --global user.name "ZCShou"
$ git config --global user.email ZCShou@live.com
```
　　如果用了 --global 选项，那么更改的配置文件就是位于你**用户主目录**下(Windows下就是：系统盘符:/用户/你的用户名/.gitconfig)，以后你所有的项目都会默认使用这里配置的用户信息。  

　　如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在**当前项目**的 .git/config 文件里。

### Git 文本编辑器
　　Git 默认使用的文本编辑器, 一般可能会是 Vi 或者 Vim。如果你不是技术大牛还是换了的好。笔者使用的是VSCode insider版本
``` bash
$ git config --global core.editor Code-Insiders.exe
```
　　**注意**：1. 确保你得编辑器在环境变量中 2. 注意 global 参数			  
### Git 差异比较工具
　　Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。
``` bash
$ git config --global merge.tool vimdiff
```
### Git 内容推送
　　不带任何参数的git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。如果要修改这个设置，可以采用git config命令。
``` bash
$ git config --global push.default matching
# 或者
$ git config --global push.default simple
```
　　配置完成后，就可以开启Git的使用之旅了。

> Git 提供了一个叫做 git config 的工具，专门用来配置或读取相应的工作环境变量。这些环境变量，决定了 Git 在各个环节的具体工作方式和行为。这些变量可以存放在以下三个不同的地方：
> * /etc/gitconfig 文件：系统中对所有用户都普遍适用的配置。若使用 git config 时用 --system 选项，读写的就是这个文件。
> * ~/.gitconfig 文件：用户目录下的配置文件只适用于该用户。若使用 git config 时用 --global 选项，读写的就是这个文件。
> * 当前项目的 Git 目录中的配置文件（也就是工作目录中的 .git/config 文件）：这里的配置仅仅针对当前项目有效。
>
> 每一个级别的配置都会覆盖上层的相同配置，所以 .git/config 里的配置会覆盖 /etc/gitconfig 中的同名变量。使用 `git config --list` 查看相关配置。

![git config --list](https://github.com/ZCShou/Docs/blob/master/images/GitUsage/git-list.png)

　　**注意**：有时，通过上面的命令，可能出现重复变量，它们来自不同的配置文件，不过，最终git会采用上面说明的最近目录中的参数。	

## Git 工作流程

　　工作流程参考下面的图片

![git process](https://github.com/ZCShou/Docs/blob/master/images/GitUsage/git-process.png)

## Git 工作区、暂存区和版本库

　　我们先来理解下Git 工作区、暂存区和版本库概念
* **工作区**：就是你在电脑里能看到的目录。
* **暂存区**：英文叫stage, 或index。一般存放在"git目录"下的index文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
* **版本库**：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

　　下面这个图展示了工作区、版本库中的暂存区和版本库之间的关系：
![git process](https://github.com/ZCShou/Docs/blob/master/images/GitUsage/git-works.png)

　　关于这部分，可以到这个网站查看，作者已经写得非常详细了 http://www.runoob.com/git/git-workspace-index-repo.html

## Git 本地仓库

　　本地仓库相对比较简单，新建立一个文件夹，git bash到 新建的文件中，执行 `git init` 即可。这样，在当前目录下，回生成一个名为.git的隐藏文件夹，git的所有东西就存在该文件夹中。

## Git 基本操作
### Git 新增文件
　　使用 `git add` 命令将新文件提交到git，让git管理该文件:
```bash
格式：$ git add <参数>  文件名          # 文件名支持通配符

注意几个参数的区别：
　　$ git add .   # 监控工作区的状态树，使用它会把工作时的所有变化提交到暂存区，包括文件内容修改(modified)以及新文件(new)，但不包括被删除的文件
　　$ git add -u   # 仅监控已经被add的文件（即tracked file），他会将被修改的文件提交到暂存区。add -u 不会提交新文件（untracked file）
　　$ git add -A   # 是上面两个功能的合集

```

### Git 提交修改
　　使用 `git commit` 命令修改提交到Git:
```bash
格式：$ git commit <参数> <-F file/ -m "msg" ...>

注意几个参数的区别：
　　$ git commit -m    # 提交说明。不用-m参数的话，git将调到一个文本编译器（通常是vim）来让你输入提交的描述信息
　　$ git commit -a   # -a 选项可只将所有被修改或者已删除的且已经被git管理的文档提交倒仓库中。如果只是修改或者删除了已被Git 管理的文档，是没必要使用git add 命令的。
```
### Git 查看日志
　　使用 `git log` 命令列出历史提交记录如下:

![git process](https://github.com/ZCShou/Docs/blob/master/images/GitUsage/git_log.png)

　　也可以使用 `git log --oneline` 命令列出历史提交记录的精简版，如下：

![git process](https://github.com/ZCShou/Docs/blob/master/images/GitUsage/git_log_oneline.png)

　　使用 `git log --graph` 命令查看历史中什么时候出现了分支、合并
```bash
git log --oneline --graph
```

　　如果只想查找指定用户的提交日志可以使用命令：git log --author=xxx
```bash
git log --author=Linus --oneline -5
```

　　如果你要指定日期，可以执行几个选项：--since 和 --before，但是你也可以用 --until 和 --after,如下：
```bash
git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges
```

## Git 使用远程仓库

　　1. 将本地仓库(有无内容均可)与已有的一个***空的***远程仓库进行关联。可以直接执行以下命令：
```bash
git remote add [shortname] [url]            # shortname 为远程仓库的简称，后续命令可以直接使用该简称，默认为origin
# 例如：
git remote add Docs git@github.com:ZCShou/Docs.git           # Docs 为远程仓库git@github.com:ZCShou/Docs.git的简称，
```
　　在关联之后，可以使用 `git remote` 进行查看当前关联的远程仓库

```bash
$ git remote
Docs
$ git remote -v
Docs    git@github.com:ZCShou/Docs.git (fetch)
Docs    git@github.com:ZCShou/Docs.git (push)
```
　　2. 如果我们已有不空的远程仓库，或者说，想要直接获取别人的仓库

　　接下来，就可以把本地库的所有内容推送到远程库上（将本地的master分支推送到Docs仓库）：
```bash
git push -u Docs master         #这里的Docs 就是上面 起的别名； -u 表示：以后操作，默认的仓库为Docs，默认关联的分支为master
```
　　使用上面的-u 以后，后续很多操作都可以简化，如下：
```bash
git push 命令： 
　　格式：$ git push <远程主机名> <本地分支名>:<远程分支名>  
　　举例：$ git push Docs master:master                   # 将本地master分支推送到远程仓库Docs的master分支 

　　# 如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。例如：
　　$ git push Docs :master
　　# 等同于
　　$ git push Docs --delete master

　　# 如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。（ 即使用 git push -u 关联的那个）
　　$ git push Docs
　　# 如果当前分支只有一个追踪分支，那么主机名都可以省略。
　　$ git push
```
　　一旦远程主机的版本库有了更新(Git术语叫做commit)，需要先将这些更新取回本地，否则，在将本地提交到远程仓库时会报错。这时就要用到git fetch或者git pull命令。
```bash
git pull 命令： 
　　格式：$ git pull <远程主机名> <远程分支名>:<本地分支名>  
　　举例：$ git pull Docs master:master                   # 将远程仓库Docs的master分支克隆到本地master分支

　　# 如果与当前本地分支，则:后可以省略：
　　$ git push Docs master                                # 取回Docs/master分支，合并到当前本地分支

　　# 在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系(tracking)。
　　# 比如，在git clone的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的master分支自动”追踪”Docs/master分支。
　　$ git branch --set-upstream master Docs/next

　　# 如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名。
　　$ git pull origin

　　# 如果当前分支只有一个追踪分支，连远程主机名都可以省略。
　　$ git pull

git fetch 命令：
　　# 将某个远程主机的更新（所有分支），全部取回本地
　　$ git fetch <远程主机名>

　　# 如果只想取回特定分支的更新，可以指定分支名
　　$ git fetch <远程主机名> <分支名>

　　# 注意：fetch后，内容并没有真正保存，修改手动合并
　　$ git merge origin/master

　　# 也可以在它的基础上，使用git checkout命令创建一个新的分支
　　$ git checkout -b newBrach Docs/master
```
　　**所取回的更新，在本地主机上要用 ”远程主机名/分支名” 的形式读取。比如Docs主机的master，就要用Docsmaster读取。**

　　**git pull 等效于 git fetch + git merge**

## 附录
　　以下是几个比较好的Git学习网站，特此记录以下
* http://www.runoob.com/git/git-tutorial.html
* http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000
* http://www.yanyaozhen.com/category/git/


