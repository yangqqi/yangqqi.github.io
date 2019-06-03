---
layout: post
title: "使用 Jekyll 默认主题初始化 GitHub Pages"
date: 2019-05-14 18:20:00 +0800
categories: blog
---
记录第一次使用 [Jekyll](https://www.jekyll.com.cn/) 初始化 [GitHub Pages](https://yngkay.github.io/)。

## 安装 Ruby

**win10** 使用 [RubyInstaller](https://rubyinstaller.org/downloads/) 安装。

检查 **Ruby** & **Gem** 版本号：

    ruby --version

    gem --version

## 安装 Jkeyll & Bundler

    gem install jekyll bundler

检查 **Jekyll** 版本号：

    jekyll --version

新建项目：

    jekyll new myblog

## 运行服务器

    cd myblog

    bundle exec jekyll serve

测试访问：[http://127.0.0.1:4000/](http://127.0.0.1:4000/)

---

## 遇到问题

报错：

    Traceback (most recent call last):
        5: from C:/Ruby25-x64/bin/jekyll:23:in `<main>'
        4: from C:/Ruby25-x64/bin/jekyll:23:in `load'
        3: from C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/jekyll-3.8.5/exe/jekyll:11:in `<top (required)>'
        2: from C:/Ruby25-x64/lib/ruby/gems/2.5.0/gems/jekyll-3.8.5/lib/jekyll/plugin_manager.rb:48:in `require_from_bundler'
        1: from C:/Ruby25-x64/lib/ruby/2.5.0/rubygems/core_ext/kernel_require.rb:59:in `require'
    C:/Ruby25-x64/lib/ruby/2.5.0/rubygems/core_ext/kernel_require.rb:59:in `require': cannot load such file -- bundler (LoadError)

解决：

    bundle install

**Done!**

## Reference

[windows 安装 Jekyll 步骤及问题--彭世瑜](https://blog.csdn.net/mouday/article/details/79300135)

[Jekyll 快速入门](https://www.jekyll.com.cn/docs/)
