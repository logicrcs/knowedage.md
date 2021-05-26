# git reset 版本控制

git reset 不会改变 HEAD ，所以无法实现改变工作分支的目的，它所做的都是改变HEAD指向的分支,比如HEAD指向的是master，reset会改变master这个分支指向的提交版本。

例如，当前工作分支是serverfix，HEAD指向的是serverfix

```
$ git log --oneline --decorate --graph --all
*   232d395 (lg/master, master) 冲突解决完成
|\
| * f4048a4 finished the new footer [issus 533]
| * 4f83d07 added a new footer [issue 53]
* | 3f8c340 fixed the broken email address by hotfox
|/
* 1bed63f (HEAD -> serverfix, lg/serverfix, testing) made other changes
* c6c45a9 全面梳理git diff
```

这个时候执行git reset master

```
$ git reset master


$ git log --oneline --decorate --graph --all
*   232d395 (HEAD -> serverfix, lg/master, master) 冲突解决完成
|\
| * f4048a4 finished the new footer [issus 533]
| * 4f83d07 added a new footer [issue 53]
* | 3f8c340 fixed the broken email address by hotfox
|/
* 1bed63f (lg/serverfix, testing) made other changes
* c6c45a9 全面梳理git diff

```

发现serverfix分支被移到了与master分支相同的提交版本上，而不是HEAD指向的分支发生了变化；HEAD依然指向serverfix分支。

head指针执行当前工作分支，可能是master，可能是testing，可能是创建的其他branch分支，而分支的指针就会确定某一个版本。

**git reset <version>** 调整head指向的版本，并将对应版本的文件覆盖到索引区

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test.rb


Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git reset c6c45a9

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.rb

nothing added to commit but untracked files present (use "git add" to track)

暂存区被对应版本的内容刷新
```



**git reset HEAD <file>** 将当前主分支的版本库文件覆盖到索引区，由于索引区还没有将索引提交成新的快照，所以版本库中的快照还是老版本的。使用版本库中的快照覆盖索引区中的内容，就相当于撤销了两次提交（git commit）中间的所有暂存（git add），而指定文件名称就可以指定覆盖索引区中指定文件效果，这样在实际上就形成了*取消暂存文件* 的实际效果。

**git reset --hard <version>** 增加了--hard参数，语句的效果就是将指定版本的文件覆盖到整个git项目管理目录，包括暂存区和工作区

其默认参数是--mixed，会改变暂存区，--soft只会HEAD所指向分支的位置，不会改变暂存区。

```
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.rb
        test3.txt

nothing added to commit but untracked files present (use "git add" to track)

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git add test.rb
warning: LF will be replaced by CRLF in test.rb.
The file will have its original line endings in your working directory

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git reset --hard HEAD
HEAD is now at c6c45a9 全面梳理git diff

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test3.txt

nothing added to commit but untracked files present (use "git add" to track)
```

