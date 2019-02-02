---
title:       "安装ioBroker"
lastChanged: "2019/02/01"
---

# 在Windows上安装ioBroker

?> ***这是一个占位符***.
   <br><br>
   请您帮助ioBroker完善这篇文章。  
   请注意[ioBroker风格指南][]，
   这样可以更容易地合并您的提交。

本文档将指导您逐步完成在Windows系统安装ioBroker。
如果您还不甚了解每一步的目的，请不要跳过步骤，因为每一步之间可能会相互依赖。

## 检查安装需求

!> 首先，检查系统是否满足所有必要的[安装要求][]。

ioBroker运行在Node.js环境中。
如果您之前已安装好了ioBroker，请直接跳转到[更新]()部分。

为了检测是否安装了Node.js，使用组合键<kbd>&#x229e; Windows</kbd> + <kbd>r</kbd>
打开`运行`对话框，然后在对话框内输入下面的的命令

~~~cmd
cmd.exe /C node -v & pause
~~~

点击回车后，会出现一个窗口

![Node.js-Version](media/w02nodecheck.png)  
*Node.js测试*

弹出窗口将显示错误消息或已安装Node.js的版本号。

如果显示Node.js的版本号，请首先检查它是否满足[安装要求][]中对Node.js的版本需求。

如果出现错误消息
`Der Befehl "node" ist entweder falsch geschrieben oder konnte nicht gefunden werden.`，
则表示未安装node.js，可以立即[开始安装]。

## 快速安装

?> 此安装步骤适用于安装过多次ioBroker，有经验的ioBroker用户。

初学者应遵循[详细安装](#详细安装)的步骤。

* [下载并安装][]Node.js 8.x LTS版本。
* 以管理员身份打开`cmd.exe`并按顺序执行如下命令：

  ~~~cmd
  npm install --global windows-build-tools
  md C:\iobroker
  cd /d C:\iobroker
  npm install iobroker
  npm install --production
  iobroker status  
  ~~~

## 详细安装

### 安装Node.js和npm

请按照[此教程][]完成Node.js和npm的安装。

### 安装ioBroker

?> ioBroker可以安装在本地硬盘上的任何有权限的路径下。
   如果安装路径包含空格，则必须在完整路径前后加引号。
   示例命令：`dir "C:\ioBroker Testsystem"`。

?> ioBroker的默认安装路径是`C:\iobroker`。

1. 请使用<kbd>&#x229e; Windows</kbd> + <kbd>r</kbd>组合键以`管理员`身份打开运行对话框。
   然后运行下面的命令：

   ~~~cmd
   cmd
   ~~~

 !> 输入命令后弹出的对话框标题必须以`管理员`开头。

 ?> 某些ioBroker适配器包含需要在Windows系统中实时编译的组件。
    因此，在安装ioBroker之前，需要安装`windows-build-tools`。
    关于`windows-build-tools`的更多信息可在[这里][]找到。

1. 使用以下命令安装`windows-build-tools`：

   ~~~cmd
   npm install --global windows-build-tools
   ~~~

1. 在命令行窗口中执行如下命令创建安装ioBroker的文件夹：

   ~~~cmd
   md C:\iobroker
   ~~~

1. 现在可以开始安装`ioBroker安装包`：

   ~~~cmd
   cd /d C:\iobroker
   npm install iobroker
   ~~~

   结果应如下所示：

   ~~~cmd
   ╭───────────────────────────────────────────────────────╮
   │ The iobroker files have been downloaded successfully. │
   │ To complete the installation, you need to run         │
   │                                                       │
   │                  npm i --production                   │
   │                                                       │
   ╰───────────────────────────────────────────────────────╯

   npm notice created a lockfile as package-lock.json. You should commit this file.
   npm WARN enoent ENOENT: no such file or directory, open 'C:\iobroker\package.json'
   npm WARN iobroker No description
   npm WARN iobroker No repository field.
   npm WARN iobroker No README data
   npm WARN iobroker No license field.

   + iobroker@1.3.0
   added 51 packages from 28 contributors and audited 83 packages in 6.937s
   found 0 vulnerabilities
   ~~~

1. 最后可以开始安装`ioBroker`：

   ~~~cmd
   cd /d C:\iobroker
   npm install --production
   ~~~

   安装过程可能需要一段时间。
   npm执行时，可能会出现与`unix-dgram`模块相关的红色字符的错误消息`(gyp！ERR)`。
   可以忽略这些错误消息。

   正确安装完成的最后几行应该以如下的信息结尾：

   ~~~cmd
   Write "iobroker start" to start the ioBroker
   npm install node-windows@0.1.14 --production --save --prefix "C:/iobroker"
   ioBroker service installed. Write "serviceIoBroker start" to start the service and go to http://localhost:8081 to open the admin UI.
   To see the outputs do not start the service, but write "node node_modules/iobroker.js-controller/controller"
   npm WARN optional SKIPPING OPTIONAL DEPENDENCY: unix-dgram@0.2.3 (node_modules\unix-dgram):
   npm WARN optional SKIPPING OPTIONAL DEPENDENCY: unix-dgram@0.2.3 install: `node-gyp rebuild`
   npm WARN optional SKIPPING OPTIONAL DEPENDENCY: Exit status 1

   added 514 packages from 300 contributors and audited 1808 packages in 61.874s
   found 23 vulnerabilities (17 low, 6 high)
   run `npm audit fix` to fix them, or `npm audit` for details
   ~~~

1. 随后，用如下命令检查ioBroker是否已经安装完成并自动启动

   ~~~cmd
   iobroker status
   ~~~

   正确的情况应该显示：

   ~~~cmd
   iobroker is running
   ~~~

   如果显示如下内容，说明ioBroker已经安装完成，但是*没有*自动启动：

   ~~~cmd
   iobroker is not running
   ~~~

   如果遇到上述情况，则使用如下命令令ioBroker自动启动：

   ~~~cmd
   net start iobroker.exe
   ~~~

   再次检查ioBroker的运行状态：

   ~~~cmd
   iobroker status
   ~~~

   此时应该显示如下内容：

   ~~~cmd
   iobroker is running
   ~~~

 ?> 之后，每次重启系统时，ioBroker都会在后台自动启动。

1. 最后，可以通过以下命令退出命令行窗口：

   ~~~cmd
   exit
   ~~~

?> ioBroker的进一步配置可以在`Admin`适配器的帮助下在浏览器中进行。
   打开浏览器，并且输入地址`http://localhost:8081`打开web配置界面。
   有关ioBroker的进一步配置，将在[ioBroker配置][]章节中详细介绍。

?> 对于初学者，推荐继续浏览该[基础教程][]。
   此教程将介绍ioBroker的基本概念，和如何配置ioBroker。

## 更新

@@@ tbd @@@

## 疑难解答

@@@ tbd @@@

[ioBroker风格指南]: _zh-cn/community/styleguidedoc
[安装要求]: _zh-cn/install/requirements
[下载并安装]: _zh-cn/install/nodejs
[此教程]: _zh-cn/install/nodejs
[这里]: https://github.com/felixrieseberg/windows-build-tools
