# git学习
## 建立版本库
- git init 将当前目录变为git可管理的仓库
- 添加文件  git add 文件名
- 提交到仓库 git commit -m "描述性文字"
- 可以添加多个文件然后一次性提交
- 查看工作区状态 git status
- 查看修改内容 git diff
## 切换版本
- 查看日志 git log 参数--pretty=oneline令信息在一行显示
    ```
    PS D:\git_test> git log --pretty=oneline
    15857830fc42362dedb1e0e004bf44d7b5d0bac1 (HEAD -> master) 删除readme
    2d2c2a95162e909e166c36e1e87b3baeeafefd0b 用来练手的
    5c75aa119220d53af91255b0b1f543b6ada708cf 修改了文件名从readme到git_notes
    0aae8c93fc19980e5c3a08cbdf6312088ded9f5d git commit
    fdca2887acb39f304dd9c1db006b086e4ddfeed2 git 学习记录
    ```
长串十六进制数为commit id 即版本号
HEAD 指向当前版本（类似C语言指针） 上个版本写作HEAD^，上上个版本写作HEAD^^，
上N个版本HEAD~N
- 切换版本 git reset -hard commit id(HEAD 指针)
- 查看历史命令 git reflog
## 工作区和暂存区
- 工作区：目录中可见可的部分
- 暂存区：git add文件进入暂存区， git commint 将暂存区的所有文件提交到分支
## 撤销修改
- `git checkout -- file`:撤销工作区的修改，使其恢复到最近一次git add或git commit状态
## 删除文件
- `git rm file`：删除文件，已存入版本库的文件可通过`git checkout`恢复

