---
title: 基于Github和Hexo搭建个人博客
date: 2024-06-28 20:02:50
tags: 
---

本文参考了[Byron4j](https://github.com/Byron4j/CookBook/blob/master/Git/1-Github_Hexo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2.md )的部分工作，希望给新手一个足够详细的路径搭建自己的个人博客，并在过程中介绍所用到的各种工具。

## 基本工具介绍

### Github

[GitHub](https://github.com/) 是一个基于 Web 的平台，主要用于版本控制和协作开发。它利用了 Git 版本控制系统，提供了一个直观的界面，使开发者能够更方便地管理和共享代码项目。再直观点来说，GitHub就是一个线上的平台，用户可以建立自己的仓库，每个仓库可以视为不同的项目，储存有各种代码等资料信息。在搭建博客的过程中，建立一个GitHub仓库目的在于提供一个博客站点，如[Hawaii's Blog](https://hwyii.github.io/hwyii/)，让我们的Blog可以被大家看到。

### Git

[Git](https://git-scm.com/) 是一个免费的开源分布式版本控制系统，最初由 Linus Torvalds 于 2005 年开发，旨在更好地管理 Linux 内核开发。Git 的主要功能是跟踪和记录文件的更改历史，使得多个开发者可以协同工作，并在需要时回溯到以前的版本。

### Node.js

Node.js 是一个开源的、跨平台的 JavaScript 运行时环境，允许开发者在服务器端运行 JavaScript 代码，它非常适合构建高性能、可扩展的 Web 服务器。Node.js 附带了 npm（Node Package Manager），这是世界上最大的开源库和软件包注册中心。

### Hexo

Hexo 是一个快速、简洁且功能强大的静态博客框架，它基于 Node.js 构建，主要用于创建和管理静态博客网站。Hexo 使用 Markdown 语言撰写文章，通过命令生成静态文件，并支持一键部署到各种托管平台（如 GitHub Pages）。

## 环境准备

#### 创建Github仓库

创建账号后新建New repository即可，后面均假设新的仓库名为hwyii。扔一个自己的账号[hwyii](https://github.com/hwyii).

#### 安装Git

根据自己电脑版本从此处下载即可[Git](https://git-scm.com/).

#### 安装Node.js

Hexo基于Node.js，所有还需要安装Node.js。根据自己电脑版本从此处下载即可[Node.js](https://nodejs.cn/download/). 通过以下指令检查是否安装成功：

```bash
node -v
```

显示版本号说明安装成功。

#### 安装Hexo

Hexo的官网：https://hexo.io/zh-cn/，以及官方文档：https://hexo.io/zh-cn/docs/，官方文档中也对Git和Node.js的安装做了指导。所有必备的应用程序安装完成后，即可在**命令行界面**使用npm安装Hexo：

```bash
npm install -g hexo-cli
```

## 使用Hexo搭建个人博客

自选合适的目录新建文件夹，下面给出一个例子，在命令行界面使用。注意这里是绝对路径，且是空目录：

```bash
hexo init D:\Study\Blog
```

将会看到：

```bash
INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
INFO  Install dependencies
INFO  Start blogging with Hexo!
```

新建完成后将会生成如下目录文件：

```bash
.gitignore
node_modules
package-lock.json
package.json
scaffolds
source
themes
_config.yml
```

### 目录文件简单说明

#### _config.yml

Hexo 的主配置文件，包含了网站的基本设置、URL 配置、目录结构、写作设置、生成设置、部署设置等。你可以通过修改此文件来配置 Hexo 网站的各种参数。关于它的详细配置信息在https://hexo.io/zh-cn/docs/configuration。

#### source

`source` 目录是 Hexo 用来存放博客内容的地方。这个目录包含了你所有的 Markdown 文件和资源文件。默认情况下，有 `_posts` 子目录用于存放博客文章。

#### scaffolds

该目录包含了 Hexo 创建新内容时的模板文件。默认情况下，它包括 `post.md`、`page.md` 和 `draft.md`，可以根据需要进行定制。它的详细信息在https://hexo.io/zh-cn/docs/writing。

### 浏览本地博客

经过如上的准备，我们已经可以初步浏览博客了。首先进入hexo的项目目录，然后使用如下命令开启博客服务：

```bash
cd /d D:\Study\Blog
D:\Study\Blog>hexo s
```

将会显示如下结果：

```bash
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```

在浏览器中访问http://localhost:4000/即可看到博客

![image-20240628211724308](C:\Users\DELL\AppData\Roaming\Typora\typora-user-images\image-20240628211724308.png)

需要注意的是，此时浏览的博客是本地的。这是因为hexo server启动了一个本地开发服务器（通常在 `localhost:4000`），用于在你的计算机上预览博客。这个服务器仅在你的计算机上运行，不对外公开。本地服务器使你能够快速查看更改后的效果，而不需要每次修改后都将网站部署到远程服务器。

#### 使用Hexo写文章

在项目目录下使用命令

```bash
hexo new [layout] <title>
```

可以在命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局。

举一个例子：

```bash
D:\Study\Blog>hexo new post 基于Github和Hexo搭建个人博客
INFO  Validating config
INFO  Created: D:\Study\Blog\source\_posts\基于Github和Hexo搭建个人博客.md
```

#### 部署到远程服务器Github

如何将本地博客部署到远程服务器？Hexo 提供了快速方便的一键部署功能。但是首先我们需要修改本地配置文件_config.yml中的一些信息：

##### 1. 修改url

将url设置为'https://username.github.io/project'，username是 GitHub 用户名，是您的 GitHub 账号的唯一标识符。project是 GitHub 仓库（repository）的名称，是你在 GitHub 上创建的一个项目或仓库的名称。每个仓库都有一个唯一的名称，用于区分不同的项目。下面是我们的例子：

```yaml
url: https://hwyii.github.io/hwyii
```

##### 2. 修改deploy

```yaml
deploy:
  type: git
  repo: https://github.com/hwyii/hwyii.git
  branch: gh-pages
```

这段配置表明您希望使用 Git 将生成的静态网页部署到 GitHub Pages 上，使其可以通过 `https://username.github.io/project` 这样的 URL 访问到。

- `type: git`：指定部署类型为 Git，这表明 Hexo 会使用 Git 来管理和发布静态网站文件。
- `repo: https://github.com/hwyii/hwyii.git`：这是您的 GitHub 仓库地址。具体来说，
  - `https://github.com` 是 GitHub 的域名。
  - `hwyii` 是您的 GitHub 用户名或组织名。
  - `hwyii.git` 是您的仓库名称，`.git` 后缀表明这是一个 Git 仓库地址。
  - 这个地址指向您的 GitHub 仓库，Hexo 将会把生成的静态网站文件推送到这个仓库中。
- `branch: gh-pages`：这指定了部署到 GitHub Pages 的分支。在大多数情况下，GitHub Pages 使用 `gh-pages` 分支来托管静态网页内容。



然后我们进行如下操作：

- 安装插件

```bash
npm install hexo-deployer-git --save
```

- 生成静态文件

```bash
hexo generate
```

- 部署到GitHub Pages

```bash
hexo deploy
```





以上是关于Hexo的一些最基本的操作，更多指令可以见上文中提到的Hexo官方文档，本文也将持续更新一些细节。



### 典型开发流程

1. **创建和编辑内容**：
   - 使用 Hexo 命令创建新文章或页面，并在 `source/_posts` 或其他目录中编辑 Markdown 文件。
2. **启动本地服务器**：
   - 使用 `hexo server` 启动本地服务器，浏览器会自动打开并显示当前博客内容。
3. **查看和调整**：
   - 在浏览器中查看博客效果，根据需要进行调整和修改。每次保存修改后，Hexo 会自动重新生成静态文件并刷新浏览器页面。
4. **部署到远程服务器**：
   - 当你对本地预览效果满意后，可以使用 `hexo deploy` 命令将博客部署到远程服务器（例如 GitHub Pages、Netlify 等），使其对外公开访问。
