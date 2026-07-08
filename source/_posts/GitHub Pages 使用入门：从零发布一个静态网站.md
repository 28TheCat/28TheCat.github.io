---
title: GitHub Pages 使用入门：从零发布一个静态网站
date: 2024-05-08 20:00:00
categories:
  - 技术笔记
tags:
  - Hexo
  - 博客
  - GitHub Pages
  - Fluid
---

这篇文章不是一篇纯粹的 GitHub Pages 入门笔记，而是记录我这次从零搭建个人博客的过程：用 Hexo 生成静态网站，用 Fluid 作为博客主题，再通过 GitHub Actions 部署到 GitHub Pages。

最后网站会发布到：

```text
https://28thecat.github.io/
```

## 我的技术栈

这次博客主要用了下面这些技术：

- GitHub Pages：托管最终生成出来的静态网页
- GitHub Actions：自动构建和部署网站
- Hexo：静态博客生成器
- Fluid：Hexo 主题，负责博客的页面样式、导航、搜索、Banner 等
- Node.js / npm：安装 Hexo、主题和搜索插件
- Markdown：写文章
- Git：管理代码并推送到 GitHub

整体流程可以理解成：

```text
Markdown 文章
  -> Hexo 生成 public 静态文件
  -> GitHub Actions 上传 public
  -> GitHub Pages 发布网站
```

GitHub Pages 本身只负责托管静态文件，它不会直接运行 Hexo。真正把 Markdown、主题配置和文章转换成网页的是 Hexo。

## 为什么选择 Hexo + Fluid

GitHub Pages 默认支持 Jekyll，但我这次没有用 Jekyll，而是选择了 Hexo。原因很简单：Hexo 对博客场景比较友好，目录结构清晰，写文章就是写 Markdown，主题生态也比较成熟。

Fluid 是 Hexo 里一个比较完整的主题。它提供了很多博客常用功能，例如：

- 首页 Banner
- 导航栏
- 分类页
- 标签页
- 归档页
- 关于页
- 本地搜索
- 代码高亮样式
- 暗色模式

对于个人博客来说，这些功能基本够用了，不需要从零写页面样式。

## 创建 GitHub Pages 仓库

个人主页仓库的名字需要写成：

```text
用户名.github.io
```

我的仓库是：

```text
28TheCat/28TheCat.github.io
```

这种仓库发布后，访问地址就是：

```text
https://28thecat.github.io/
```

这里有一个容易踩坑的地方：如果仓库是 Hexo 项目，就不要让 GitHub Pages 用默认的 Jekyll 构建源码。因为 Jekyll 会读取 `_config.yml`，看到 `theme: fluid` 时，会把它当成 Ruby 主题去找，结果就会报错。

正确做法是：用 GitHub Actions 先运行 Hexo，把网站生成到 `public/`，再部署 `public/`。

## 初始化 Hexo 博客

Hexo 项目初始化后，核心目录大概是这样：

```text
my-blog/
  _config.yml
  package.json
  source/
    _posts/
  scaffolds/
  themes/
```

其中最重要的是：

- `_config.yml`：Hexo 根配置
- `source/_posts/`：文章目录
- `source/`：页面、图片等资源目录
- `package.json`：项目依赖和命令

我在根配置里设置了站点基础信息：

```yml
title: 28theCat
subtitle: Welcome to 28theCat's Blog!
description: 个人博客
author: wangyating
language: zh-CN
timezone: Asia/Shanghai
url: https://28thecat.github.io/
theme: fluid
```

`theme: fluid` 表示 Hexo 使用 Fluid 主题生成网站。

## 配置 Fluid 主题

Fluid 的主题配置文件是：

```text
_config.fluid.yml
```

我把导航栏配置成了博客常见的几个入口：

```yml
navbar:
  blog_title: "28theCat"
  menu:
    - { key: "home", link: "/", icon: "iconfont icon-home-fill" }
    - { key: "archive", link: "/archives/", icon: "iconfont icon-archive-fill" }
    - { key: "category", link: "/categories/", icon: "iconfont icon-category-fill" }
    - { key: "tag", link: "/tags/", icon: "iconfont icon-tags-fill" }
    - { key: "about", link: "/about/", icon: "iconfont icon-user-fill" }
```

