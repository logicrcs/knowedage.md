# git push&git fetch

**git push <remote> <localbranch>:<remotebranch>**  向远程推送代码

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
http://ask.sov5.cn/q/tEID7uXpZP


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

**git push -f <remote> <localbranch>:<remotebranch>**    

向远程强制推送代码

**-u** 建立追踪关系

```
$ git push -f -u lg serverfix:serverfix
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/logicrcs/learngit.git
 + 232d395...1bed63f serverfix -> serverfix (forced update)
Branch 'serverfix' set up to track remote branch 'serverfix' from 'lg'.
同时使用两个参数
```

**git push <remote> --delete <branch>** 删除一个远程分支

**git push <remote> :<branch>** 删除远程分支（原理是将空白分支推送到远程）

personal access token

```
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
```

**git fetch <remote>** 访问远程仓库，从中拉取所有没有的数据.只会将数据下载到本地仓库,不会自动合并或修改当前的工作区内容，必须手动将其合并入工作区