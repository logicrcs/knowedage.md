# git diff

***git diff*** 工作目录中当前文件和暂存区域快照之间的差异。 也就是修改之后还没有暂存起来的变化内容。就是对比工作区与暂存区。即显示尚未暂存的改动。

```
$ git diff
diff --git a/test2.txt b/test2.txt
index e69de29..d16e5d5 100644
--- a/test2.txt
+++ b/test2.txt
@@ -0,0 +1 @@
+测试git存储方案
```



**git diff --staged** 比较暂存区与版本库的区别

```
$ git diff --staged
diff --git a/test2.txt b/test2.txt
index e69de29..d16e5d5 100644
--- a/test2.txt
+++ b/test2.txt
@@ -0,0 +1 @@
+测试git存储方案
```



**git diff <version> -- <filename>** 比较版本库指定版本和工作区中的指定文件的差别

```
$ git diff HEAD -- test2.txt
diff --git a/test2.txt b/test2.txt
index e69de29..e28d62e 100644
--- a/test2.txt
+++ b/test2.txt
@@ -0,0 +1,2 @@
+测试git存储方案
+测试 git diff <version> -- <filename> 与git diff --staged区别
\ No newline at end of file

$ git diff 167c574 -- test.txt
diff --git a/test.txt b/test.txt
index e69de29..f76da64 100644
--- a/test.txt
+++ b/test.txt
@@ -0,0 +1 @@
+测试通过版本号来指定git diff版本的效果
\ No newline at end of file

```

**git diff <localbranch> <remote>/<remotebranch>** 比较本地版本库分支与远程仓库对应分支的差别

```
$ git diff main lnx/main
diff --git a/README.md b/README.md
index b4b20bc..cd7e64f 100644
--- a/README.md
+++ b/README.md
@@ -1 +1 @@
-# learnXmind
\ No newline at end of file
+# learnNote.Xmind
```

