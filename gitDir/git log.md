# git log

**git log --oneline** 单行显示

```
$ git log --oneline
8e78c81 (HEAD -> master) Merge remote-tracking branch 'lg/master'
d4bad23 (lg/master) Update readme.txt
4fc9ee5 update modified test3.txt
63b1e15 create test3.txt
232d395 冲突解决完成
```

**git log --graph** 查看分支

```
$ git log --graph --oneline
*   8e78c81 (HEAD -> master) Merge remote-tracking branch 'lg/master'
|\
| * d4bad23 (lg/master) Update readme.txt
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
```

**git log --abbrev-commit** 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。说是这样，实际没什么卵用

```
$ git log --oneline --abbrev-commit
8e78c81 (HEAD -> master) Merge remote-tracking branch 'lg/master'
d4bad23 (lg/master) Update readme.txt
4fc9ee5 update modified test3.txt
63b1e15 create test3.txt
232d395 冲突解决完成
f4048a4 finished the new footer [issus 533]
3f8c340 fixed the broken email address by hotfox
4f83d07 added a new footer [issue 53]
```

**git log --decorate** 参数用来显示一些相关的信息，如HEAD、分支名、tag名等 确实显示了更多的信息，当时对比之前效果不明显

```
$ git log --decorate
commit ac27da34138fdc4590dba33d1862c6bd9e048d48 (HEAD -> master, lg/master)
Author: logic <1721549340@qq.com>
Date:   Fri Apr 16 11:17:01 2021 +0800

    创建超前远程分支

commit 295ee265506805fa63cad8372d905b494040738b (dev)
Author: logic <1721549340@qq.com>
Date:   Fri Apr 9 17:10:37 2021 +0800

    add merge and testing rebase fix compile

commit 8cec7066d61459d06bc3dc8f740435c3ceca0e50
Author: logic <1721549340@qq.com>
Date:   Fri Apr 9 17:46:31 2021 +0800

    testing rebase

$ git log
commit ac27da34138fdc4590dba33d1862c6bd9e048d48 (HEAD -> master, lg/master)
Author: logic <1721549340@qq.com>
Date:   Fri Apr 16 11:17:01 2021 +0800

    创建超前远程分支

commit 295ee265506805fa63cad8372d905b494040738b (dev)
Author: logic <1721549340@qq.com>
Date:   Fri Apr 9 17:10:37 2021 +0800

    add merge and testing rebase fix compile

commit 8cec7066d61459d06bc3dc8f740435c3ceca0e50
Author: logic <1721549340@qq.com>
Date:   Fri Apr 9 17:46:31 2021 +0800

    testing rebase
```

如果在显示的过程中出现显示不全的问题时，可以用enter一直回车到end出现，也可以用wq退出

