# rebase 变基的使用

正常的多分支是由一个提交版本创建出的分支，开发者在新分支上进行一些修改，而其他开发者或者自己又在之前的分支进行了操作。在工作完成后就一定要合并分支，但这要产生 merge 并且在历史中产生复杂的分支线。难以分辨。

git rebase --abort 会放弃合并，回到rebase操作之前的状态，之前的提交的不会丢弃；

​	***撤销rebase*** 

git rebase --skip 则会将引起冲突的commits丢弃掉（慎用！！）；

​	***会抛弃dev分支修改的所有内容*** 

git rebase --continue 合并冲突，结合"git add 文件"命令一起用与修复冲突，提示开发者，一步一步地有没有解决冲突。（fix conflicts and then run “git rebase --continue”）

​	***处理问题推荐使用*** 

例如：

创建一个dev分支开发新功能

```
$ git log --oneline --abbrev-commit
8e78c81 (HEAD -> master) Merge remote-tracking branch 'lg/master'
d4bad23 (lg/master) Update readme.txt
4fc9ee5 update modified test3.txt
63b1e15 create test3.txt
232d395 冲突解决完成
```

这是目前的工作分支是master,基于master分支创建dev分支

```
$ git switch -c dev
Switched to a new branch 'dev'
```

现在dev分支与master分支内容一样，接下来开始进行一次改造

```
$ vim readme.txt
$ git add readme.txt
$ git commit -m 'add merge'
[dev 6701a8c] add merge
 1 file changed, 1 insertion(+)
```

提交完成之后可以看到，dev分支已领先master分支一个版本

```
$ git log --oneline --graph
* 6701a8c (HEAD -> dev) add merge
*   8e78c81 (master) Merge remote-tracking branch 'lg/master'
```

现在回到master分支

```
$ git switch master
Switched to branch 'master'
Your branch is ahead of 'lg/master' by 3 commits.
  (use "git push" to publish your local commits)
```

对同一个文件改造一个版本

```
$ vim readme.txt
$ git commit -a -m 'testing rebase'
[master 8cec706] testing rebase
 1 file changed, 1 insertion(+)
```

查看发现master分支也更新了一个版本

```
$ git log --oneline --graph
* 8cec706 (HEAD -> master) testing rebase
*   8e78c81 (lg/master) Merge remote-tracking branch 'lg/master'
|\
| * d4bad23 Update readme.txt
* | 4fc9ee5 update modified test3.txt
```

回到dev分支,进行变基操作，因为操作同一个文件，所以报了错

```
$ git checkout dev
Switched to branch 'dev'

$ git rebase master
error: could not apply 6701a8c... add merge
Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 6701a8c... add merge
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
```

查看版本，会发现程序创建了一个新分支作为容纳冲突的分支,这里显示没有分支，dev在变基的过程中，后面的信息显示，变基的对象信息（提交版本号，提交说明）

```
$ git branch -vv
* (no branch, rebasing dev) 8cec706 testing rebase
  dev                       6701a8c add merge
  master                    8cec706 [lg/master: ahead 1] testing rebase
  serverfix                 1bed63f [lg/serverfix] made other changes
  testing                   167c574 [lg/testing] test git commit --amend again

```



发生冲突后，找到发生冲突的readme.txt文件，解决了冲突，就可以提交了

```
$ git add .

$ git rebase --continue
[detached HEAD 295ee26] add merge and testing rebase fix compile
 1 file changed, 3 insertions(+)
Successfully rebased and updated refs/heads/dev.
```

查看分支视角，发现问题已经被解决

```
$ git branch -vv
* dev       295ee26 add merge and testing rebase fix compile
  master    8cec706 [lg/master: ahead 1] testing rebase
  serverfix 1bed63f [lg/serverfix] made other changes
  testing   167c574 [lg/testing] test git commit --amend again
```

查看历史界面，发现问题已经被解决，dev分支已经被合到master分支后面

```
$ git log --graph --oneline
* 295ee26 (HEAD -> dev) add merge and testing rebase fix compile
* 8cec706 (master) testing rebase
*   8e78c81 (lg/master) Merge remote-tracking branch 'lg/master'
|\
| * d4bad23 Update readme.txt

```

最后回到主分支，进行快进合并

```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'lg/master' by 1 commit.
  (use "git push" to publish your local commits)

$ git merge dev
Updating 8cec706..295ee26
Fast-forward
 readme.txt | 3 +++
 1 file changed, 3 insertions(+)

```

