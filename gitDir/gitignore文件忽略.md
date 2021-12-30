# git需要忽略某些文件的提交

```bash
https://blog.csdn.net/sunxiaoju/article/details/86495234
原文的链接
忽略的规则
    target          //忽略这个target目录
    angular.json    //忽略这个angular.json文件
    log/*           //忽略log下的所有文件
    css/*.css       //忽略css目录下的.css文件
```

- gitignore只能忽略未被git跟踪的文件，如果对应的项目文件已经被git跟踪了。就不起作用

  ```bash
  git rm -r --cached .
  清除目前的所有跟踪的文件
  git add .
  $ git commit -m 'update .gitignore'
  [master 3cd11b7] update .gitignore
   1 file changed, 10 deletions(-)
   delete mode 100644 .gitignore
  ```

  