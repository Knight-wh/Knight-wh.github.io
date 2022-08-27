## 创建版本库

`git init`

`git add file_1`以及`git add file_2`

`git commit -m "message"`

## 跳转版本

`git reset --hard commit_id` 跳转到指定的版本，代码改变。`HEAD`是当前版本，`HEAD^`是上一个版本。

`git log` 查看提交历史，以确定要回退的版本

`git reflog` 查看命令历史，以确定要回到未来的哪个版本

### 一些命令

`git status` 查看状态

`git diff` 查看某个文件的修改内容

`git checkout` 用版本库里的版本替换工作区的版本。

`git rm` 用于删除一个文件。

## 远程仓库

`git remote add origin HTTP/SSH` 把本地仓库与Github仓库关联。Git支持多种协议，可用ssh或http。http速度慢，而且每次推送都必须输入口令。

`git push -u origin master` 把本地仓库的内容推送到Github仓库。第一次推送master分支时，加上-u参数，git会把本地的master分支和远程的master分支关联起来。

`git push origin master`

`git remote rm origin` 删除与远程仓库的绑定关系。

## 分支管理

`git branch dev`+`git checkout dev`等效于`git checkout -b dev`，表示创建分支并切换。


`git merge <name>`合并指定分支到当前分支。

`git branch -d <name>`删除指定分支。

`git switch <name>`切换到已有的分支。`-c`创建并切换.

### 一些命令

`git branch`查看分支

`git branch <name>`创建分支

`git log --graph --pretty=oneline --abbrev-commit`查看分支树

## 多人协作

`git checkout -b branch-name origin/branch-name`把远程仓库的dev分支创建到本地

`git branch --set-upstream branch-name origin/branch-name`建立本地分支和远程分支的关联。

`git pull`从远程抓取分支