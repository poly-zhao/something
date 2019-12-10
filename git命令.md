 https://www.jianshu.com/p/92305d949c0e?utm_source=desktop&utm_medium=timeline 

配置用户名和邮箱

```git
$ git config --global user.name "knight"
$ git config --global user.email "knight@dayuan.com"
```



#### 创建本地仓库，关联远程仓库并提交

在本地的一个文件夹中右击打开git bash

1. `git init`初始化一个本地git仓库
2. `git add 日常总结.md`将一个文件添加到本地stage暂存区
3. `git commit -m "comments"`将文件提交到本地仓库
4. `git remote add origin https://github.com/poly-zhao/something.git `把本地刚创建仓库与github上的仓库关联
5. `git push -u origin master`最后把本地仓库内容推送到github上(以后再提交代码时不需要加 -u)

#### GitLab 配置公钥 SSH Key

1. 桌面右键鼠标打开 "Git Bash Here" 
2. 键入命令：ssh-keygen -t rsa -C "gitlab的邮箱账号" 
3. 提醒你输入key的名称，输入 id_rsa (一定要是id_rsa )
4. 在C:\Users\Administrator\.ssh下产生两个文件：id_rsa和id_rsa.pub 如果找不到的话请到桌面上找,找到之后将这两个文件拷贝到C:\Users\Administrator\.ssh目录下即可
5. 用编辑器打开id_rsa.pub文件，复制内容，在gitlab.com的网站上到ssh密钥管理页面，在Key一栏粘贴刚才复制的内容，Title一栏输入名称，这个名称随便起，建议英文，然后点击Add。 
6. 完成

#### Github配置公钥



#### 克隆Github项目到本地

git clone https://github.com/poly-zhao/KotlinMall(远程地址)

#### 查看分支

查看所有分支

```
$ git branch -a
* master
  remotes/origin/maste
```

查看远程分支

```
$ git branch -r
  origin/master
```

查看本地分支

```$ git branch
$ git branch
* master
```

#### 拉取远程分支

从远程分支`origin/master` 拉取并创建新的本地分支`dev1`

```
$ git checkout -b dev1 origin/master
Switched to a new branch 'dev1'
Branch dev1 set up to track remote branch master from origin.
$ git branch -a
* dev1		//新建的本地分支, 本地当前所在的分支
  master
  remotes/origin/master
```

#### 切换本地分支

```
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'. //表示本地分支`master`与远程分支内容一样
```

还有可能出现内容不一样的情况: 假如有人向远程库提交了内容, 将本地分支切换到其他本地分支时会有以下提示, 按照提示拉取以下即可

`Your branch is behind 'origin/master' by 1 commit` 

#### 提交新的本地分支

提交本地分支`dev1` 并建立对应新的远程分支

```
$ git push origin dev1
Total 0 (delta 0), reused 0 (delta 0)
remote: Updating references: 100% (1/1)
To ssh://192.168.1.180:29418/test.git
 * [new branch]      dev1 -> dev1

$ git branch -a
* dev1
  master
  remotes/origin/dev1		//新建的远程分支
  remotes/origin/master
```

####  建立本地分支与远程分支的映射关系 

 这样使用git pull或者git push时就不必每次都要指定从远程的哪个分支拉取合并和推送到远程的哪个分支了。 

- 查看映射关系

  ```
  $ git branch -vv
  * dev1   6f1a8ba other user commit	//没有和远程库建立映射关系,在该分支上提交和拉取代码都需要指定远程分支
    master 6f1a8ba [origin/master] other user commit	//本地master分支都是向origin/master提交和从origin/master拉取
  ```

- 建立本地分支与远程分支的映射关系

  ```
  $ git branch -u origin/dev1
  Branch dev1 set up to track remote branch dev1 from origin.
  $ git branch -vv
  * dev1   6f1a8ba [origin/dev1] other user commit//与远程分支建立映射
    master 6f1a8ba [origin/master] other user commit
  ```

- 取消本地分支与远程分支的映射关系

  ```bash
  git branch --unset-upstream
  ```

#### 合并分支

``` 
 git merge --no-ff dev
```



#### 使用上面代码向新建的空的repository时 Permission deny 异常

方法有两种

1. 使用`git remote rm origin`移除本地初始化仓库 , 然后重新使用`git remote add origin http://123.57.243.182/zhaole/ejia7_mvp.git` 后再push就没有问题了. 原来使用的是ssh链接
2. 重新配置GitLab的公钥, 如上

#### 期间遇到的错误

```java
 warning: LF will be replaced by CRLF
```

按如下步骤解决
`$ rm -rf .git`  删除原来的git库
`$ git config --gobal core.autocrlf false `
`$ git init`

#### 使用命令解决冲突

