### git 查漏补缺

------



创建.gitignore



```shell
.vscode

.history

node_modules
```



git 命令



```shell
git init 初始化仓库

git add .     将代码提交到暂存区

git pull 

git log  查看日志

git log --author="XXXX"  查看单一用户的提交记录

git status     查看当前项目改动

git commit -m   // 第一次上传文件

git branch   查看本地分支

git remote add origin "你的仓库地址"

git remote -v  查看现有远程仓库信息

git remote rm origin   删除现有仓库信息

git push -u origin 分支

git merge xx 合并分支

git diff  查看修改文件

git checkout .  撤销修改/切换分支

git stash 将文件先放一边 

git stash pop 将放一边的文件在拿回来
```

