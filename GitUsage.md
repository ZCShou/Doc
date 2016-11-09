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
![git process](https://github.com/ZCShou/Docs/blob/master/images/GitUsage/git-process.png)

　　关于这部分，可以到这个网站查看，作者已经写得非常详细了 http://www.runoob.com/git/git-workspace-index-repo.html

## Git 本地仓库

　　略

## Git 使用远程仓库

　　略

## 附录
　　以下是几个比较好的Git学习网站，特此记录以下
* http://www.runoob.com/git/git-tutorial.html
* http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000
* http://www.yanyaozhen.com/category/git/


