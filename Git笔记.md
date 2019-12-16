# Git笔记

## 为什么用git

- 版本回退
- 多人协作
- 多人开发代码同步

## Git命令

### 查看当前目录

> pwd

### 进入文件夹

> cd dirname/

### 初始化仓库

> git init

### 查看当前状态

> git status                 //红色为未添加，绿色为已添加

### 添加文件到暂存区

> git add filename      //添加单个文件
>
> git add .                  //添加当前目录下的所有文件

### 提交代码到本地仓库

> git commit -m "这里写备注"      //提交后文件纳入版本控制

### 远程仓库

#### 查看远程仓库地址

> git remote -v

#### 设置远程仓库地址

> git remote add origin https://github.com/hubname/projname.git     
>
>  //  origin是远程仓库的名字

#### 提交代码到远程仓库

> git push -u origin master            //首次提交
>
> git push                                      //直接提交

#### 从远程仓库拉取代码

> git pull                                         //在提交代码前应该先拉取代码

### 查看修改日志

> git log

## ？疑问

- SVN和Git