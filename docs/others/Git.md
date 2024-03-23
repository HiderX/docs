# Git

## 1、概述

### 1.1、为什么要git？

- 备份
- 代码还原
- 协同开发
- 追溯问题代码

### 1.2、版本控制方式

- 集中式版本控制工具，如SVN
- 分布式版本控制工具，如Git

### 1.3、Git

![1](https://s2.loli.net/2023/11/30/FqfysDEIZLKpnYj.png)

工作流程

![2](https://s2.loli.net/2023/11/30/eAv4Mh1pDLlmycW.png)

命令如下：

1. clone（克隆）: 从远程仓库中克隆代码到本地仓库

2. checkout （检出）:从本地仓库中检出一个仓库分支然后进行修订

3. add（添加）: 在提交前先将代码提交到暂存区

4. commit（提交）: 提交到本地仓库。本地仓库中保存修改的各个历史版本

5. fetch (抓取) ： 从远程库，抓取到本地仓库，不进行任何的合并动作，一般操作比较少。

6. pull (拉取) ： 从远程库拉到本地库，自动进行合并(merge)，然后放到到工作区，相当于 fetch+merge

7. push（推送） : 修改完成后，需要和团队成员共享代码时，将代码推送到远程仓库

## 2、常用命令

### 2.1、基础操作指令

Git工作目录下对于文件的修改(增加、删除、更新)会存在几个状态，这些修改的状态会随着我们执行Git 的命令而发生变化。

![3](https://s2.loli.net/2023/11/30/5Yg3DRtV2AodEGv.png)

- git add

  作用：添加工作区一个或多个文件的修改到暂存区

  命令形式：git add 单个文件名|通配符

  将所有修改加入暂存区：git add .

- git commit

  作用：提交暂存区内容到本地仓库的当前分支

  命令形式：git commit -m '注释内容'

- git status

  查看修改的状态（暂存区、工作区）

- git log

  作用:查看提交记录

  命令形式：git log [option] options

  --all 显示所有分支

  --pretty=oneline 将提交信息显示为一行

  --abbrev-commit 使得输出的commitId更简短

  --graph 以图的形式显示

- git reset

  作用：版本切换

  命令形式：git reset --hard commitID

  commitID 可以使用 git-log 或 git log 指令查看

  如何查看已经删除的记录？

  git reﬂog 这个指令可以看到已经删除的提交记录

- .gitignore

  一般我们总会有些文件无需纳入Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动 生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以在工作目录 中创建一个名为 .gitignore 的文件（文件名称固定），列出要忽略的文件模式。下面是一个示例：

  ```
  # no .a files
  *.a
  # but do track lib.a, even though you're ignoring .a files above
  !lib.a
  # only ignore the TODO file in the current directory, not subdir/TODO
  /TODO
  # ignore all files in the build/ directory
  build/
  # ignore doc/notes.txt, but not doc/server/arch.txt
  doc/*.txt
  # ignore all .pdf files in the doc/ directory
  doc/**/*.pdf
  ```

### 2.2、分支

- 切换分支

  git checkout 分支名

  如果分支不存在，可以使用git checkout -b 分支名直接创建并切换到该分支

- 删除分支

  不能删除当前分支，只能删除其他分支

  git branch -d b1 删除分支时，需要做各种检查

  git branch -D b1 不做任何检查，强制删除

- 合并分支

  先切换到要被合并到的分支，然后git merge 分支名

  例如把dev合并到master，就在master分支下执行git merge dev

- 解决冲突

  当两个分支上对文件的修改可能会存在冲突，例如同时修改了同一个文件的同一行，这时就需要手动解决冲突，解决冲突步骤如下：

  1. 处理文件中冲突的地方

  2. 将解决完冲突的文件加入暂存区(add)

  3. 提交到仓库(commit)

- 开发中分支使用原则与流程

  几乎所有的版本控制系统都以某种形式支持分支。 使用分支意味着你可以把你的工作从开发主线上分离开来进行重大的Bug修改、开发新的功能，以免影响开发主线。

  在开发中，一般有如下分支使用原则与流程：

  master （生产） 分支

  线上分支，主分支，中小规模项目作为线上运行的应用对应的分支；

  develop（开发）分支

  是从master创建的分支，一般作为开发部门的主要开发分支，如果没有其他并行开发不同期上线 要求，都可以在此版本进行开发，阶段开发完成后，需要是合并到master分支,准备上线。

  feature/xxxx分支

  从develop创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完 成后合并到develop分支。

  hotﬁx/xxxx分支

  从master派生的分支，一般作为线上bug修复使用，修复完成后需要合并到master、test、 develop分支。

  还有一些其他分支，在此不再详述，例如test分支（用于代码测试）、pre分支（预上线分支）等等。

  ![](https://s2.loli.net/2023/12/01/7MFuGnQYq4pzdgf.png)

## 3、Git远程仓库

### 3.1、创建远程仓库

Gitee/Github 新建即可

可以选择公开/私有

### 3.2、配置SSH公钥

- 生成SSH公钥

  ```bash
  ssh-keygen -t rsa
  ```

- 不断回车 如果公钥已经存在，则自动覆盖

- 获取公钥

  ```bash
  cat ~/.ssh/id_rsa.pub
  ```

- Gitee/Github设置账户共公钥（设置页面）

### 3.3、操作远程仓库

- 添加远程仓库

  此操作是先初始化本地库，然后与已创建的远程库进行对接。
  命令： git remote add <远端名称> <仓库路径>

  - 远端名称，默认是origin，取决于远端服务器设置
  - 仓库路径，从远端服务器获取此URL
    例如: git remote add origin git@gitee.com:czbk_zhang_meng/git_test.git

- 查看远程仓库

  命令：git remote

- 推送到远程仓库

  命令：git push [-f] [--set-upstream] [远端名称 [本地分支名][:远端分支名] ]

  - 如果远程分支名和本地分支名称相同，则可以只写本地分支 git push origin master

  - -f 表示强制覆盖

  - --set-upstream 推送到远端的同时并且建立起和远端分支的关联关系。

    git push --set-upstream origin master

  - 如果当前分支已经和远端分支关联，则可以省略分支名和远端名。 git push 将master分支推送到已关联的远端分支。

- 本地分支与远程分支的关联关系

  查看关联关系我们可以使用`git branch -vv`命令

- 从远程仓库克隆

  如果已经有一个远端仓库，我们可以直接clone到本地。

  命令: git clone <仓库路径> [本地目录]

  - 本地目录可以省略，会自动生成一个目录

- 从远程仓库中抓取和拉取

  远程分支和本地的分支一样，我们可以进行merge操作，只是需要先把远端仓库里的更新都下载到本地，再进行操作。

  抓取 命令：git fetch [remote name] [branch name]

  - 抓取指令就是将仓库里的更新都抓取到本地，不会进行合并 如果不指定远端名称和分支名，则抓取所有分支。 
  
  拉取 命令：git pull [remote name] [branch name]

  - 拉取指令就是将远端仓库的修改拉到本地并自动进行合并，等同于fetch+merge
  - 如果不指定远端名称和分支名，则抓取所有并更新当前分支。
  
- 解决合并冲突

  在一段时间，A、B用户修改了同一个文件，且修改了同一行位置的代码，此时会发生合并冲突。 A用户在本地修改代码后优先推送到远程仓库，此时B用户在本地修订代码，提交到本地仓库后，也需要推送到远程仓库，此时B用户晚于A用户，故需要先拉取远程仓库的提交，经过合并后才能推送到远端分支。
  即git pull之后处理完冲突再push。

  ![](https://s2.loli.net/2023/12/01/6mFAJUzrabOe2M7.png)
