---
title: 基于Github和Hexo搭建个人博客
date: 2024-06-28 20:02:50
tags: 

---

本文参考了[Byron4j](https://github.com/Byron4j/CookBook/blob/master/Git/1-Github_Hexo%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2.md )和[dongself](https://doingself.github.io/2017/06/16/2017-06-16-Hexo%E4%B8%BB%E9%A2%98-NexT-%E4%BD%BF%E7%94%A8%E6%80%BB%E7%BB%93/)的部分工作，希望给新手一个足够详细的路径搭建自己的个人博客，并在过程中介绍所用到的各种工具。

## 基本工具介绍

### Github

[GitHub](https://github.com/) 是一个基于 Web 的平台，主要用于版本控制和协作开发。它利用了 Git 版本控制系统，提供了一个直观的界面，使开发者能够更方便地管理和共享代码项目。再直观点来说，GitHub就是一个线上的平台，用户可以建立自己的仓库，每个仓库可以视为不同的项目，储存有各种代码等资料信息。在搭建博客的过程中，建立一个GitHub仓库目的在于提供一个博客站点，如[Hawaii's Blog](https://hwyii.github.io/hwyii/)，让我们的Blog可以被大家看到。

### Git

[Git](https://git-scm.com/) 是一个免费的开源分布式版本控制系统，最初由 Linus Torvalds 于 2005 年开发，旨在更好地管理 Linux 内核开发。Git 的主要功能是跟踪和记录文件的更改历史，使得多个开发者可以协同工作，并在需要时回溯到以前的版本。

### Node.js

Node.js 是一个开源的、跨平台的 JavaScript 运行时环境，允许开发者在服务器端运行 JavaScript 代码，它非常适合构建高性能、可扩展的 Web 服务器。Node.js 附带了 npm（Node Package Manager），这是世界上最大的开源库和软件包注册中心。

### Hexo

Hexo 是一个快速、简洁且功能强大的静态博客框架，它基于 Node.js 构建，主要用于创建和管理静态博客网站。Hexo 使用 **Markdown**语言撰写文章（默认本文读者会使用Markdown），通过命令生成静态文件，并支持一键部署到各种托管平台（如 GitHub Pages）。

## 环境准备

#### 创建Github仓库

创建账号后新建New repository即可，后面均假设新的仓库名为hwyii。扔一个自己的账号[hwyii](https://github.com/hwyii).

#### 安装Git

根据自己电脑版本从此处下载即可[Git](https://git-scm.com/).

#### 安装Node.js

Hexo基于Node.js，所有还需要安装Node.js。根据自己电脑版本从此处下载即可[Node.js](https://nodejs.cn/download/). 通过以下指令检查是否安装成功：

```bash
$ node -v
```

显示版本号说明安装成功。注意$表示命令行提示符，输入时删去。

#### 安装Hexo

Hexo的官网：[here](https://hexo.io/zh-cn/)，官方文档：[here](https://hexo.io/zh-cn/docs/)，官方文档中也对Git和Node.js的安装做了指导。所有必备的应用程序安装完成后，即可在**命令行界面**使用npm安装Hexo：

```bash
$ npm install -g hexo-cli
```

## 使用Hexo搭建个人博客

自选合适的目录新建文件夹，下面给出一个例子，在命令行界面使用。注意这里是绝对路径，且是空目录：

```bash
$ hexo init D:\Study\Blog
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

#### `_config.yml`

Hexo 的主配置文件，包含了网站的基本设置、URL 配置、目录结构、写作设置、生成设置、部署设置等。你可以通过修改此文件来配置 Hexo 网站的各种参数。关于它的详细配置信息在[这里](https://hexo.io/zh-cn/docs/configuration)。

#### `source`

`source` 目录是 Hexo 用来存放博客内容的地方。这个目录包含了你所有的 Markdown 文件和资源文件。默认情况下，有 `_posts` 子目录用于存放博客文章。

#### `scaffolds`

该目录包含了 Hexo 创建新内容时的模板文件。默认情况下，它包括 `post.md`、`page.md` 和 `draft.md`，可以根据需要进行定制。它的详细信息在[这里](https://hexo.io/zh-cn/docs/writing)。

### 浏览本地博客

经过如上的准备，我们已经可以初步浏览博客了。首先进入hexo的项目目录，然后使用如下命令开启博客服务：

```bash
$ cd /d D:\Study\Blog
$ D:\Study\Blog>hexo s
```

将会显示如下结果：

```bash
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```

在浏览器中访问[http://localhost:4000/](http://localhost:4000/)即可看到博客



需要注意的是，此时浏览的博客是本地的。这是因为hexo server启动了一个本地开发服务器（通常在 `localhost:4000`），用于在你的计算机上预览博客。这个服务器仅在你的计算机上运行，不对外公开。本地服务器使你能够快速查看更改后的效果，而不需要每次修改后都将网站部署到远程服务器。

### 使用Hexo写文章

在项目目录下使用命令

```bash
$ hexo new [layout] <title>
```

可以在命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局。

举一个例子：

```bash
$ D:\Study\Blog>hexo new post 基于Github和Hexo搭建个人博客
INFO  Validating config
INFO  Created: D:\Study\Blog\source\_posts\基于Github和Hexo搭建个人博客.md
```

### 部署到远程服务器Github

如何将本地博客部署到远程服务器？Hexo 提供了快速方便的一键部署功能。但是首先我们需要修改本地配置文件`_config.yml`中的一些信息：

#### 修改url

将url设置为`https://username.github.io/project`，`username`是 GitHub 用户名，是您的 GitHub 账号的唯一标识符。project是 GitHub 仓库（repository）的名称，是你在 GitHub 上创建的一个项目或仓库的名称。每个仓库都有一个唯一的名称，用于区分不同的项目。下面是我们的例子：

```yaml
url: https://hwyii.github.io/hwyii
```

#### 修改deploy

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
$ npm install hexo-deployer-git --save
```

- 生成静态文件

```bash
$ hexo generate
```

- 部署到GitHub Pages

```bash
$ hexo deploy
```

#### 第一次推送到远程服务器

```bash
$ git init
$ git remote add origin https://github.com/hwyii/hwyii.git
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```

#### 非首次推送

```bash
$ hexo generate
$ hexo deploy
$ git add .
$ git commit -m "Update files"
$ git push origin master
```

以上是关于Hexo的一些最基本的操作，更多指令可以见上文中提到的Hexo官方文档，本文也将持续更新一些细节。



## 更改主题

默认的landscape不太美观，您可以在Hexo的各类主题里选择自己喜欢的[theme](https://hexo.io/themes/)，这里以[next](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/README.md)为例对常见使用方式进行介绍。next是比较常使用的一种主题，界面简约，且在使用过程中遇到的问题基本可以在网上搜到解决方式。

### 安装NexT

- 下载主题

进入Hexo的目录，使用git克隆NexT到本地

```bash
$ git clone https://github.com/theme-next/hexo-theme-next themes/next
```

此时你的Hexo项目目录结构应该类似于：

```bash
hexo/
├── _config.yml
├── node_modules/
├── package.json
├── public/
├── scaffolds/
├── source/
└── themes/
    └── next/   # 这里是克隆下来的 Next 主题
```

- 修改配置

将站点根目录下`_config.yml`文件中的`theme: next`。注意与主题next中的配置文件`_config.yml`区分。

由于Hexo在5.0之后把swig删了，需要手动安装：

```bash
$ npm i hexo-renderer -swig
```

否则页面无法显示。

### 主题设定

1. Scheme

修改theme目录下 `_config.yml` 文件中的 `scheme: Mist`
Scheme 是 NexT 提供的一种特性，借助于 Scheme，NexT 为你提供多种不同的外观。

- Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
- Mist - Muse 的紧凑版本，整洁有序的单栏外观
- Pisces - 双栏 Scheme，小家碧玉似的清新
- Gemini - 新出来的，个人感觉跟Pisces差不多，双栏。

2. 头像

修改theme目录下 `_config.yml` 文件中的 `avatar` 设置成头像的地址

- 放置在 `source/images/` 目录下 配置为：`avatar: /images/avatar.png`

3. 菜单

```yaml
menu:
  home: /|| home
  about: /about/|| user
  archives: /archives/|| archive
```

- 需要删去模板中`/`和`||`之间的空格，否则无法渲染成功。
- 对于对应的分页，需要新建页面，这里以`about`为例

```bash
$ hexo new page about
```

输入命令后，在`/source`下会生成一个新的文件夹`about`，在该文件夹下会有一个`index.md`文件，在里面写入关于自己的介绍即可。

### 第三方服务

第三方插件要在站点根目录下执行

1. 站内搜索

首先安装`hexo-generator-searchdb`插件

```bash
$ npm install hexo-generator-searchdb --save
```

在根目录`_config.yml`的任意位置新增以下内容

```yaml
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

最后在theme下的`_config.yml`启用站内搜索功能，即将`local_search`下的`enable:`值设为`true`.

2. 字数和时长统计

在theme下的`_config.yml`启用对应功能，即将`post_wordcount`下的值设为`true`.

3. 浏览量统计

在`theme`下的`_config.yml`进行如下设置

```yaml
busuanzi_count:
  # Enable busuanzi counter only if other configurations are false
  enable: true
  # Custom unique visitor span for the whole site
  site_uv: true
  site_uv_header: Visitors
  site_uv_footer: people
  # Custom page view span for the whole site
  site_pv: true
  site_pv_header: Total Views
  site_pv_footer: times
  # Custom page view span for one page only
  page_pv: true
  page_pv_header: Reads
  page_pv_footer:
```

此外，由于不蒜子的域名更改，我们需要更改源码：

进入 hexo 博客项目的 `themes` 目录下，在 next 主题目录中的 `layout/_third-party/analytics/` 下找到 `busuanzi-counter.swig` 文件，将

```html
<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

更改为

```html
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```



## FAQ：

### 如何解决网络代理问题？

因为种种原因（比如科学上网）出现报错

```bash
fatal: unable to access 'https://github.com/hwyii/hwyii.git/': Could not resolve proxy: 127.0.0.1.7890 FATAL Something's wrong.
```

主要进行了如下尝试，有关系统的部分以Win10为例。

#### 检查代理设置

查看 Git 配置中是否有设置代理 (`git config --global --get http.proxy` 和 `git config --global --get https.proxy`)。如果配置了代理但不需要使用，可以通过以下命令取消代理设置：

```bash
$ git config --global --unset http.proxy
$ git config --global --unset https.proxy
```

#### 使用SSH代替HTTPS

如果更改代理设置没用，可以考虑使用SSH。

HTTPS 和 SSH 是两种不同的协议，常用于访问 Git 仓库。HTTPS使用用户名和密码进行认证，或者使用个人访问令牌（Personal Access Tokens, PATs）来代替密码，每次访问仓库时都需要进行认证，除非使用凭证管理器来缓存认证信息。SSH使用 SSH 密钥对进行认证，用户生成一个密钥对（公钥和私钥），并将公钥添加到 Git 服务（如 GitHub、GitLab 等）的账户中，一旦设置好 SSH 密钥，后续访问无需再输入用户名和密码。

在 Windows 上生成和配置 SSH 密钥的详细步骤：

**安装 OpenSSH 客户端**

在 Windows 10 及更新版本中，OpenSSH 客户端已经包含在系统中，但默认可能没有启用。你可以按照以下步骤启用它：

1. 启用 OpenSSH 客户端：

   - 打开 **设置** -> 进入 **系统** -> 点击 **可选功能** -> 点击 **添加功能** -> 找到并安装 **OpenSSH 客户端**。

2. 验证安装： 打开命令提示符输入以下命令来验证是否安装成功：

   ```bash
   $ ssh
   ```

   如果显示 SSH 的帮助信息，则说明安装成功。

**生成 SSH 密钥**

1. 打开命令提示符，运行以下命令生成 SSH 密钥：

   ```bash
   $ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```

   按照提示操作，通常可以按 Enter 使用默认路径（例如 `C:\Users\YourUsername\.ssh\id_rsa`）。

   *Remark：这里的电子邮件地址是用于给生成的 SSH 密钥添加一个标签（comment）的参数，用于标识这个密钥。这在您管理多个 SSH 密钥时特别有用，因为可以通过这个标签轻松识别每个密钥的用途或所有者。*

2. 查看生成的公钥：

   ```bash
   $ type C:\Users\YourUsername\.ssh\id_rsa.pub
   ```

   复制输出的公钥内容。

**添加 SSH 密钥到 GitHub**

登录 GitHub -> 进入 **Settings** -> 点击 **SSH and GPG keys** -> 点击 **New SSH key** -> 将复制的公钥粘贴到键值框中，填写一个标识（例如 “My Laptop”），然后保存。

**测试 SSH 连接**

```bash
$ ssh -T git@github.com
```

你应该会看到类似以下的信息：

```bash
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

**更新远程仓库 URL并推送代码**

确保你的 Git 仓库使用的是 SSH URL：

```bash
$ git remote set-url origin git@github.com:your_username/your_repository.git
$ git push origin master
```

即可解决。





### 典型开发流程

1. **创建和编辑内容**：
   - 使用 Hexo 命令创建新文章或页面，并在 `source/_posts` 或其他目录中编辑 Markdown 文件。
2. **启动本地服务器**：
   - 使用 `hexo server` 启动本地服务器，浏览器会自动打开并显示当前博客内容。
3. **查看和调整**：
   - 在浏览器中查看博客效果，根据需要进行调整和修改。每次保存修改后，Hexo 会自动重新生成静态文件并刷新浏览器页面。
4. **部署到远程服务器**：
   - 当你对本地预览效果满意后，可以使用 `hexo deploy` 命令将博客部署到远程服务器（例如 GitHub Pages、Netlify 等），使其对外公开访问。
