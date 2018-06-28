### 创建本地仓库，关联远程仓库并提交

在github上建立一个空repository，并不做初始化

在本地的一个文件夹中右击打开git bash

1. `git init`初始化一个本地git仓库
2. `git add 日常总结.md`将一个文件添加到本地stage暂存区
3. `git commit -m "comments"`将文件提交到本地仓库
4. `git remote add origin https://github.com/poly-zhao/something.git `把本地刚创建仓库与github上的仓库关联
5. `git push -u origin master`最后把本地仓库内容推送到github上(以后再提交代码时不需要加 -u)



####使用上面代码向新建的空的repository时 Permission deny 异常

使用`git remote rm origin`移除本地初始化仓库 , 然后重新使用`git remote add origin http://123.57.243.182/zhaole/ejia7_mvp.git` 后再push就没有问题了. 原来使用的是ssh链接



​	期间遇到的错误

```java
 warning: LF will be replaced by CRLF
```

按如下步骤解决

`$ rm -rf .git`  删除原来的git库

`$ git config --gobal core.autocrlf false `

`$ git init`



### 克隆Github项目到本地

git clone https://github.com/poly-zhao/KotlinMall(远程地址)
