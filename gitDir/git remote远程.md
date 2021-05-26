# git remote远程仓库命令

**git remote add <shortname> <url>** 添加一个新的远程 Git 仓库，同时指定一个方便 使用的简写

```
git remote add lnx https://github.com/logicrcs/learnNote.Xmind.git
git remote -v
lnx     https://github.com/logicrcs/learnNote.Xmind.git (fetch)
lnx     https://github.com/logicrcs/learnNote.Xmind.git (push)

```



**git ls-remote <remote>**  获得远程引用的完整列表，这个完整的远程引用不是分支，指的是一个版本号。

```
$ git ls-remote lg
c6c45a90050b22d6ac35f0b417bdf436feab565b        HEAD
c6c45a90050b22d6ac35f0b417bdf436feab565b        refs/heads/master
f6ad7c72d9c7d71fc8b3f137b9b246de065b5d15        refs/tags/v0.7
bc26c7f09a5cbb94738f5960317ed6dd841c5400        refs/tags/v0.7^{}
779e3dcd13a3ae1932970bc02f2eb2b73f4df9ee        refs/tags/v0.8
1ebdf49a52603c4258d230b56703632e52ab21cf        refs/tags/v0.8^{}
0cba8cba868150dce286021d33ec9c197c2215d6        refs/tags/v1.0
167c574296d1a49f98eb0212ae30c969b511d99e        refs/tags/v1.0^{}
ad1a9c2d6b9a163e801e95015d9a9f3f38d07371        refs/tags/v1.1
aba4794523068d4935837803096f2a5f0f63ddb8        refs/tags/v1.1^{}
```



**git remote**  列出存在的远程仓库。

```
$ git remote
origin
```

**git remote -v** 显示需要读写远程仓库使用的git保存的简写与其对应的url

```
$ git remote -v
origin  git@github.com:lggit@github.com:lggit@github.com:lggit@github.com:lg (fetch)
origin  git@github.com:lggit@github.com:lggit@github.com:lggit@github.com:lg (push)
```

**git remote show <remote>**  列出远程仓库的 URL 与跟踪分支的信息,remote对应的是仓库名

```
$ git remote show lg
* remote lg
  Fetch URL: https://github.com/logicrcs/learngit.git
  Push  URL: https://github.com/logicrcs/learngit.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local ref configured for 'git push':
    master pushes to master (up to date)
HEAD branch:所处分支
Remote branch:远程分支
```



**git remote rename <oldname> <newname>** 修改一个远程仓库的简写名

```
$ git remote rename origin lg

Administrator@PC-20210218IXTW MINGW64 /d/soft/workspace/learngit (master)
$ git remote
lg
lg是learngit的简写
```

**git remote remove <remote>**  移除远程仓库

**git push <remote> <branch>**  向远程推送代码

```
refused:拒绝
fatal:致命的，灾难性的
$ git push origin master:master
ssh: connect to host github.com port 22: Connection refused
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
端口被拒绝
https://blog.csdn.net/s740556472/article/details/80318886，有答案

$ git push origin master
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 4 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (11/11), 2.46 KiB | 2.46 MiB/s, done.
Total 11 (delta 4), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (4/4), done.
To https://github.com/logicrcs/learngit.git
   d6703a5..167c574  master -> master
```

**git fetch <remote>** 访问远程仓库，从中拉取所有没有的数据.只会将数据下载到本地仓库,不会自动合并或修改当前的工作区内容，必须手动将其合并入工作区

```

```

**git clone -o <remote>** 可以在clone的时候指定仓库的名字

