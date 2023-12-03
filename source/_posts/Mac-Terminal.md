---
title: Mac 笔记本 Terminal 美化 
date: 2023-11-26 13:16:27
updated: 2023-11-26 13:17:11
cover: /img/terminal.png
---

关于mac的terminal主题配置有用到oh-my-zsh，oh-my-zsh是一个基于 zsh 命令行，提供主题配置的工具
其他的主题可以前往自行查看

官网：https://ohmyz.sh/

我这里自己用到的是powerlevel10k

下面是具体的操作步骤

## 安装oh-my-zsh

```sh
sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"
```

我这里使用的是国内镜像源，完成后输出结果如下展示：

![oh-my-zsh](http://lc-u11PV6WA.cn-n1.lcfile.com/G6z6AMmO6uvluDY0JQ2ir4qsCsh73TEv/oh-my-zsh.png)

## 设置主题

我们进入到oh-my-zsh主题目录下，并克隆powerlevel10k主题

```sh
cd ~/.oh-my-zsh/themes
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git
```

修改zshrc配置文件

```sh
open ~/.zshrc

# 找到 ZSH_THEME
# 修改为我们需要的主题
ZSH_THEME="powerlevel10k/powerlevel10k"

# ZSH_THEME="样式名称" 
```

修改完成后 source 配置文件
```sh
source ~/.zshrc
```

重新打开终端会直接进入到powerlevel10k的配置页面，如果需要重新修改配置信息，执行配置命令

```sh
p10k configure
```

![p10k configure](http://lc-u11PV6WA.cn-n1.lcfile.com/VHSPdsHGV63Iy8Ns9HjPthhyT0OojFbQ/p10k%20configure.png)

可能有些图标会乱码，这个时候需要在自己电脑上下载一下字体文件，这里准备好了 

## 安装 Nerd Font

首先找个文件夹克隆一下仓库，文件夹随意哪里都可以

```sh
git clone https://github.com/ryanoasis/nerd-fonts.git --depth 1
```

在克隆的过程中可能会有些漫长，字体文件包约有1G，请耐心等待

![nerd-fonts](http://lc-u11PV6WA.cn-n1.lcfile.com/EgJxrTjIzbVvWHv1yPr00KLJMSsqIKMa/nerd-fonts.png)

开始安装字体

```sh
nerd-fonts/install.sh
```

设置终端字体，选择后缀带有Nerd Font的字体，在重新打开终端，乱码就解决了

下面可以跟随指引配置自己的终端主题。

![use](http://lc-u11PV6WA.cn-n1.lcfile.com/qo5GC4IKdQ2DdDNQhoNQ9sBJtn1oJwF2/user-nerd-font.png)

## 效果展示

![shell](http://lc-u11PV6WA.cn-n1.lcfile.com/UGL6ouiJYeYYhcy3opBnGn7rCg18zL2y/shell.png)

下面这个是我自己在用的终端背景图，使用过程图片调整了暗度

![mac](http://lc-u11PV6WA.cn-n1.lcfile.com/rOoiANLXrI8MsfHmrAqJTzOb32ra6HrB/mac.jpg)
