#  Git笔记

## 为什么用git

- 版本回退
- 多人协作
- 多人开发代码同步

## Git命令

#### 配置

~~~~bash
//用户文件夹下  ->.gitconfig
git config --global user.name "qieee"
git config --global user.email "1209791748@qq.com" //github 账号邮箱
//查询配置
git config --global user.name 
git config --global user.email

//更换账户
控制面板-用户账户-凭据管理-github.com
~~~~

### git三区

~~~~js
1.工作区 项目文件夹 进行增删改
git add xxxx
2.暂存区  暂时保存，即将交给git进行版本管理
git commit -m '提交信息'
3.版本区   已经被git管理
~~~~

警告 warning :LF will be replaced by CRLF in

git config --global core.autocrlf false/true

### 差异对比

~~~~bash
git diff --工作区 和 暂存区 对比
git diff --cached --版本区和暂存区
git diff master --版本区和工作区
~~~~



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
> git add . |*                 //添加当前目录下的所有文件

### 提交代码到本地仓库

> git commit -m "这里写备注"      //提交后文件纳入版本控制

### 分支

~~~~bash
git checkout -b dev -- 创建并切换到dev分支  b branch
git branch   -- 查看分支 和 当前的分支
git checkout master -- 切换分支到 master

-- 分支合并
git merge dev		-- dev 合并到当前分支
git branch -d dev	-- 删除分支 dev 

-- 分支差异
git diff branch1 branch2	-- 显示两个分支所有差异文件的象系差异
git diff branch1 branch2 -stat --显示两个分支的差异文件列表
git diff branch1 branch2 -- xxx显示指定文件的详细差异
~~~~



### 版本回退

~~~~bash
git log -- 所有提交日志
git reflog --精简日志，版本号

git reset --hard HEAD^		--回退一次提交 hard强制 ^^回退两次
git reset --hard 版本号		--指定回退版本号

--一般不用
git reset HEAD		--用版本库文件替换暂存
git checkout --x.txt		--用暂存区文件替换 工作区
git checkout HEAD x.txt		--用版本库文件替换暂存和工作区文件

git rm --cached x.txt		--从暂存区删除文件
~~~~

### 删除文件

~~~~bash
git rm x.txt		--删除文件 文件必须被版本控制
git rm -r xxxx		--删除文件夹  忽略空文件夹
~~~~

## Github

~~~~bash
-- GitHub --git项目托管网站

~~~~

### 远程仓库

#### 查看远程仓库地址

> git remote -v

#### 设置远程仓库地址

> git remote add origin https://github.com/hubname/projname.git     
>
>  //  origin是远程仓库的名字  别名

#### 提交代码到远程仓库

> git push -u origin master            //首次提交  -u第一次  master分支主分支
>
> git push  [origin master]           //直接提交  需要授权 推送到origin仓库的master分支
>
> git config --global credential.helper store		记住密码，一般自动记住
>
> git remote remove origin	删除关联仓库

#### 从远程仓库拉取代码

> git pull                                         //在提交代码前应该先拉取代码
>
> git pull origin master		拉取仓库的分支中的文件 会产生冲突
>
> git fetch origin master:tmp		把远程master分支拉去到本地tmp分支，不会自动合并，比面使用

#### 克隆仓库

~~~~bash
git clone http://github.com/reposito .git  -- 保持连接
git pull 拉取仓库内所有  包括分支
~~~~



### 查看修改日志

> git log

#### 提交文件忽略

~~~~bash
新建文件 .gitignore
:
.idea
.vscode
~~~~

### 多人协作开发

~~~~bash
team
~~~~



## ？疑问

- SVN和Git