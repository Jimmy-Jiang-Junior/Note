# git命令

## 1. 在本地clone代码，创建分支，追踪远程分支

if you have a local clone, you can update it by running the following commands
git branch -m main main_branch
git fetch origin
git branch -u origin/main_branch main_branch
git remote set-head origin -a

似乎还有另外一种方法

git branch --set-upstream-to=origin/master master