首页 Banner 使用：

```yml
index:
  banner_img: /img/bg/banner.jpg
  slogan:
    enable: true
    text: "Welcome to 28theCat's Blog!"
```

对应图片放在：

```text
source/img/bg/banner.jpg
```

因为 Hexo 会把 `source/img/bg/banner.jpg` 生成到网站里的 `/img/bg/banner.jpg`。

## 创建常用页面

博客除了文章，还需要一些固定页面。我创建了：

```text
source/about/index.md
source/links/index.md
source/categories/index.md
source/tags/index.md
```

分类页内容是：

```md
---
title: 分类
layout: categories
---
```

标签页内容是：

```md
---
title: 标签
layout: tags
---
```

这样 Fluid 就会用主题内置布局显示分类和标签。

## 写文章

Hexo 的文章放在：

```text
source/_posts/
```

文章本身是 Markdown 文件。比如这篇文章的开头就是 front matter：

```yml
---
title: GitHub Pages 使用入门：从零发布一个静态网站
date: 2026-07-08 20:00:00
categories:
  - 技术笔记
tags:
  - Hexo
  - 博客
  - GitHub Pages
  - Fluid
---
```

下面就可以正常写 Markdown 正文。代码块也可以直接写：

```js
console.log('hello hexo')
```

Hexo 会把 Markdown 转成 HTML，Fluid 负责把页面渲染得更像一个完整博客。

## 配置本地搜索

我使用 `hexo-generator-search` 生成搜索索引。在 `_config.yml` 中配置：

```yml
search:
  path: local-search.xml
  field: post
  content: true
```

在 `_config.fluid.yml` 中保持搜索开启：

```yml
search:
  enable: true
  path: /local-search.xml
  generate_path: /local-search.xml
  field: post
  content: true
```

这样生成网站时，会多出一个 `local-search.xml`，Fluid 的搜索框会读取这个文件完成本地搜索。

## 本地预览

修改文章或配置后，可以先在本地预览：

```bash
npx hexo server
```

然后打开：

```text
http://localhost:4000
```

如果只是想生成静态文件，可以运行：

```bash
npx hexo generate
```

生成结果会放在 `public/` 目录里。

## 自动部署到 GitHub Pages

我没有直接把 `public/` 手动提交到仓库，而是使用 GitHub Actions 自动部署。

流程是：

```text
推送 main 分支
  -> GitHub Actions 安装依赖
  -> 运行 npx hexo generate
  -> 上传 public 作为 Pages artifact
  -> GitHub Pages 发布网站
```

工作流文件放在：

```text
.github/workflows/pages.yml
```

核心步骤包括：

```yml
- name: Install dependencies
  run: npm ci

- name: Build with Hexo
  run: npx hexo generate

- name: Upload artifact
  uses: actions/upload-pages-artifact@v3
  with:
    path: public
```

这样以后只要提交文章并推送到 GitHub，网站就会自动更新。

## 遇到的问题：Jekyll 找不到 Fluid 主题

刚开始部署时，GitHub Pages 的默认构建失败了，错误大概是：

```text
The fluid theme could not be found.
```

原因是 GitHub Pages 默认走 Jekyll，而我的项目是 Hexo。Jekyll 看到 `_config.yml` 里的：

```yml
theme: fluid
```

会以为我要使用一个 Ruby 主题 `fluid`。但 Fluid 是 Hexo 的 npm 主题，不是 Ruby Gem，所以 Jekyll 找不到它。

解决方式不是换成 Jekyll 能找到的主题，而是改用 GitHub Actions 构建 Hexo。因为我真正想用的是 Hexo + Fluid，而不是 Jekyll。

## 总结

这次博客搭建下来，我对 GitHub Pages 的理解更清楚了：它不是只能发布一个 `index.html`，也可以配合静态站点生成器来发布更完整的网站。

我的技术方案是：

- 用 Hexo 管理博客内容
- 用 Fluid 提供博客主题
- 用 Markdown 写文章
- 用 GitHub Actions 自动构建
- 用 GitHub Pages 托管最终网站

这个方案不需要自己买服务器，也不需要维护后端服务。对个人博客来说，它足够轻量，也足够清晰。
