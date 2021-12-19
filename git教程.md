1. 什么是git 和GitHub？

```
Git是一款免费、开源的分布式版本控制系统

Github是用Git做版本控制的代码托管平台

类似与conda 和anaconda 的关系
```

2. 分布式版本控制系统的特点

```
 分布式版本控制系统的优点：

1.版本库本地化，版本库的完整克隆，包括标签、分支、版本记录等

2.支持离线提交，适合跨地域协同开发

3.分支切换快速高效，创建和销毁分支方便

分布式版本控制系统的缺点：

1.学习成本高，不容易上手

2.只能针对整个仓库创建分支，无法根据目录建立层次性的分支
```

3. Github基础教程

可以GitHub配合编译器使用会更加的高效，需要熟悉快捷键的使用

在GitHub 上创建一个新仓库

```
在任意的页面右上角点击+，然后点击新建仓库New repository。
为你的仓库取一个的名字
为你的仓库添加一个描述（optional）
选择你的仓库类型为公有或者私有
选择是否添加readme文件
Initialize this repository with:
Add a README file 添加更全面的project描述
Add .gitignore 从模板列表中选择不跟踪的文件，即可以选择性push文件
Choose a license 许可证告诉其他人他们可以用您的代码做什么，不可以做什么
```

了解分支branch

```
查看分支 git branch
查看所有分支 git branch -a
创建分支 git branch [branch name]
切换分支 git checkout [branch name]，*代表当前分支
创建 + 切换分支 git checkout -b [branch name]
将新分支推动到GitHub git push origin [branch name]
删除本地分支 git branch -d [branch name]
删除GitHub远程分支 git push origin :[branch name]
在编译器上进行分支的创建和切换，以及管理会更加容易
mian分支可以存放已经完成的代码，develop适合存放更在开发的代码
```

什么是tag

```
可以创建一个tag来指向软件开发中的一个关键时期，比如版本号更新的时候可以建一个“v2.0”的标签，这样在以后回顾的时候会比较方便。
主要操作有：查看tag、创建tag、验证tag以及共享tag
查看标签 git tag
创建标签 git tag [tag name]
共享标签 git push origin [tag name] 或者 git push origin --tags一次性push 全部的标签
```

什么clone

```
git clone是git中常用的命令，其作用是将存储库克隆到新目录中
克隆仓库 git clone <版本库的网址>，这里的地址有两种，分别是HTTPS和SH
HTTPS利于匿名访问，适合开源项目，可以方便被别人克隆和读取(但没有push权限) 
SSH不利于匿名访问，比较适合内部项目，只要配置了SSH公钥极可自由实现clone和push操作


在使用git clone命令时，如果不指定分支，则默认克隆主分支
克隆特定的分支 git clone -b [branch name] <版本库的网址>
```

merge功能

```
git merge命令是用于将两个或两个以上的开发历史合并在一起的操作
进入特定的分支，git merge [branch name]，这里填写你想要合并的分支，然后push一下
可以自定义分支节点，也可以将合并好的分支拆开
```

git的常用命令

下图用于帮助我理解git的常用命令，workspace指的是当前活动分支

![Screenshot 2021-12-17 at 23.09.27.png](/var/folders/5f/11d409g140lf_yxwc5zyfrl80000gq/T/TemporaryItems/NSIRD_screencaptureui_DPSrKf/Screenshot%202021-12-17%20at%2023.09.27.png)

```
git init 初始化仓库
git status 查看仓库当前的状态，显示有变更的文件
git add . 添加文件到暂存区
git commit 将暂存区内容添加到仓库中
git push 上传远程代码并合并
git pull 下载远程代码并合并
```

查看历史commits

在仓库的右上角，点击commit图标即可以查看历史修改记录

Homework：在编译器中学习git常用命令
