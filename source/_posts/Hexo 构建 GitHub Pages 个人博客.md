---
title: Hexo 管理 GitHub Pages 个人博客
date: 2020-06-05
category: technology
---

最近想把闲置了一年的 GitHub Pages 用起来，选了个简约的主题 [Maupassant](https://github.com/pagecho/maupassant) 整理下。

<!--more-->

## 安装 [Maupassant-hexo](https://github.com/tufu9441/maupassant-hexo)

安装 [Hexo](https://hexo.io/zh-cn/docs/) 前提：

- [Node.js](https://nodejs.org/en/docs/)
- [Git](https://git-scm.com/)

安装 Hexo：

````shell
    npm install -g hexo-cli
    hexo verson // 检查版本号

    hexo init <folder> // 初始化项目
    cd <folder>
    npm install
    npm run build
````

这样就可以初始化一个简单的 hexo 项目。

我选取了 Maupassant-hexo 作为主题模板，直接从仓库克隆下来：

````shell
    git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
    npm install hexo-renderer-pug --save
    npm install hexo-renderer-sass --save
````

拉取主题之后，编辑Hexo目录下的 _config.yml，将 theme 的值改为 maupassant 就可以了。

## 使用 [Travis CI](https://travis-ci.com/) 将 Hexo 博客部署到 [GitHub Pages](https://pages.github.com/)

- [将 Hexo 部署到 GitHub Pages](https://hexo.io/zh-cn/docs/github-pages)

Hexo 官方文档对使用 Travis CI 自动化构建有详细说明，需要注意的是，现在 GitHub Pages 以 <用户名>.github.io 为域名访问的仓库默认发布 master 分支为 pages，不允许设置其它分支；当然其它仓库依然允许设置其它分支为 pages。基于这个点，我们将 Hexo 站点文件夹推送到 hexo-project 分支，将 master 用来发布静态文件资源，并将 .travis.yml 配置文件改为：

````yml
    sudo: false
    language: node_js
    node_js:
      - 10 # use nodejs v10 LTS
    cache: npm
    branches:
      only:
        - hexo-project # build master branch only
    script:
      - hexo generate # generate static files
    deploy:
      provider: pages
      skip-cleanup: true
      github-token: $GH_TOKEN
      keep-history: true
      target_branch: master
      on:
        branch: hexo-project
      local-dir: public
````

这样 Travis CI 就会帮我们监听 hexo-project 分支，当分支变动时，自动构建我们的静态博客到 master 分支，再由 GitHub Pages 自动部署个人主页。

## Reference

- [关于 GitHub Pages](https://help.github.com/cn/github/working-with-github-pages/about-github-pages)
- [大道至简 —— Hexo 简洁主题推荐](https://www.haomwei.com/technology/maupassant-hexo.html)
- [将 Hexo 部署到 GitHub Pages](https://hexo.io/zh-cn/docs/github-pages)
