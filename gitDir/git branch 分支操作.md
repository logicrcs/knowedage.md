

# git branch/checkout 分支操作

**git branch** 什么参数都没有，查看所有分支

```
$ git branch
  iss533
* master
  testing
  *字符代表当前
```

**git branch -r** 查看远程所有分支

```
远程仓库地址https://github.com/logicrcs/learnXmind.git
$ git branch -r
  lx/main
  lx/master
```

**git branch -a** 查看本地和远程的所有分支

```
远程仓库地址https://github.com/logicrcs/learnXmind.git
$ git branch -a
* master
  remotes/lx/main
  remotes/lx/master
```

**git branch -m <branch>** 改变分支名称

```
Administrator@PC-20210218IXTW MINGW64 ~/Desktop/企管处考核系统/knowedage.md (test)
$ git branch -m textt

Administrator@PC-20210218IXTW MINGW64 ~/Desktop/企管处考核系统/knowedage.md (textt)
$ git branch
  main
* textt
```



**git branch -v** 查看每一个分支的最后一次提交

```
$ git branch -v
  iss533  f4048a4 finished the new footer [issus 533]
* master  232d395 冲突解决完成
  testing 09698e1 made a change

```

**git branch -vv** `查看当前详细分支信息（可看到当前分支与对应的远程追踪分支）` 

```
$ git branch -vv
* master    4fc9ee5 [lg/master: ahead 2] update modified test3.txt
  serverfix 1bed63f [lg/serverfix] made other changes
  testing   167c574 [lg/testing] test git commit --amend again
  信息的组成是：
  分支名   提交的版本号  [远程库/分支] 对应的commit信息
  master 分支正在跟踪 lg/master 并且 “ahead” 是 2，意味着本地有两个提交还没有推送到服务器上。如果是behind，就意味着落后
```



**git branch -f  <branch> <version>** `强制切换提交的位置` 

```
//这是serverfix在最新的提交上
$ git log --oneline --decorate --graph --all
*   232d395 (HEAD -> serverfix, lg/serverfix, lg/master, master) 冲突解决完成
|\
| * f4048a4 finished the new footer [issus 533]
| * 4f83d07 added a new footer [issue 53]
* | 3f8c340 fixed the broken email address by hotfox
|/
* 1bed63f made other changes
* c6c45a9 全面梳理git diff

$ git branch -f serverfix 1bed63f

//分支serverfix 成功切换了位置
$ git log --oneline --decorate --graph --all
*   232d395 (HEAD -> master, lg/serverfix, lg/master) 冲突解决完成
|\
| * f4048a4 finished the new footer [issus 533]
| * 4f83d07 added a new footer [issue 53]
* | 3f8c340 fixed the broken email address by hotfox
|/
* 1bed63f (serverfix) made other changes
* c6c45a9 全面梳理git diff
```



**git branch --merged <branch>** 查看哪些分支已经合并到指定分支，默认当前分支

```
$ git branch --merged
  iss533
* master
```

**git branch --no-merged<branch>** 查看未合并到指定分支的有哪些，默认当前分支

```
$ git branch --no-merged
  testing
```

**git branch --set-upstream-to= <remote>/<branch> <branch>** 与远程分支创建跟踪关系

```
$ git branch --set-upstream-to=lg/master master
Branch 'master' set up to track remote branch 'master' from 'lg'.
```



**git branch <branchname>**  创建新分支，本质是创建了一个可以移动的新的指针。然后指向版本库中的版本

```
git branch testing
$ git log --oneline --decorate
c6c45a9 (HEAD -> master, lg/master, testing) 全面梳理git diff
aba4794 测试git 保存的是什么
167c574 (tag: v1.0) test git commit --amend again
002c1cc 工作流程测试
1ebdf49 (tag: v0.8) 老版本提交
bc26c7f (tag: v0.7) 删除错误文件
d6703a5 add test.txt
c183b5f update license
2d5a091 merge
8a3553d git tracks changes
6d0caa7 understand how stage works
49a98d1 append GPL
b3b37a2 add distributed
af19cb7 update
81c8d32 wrote a readme file
```



