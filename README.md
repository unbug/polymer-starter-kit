![](https://cloud.githubusercontent.com/assets/110953/7877439/6a69d03e-0590-11e5-9fac-c614246606de.png) 
## Polymer Starter Kit

> 一个基于 Polymer 1.0 构建 web 应用的出发点

### 里面直接包含以下内容:

* [Polymer](http://polymer-project.org), Paper 和 Iron elements
* [Material Design](http://www.google.com/design/spec/material-design/introduction.html) 布局 
* 使用 [Page.js](https://visionmedia.github.io/page.js/) 进行路由
* 使用 Web Component Tester 进行单元测试
* 基本 Service Worker elements 实现离线
* 端对端的构建工具 (包括 [Vulcanize](https://github.com/Polymer/vulcanize))

## 准备开始

要想充分享受 Polymer Starter Kit 的优势你需要:

1. 拷贝一份源码.
2. 安装你没有依赖.
3. 按你的喜好修改应用.
4. 发布到生产环境.

## 获取源码

[下载](https://github.com/polymerelements/polymer-starter-kit/releases/latest) 并解压 Polymer Starter Kit 到你的工作目录.

### 安装依赖

确保 [Node.js](http://nodejs.org) 和 npm 已经安装, 运行:

```sh
$ npm run deps
```

这将会安装 element 集合 (Paper, Iron, Platinum) 和我们用来构建及服务应用的工具.

### 运行服务 / 监听代码

```sh
$ gulp serve
```

会打印出一个你用来本地预览和一个远程预览的 IP 地址。

### 运行测试

```sh
$ gulp test:local
```

会通过 [web-component-tester](https://github.com/Polymer/web-component-tester)运行在 `app/test` 目录里定义的测试.

### 构建 & Vulcanize

```sh
$ gulp
```

构建并优化项目并准备好部署. 过程包括处理并合并, 图片, 脚本, 样式 和 HTML 的优化及压缩.

## 给应用上主题

Polymer 1.0 引入了自定义 CSS 样式的 shim.我们借了 `app/elements/app-theme.html` 的优势给你的应用上主题。 你当然也可以在此文件里找到我们预设的 Material Design 插入点.

## 单元测试

基于 Polymer Starter Kit 的 web app 支持配置 [Web Component Tester](https://github.com/Polymer/web-component-tester) - Polymer 首先的测试工具. 这会使你轻松测试你的应用.

## 管理依赖

Polymer 通过 [Bower](http://bower.io) 进行包管理. 意味着你的 element 能保持更新并版本分明。 NPM 则用于管理 Node 的依赖.

## Service Worker

Polymer Starter Kit 提供了一个离线优先的体验，得益于 Service Worker 和 the [Platinum Service Worker elements](https://github.com/PolymerElements/platinum-sw). 不了解 Service Worker? 阅读这篇[介绍](http://www.html5rocks.com/en/tutorials/service-worker/introduction/) 了解它的原理.

我们默认的离线设置对付简单的应用应该是没问题的. 对于复杂的应用,我们推荐你学习 Service Worker 的原理，如此你将可以对 Platinum Service Worker element 进行抽象. 

#### 将 bug 提到对的地方

如果你遇到 Service Worker 的问题, 检查下边的 issue 列表:

* [sw-toolbox](https://github.com/GoogleChrome/sw-toolbox/issues)
* [platinum-sw](https://github.com/PolymerElements/platinum-sw/issues)
* [platinum-push-notifications-manager](https://github.com/PolymerElements/push-notification-manager/)
* 以上没有提到的 issue 可以提交到 [这里](https://github.com/polymerelements/polymer-starter-kit/issues).

#### 我遇到一个错误信息 "Only secure origins are allowed"

Service Workers 只能在"信任源" 下工作. (HTTPS 网站, 基本上是) 安全度比较高的信任源下. 不过 http://localhost 默认是个信任源, 因此如果可以, 部署到 localhost 是避免此问题最简单的方式. 生产环境下你的网站必须支持 HTTPS. 

#### 我如何调试 Service Worker?

如果你要调试事件监听可以使用 `chrome://serviceworker-internals`.

#### chrome://serviceworker-internals 上的按钮都什么用?

本页面显示已经注册的 workers 并且提供一些基本的操作.

* Unregister: 注销 worker.
* Start: 启动 worker. 在你打开worker 的作用下的网站会自动启动的。
* Stop: 停止 the worker.
* Sync: 分发 'sync' 事件给 worker. 如果你没有监听此事件啥也不会发生.
* Push: 分发一个 'push' 事件给 worker. 如果你没有监听此事件啥也不会发生.
* Inspect: 在 Inspector 里打开 worker.

#### 开发流程 

为了确保你使用的 Service Worker 是最新的, 按以下的指南:

* 你修改你的 service worker 脚本后, 关闭其他标签保留一个你应用的标签。
* 按住shift强刷你的页面确保没有其他标签在使用你的 service worker
* 刷新直到让新版的 Service Worker 控制你的页面.

如果你发现还没有全部更新, 直接到 `chrome:serviceworker-internals` (用 Chrome), 找到相应的 Service Worker 并点击 'Unregister' 然后再刷新你的页面. 这只会 (显然的) 只能从本地环境清除它。如果你已经部署到生产环境, 那你要做更多的工作才能从用户的机子上清除了。

#### 还没准备好使用 Service Worker?

如果你有理由不使用 Service Worker, 你可以从以下三步在你的 Polymer Starter Kit 项目中禁用它:

* 在 gulp 的 'default' 任务里删除 'precache' ([gulpfile.js](https://github.com/PolymerElements/polymer-starter-kit/blob/master/gulpfile.js)) 
* 删除那两个 Platinum Service Worker elements (platinum-sw/..) in [app/elements/elements.html](https://github.com/PolymerElements/polymer-starter-kit/blob/master/app/elements/elements.html)
* 在你的应用里删除对 platinum-sw elements 的[引用](https://github.com/PolymerElements/polymer-starter-kit/blob/master/app/index.html). 

你还需要到 `chrome://serviceworker-internals` 里注销掉所有 Polymer Starter Kit 为你的应用注册的 Service Workers 确保缓存的影响. 

## 贡献

Polymer Starter Kit 是一个全新的项目，并且是一个被 Web Component 社区不断改进的项目. 我们期待你的 bug 反馈, 与改进, 文档和任何一切你觉得会帮助到其他 Polymer 开发者的改进相关的 pull request.
