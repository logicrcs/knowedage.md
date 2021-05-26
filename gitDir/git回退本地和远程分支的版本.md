# git回退本地和远程分支的版本

1. 查看提交日志 

   ```
   $ git log --oneline --decorate --graph --all
   *   232d395 (HEAD -> serverfix, lg/serverfix, lg/master, master) 冲突解决完成
   |\
   | * f4048a4 finished the new footer [issus 533]
   | * 4f83d07 added a new footer [issue 53]
   * | 3f8c340 fixed the broken email address by hotfox
   |/
   * 1bed63f made other changes
   * c6c45a9 全面梳理git diff
   * aba4794 (tag: v1.1) 测试git 保存的是什么
   * 167c574 (tag: v1.0) test git commit --amend again
   * 002c1cc 工作流程测试
   * 1ebdf49 (tag: v0.8) 老版本提交
   * bc26c7f (tag: v0.7) 删除错误文件
   * d6703a5 add test.txt
   * c183b5f update license
   * 2d5a091 merge
   * 8a3553d git tracks changes
   * 6d0caa7 understand how stage works
   * 49a98d1 append GPL
   * b3b37a2 add distributed
   * af19cb7 update
   * 81c8d32 wrote a readme file
   serverfix分支与master分支处于一个
   ```

2. 切换本地分支的版本

   1. 查看当前分支是否为想要改变版本的分支

      1. 是

      2. 不是

         **git checkout [branch]** 

         ```
         $ git checkout serverfix
         Switched to branch 'serverfix'
         ```

         **git switch [branch]** 

          ```
         $ git switch -f master
         Switched to branch 'master'
         Your branch is up to date with 'lg/master'.
          ```

   2. 切换提交版本

      **git reset [commit]** 

      ```
      $ git reset 1bed63f
      $ git log --oneline --decorate --graph --all
      *   232d395 (lg/serverfix, lg/master, master) 冲突解决完成
      |\
      | * f4048a4 finished the new footer [issus 533]
      | * 4f83d07 added a new footer [issue 53]
      * | 3f8c340 fixed the broken email address by hotfox
      |/
      * 1bed63f (HEAD -> serverfix) made other changes
      * c6c45a9 全面梳理git diff
      ```

      **git branch -f  <branch> <version>** 

      ```
      $ git branch -f testing 167c574
      $ git log --oneline --decorate --graph --all
      *   232d395 (HEAD -> master, lg/master) 冲突解决完成
      |\
      | * f4048a4 finished the new footer [issus 533]
      | * 4f83d07 added a new footer [issue 53]
      * | 3f8c340 fixed the broken email address by hotfox
      |/
      * 1bed63f (lg/serverfix, serverfix) made other changes
      * c6c45a9 全面梳理git diff
      * aba4794 (tag: v1.1) 测试git 保存的是什么
      * 167c574 (tag: v1.0, testing) test git commit --amend again
      * 002c1cc 工作流程测试
      ```

3.  强制推送到远程仓库

   将修改强制push到远端默认主机仓库分支上
   git push -f -u origin 分支名称

   例如：
   将修改强制push到远端默认主机仓库master分支上
   git push -f -u origin master

   将修改强制push到远端默认主机仓库dev分支上
   git push -f -u origin dev

   ```
   $ git push -f -u lg testing:testing
   Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
   remote:
   remote: Create a pull request for 'testing' on GitHub by visiting:
   remote:      https://github.com/logicrcs/learngit/pull/new/testing
   remote:
   To https://github.com/logicrcs/learngit.git
    * [new branch]      testing -> testing
   Branch 'testing' set up to track remote branch 'testing' from 'lg'.
   ```

   