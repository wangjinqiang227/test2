# git学习笔记

## 创建版本库

初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：

* 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；

- 第二步，使用命令`git commit`，完成。

## 版本回退

- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。
- Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

## 撤销修改

* 丢弃工作区修改，用`git checkout --file`
* 丢弃缓存区修改，用`git reset HEAD  file`

## 删除文件

* 确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`

* 错删用`git checkout --<filename>`

  `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

## 添加远程库

* 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`。
* 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容。
* 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改。

## 远程库克隆

* 用`git clone git@server-name:path/repo-name.git`

## 创建合并分支

* 查看分支：`git branch`
* 创建分支：`git branch <name>`
* 切换分支：`git checkout <name>`
* 创建+切换分支：`git checkout -b <name>`
* 合并某分支到当前分支：`git merge <name>`
* 删除分支：`git branch -d <name>`

## bug分支

* 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场。
* 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

## 多人协作

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## 标签

- 命令`git tag <name>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- `git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- `git tag -s <tagname> -m "blablabla..."`可以用PGP签名标签；
- 命令`git tag`可以查看所有标签。
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。