1. 远程repository的内容更改, 本地没有pull也更改了, 这时想把本地的更改内容push到远程时会出现conflict

   ```git
   Administrator@zhaole MINGW64 ~/Desktop/asdf/something (master)
   $ git add git命令.md
   
   Administrator@zhaole MINGW64 ~/Desktop/asdf/something (master)
   $ git commit -m "conflict"
   [master cc8bbfc] conflict
    1 file changed, 1 insertion(+), 1 deletion(-)
   
   Administrator@zhaole MINGW64 ~/Desktop/asdf/something (master)
   $ git pull
   Auto-merging git命令.md
   CONFLICT (content): Merge conflict in git命令.md
   Automatic merge failed; fix conflicts and then commit the result.//有冲突, 提示合并冲突
   ```

2. 这时要找到发生冲突文件, 然后将有如下标识的代码, 修改为你想要![git冲突](.\imgs\git冲突.png)

   修改后

   ```java
   创建本地仓库，(bdca测试一下Adcb)关联远程仓库并提交
   ```

3. 然后重新`add`, `commit`,`push` ,  //注意**解决冲突时`add`, `commit`操作都是分支(master|MERGING)上进行的**, 执行完`master`后才又回到`master`分支

   ```java
   Administrator@zhaole MINGW64 ~/Desktop/asdf/something (master|MERGING)
   $ git add git命令.md
   
   Administrator@zhaole MINGW64 ~/Desktop/asdf/something (master|MERGING)
   $ git commit -m "conflict solved"
   [master 2daa4b9] conflict solved
   
   Administrator@zhaole MINGW64 ~/Desktop/asdf/something (master)
   $ git push
   Counting objects: 6, done.
   Delta compression using up to 4 threads.
   Compressing objects: 100% (6/6), done.
   Writing objects: 100% (6/6), 619 bytes | 0 bytes/s, done.
   Total 6 (delta 4), reused 0 (delta 0)
   remote: Resolving deltas: 100% (4/4), completed with 2 local objects.
   To https://github.com/poly-zhao/something.git
      945f1b0..2daa4b9  master -> master
   
   ```


#### fatal: HttpRequestException encountered.

Github 禁用了TLS v1.0 and v1.1，必须更新Windows的git凭证管理器 

解决方法:https://blog.csdn.net/txy864/article/details/79557729 
或者 直接到https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.16.2下载[**GCMW-1.16.2.exe**](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/download/v1.16.2/GCMW-1.16.2.exe) 并安装即可



#### 输入账号密码后无法再次弹出认证窗口且一直认证失败[fatal: Authentication failed for]的解决办法

git提交代码时输入账号密码后一直提示如下错误, 并且无法再次弹出账号密码输入框

```git
$ git push -u origin master
fatal: Authentication failed for 'http://192.168.1.222:8099/zhaol/pan_android.git/'
```



解决方法一: (无效)

git config --system --unset credential.helper

解决方法二: (有效)

在下面方框中选择 两项中的一个

- 编辑 修改已经输入的账号密码
- 删除 再次提交代码时 输入git 的账号密码

![Authentication failed for](C:\Users\Administrator\Desktop\总结\something\imgs\Authentication failed for.png)



#### 修改远程仓库

- 查看当前的远程仓库

  git remote -v

- 修改为想要设置的远程仓库

  git remote set-url origin https://where you want to put your repository to.git

- 验证一下

  git remote -v

#### 忽略已提交的文件

如果文件已提交, 再在.gitignore中添加对此文件的忽略是无效的. 

想要忽略已提交的文件执行可下步骤:

1. 使用 `git rm --cached （文件名）` 删除掉这个你想忽略的文件； 
2. 然后更新 .gitignore ，忽略掉目标文件。 

#### stash命令

该命令可以认为是将没有commit的修改暂存起来, 可以进行多次暂存,以栈的形式保存这些暂存

`git stash`会把所有未提交的修改（包括暂存的和非暂存的）都保存起来，用于后续恢复当前工作目录

`git stash save "test-cmd-stash` 同上, 给stash加一个message，用于记录版本，

`git stash list` 查看现有stash

`git stash apply stash@{0}` 恢复指定的暂存到工作目录,`stash@{0}`为暂存的名字, 该命令不带名字时恢复最新的暂存到工作目录

`git stash drop stash@{0}` 删除指定的暂存, 不带名字时删除最新的暂存

`git stash pop`命令恢复最新缓存的工作目录, 并删除该最新缓存(); 等同于先`git stash apply `,再`git stash drop `

`git stash clear` 清除所有的暂存

```git
git status  //查看当前状态
//工作目录不是clean的
git stash	//工作目录恢复到了上次commit的状态
//工作目录clean, 且与上次commit后的内容一样
...做一些工作...
git stash pop //回复到行3时的状态
```

