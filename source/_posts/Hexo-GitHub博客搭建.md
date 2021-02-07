---
title: Hexo-GitHub博客搭建
categories:
  - technology
tags:
  - Blog 搭建
toc: true
date: 2021-02-06 20:30:40
sidebar:
---



# 准备（本文基于Windows平台）

​	Hexo的官方文档写的很好，本文只是个人建站总结，如需实际操作，建议看着官方文档来操作：[文档 | Hexo](https://hexo.io/zh-cn/docs/)

## Hexo安装

- 关于

  > Hexo 是一个快速、简洁且高效的博客框架。 Hexo 使用Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

- 安装（官网：https://hexo.io/）

  Hexo需要电脑上已经安装node.js和git（已安装的可跳过）

  - 安装Git

    网址： https://git-scm.com/downloads
    与普通软件一样，更换软件安装位置之后，一直点击下一步，直至开始安装

  - 安装node.js

    下载安装程序：[Download | Node.js](https://nodejs.org/en/download/)安装即可(使用 Node.js 官方安装程序时，请确保勾选 **Add to PATH** 选项（默认已勾选）)

  - 安装Hexo

    - 打开右键菜单选择*Git Bash Here*(如果你正常安装好git后应该会有这个选项的)

    <img src="https://s3.ax1x.com/2021/02/06/yYfs0K.png" alt="右键菜单" style="zoom:50%;" />

    ​	执行

    ```bash
  $ npm install -g hexo-cli
    ```

    ​	安装Hexo

    - 此时，可以使用`npx hexo <command>`来使用hexo命令，但为了方便直接使用`hexo <command>`,

      我们执行
      
      ````bash
      echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
      ````
      
      将 Hexo 所在的目录下的 `node_modules` 添加到环境变量之中
  
  - 初始化
  
    - 打开作为博客文件的文件夹，在此文件夹中打开git bash，
  
      ```bash
      $ hexo init <folder>
      $ cd <folder>
      $ npm install
      ```
      - 第一条是新建存放各种文件的文件夹，不指定`folder`的话即直接将各种文件放在当前文件夹中
      - 第二条是切换到新建的文件夹路径下，如果第一步没有新建文件夹，则不需要执行此命令
      - 第三条是安装一些必需的程序
      
    - 此时，你的文件夹里应该是这样的：
    
    ```
      .
      ├── _config.yml
      ├── package.json
      ├── scaffolds
      ├── source
      |   ├── _drafts
      |   └── _posts
      └── themes
    ```
    - 执行`hexo s`
    
      ![hexo_s](https://s3.ax1x.com/2021/02/06/yYTQl4.png)
    
      在浏览器中输入[localhost:4000](http://localhost:4000)可看到预置的博客主题，之后在git bash中按*ctrl+c*可关闭hexo服务
    
    - 为了之后使用git进行发布博客，还需要安装一个扩展
    
    - ```bash
      npm i hexo-deployer-git
      ```

## GitHub

- 参见上一篇[Lyunvy's Blog](https://lyunvy.tk/#Part-1—配置)

# 配置

## 站点配置文件

​	关于配置文件，官方文档解释的最为详细，再次建议去查阅官方文档[配置 | Hexo](https://hexo.io/zh-cn/docs/configuration)

## Hexo主题及配置

​	Hexo有许多开源的主题[Themes | Hexo](https://hexo.io/themes/)我们可以选择一个喜欢的主题，这里pure主题为例：主题仓库：[Hexo theme pure](https://github.com/cofess/hexo-theme-pure) 主题预览：[Cofess - Web Developer & Designer](https://blog.cofess.com/)  ，在主题预览中可以找到作者关于主题的使用说明，可参照[Hexo博客主题pure使用说明](https://blog.cofess.com/2017/11/01/hexo-blog-theme-pure-usage-description.html) 

- 在你的文件夹路径下打开git bash，执行

  ````bash
  git clone https://github.com/cofess/hexo-theme-pure.git themes/pure
  ````

  将主题clone到themes文件夹下

- 打开站点文件夹下的配置文件*_config.yml*，修改theme那一行为`theme: pure`,这样即启用了pure主题

- 安装各种插件：

  -  [hexo-wordcount ](https://link.jianshu.com/?t=https://github.com/willin/hexo-wordcount)

    ```bash
    npm install hexo-wordcount --save
    ```

  - [hexo-generator-json-content](https://link.jianshu.com/?t=https://github.com/alexbruno/hexo-generator-json-content)

    ```bash
    npm install hexo-generator-json-content --save
    ```

  - [hexo-generator-feed](https://link.jianshu.com/?t=https://github.com/hexojs/hexo-generator-feed)

    ```bash
    npm install hexo-generator-feed --save
    ```

  - [hexo-generator-sitemap](https://link.jianshu.com/?t=https://github.com/hexojs/hexo-generator-sitemap)

    ```bash
    npm install hexo-generator-sitemap --save
    ```

  - [hexo-generator-baidu-sitemap](https://link.jianshu.com/?t=https://github.com/coneycode/hexo-generator-baidu-sitemap)

    ```bash
    npm install hexo-generator-baidu-sitemap --save
    ```

  - [hexo-neat](https://link.jianshu.com/?t=https://github.com/rozbo/hexo-neat)

    ```bash
    npm install hexo-neat --save
    ```

    在配置文件中添加一下内容：

    ```yaml
    # hexo-neat
    neat_enable: true
    neat_html:
      enable: true
      exclude:  
    neat_css:
      enable: true
      exclude:
        - '*.min.css'
    neat_js:
      enable: true
      mangle: true
      output:
      compress:
      exclude:
        - '*.min.js' 
    ```


## 连接Github与本地

- 打开git bash，然后输入下面命令：

```bash
git config --global user.name "username"
git config --global user.email "usermail"
```

​		用户名和邮箱根据你自己的github的信息自行修改。

- 生成密钥SSH key：

```bash
ssh-keygen -t rsa -C "usermail"
```

​		打开[github](https://link.zhihu.com/?target=http%3A//github.com/)，在头像下面点击`settings`，再点击`SSH and GPG keys`，新建一个SSH，名字随便。

​		git bash中输入

```bash
cat ~/.ssh/id_rsa.pub
```

​		将输出的内容复制到框中，点击确定保存

- 打开打开站点配置文件修改最后一行的配置：

```yaml
deploy:
  type: git
  repository: https://github.com/***/***.github.io
  branch: master
```

​		repository修改为你自己的github项目地址

# 写作

新建文章 ：在git bash 中输入

```bash
hexo new <title>
```

​	*< title>*即为文章的标题，执行此命令后会在博客文件夹下的*source\\_posts*目录下创建一个*< title>.md*文件，此文件即为你新建的文章，在此文件中输入你的文章内容（最好使用markdown编辑工具来输入内容）

# 发布

在博客目录下执行`hexo g`生成静态网页，然后执行`hexo s`可以本地预览效果，最后执行`hexo d`上传到github上。这时打开你的github.io主页即可以看到你新发布的博客啦



至此，基础的Hexo+GitHub已经搭建好啦，至于如何将它更加个性化，还是需要好好看文档呀~



预告~下一篇：Hexo-GitHub博客搭建