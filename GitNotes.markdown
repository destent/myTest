# git学习
## 添加文件  git add 文件名
## 提交到仓库 git commit -m "描述性文字"
    可以添加多个文件然后一次性提交
## 查看工作区状态 git status
## 查看修改内容 git diff
## 查看日志 git log 参数--pretty=oneline令信息在一行显示
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

## 切换版本 git reset -hard commit id(HEAD 指针)
## 查看历史命令 git reflog