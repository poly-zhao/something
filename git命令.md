### 创建本地仓库，关联远程仓库并提交

在github上建立一个空repository，并不做初始化

在本地的一个文件夹中右击打开git bash

1. `git init`初始化一个本地git仓库
2. `git add 日常总结.md`将一个文件添加到本地stage暂存区
3. `git commit -m "comments"`将文件提交到本地仓库
4. `git remote add origin https://github.com/poly-zhao/something.git `把本地刚创建仓库与github上的仓库关联
5. `git push -u origin master`最后把本地仓库内容推送到github上



​	期间遇到的错误

```java
 warning: LF will be replaced by CRLF
```

按如下步骤解决

`$ rm -rf .git`  删除原来的git库

`$ git config --gobal core.autocrlf false `

`$ git init`