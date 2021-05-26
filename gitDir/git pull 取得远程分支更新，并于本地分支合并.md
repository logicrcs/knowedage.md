# git pull 取得远程分支更新，并于本地分支合并

**git pull <remote> <remotebranch>:<localbranch>**  将远程存储库中的更改合并到当前分支中。在默认模式下，`git pull`是`git fetch`后跟`git merge FETCH_HEAD`的缩写。

更准确地说，`git pull`使用给定的参数运行`git fetch`，并调用`git merge`将检索到的分支头合并到当前分支中。 使用`--rebase`，它运行`git rebase`而不是`git merge`。

**高难度的git pull** 

​		先查看各个分支所处的位置，可以看到已经创建了一个超前的master分支，这个就是主分支，在整个版本库中是最新的版本，接下来就要模拟一个项目组中的一个成员在老旧的分支上开发，但是在提交和上传版本库的时候需要将最新远程主分支上的文件合到自己的本地分支上，在将同时拥有最新版本远程分支和本地修改的内容推送到自己的远程分支上

```
$ git log --oneline --graph
* ac27da3 (HEAD -> master, lg/master) 创建超前远程分支
* 295ee26 (dev) add merge and testing rebase fix compile
* 8cec706 testing rebase
*   8e78c81 Merge remote-tracking branch 'lg/master'
|\
| * d4bad23 Update readme.txt
* | 4fc9ee5 update modified test3.txt
* | 63b1e15 create test3.txt
|/
*   232d395 冲突解决完成
|\
| * f4048a4 finished the new footer [issus 533]
| * 4f83d07 added a new footer [issue 53]
* | 3f8c340 fixed the broken email address by hotfox
|/
* 1bed63f (lg/serverfix, serverfix) made other changes
* c6c45a9 全面梳理git diff
* aba4794 (tag: v1.1) 测试git 保存的是什么
* 167c574 (tag: v1.0, lg/testing, testing) test git commit --amend again
* 002c1cc 工作流程测试
* 1ebdf49 (tag: v0.8) 老版本提交
* bc26c7f (tag: v0.7) 删除错误文件
* d6703a5 add test.txt
```

​		在这个测试中选择的是位于1bed63f版本上的serverfix分支，接下来就将serverfix检出（checkout）或是切换到本地仓

```
$ git switch serverfix
Switched to branch 'serverfix'
Your branch is up to date with 'lg/serverfix'.
```

​		接下来在serverfix分支上进行一定的修改

```
$ vim test.txt

$ git commit -a -m '进行落后分支的开发'
warning: LF will be replaced by CRLF in test.txt.
The file will have its original line endings in your working directory
[serverfix 139e2a1] 进行落后分支的开发
 1 file changed, 4 insertions(+), 1 deletion(-)
```

​		关键的一步：拉取主分支上的代码

```
$ git pull lg master:serverfix
From https://github.com/logicrcs/learngit
 ! [rejected]        master     -> serverfix  (non-fast-forward)
```

​		这个时候就会发现在拉取主分支上的代码就会出现rejected被拒绝的情况，原因是无法进行快进合并,这是进行拉取，就可以合并了

```
$ git pull lg master
From https://github.com/logicrcs/learngit
 * branch            master     -> FETCH_HEAD
Merge made by the 'recursive' strategy.
 index.html      |  9 +++++++++
 index.html.orig |  7 +++++++
 readme.txt      | 11 ++++++++---
 test3.txt       |  2 ++
 test4.txt       |  3 +++
 5 files changed, 29 insertions(+), 3 deletions(-)
 create mode 100644 index.html
 create mode 100644 index.html.orig
 create mode 100644 test3.txt
 create mode 100644 test4.txt
```

​		最后推送自己的分支上

```
$ git push lg serverfix:serverfix
Enumerating objects: 9, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 738 bytes | 738.00 KiB/s, done.
Total 5 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To https://github.com/logicrcs/learngit.git
   1bed63f..34e95ce  serverfix -> serverfix
```

