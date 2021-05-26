# git 文件转换流程

## 工作区

1.工作区中的文件经过git add <file> 转变为等待被提交到版本库

的暂存区文件

```
Changes to be committed://等待被提交的改变
  (use "git restore --staged <file>..." to unstage)
        deleted:    test.txt
```

而使用***git restore --staged <file>*** 就可以将暂存区的记录移除，但是不会修改工作区的文件，仅仅是暂存区中没有这个文件讲的记录了。

实际上***git reset HEAD <file>*** 有相同的效果，详见git reset

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   wenben.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   wenben.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt
上面第一个是暂存区中的老版本文件 wenben.txt，但是并未commit到版本库。
第二个是工作区中的文件 wenben.txt被修改过，但是修改并没有被提交的暂存区。
第三个是在工作区中没有被提交的暂存区中的文件，所以显示没有被追踪的状态。
```

```
执行下面命令的结果是
$ git restore --staged wenben.txt

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt
        wenben.txt

nothing added to commit but untracked files present (use "git add" to track)
只有test.txt,wenben.txt两个未追踪的工作区文件，对比上面的状态发现，暂存区中存的老版本文件都没有了，所以没有了需要被提交的版本库中的文件，所以就没有commit提示了。就只剩下了git add 提示了。
```

但查看工作区中的 wenben.txt文件，实际上，wenben.txt文件并没有被改变。

***git restore <file>*** 则是会撤销文件的修改，撤销到最近一次执行git add的内容。即撤销到最近一次暂存区更新的内容。实际上

执行前：

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   wenben.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   wenben.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt

一个暂存区中的老版本 wenben.txt 文件需要被commit到版本库，一个工作区中的wenben.txt修改需要被add到暂存区。一个工作区中的test.txt新文件需要被add到暂存区。
```

执行后：

```
$ git restore wenben.txt

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   wenben.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt
在执行后，一个暂存区中的老版本 wenben.txt，一个工作区中的test.txt新文件需要被add到暂存区。
```

并且工作区中的修改被撤销了，但是暂存区中的记录没有撤销

此时将暂存区中的老版本文件提交

```
$ git commit -m "老版本提交"
[master 1ebdf49] 老版本提交
 1 file changed, 141 insertions(+)
 create mode 100644 wenben.txt

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt
 就只有test.txt文件现在需要被add
```

此时对wenben.txt进行新的修改

```
······
</fieldset>
				
				
			</div>
末尾新加入的一行
$ git status
On branch master
Changes not staged for commit://已跟踪文件的内容发
生了变化，但还没有放到暂存区
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   wenben.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt
有一个未追踪的修改应该提交到本地库，下面就有两个提示，第一个是git add更新修改到暂存区，第二个是撤销工作区发生的修改使用git restore命令
```

如果只是简单地从工作目录中手工删除文件，运行 git status 时就会在 “Changes not staged for commit” 部分（也就是 未暂存清单）看到：

```
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    test.txt

```

这是可以使用**git restore**  命令恢复工作区中的文件

```
$ git restore test.txt

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ ls -f1
./
../
.git/
license.txt
readme.txt
test.txt
wenben.txt
可以看见，被删除的test.txt文件被复原了
```

***git rm*** 命令用于从 **[工作区+暂存区]** 中删除文件，因为其默认调用-f参数,如果在输入时显式的添加--cached,就可以只删除暂存区中的记录。

```
$ git status
On branch master
nothing to commit, working tree clean

```



## 暂存区

2.暂存区的文件使用**git commit**  向快照提交到版本库，

**git log -p/--patch** 显示每次提交所引入的差异（按 补丁 的格式输出）。--pretty=oneline/--oneline设置文本一行显示



