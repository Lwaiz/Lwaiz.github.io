---
title: Hello World
date: 2026-05-08 14:24:05
cover: /img/background/bg9.png
tags: [Hello World]
categories: Hello World
description: Welcome to Hexo！
---

Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

# Hexo + Butterfly 使用教程

1. 新建文章
```bash
运行
hexo new "文章标题"
生成文件：source/_posts/文章标题.md
生成图片文件夹：source\_posts\文章标题
```

2. Front-matter（头部配置，必须）
```markdown
---
title: Hexo + Butterfly 教程
date: 2026-06-01 12:00:00
updated: 2026-06-01 12:00:00
tags:
  - Hexo
  - Butterfly
categories:
  - 博客搭建
description: 从零开始搭建 Hexo + Butterfly 博客
top_img: https://xxx.com/top.jpg  # 顶部图
cover: https://xxx.com/cover.jpg    # 封面图
toc: true                            # 显示目录
toc_number: true                     # 目录编号
copyright: true                      # 显示版权
---
```

3. 标题居中
``` 
<h1 style="text-align:center">使用html标题居中</h1>
```

4. 本地预览与部署
    1. 本地运行
    ```bash
    运行
    hexo clean   # 清缓存
    hexo g       # 生成静态文件
    hexo s       # 本地预览
    ```
    2. 部署到 GitHub Pages
        1. 安装部署插件
        ```bash
        运行
        npm install hexo-deployer-git --save
        ```
        2. 配置 _config.yml
        ```yaml
        deploy:
        type: git
        repo: https://github.com/你的用户名/你的用户名.github.io.git
        branch: main
        ```
            3. 一键部署
        ```bash
        运行
        hexo d
        ```
5. 常用命令速查
```bash
运行
hexo new "标题"      # 新建文章
hexo new page "页面" # 新建页面
hexo clean            # 清除缓存
hexo g                # 生成静态文件
hexo s                # 本地启动
hexo d                # 部署到远程
```