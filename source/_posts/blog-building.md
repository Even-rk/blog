---
title: 使用hexo部署个人博客网站
date: 2020-07-31 07:04:35
updated: 2020-08-2 15:11:26
cover: /img/hexo.jpg
---

**Hexo是一款基于Node.js的静态博客框架，搭建静态博客网页，因为是静态的，所以加载也会比较的快，可以进入[hexo官网](https://hexo.io/zh-cn/)进行详细查看**

# Hexo的具体部署步骤

## 1：安装git

 首先需要安装git，mac本的话，一般都是有自带git的，windows电脑可以前往[git官网](https://gitforwindows.org/ )，直接下载

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/h19WgcmELC724rTUWIvVt1oI9WNstMbE/git-v.jpg)

终端执行git -v查看版本，能查看到就是git已经安装好了

## 2：安装node环境

这里选择适合自己电脑系统的安装就可以，[node官网](https://nodejs.org/en/download)，选择LTS最新版本即可

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/4DFwYmGgPS3xKRLXxykRf9dpVtkJGDhu/node.jpg)

启动终端查看node 和 npm 版本

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/s22p2VXGWoLHwebiFACm4GD1PvXQYAHz/node-v.jpg)

我这里用的是node是 18.16.0版本的 npm 是 9.5.1

npm 是node自带的一个第三方包管理器（不了解知道怎么用就好）

## 3：安装 Hexo 脚手架

```bash
# mac
sudo npm install hexo-cli -g 

# win
npm install hexo-cli -g 
```

mac本下载需要前面加上 sudo 以管理员身份安装

win电脑的可以直接使用 npm 安装

## 4：初始化hexo项目

你可以先创建一个文件夹myblog，然后到这个文件夹下打开终端

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/IE78nAxvQ8A10asIkprw60KgeeiYrP0w/init.jpg)

执行命令 `hexo init blog`

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/6HqoThxWWilFTR9zIUNwBc7TrT9sLWmM/hexoinit.jpg)

执行完命令后会自动生成一个文件夹 cd 到文件夹下，并执行 npm install 安装组件

```bash
cd blog # 进入到blog文件夹

npm install # 安装组件
```

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/q1oCVmeRdge9aO1h8F49KSApG8pr1RBH/npmInit.jpg)

启动本地服务器进行预览

```bash
hexo server
```



![image](http://lc-u11PV6WA.cn-n1.lcfile.com/MNflE9971bvYFRFpErvPn5NBpnDDkBy3/server.jpg)

`http://localhost:4000` 复制浏览器打开

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/G8j8DgQJtRASxgI2xqnNa7RYMIzU28Iw/hexodemo.png)

## 5：创建 git 仓库

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/OeMfdY7lrxd8kkgKsJDvmFQNRChDjSlV/gitee.jpg)

修改配置文件 _config.yml

```yaml
# 这里是写你创建仓库生成的仓库地址
url: http://kang-wenrui-aeary.gitee.io/blog/
# 以你创建的仓库名为准
root: /blog/ 

# 文件末尾的 Deployment 部分，修改成如下
deploy:
  type: git
  repo: git@gitee.com:kang-wenrui-aeary/blog.git
  branch: master
```

这里推送到远程仓库需要下载一个插件 hexo-deployer-git

执行命令

```bash
npm install hexo-deployer-git --save
```

完成后运行 hexo d 将网站上传部署到 gitee上。

```bash
hexo cl
hexo g
hexo d
```

## 6：网站部署

刷新gitee仓库

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/mSWUmuE2OkqakQRX315XTYfplln8bwbJ/gitpage.jpg)

点开服务中的Gitee Pages

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/aQ8EVln4b6ia01OuD0gFBJY48L44zEqL/fuwu.jpg)

直接点击启动等待一会

![image](http://lc-u11PV6WA.cn-n1.lcfile.com/d0nV7FebDRKNbhvnT0pt3O3f7GLTSH6P/qidong.jpg)

# 至此网站就部署成功，更多内容静待后续更新



