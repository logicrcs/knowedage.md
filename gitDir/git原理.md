# git原理

git是使用快照原理存储文件的。就是对修改的索引进行保存。是一个内容寻址(content-addressable)文件系统。即核心是一个键值对数据库(key-value data store)

Working Directory ---git add--- Staging Area

Staging Area ---git commit--- .git directory(Repository)

.git directory ---git checkout--- Working Directory

 ***Working Directory*** 工作区：保存由用户修改使用的内容，用户在工作区中修改内容。

 ***Staging Area*** 暂存区：是一个文件，保存着下次要提交的文件列表信息，保存在Git仓库中，与git的版本库放在一起。git专业术语叫“索引”

***.git directory*** 版本库：git中最重要的部分，保存元数据和对象数据库，从这里复制数据来实现克隆。

***基本的 Git 工作流程*** 

1.在工作区中修改文件。

2.将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。

3.提交更新，找到暂存区的文件，将快照永久性存储到 Git 目录。

```
目录列表
config
description
HEAD
hooks/
info/
objects/
refs/
```

description 文件仅供 GitWeb 程序使用， config 文件包含项目特有的配置选项。 info 目录包含一个全局性排除（global exclude）文件 ， 用以放置那些不希望被记录在 .gitignore文件中的忽略模式（ignored patterns）。 hooks 目录包含客户端或服务端的钩子脚本（hook scripts）， 在Git 钩子 中这部分话题已被详细探讨过。剩下的四个条目很重要：HEAD 文件，index 文件，objects 、refs 目录。 它们都是
Git 的核心组成部分。 objects 目录存储所有数据内容；refs 目录存储指向数据（分支、远程仓库和标签等）的提交对象的指针； HEAD 文件指向目前被检出的分支；index 文件保存暂存区信息。