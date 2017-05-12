## 1 准备
sudo apt-get install git curl atom   下载git, curl, atom软件  
sudo apt-get update   更新  
git clone [url] 克隆到本地  
git status  查看仓库状态  
git log  查看仓库日志

#### 修改后上传更新
git add .  添加到git 暂时保存下来  
git commit -m 'message'  做版本  
git push   提交

#### atom 装包命令
apm install [packagename]  
包：
emmet  
open-in-browser  
autocomplete-paths  
language-babel

手动创建.gitignore里面写名称,忽略不想上传的文件或文件夹

#### 本地项目上传
ssh-keygen 生成电脑钥匙 .put公有,将里面内容复制到github的SSH and GPG keys  
git init 初始化成一个仓库  
git remote add origin 地址  
git push -u origin master

#### 分支
切换分支之前必须全部做成版本才能切换分支  
git branch 查看所有分支和当前分支 `*`代表当前分支  
git branch dev 创建新的dev分支  
git checkout dev  切换到dev分支  
git push -u origin dev 向远端推送dev分支  
git merge dev 把dev分支上领先的操作拉取过来  
git branch -d dev 删除本地dev分支，不能删master分支，并且不能删当前所在分支  
git push origin :dev  删除远端的dev分支

gh-pages是一个十分特殊的分支，内容可以被访问，地址为learnerty.github.io/仓库名

#### 安装node
先在github上安装nvm  

nvm ls-remote  从远端查看nodejs的版本  
nvm install 版本号  下载安装最新的nodejs版本  
自动会把npm装上，npm是最大的nodejs的包管理工具  
nvm use 版本 切换node的版本  
nvm alias default 版本  设置默认的版本  
nvm uninstall 版本  卸载nodejs

#### 安装idoc
1. npm install idoc -g
2. idoc init 初始化
```
? Package name
>> Must be only lowercase letters, numbers, dashes or dots, and start with lowercase letter.
tian@tian-pc:~/Desktop/doc$ idoc init
? Package name doc
? Version 1.0.0
? Description 我的笔记
? keywords note
? Licenses MIT
? Choose a theme. default
? Author learnerty <1083089451@qq.com>
```
3. idoc build 生成
