# git学习
## 建立版本库
- git init 将当前目录变为git可管理的仓库
- 添加文件  git add 文件名
- 提交到仓库 git commit -m "描述性文字"
- 可以添加多个文件然后一次性提交
- 查看工作区状态 git status
- 查看修改内容 git diff
## 版本控制和管理修改
### 切换版本
- 查看日志 git log 参数--pretty=oneline令信息在一行显示
    ```
    PS D:\git_test> git log --pretty=oneline
    15857830fc42362dedb1e0e004bf44d7b5d0bac1 (HEAD -> master) 删除readme
    2d2c2a95162e909e166c36e1e87b3baeeafefd0b 用来练手的
    5c75aa119220d53af91255b0b1f543b6ada708cf 修改了文件名从readme到git_notes
    0aae8c93fc19980e5c3a08cbdf6312088ded9f5d git commit
    fdca2887acb39f304dd9c1db006b086e4ddfeed2 git 学习记录
    ```
> 长串十六进制数为commit id 即版本号
  HEAD 指向当前版本（类似C语言指针） 上个版本写作HEAD^，上上个版本写作HEAD^^，
  上N个版本HEAD~N
- 切换版本 git reset -hard commit id(HEAD 指针)
- 查看历史版本 git reflog
### 工作区和暂存区
- 工作区：目录中可见可的部分
- 暂存区：git add文件进入暂存区， git commint 将暂存区的所有文件提交到分支
### 撤销修改
- `git checkout -- file`:撤销工作区的修改，使其恢复到最近一次git add或git commit状态
### 删除文件
- `git rm file`：删除文件，已存入版本库的文件可通过`git checkout`恢复
## 远程仓库
### 准备工作
1. 创建一个GitHub账户
2. 创建SSH KEY（如果没有）
    > 在shell中`$ ssh-keygen -t rsa -C "youremail@example.com"`
    此时在用户目录中会出现.ssh文件夹，其中id_rsa是私钥，id_rsa.pub是公钥将公钥添加到GitHub账户
### 添加远程仓库
1. 在github上创建一个新的仓库
2. `git remote add origin git@github.com:username/reponame.git` 关联远程仓库
3. `git push -u origin master` 将本地master分支推送到origin的maste分支并将两者关联起来。后续推送只需`git push origin master`
4. `git remote rm origin`:删除远程仓库。删除前可用`git remote -v`查看远程仓库信息
### 克隆远程仓库
`git clone 仓库代码`，不同协议的仓库代码可在github上直接获取。
## 分支管理
### 创建与合并分支
- 创建分支：`git branch <name>`
- 切换分支：`git switch <name>`
- 创建并切换分支： `git switch -c <name>`
- 合并分支： `git merge <name>`将指定分支与当前分支合并
- 删除分支： `git branch -d <name>`不能删除当前分支
### 解决冲突
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。
### 分支管理策略
#### 分支策略
在实际开发中，我们应该按照几个基本原则进行分支管理：
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
所以，团队合作的分支看起来就像这样：
![fenzhi](.\img\0.png)
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并
### bug分支
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到**当前分支**，避免重复劳动。
### feature分支
开发一个新feature，最好新建一个分支；
feature分支合并类似bug分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
### 多人协作
1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；

2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；

3. 如果合并有冲突，则解决冲突，并在本地提交；

4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。
### rebase
rebase操作可以把本地未push的分叉提交历史整理成直线；

rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比