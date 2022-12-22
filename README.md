# gitPractice

### 冷知识
+ .gitignore 文件（记录了你不希望提交到仓库的⽬录和⽂件的名称或类型）TODO
+ .git 目录（本地仓库）
    + 所有的版本信息
    + 所在的根目录--》工作目录

### 查看工作目录
+ git status


### 拉代码
+ git clone

### 提交
+ git add ---> 变已暂存，被记录进了staging area（暂存区）
    + git add 文件名
    + git add .
+ git commit ---> 提交 TODO-
    + 初始状态下：命令模式
    + "i"（⼩写）来切换到插⼊模式，输⼊你的提交信息 
    + 输⼊完成后，按ESC键返回到命令模式，然后连续输⼊两个⼤写的"Z"（⽤Shift键或Capslock键都可以），就保存并退出了。
    + git commit --amend 修改提交 TODO
+ git push --> 推送提交到中央仓库
    + git push【远程仓库名】【分支名]
        + 若当前分支是一个本地创建的分支，需要指定【远程仓库名】【分支名】

### git pull拉代码
+ git fetch取下来
+ 再进⾏merge操作

### git merge 合并commits（指定一个commit，把它合并到当前的 commit 中来）
+ 实例：将自己当前写的这个分支上的代码合并到test分支上，然后打包test分支上的代码，发布到服务器 TODO-
    + git checkout test 切换到test分支
    + git merge 分支（要合并到test上的分支）

### HEAD：当前commit的引⽤
### master：默认branch
### branch：⼀个指向commit的引⽤

### git branch 分支名
+ （基于当前所在的分支，创建分支）TODO-
### git checkout 分支名 
+ （切换当前所在分支）(实际：切换HEAD)

### git checkout -b 分支名 
+ 简介写法

### git branch -d 分支名 
+ 删除分支

### 冲突 TODO-
+ 两个分支，修改同一文件（具体场景是啥）
    + 解决冲突
    + 手动 commit
+ 放弃解决冲突
    + git merge --abort

### 最流行的工作流
+ master分支（生产环境）
+ pre分支（预发环境）
+ test分支（测试环境）
+ 其它分支（开发环境）
    + 一个任务开一个自己的分支
    + 开发完 -》 合到test -》测试 ->合到pre -》 测试 -》 合到master，发布上线 -》 确认无误
    + 删除该分支

### git log 查看历史记录
+ git log -p 查看详细历史
+ git log --stat 查看简要统计
+ git show
    + 查看当前commit
    + git show commit引用 查看该commit的详细信息

### 看未提交的内容
+ git diff（不常用，不赘述）

### 区分几个概念
+ 暂存区 --》 git add 
+ 工作目录 --》 git add git commit
+ 上一条提交 --》 最新的push

### 变基
+ git rebase
    + 背景：消除分叉再汇合的结构
    + 给你的commit序列重新设置基础点--以指定的commit为基础，依次重新提交一次（领先的commits重新提交）
+ 应用一：将自己开发的分支合并到重要的分支上（例如，将_ting分支的代码合并到test分支）TODO
    + 切换到你修改的分支 - git checkout _ting
    + 变基（改变所在分支的基础commit为指定的commit）- git rebase test(commit的引用方式有几种，除了分支名，序列的方式不知是否可行)
    + 将 _ting 分支合并到 test 分支
        + git checkout test (切换到test分支)
        + git merge _ting 
    + 小结：白话理解：相当于把在 _ting 分支上开发的commits复制了一份，然后改变它的父commit为test分支上最新的commit（就相当于是基于最新的test分支创建了一个_ting分支并在_ting分支上提交了许多commits），再'更新'下test分支（更准确的说法是：将_ting分支上的代码合并到test分支上）
+ 应用一：将某条分支的代码合并到另一条分支上
    + 除几个重要的分支（master、pre、test）外，直接rebase就可以了
    + 例如：自己开发的分支1，另一个分支2
        + 直接 切换到分支2,然后变基
        + git checkout 分支2
        + git rebase 分支1

### 场景
+ 两个人开发同一分支，修改同一个文件的同一处（非同一处呢），小红push了，小明也在本地做了自己的修改，此时小明更新小红的代码会怎么样

+ 小刘有个开发分支，开发完合并到test分支上， （当前test分支）git merge _xiaoliu 之后，控制台显示有偏离的分支，需要调和
    + 小刘发现原来是自己 merge 之前忘记拉test分支的最新代码了
    + 解决：调和的三种
        + git config pull.rebase false #合并
        + git config pull.rebase true  #变基
        + git config pull.ff only      #仅快进
    + 小刘选择了第二种，然后git push提交 --》 解决
    + 小结： git merge 合并后会保留原有分支记录，git rebase 不会