---
title: Hexo + GitHub Page搭建过程及踩过的坑
date: 2018-05-15 22:00:41
tags: 环境搭建
categories: 环境搭建
---
[Hexo](https://hexo.io)是一个快速、简洁且高效的博客框架，拥有超快的速度，支持Markdown语法，而且还支持很多插件。我觉得是非常优秀的。

搭建一个hexo+next主题的博客其实是很简单的，可能刚开始对这个东西不熟悉，不知道怎么使用，如何部署、搭建。但自己动动手，其实你已经成功了一大步，毕竟只有自己踩过了坑，才深有体会。**不试一试怎么知道自己那么优秀呢。**

总结下来就三个步骤：*搭建+部署+备份*

<!--more-->

### 搭建
- 准备hexo的搭建环境(基于windows)
1. 安装[git](https://git-scm.com/downloads),基本是傻瓜式下一步就好了，注意勾选git bash
 
![9d4ef1ea-7c2f-488b-b8a3-f9c73dfec543.png](https://upload-images.jianshu.io/upload_images/2568189-e616dfaf775f17e9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  
2. 安装 [Node.js](https://nodejs.org/en/download/),选择对应版本安装就好。
3.  打开git bash  ,执行以下命令，显示 Node.js 版本，安装成功
```
node -v
```
- 安装hexo-cli
1. 安装 Hexo，在电脑中新建一个 compassblog 文件夹存放自己的博客，在文件夹内右键点击 Git Bash 进入命令窗口，执行以下代码：
```
npm install -g hexo-cli
```
2. 初始化 Hexo，得到 hexo 文件夹，用于存放 Hexo 博客所有的文件，包括下面会讲到的主题文件，Git Bash 窗口执行以下代码：（无特别提示，以下代码基本都在 Git Bash 命令窗口执行）
```
hexo init hexo
```
3. 配置 Hexo，进入 hexo 文件夹安装依赖，部署形成的文件，分别执行以下代码：
```
cd hexo
npm install
hexo generate
```
4. 启动服务器：执行以下代码，可以看到服务器端口号是 4000,
```
hexo server
```
![image.png](https://upload-images.jianshu.io/upload_images/2568189-17fddc82118151ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 打开浏览器，地址栏输入http://localhost:4000/ ，结果如下图，可以看到，初始化的 Hexo 博客搭建成功，可以访问，（提示：如果访问不到，可能4000端口被占用，如安装了福昕阅读器，使用$ hexo s -p 8080  地址栏输入http://localhost:8080 ）
![12](http://p5xem2laz.bkt.clouddn.com/2018/03/21/15.png)
6.至此，hexo本地服务端就已经搭好了
### 部署
1. 将初始化的 Hexo 博客部署到 GitHub Pages
2. 注册一个 Github 帐号，新建一个仓库，仓库名为：githubname.github.io ，如下图所示：（由于我的仓库已经创建，所以会显示仓库已经存在，并且这个仓库的名称必须严格按照 username.github.io 的格式来命名）
3. 进入已经建好的仓库，点击 settings ，找到 GitHub Pages 选项，点击 Choose a theme 选择一个主题，然后点击 select theme 选择主题，如下图所示：
![image.png](https://upload-images.jianshu.io/upload_images/2568189-57d10da268e04f12.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.  配置 Git 个人信息并建立远程连接：打开一个 Git Bash 窗口，输入下面的命令，具体参考：[windows下使用git和github建立远程仓库](http://www.cnblogs.com/lhyz/p/4051297.html)
```
git config --global user.name " GitHub 用户名 "
git config --global user.email " GitHub 邮箱 "
```
5. 修改 hexo 文件夹下的 _config.yml 全局配置文件，修改 deploy 属性代码，将本地 hexo 项目托管到 GitHub 上，如下图所示：
```
deploy:
  type: git     #部署的类型
  repository:  xxx.git # 仓库地址
  branch: master        #分支名称
  message: hexo deploy  #提交信息
```
6. 执行下面的命令，安装 hexo-deployer-git 插件，快速把代码托管到 GitHub 上
```
npm install hexo-deployer-git --save
```
7. 执行下面的代码命令，将 hexo 项目托管到 GitHub 上  (注：hexo generate 可缩写为 hexo g ， hexo deploy 可缩写为 hexo d)
```
hexo clean && hexo generate && hexo deploy
```
8. 浏览器地址栏输入 https://username.github.io/ 访问，可以看到博客已经部署到 GitHub 上，正常访问，如下图所示：![33](http://p5xem2laz.bkt.clouddn.com/2018/03/21/25.png)

##### 我使用的是[next](https://github.com/theme-next/hexo-theme-next)主题,具体怎么切换主题可以参考[Hexo  next配置](http://www.cnblogs.com/compassblog/p/8629626.html)

### 备份
1.  为什么要给博客备份呢？ 
当你换台电脑工作或者重装系统了，你的hexo本地环境就没有了，那么辛辛苦苦每话好的主题就得重新配置了。
2.  备份之前先了解下[hexo的目录结构](https://www.jianshu.com/p/17d55d420d94)
3.  如何备份？
采用git的分支操作进行备份。git这个东西用的好就是把利器，用不好就可能会很坑，建议多学学。首先要求一定的git功底,不然很多操作是看不懂的。主要备份的文件是**不在hexo目录下的.gitignore文件中的内容**，这点hexo官方可能都已经给我们想好了。
###### 具体操作
1.克隆下自己的仓库到本地(主要拿到.git文件)
```
git clone git@github.com:you/you.github.io.git
```
2. 打开仓库的文件夹  查看隐藏的项目 **复制.git文件**到你hexo的文件夹下。
![image.png](https://upload-images.jianshu.io/upload_images/2568189-9f22a3b710634933.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 打开git bash 看到master字样就OK了
![image.png](https://upload-images.jianshu.io/upload_images/2568189-29867fd815e830b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
4. 输入以下命令
```
git checkout -b backup
git add .
git commit -m 'backup'
git push origin backup
```
5 .然后去你的git仓库去看以下是否成功了
![image.png](https://upload-images.jianshu.io/upload_images/2568189-5d280a93521505ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
备份这里有个大坑
永远不要在这里切换分支 ，要不你master中的文件就会到你的工作目录里，影响备份，这还不是最骚的，最骚的是你的hexo环境就被破坏了  ，需要你重新配置。如果你git玩的66的，那就当我没说(哈哈)。
