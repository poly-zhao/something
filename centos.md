

#### 查看已安装软件的信息

查看安装目录: `rpm -ql nodejs`
查看软件版本: `rpm -q nodejs`

#### 重定向

我想查看 当前系统中安装的所有包 但是数量有太多的, 我可以将`yum list` 的输出重定向到文件中然后在从文件中查找

```
当前所在文件为home
yum list > list.txt	//重定向到list.txt文件中
grep ^node list.txt	//找出所有以node开头的行
```



```
1.1      重定向符号

>               输出重定向到一个文件或设备 覆盖原来的文件
>!              输出重定向到一个文件或设备 强制覆盖原来的文件
>>             输出重定向到一个文件或设备 追加原来的文件
<               输入重定向到一个程序 

1.2标准错误重定向符号

2>             将一个标准错误输出重定向到一个文件或设备 覆盖原来的文件  b-shell
2>>           将一个标准错误输出重定向到一个文件或设备 追加到原来的文件
2>&1         将一个标准错误输出重定向到标准输出 注释:1 可能就是代表 标准输出
>&             将一个标准错误输出重定向到一个文件或设备 覆盖原来的文件  c-shell
|&              将一个标准错误 管道 输送 到另一个命令作为输入
```

####  rpm查询

`rpm -q 包名` 查询是否安装, 包名:不需要时完整包名

```
rpm -q node
```

`rpm -qa` 查询所有已安装的rpm包

```
rpm -qa		//返回有rpm包
rpm -qa | grep node	//   筛选出包名中包含node的rpm
```



## yum

#### 查看包信息

`yum info nodejs` 

#### 安装

`yum -y install nodejs` 安装nodejs, `nodejs` 包名
`-y` 自动回答yes

#### 升级

`yum -y update nodejs` 升级命令; `nodejs`包名, **如果不指定包名,则升级所有包和linux内核**

#### 卸载

`yum -y remove 包名` 卸载命令

#### 软件组管理命令

`yum grouplist`:  列出所有可用的软件组列表

` yum groupinstall 软件组名`   : 安装指定的软件组

`yum groupremove 软件组名`:  下载

## 更改语言(临时修改)

`LANG=zh_CN.utf8`  改为中文

`LANG=en_US` 改为英文

## 安装nodejs

`yum install nodejs`

使用上面命令安装完nodejs后发现版本太低, 需要进行升级. 参考 https://blog.csdn.net/qq_26744901/article/details/81609203 

上面文章中使用了`n` 对node进行升级. `n` 实际上也一个js库. 用于管理nodejs的版本管理 

## 安装mariadb

https://www.cnblogs.com/zhanzhan/p/7729981.html

## 安装ftp

https://cloud.tencent.com/document/product/213/10912

仅是按上面文档安装ftp还是无法正常的使用ftp的, 需要在腾讯云的控制台为云服务器实例添加安全组暴露ftp的端口

1. 先到控制台新建安全组, 我开放了所有端口

![1新建安全组](.\imgs\1新建安全组.png)

2. 将服务器实例添加到安全组中

![2添加安全组](.\imgs\2添加安全组.png)

![3添加安全组](.\imgs\3添加安全组.png)

- ftp windows客户端需要将连接方式该为主动

## 用npm安装pm2

`npm install -g pm2` 全局安装pm2

## 安装VS  Code

https://code.visualstudio.com/docs/setup/linux

下面的步骤也是参考官方文档. 与官方文档略有不同: 手动创建了`vscode.repo` 文件, 官方文档中使用命令创建的

1. 

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```

2. 

```
touch /etc/yum.repos.d/vscode.repo
vi /etc/yum.repos.d/vscode.repo
```

输入以下内容

```
[code]
name=Visual Studio Code
baseurl=https://packages.microsoft.com/yumrepos/vscode
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc
```

3. 

```
yum check-update
sudo yum install code
```

Due to the manual signing process and the system we use to publish,  the yum repo may lag behind and not get the latest version of VS Code  immediately

4. 建立软连接

```
ln -s /usr/share/code/bin/code /usr/bin/vscode
```

`.repo`文件: 指定了使用`yum`命令安装软件时从哪里获取软件安装包(`rpm`包). 

## 常用命令

 https://blog.51cto.com/14449524/2429254?source=dra 