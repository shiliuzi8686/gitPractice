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

### 冲突 TODO
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

### git commitlog 提交规范
+ feat: 新功能
+ fix: 修复 bug
+ docs: 文档新增或修改
+ refactor: 重构代码，不影响现有功能
+ perf: 为了优化性能的改动
+ test: 增加或修正测试
+ build: 编译脚本、工具或依赖等项目构建相关的改动
+ ci: CI构建配置文件或脚本相关的改动
+ chore: 无法匹配以上类别的其它改动
其中feat 、fix 与 perf 类型的提交将被用于自动生成项目 changelog.
