### 创建本地仓库，(测试一下)关联远程仓库并提交

在github上建立一个空repository，并不做初始化

在本地的一个文件夹中右击打开git bash

1. `git init`初始化一个本地git仓库
2. `git add 日常总结.md`将一个文件添加到本地stage暂存区
3. `git commit -m "comments"`将文件提交到本地仓库
4. `git remote add origin https://github.com/poly-zhao/something.git `把本地刚创建仓库与github上的仓库关联
5. `git push -u origin master`最后把本地仓库内容推送到github上(以后再提交代码时不需要加 -u)

### GitLab 配置公钥 SSH Key

1. 桌面右键鼠标打开 "Git Bash Here" 
2. 键入命令：ssh-keygen -t rsa -C "gitlab的邮箱账号" 
3. 提醒你输入key的名称，输入 id_rsa (一定要是id_rsa )
4. 在C:\Users\Administrator\.ssh下产生两个文件：id_rsa和id_rsa.pub 如果找不到的话请到桌面上找,找到之后将这两个文件拷贝到C:\Users\Administrator\.ssh目录下即可
5. 用编辑器打开id_rsa.pub文件，复制内容，在gitlab.com的网站上到ssh密钥管理页面，在Key一栏粘贴刚才复制的内容，Title一栏输入名称，这个名称随便起，建议英文，然后点击Add。 
6. 完成

#### 使用上面代码向新建的空的repository时 Permission deny 异常

方法有两种

1. 使用`git remote rm origin`移除本地初始化仓库 , 然后重新使用`git remote add origin http://123.57.243.182/zhaole/ejia7_mvp.git` 后再push就没有问题了. 原来使用的是ssh链接
2. 重新配置GitLab的公钥, 如上



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
