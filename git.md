#  第1章 Git 概述 

Git 是一个免费的、开源的分布式版本控制系统，可以快速高效地处理从小型到大型的各种 项目。 

Git 易于学习，占地面积小，性能极快。 它具有廉价的本地库，方便的暂存区域和多个工作 流分支等特性。其性能优于 Subversion、CVS、Perforce 和 ClearCase 等版本控制工具。 

## 1.1 何为版本控制 

版本控制是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统。 

版本控制其实最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本， 方便版本切换。 

## 1.2 为什么需要版本控制 

个人开发过渡到团队协作。

## 1.3 版本控制工具 

➢ **集中式版本控制工具** 

CVS、SVN(Subversion)、VSS…… 

集中化的版本控制系统诸如 CVS、SVN 等，都有一个单一的集中管理的服务器，保存 所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或 者提交更新。多年以来，这已成为版本控制系统的标准做法。

这种做法带来了许多好处，每个人都可以在一定程度上看到项目中的其他人正在做些什 么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个集中化的版本控制系统，要 远比在各个客户端上维护本地数据库来得轻松容易。 

事分两面，有好有坏。这么做显而易见的缺点是中央服务器的单点故障。如果服务器宕 机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。 

➢ **分布式版本控制工具** 

Git、Mercurial、Bazaar、Darcs…… 

像 Git 这种分布式版本控制工具，客户端提取的不是最新版本的文件快照，而是把代码 仓库完整地镜像下来（本地库）。这样任何一处协同工作用的文件发生故障，事后都可以用 其他客户端的本地仓库进行恢复。因为每个客户端的每一次文件提取操作，实际上都是一次 对整个文件仓库的完整备份。 

分布式的版本控制系统出现之后,解决了集中式版本控制系统的缺陷: 

1. 服务器断网的情况下也可以进行开发（因为版本控制是在本地进行的） 
2. 每个客户端保存的也都是整个完整的项目（包含历史记录，更加安全） 

## 1.4 Git 简史 

Linux系统版本控制历史 Linus本人手动合并代码 商业软件：BitKeeper 1991年 2002年 BitKeeper的东家 BitMover公司出于人 道主义精神，授权 Linux社区免费使用这 个版本控制系统。但 要求不能进行破解。 2005年 开发Samba的Andrew 试图破解BitKeeper的 协议，被BitMover公司 发现，要收回Linux社 区的免费使用权。 Linux社区无法像 商业公司那样对参 与开发者进行强有 力的约束 Linus自己用C语言开发了一个 分布式版本控制系统：Git 主体程序开发完成只用了两周 一个月后Linux系统代码由Git管理 GitHub上线 2008年 jQuery Ruby PHP ……….  

## 1.5 Git 工作机制 

| 区域   | 作用           | 进入下一级操作 |
| ------ | -------------- | -------------- |
| 工作区 | 写代码         | git add        |
| 暂存区 | 临时存储       | git commit     |
| 本地库 | 历史版本       | push           |
| 远程库 | 保存版本和代码 |                |

## 1.6 Git 和代码托管中心 

代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为远程库。 

➢ **局域网** 

✓ GitLab 

➢ **互联网** 

✓ GitHub（外网） 

✓ Gitee 码云（国内网站） 

# 第2章 Git 安装 

官网地址： https://git-scm.com/ 

# 第3章 Git 常用命令 

| 命令名称                             | 作用             |
| ------------------------------------ | ---------------- |
| git config --global user.name 用户名 | 设置用户签名     |
| git config --global user.email 邮箱  | 设置用户签名     |
| git init                             | 初始化本地库     |
| git status                           | 查看本地库状态   |
| git add 文件名                       | 添加到暂存区     |
| git rm --cached 文件名               | 删除暂存区的文件 |
| git commit -m "日志信息" 文件名      | 提交到本地库     |
| git reflog                           | 查看历史记录     |
| git log                              | 查看历史详细记录 |
| git reset --hard 版本号              | 版本穿梭         |

# 第4章 Git 分支操作

| 命令名称               | 作用                         |
| ---------------------- | ---------------------------- |
| git branch 分支名      | 创建分支                     |
| git branch -v          | 查看分支                     |
| git branch -d 分支名   | 删除分支                     |
| git checkout 分支名    | 切换分支                     |
| git checkout -b 分支名 | 创建并切换分支               |
| git merge 分支名       | 把指定的分支合并到当前分支上 |

## 4.1 解决冲突

- 假如master和分支都有不同的提交
- 合并冲突分支后，Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容
- 修改冲突，再次提交（提交命令后不能带文件名）

## 4.2 解决BUG

1. git stash：把当前工作现场“储藏”起来，等以后恢复现场后继续工作
2. git checkout master：切换到需要修复Bug的分支
3. git checkout -b issue-101：创建Bug分支
4. 修复Bug=》提交到分支=》切换到master=》合并分支=》删除分支
5. git checkout dev：切换到工作的分支
6. git stash list：可查看储存
7. git stash apply stash@{0}：恢复指定的stash（假如stash了多个）
8. git stash apply（恢复工作区）=》git stash drop（删除stash）
9. 或者：git stash pop（恢复的同时删除stash）

## 4.3 Feature分支

- 添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。
- 假如在合并前不需要了用git branch -D feature强行删除

# 第5章 Github远程仓库

## 5.1 链接

1. 注册/登录Github账号
2. 创建本机SSH key（如果没有）：`ssh-keygen -t rsa -C 邮箱`（可不设置密码）
3. 在主用户目录找到.ssh文件夹：id_rsa是私钥；id_rsa.pub是公钥
4. 登陆GitHub，点“Add SSH Key”，填上任意Title，并粘贴id_rsa.pub文件的内容

## 5.2 同步仓库

1. 在Github创建一个新的仓库

2. 在本地仓库下运行：

   ```
   //为链接设置为origin的别名
   //ssh协议必须在仓库关联到本机SSH key
   git remote add origin git@github.com:***/test.git（ssh协议）
   git remote add origin https://github.com/***/test.git（https协议）
   ```

3. 推送：`git push origin master`

## 5.3 从远程库克隆

```
//ssh协议必须在仓库关联到本机SSH key
git clone git@github.com:***/othertest.git（ssh协议）
git clone https://github.com/***/othertest.git（https协议）
```

## 5.4 查看远程库信息

```
git remote
git remote -v（详细信息）
```

## 5.5 推送分支

```
//把该分支上的所有本地提交推送到远程库
git push origin master
```

## 5.6 抓取分支

```
//把最新的提交从origin/dev抓下来
git pull

//建立本地分支和远程分支的关联
git branch --set-upstream branch-name origin/branch-name
```

tessssst