**git branch -d <branchname>**  删除指定的分支,如果参数是-D则可以强制删除分支。

```
$ git branch -d hotfix
Deleted branch hotfix (was 3f8c340).

* 3f8c340 (HEAD -> master) fixed the broken email address by hotfox
| * 4f83d07 (iss533) added a new footer [issue 53]
|/
* 1bed63f made other changes
| * 09698e1 (testing) made a change
|/
* c6c45a9 (lg/master) 全面梳理git diff

```

```
$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
//如果分支中存在未合并的工作,就要强制删除
```

```
$ git branch -D testing
Deleted branch testing (was 09698e1).
```

**git checkout <branchname>**  切换到一个已存在的分支，本质为将head指针执行切换的分支,切换分支会更改工作区文件

```
$ git checkout testing
Switched to branch 'testing'
```

**git checkout -b <newbranchname>** 创建新分支的同时切换过去

```
$ git checkout -b iss533
Switched to a new branch 'iss533'
```

创建一个新的应急分支

```
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
```



在这个分支上添加文件

```
$ git add index.html
warning: LF will be replaced by CRLF in index.html.
The file will have its original line endings in your working directory

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (hotfix)
$ git commit -a -m 'fixed the broken email address by hotfox'
[hotfix 3f8c340] fixed the broken email address by hotfox
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
```

**git merge** 合并分支

先切换到主分支上，再将hotfix合并到主分支上

```
https://www.cnblogs.com/shine1234/p/14768585.html
$ git checkout master
Switched to branch 'master'

$ git merge hotfix
Updating 1bed63f..3f8c340
Fast-forward
 index.html | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
 由于hotfix是master的直接后继，所以在合并代码上不会产生冲突。
$ git log --oneline  --decorate --graph --all

* 3f8c340 (HEAD -> master, hotfix) fixed the broken email address by hotfox
| * 4f83d07 (iss533) added a new footer [issue 53]
|/
* 1bed63f made other changes
| * 09698e1 (testing) made a change
|/
* c6c45a9 (lg/master) 全面梳理git diff

```

在新的与maste分支没有后继关系的iss533分支上进行开发工作

```
//切换分支
$ git checkout iss533
Switched to branch 'iss533'

//完成工作
$ vim index.html

//提交到工作分支
$ git commit -a -m 'finished the new footer [issus 533]'
[iss533 f4048a4] finished the new footer [issus 533]
 1 file changed, 1 insertion(+)
 
//回到主分支
$ git checkout master
Switched to branch 'master'

//合并iss533分支到master上，但产生合并冲突
$ git merge iss533
CONFLICT (add/add): Merge conflict in index.html
Auto-merging index.html
Automatic merge failed; fix conflicts and then commit the result.

//查看因包含合并冲突而处于未合并（unmerged）状态的文件
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      index.html

no changes added to commit (use "git add" and/or "git commit -a")

//查看冲突解决后的结果
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
//冲突已被合并
Changes to be committed:
        modified:   index.html
//之前的冲突历史文件
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html.orig

//最后提交最新的版本库
$ git commit -a -m '冲突解决完成'
[master 232d395] 冲突解决完成

```

**发生未关联历史合并错误**

```
$ git merge FETCH_HEAD
fatal: refusing to merge unrelated histories
```

​		*解决办法* :在后面加入--allow-unrelated-histories，允许不关联的历史

```
$ git merge FETCH_HEAD --allow-unrelated-histories
Merge made by the 'recursive' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```



**git switch <branch>** 切换分支，作用与git checkout <branch>相同

**git switch -c <branch>** 创建分支并立即切换，作用与**git checkout -b <branch>**及**git branch -b <branch>**相同

**git switch -f <branch>** 强行切换工作区分支

```
$ git switch -f master
Switched to branch 'master'
Your branch is up to date with 'lg/master'.
```

