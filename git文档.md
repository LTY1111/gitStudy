# Git

### 三种状态：已提交（committed）、已修改（modified） 和 已暂存（staged）

1. 已修改表示修改了文件，但还没保存到数据库中。

2. 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。

3. 已提交表示数据已经安全地保存在本地数据库中。

   ### 

## 一、基础流程

### 1、创建一个github账号

### 2、配置github账号信息

```sh
//创建id_rsa.pub
ssh-keygen -t rsa -C "自己邮箱"
ssh -T git@github.com
git config --global user.name "my name"
git config --global user.email "my email"
```

​		如果用了 **--global** 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。

​		如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。

### 3、本地项目上传Github

```sh
//造一个新的文件夹，git bash here 产生.git文件，本地仓库建好
git init
//将项目所有文件添加到缓存，如果只添加某个文件,只需把 . 换成你要添加的文件名即可;
git add .
//将缓存中的文件Commit到git库
git commit -m "注释"
git remove add origin git@github.com:***/***.git
git push --set-upstream origin master
```

#### 问题点1连接远程仓库方式

##### 1.使用**SSH协议**连接远程仓库

$ git remove -v //查看当前git远程仓库版本

命令：git remote add 远程仓库别名 SSH协议地址

##### 2.使用**HTTPS协议**连接远程仓库

命令：git remote add 远程仓库别名 HTTPS协议地址

#### 问题点2git提交的过程中如何忽略某些内存较大的配置文件

解决：项目目录下创建.[gitignore](https://so.csdn.net/so/search?q=gitignore&spm=1001.2101.3001.7020)文件

```shell
#          表示此为注释,将被Git忽略
1.txt      表示忽略1.txt 文件
*.txt      表示忽略所有 .txt 结尾的文件
!2.txt     不忽略2.txt这个文件
/TODO`     `表示仅仅忽略项目根目录下的 TODO 文件，如果这个文件不在根目录下，则不会忽略
build/     表示忽略 build/目录下的所有文件，过滤整个build文件夹，不管是否在根目录下；
```

注意点：如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。简单来说出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。所以大家一定要养成在项目开始就创建.gitignore文件的习惯，否则一单push，处理起来会非常麻烦。

## 二、分支

### 创建分支

```sh
git branch branchName(在本地创建一个命名为branchName的分支)
git branch 查看当前自己所在的分支
git branch -a 查看服务器的所有分支以及自己当前所在的分支
git push origin branchName(把命名为branchName的本地分支推送到服务器)
git checkout --track origin/branchName (切换为远程服务器上的命名为branchName的远程分支)
//如果你的搭档要把他本地的分支给关联到服务器上命名为branchName的远程分支，请执行以下操作
git branch --set-upstream localBranchName origin/branchName （为本地分支添加一个对应的远程分支与之相对应）->这行命令用来关联本地的分支与服务器上的分支
```

### 提交代码到分支

完成以上操作之后，可以进行提交代码，在提交代码之前，要确定当前所在的分支

```sh
git push origin branchName//（提交代码到远程服务器上命名为branchName的分支上）
git pull origin branchName //（从远程分支上拉取代码）
```

### 分支命名规范

1、master:：master 分支就叫master 分支。

2、develop：develop分支就叫develop 分支。

3、feature feature分支咱们暂时可以按 feature_wechat_y2.0.1，v2.0.1标当前迭代的版本号，wechat表示当前迭代的名称，这里是开发小程序迭代，就命名了wechat

4、release： release分支的名称我们直接命名为这次需求的版本号，如:2.0.1，因为后面当我们使用gifFlow 工具时，当我们完成release分支时，这个release分支名会直接当做在master 上的 tag名，这样我们就不需要再在master分支上打tag了。

5、hotfix：hoflix分支的命名我们暂时可以按hotfix_v2.0.2这种来进行命名，v2.0.2表示这次修复的版本的版本号。

## 三、提交文件

### 1.提交部分新增文件

```
git add 文件名
git status//
```

