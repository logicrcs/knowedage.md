# git tag/标签

Git 支持两种标签：**轻量标签（lightweight）** 与**附注标签（annotated）** 。
轻量标签很像一个不会改变的分支——它只是某个特定提交的引用。
而附注标签是存储在 Git 数据库中的一个完整对象， 它们是可以被校验的，其中包含打标签者的名字、电子邮件地址、日期时间， 此外还有一个标签信息，并且可以使用 GNU Privacy Guard （GPG）签名并验证。 通常会建议创建附注标签，这样你可以拥有以上所有信息。但是如果你只是想用一个临时的标签， 或者因为某些原因不想要保存这些信息，那么也可以用轻量标签。

**git tag -a** 创建附注标签,-m 选项指定了一条将会存储在标签中的信息。 如果没有为附注标签指定一条信息，Git 会启动编辑器要求你输
入信息。

```
$ git tag -a v1.0 -m "my version learngit 1.0"
```

**git tag <version>**  创建轻量标签,不用加-a,-s,-m选项

```
$ git tag v0.9 002c1cc(版本的哈希值)
$ git show v0.9
commit 002c1ccc91fbe0ecb60220c29f7a3aaea749b1eb (tag: v0.9)
Author: logic <1721549340@qq.com>
Date:   Wed Apr 7 15:46:10 2021 +0800

    工作流程测试

diff --git a/wenben.txt b/wenben.txt
index 3a4ac4b..416e910 100644
--- a/wenben.txt
+++ b/wenben.txt
@@ -138,4 +138,4 @@ html {


                        </div>
-
+末尾新加入的一行
\ No newline at end of file

```



**git tag** 列出已有的标签

```
$ git tag
v1.0

```

**git show** 查看标签信息和与之对应的提交信息

```
$ git show v1.0
tag v1.0
Tagger: logic <1721549340@qq.com>
Date:   Wed Apr 7 17:37:30 2021 +0800

my version learngit 1.0 //附注信息
具体的提交信息:
commit 167c574296d1a49f98eb0212ae30c969b511d99e (HEAD -> master, tag: v1.0, lg/master)
Author: logic <1721549340@qq.com>
Date:   Wed Apr 7 16:35:36 2021 +0800

    test git commit --amend
    again

diff --git a/forgotten_file.txt b/forgotten_file.txt
new file mode 100644
index 0000000..e69de29
diff --git a/test.txt b/test.txt
new file mode 100644
index 0000000..e69de29



Tagger:打标签者的信息
Date:打标签的日期时间
```

**git  tag -a <remote>  -m <标签的说明>** 在给过去打标签时，需要指定标签的校验和，就是标签的数字id

```
git tag -a v0.7 bc26c7f -m '第二次指定位置提交'
```

**git push <remote> <tagname>** 

```
$ git push lg v1.0
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 164 bytes | 164.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/logicrcs/learngit.git
 * [new tag]         v1.0 -> v1.0

```

**git push <remote> --tags** 把所有不在远程仓库服务器上的标签全部传送

```
$ git push lg --tags
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 188 bytes | 188.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/logicrcs/learngit.git
 * [new tag]         v0.7 -> v0.7

```

**git tag -d <tagname>** 删除掉你本地仓库上的标签

```
$ git tag -d v0.9
Deleted tag 'v0.9' (was 002c1cc)
```

**git push <remote> :refs/tags/<tagname>** 删除远程仓库的标签

```
$ git push lg :refs/tags/v0.9
To https://github.com/logicrcs/learngit.git
 - [deleted]         v0.9
 将冒号前面的空值推送到远程标签名，从而高效地删除它
```

**git push <remote> --delete <tagname>** 直观的删除远程仓库的标签