---
title:       "基本概念"
lastChanged: "2019/02/02"
---

# 系统设计 {docsify-ignore-all}

?> ***这是一个占位符***.
   <br><br>
   请您帮助ioBroker完善这篇文章。  
   请注意[ioBroker风格指南][]，
   这样可以更容易地合并您的提交。

## 架构

ioBroker系统是模块化的，即由许多单独的组件组成。每个模块都有一个特定的任务。
ioBroker为称每一个模块为`适配器`的`实例`。模块仅在需要时由用户安装。
为了跟踪，ioBroker为其所有模块提供了一个中央协调器，该协调器运行在后台程序`js-controller`中。
他负责数据管理以及所有模块之间的管理和通信。
基于Web的管理界面`admin`本身也是一个适配器。
管理员通常通过地址[http://localhost:8081][]访问该web管理页面。

通过`admin`web管理页面安装新`适配器`时，
首先从Internet下载`适配器`文件并将其写入服务器磁盘。
如果要启动`适配器`，则首先生成一个适配器的`实例`。
`实例`是`适配器`的可执行副本，可以单独配置，运行和停止适配器的实例。
`实例`由admin独立启动。
每个实例都独立运行在自己的进程中，该进程在后台与ioBroker`js-controller`进行通信。

多个ioBroker服务器可以共同组成一个`多主机系统`。
在多主机系统中，适配器实例可以分布在不同的服务器上。
因此，可以分配负载，也可以让直接连接在不同的服务器上的硬件（例如IO端口，USB）互联互通。

适配器，js-controller，数据库和Web前端之间的通信通过多个TCP/IP连接进行。
可以配置数据是否加密传输。

ioBroker和适配器主要用JavaScript语言编写。要运行JavaSript，您需要一个相应的运行时环境。
因此ioBroker需要运行在`Node.js`解释器上。
`Node.js`可以运行在各种软件平台，例如Linux，Windows和macOS。
因此ioBroker也可以运行在各种平台上。
`npm`是`Node.js`的包管理器，ioBroker和适配器也通过此包管理器发布和安装。

@@@需要一张示意架构的图片@@@  
@@@说明JS-Controller，适配器和实例之间的关系@@@

[ioBroker风格指南]: _zh-cn/community/styleguidedoc
[http://localhost:8081]: http://localhost:8081
