# git checkout

**git checkout -- <file>** 撤销修改



**git checkout <branchname>**  切换到一个已存在的分支，本质为将head指针执行切换的分支,切换分支会更改工作区文件

```
$ git checkout testing
Switched to branch 'testing'
```

但存在两个分支是显示版本路线如下

```
$ git log --oneline --decorate --graph --all
* 1bed63f (HEAD -> master) made other changes
| * 09698e1 (testing) made a change
|/
* c6c45a9 (lg/master) 全面梳理git diff
* aba4794 (tag: v1.1) 测试git 保存的是什么
* 167c574 (tag: v1.0) test git commit --amend 
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

**git checkout --track <remote>/<branch>** 自动跟踪远程分支，没有就创建