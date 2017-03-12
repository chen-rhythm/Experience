# 利用Hexo生成博客并部署到Github
<span id="index7"></span>
>* [环境准备](#index1)
>* [安装Hexo并初始化站点](#index2)
>* [部署到Github Pages](#index3)
>* [设置SSH keys](#index4)
>* [请开始你的表演](#index5)
>* [Tips](#index6)

- PS：我可能设置了一个假的页内跳转，求大佬帮忙改改
<span id="index1"></span>
## 一、环境准备
### 1.安装Git
### 2.安装Node.js
<span id="index2"></span>
## 二、安装Hexo并初始化站点
### 1.准备工作
  新建MD文件夹（下文以建在D盘的MD文件夹为例），在该目录下右键选择**Git Bash Here**
### 2.设置npm淘宝镜像
```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
### 3.安装Hexo
```
$ npm install -g hexo-cli
```
### 4.初始化站点
```
$ hexo init hexo
$ cd /d/MD/hexo
$ npm install
```
### 5.本地部署测试
```
$ hexo s
```
服务运行起来之后，打开浏览器，输入http://localhost:4000/即可打开Hexo的默认页面
<span id="index3"></span>
## 三、部署到Github Pages
### 1.新建仓库
登录[Github](https://github.com "Github")，创建一个repository，名称必须是——**用户名.github.io**
### 2.修改配置文件
打开hexo目录下的**_config.yml**文件，找到最后**Deployment**的配置并修改，在repo一行中填上自己的Github用户名，注意**冒号**和末尾的**.git**，格式如下：
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:用户名/用户名.github.io.git
  branch: master
```
### 3.安装Hexo-deployer-git
在hexo目录下，右键选择**Git Bash Here**
```
$ npm install hexo-deployer-git --save
```
### 4.配置Git全局邮箱&用户名
```
$ npm install hexo-deployer-git --save
$ git config --global user.email "邮箱"
$ git config --global user.name "用户名"
```
### 5.生成并部署博客
```
$ hexo g
$ hexo d
```
deploy之后报错，继续看标题四
<span id="index4"></span>
## 四、设置SSH keys
### 1.检查是否已经存在SSH keys
```
$ ls -al ~/.ssh
```
若不存在就没有关系，若存在，直接删除.SSH文件夹里的所有文件，该文件夹路径为C:\Users\PC\.ssh
### 2.获取SSH keys
```
$ ssh-keygen -t rsa -C "Github的注册邮箱"
```
出现冒号的地方不用管，一直回车
```
$ ssh-agent -s
$ ssh-add ~/.ssh/id_rsa
```
到这里出错，就输入如下指令
```
$ eval `ssh-agent -s`
$ ssh-add
```
### 3.复制密钥
```
$ clip < ~/.ssh/id_rsa.pub
```
通过指令复制密钥，之后可以直接Ctrl+V粘贴密钥
### 4.在Github上添加密钥
打开[Github](https://github.com "Github")，在同名repo的右上角**Settings**里选择**Deploy keys**选项卡，点击**Add deploy keys**，将刚复制好的密钥粘贴上去，点击**Add key**，在弹出来的框中输入Github的登陆密码即可完成添加
### 5.测试一下
```
$ ssh -T git@github.com
```
看到警告输入yes
### 6.重新部署博客
```
$ hexo g
$ hexo d
```
<span id="index5"></span>
## 五、请开始你的表演
打开浏览器输入<https://用户名.github.io/>，比如<https://chen-rhythm.github.io/>，然后……就没有然后了
<span id="index6"></span>
## Tips：
- 做到一半不会做，需要重新搭建的，请删除C:\Users\PC目录下的**.gitconfig**文件和**.SSH**文件夹，以及MD目录下的**hexo**文件夹

## [***>>点此回到开头<<***](#index7)
