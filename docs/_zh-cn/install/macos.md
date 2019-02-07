---
title:       "安装ioBroker"
lastChanged: "2019/02/02"
---

# 在MACOS上安装ioBroker

?> ***这是一个占位符***.
   <br><br>
   请您帮助ioBroker完善这篇文章。  
   请注意[ioBroker风格指南][]，
   这样可以更容易地合并您的提交。

## 检查安装需求

!> 首先，检查系统是否满足所有必要的[安装要求][]。

ioBroker运行在Node.js环境中。
如果您之前已安装好了ioBroker，请直接跳过此部分。

为了检测是否安装了Node.js，请打开Linux发行版对应的`终端`，并执行如下命令确认node.js和npm版本

~~~bash
node -v
npm -v
~~~

请首先检查版本号是否满足[安装要求][]中对Node.js和npm对版本需求。
如果不满足，请参考[Node.js安装指南][]完成Node.js和npm的安装。

## 安装ioBroker
请打开`终端`并执行如下自动安装脚本。

~~~bash
curl -sL https://raw.githubusercontent.com/ioBroker/ioBroker/stable-installer/installer.sh | bash -
~~~

自动脚本安装过程大致可以分为4步，用户可以清楚的在终端中看到每一步的执行情况

~~~bash
* Creating ioBroker directory (1/4)
* Downloading installation files (2/4)
* Installing ioBroker (3/4)
* Finalizing installation (4/4)
~~~

在最后，如果安装成功，将显示

~~~bash
ioBroker was installed successfully
Open http://localhost:8081 in a browser and start configuring!
~~~

ioBroker相关的程序和`适配器`将都以**当前登录的用户**运行。

?> ioBroker的进一步配置可以在`Admin`适配器的帮助下在浏览器中进行。
   打开浏览器，并且输入地址`http://localhost:8081`打开web配置界面。
   有关ioBroker的进一步配置，将在[ioBroker配置][]章节中详细介绍。

?> 对于初学者，推荐继续浏览该[基础教程][]。
   此教程将介绍ioBroker的基本概念，和如何配置ioBroker。

[ioBroker风格指南]: _zh-cn/community/styleguidedoc
[安装要求]: _zh-cn/install/requirements
[Node.js安装指南]: _zh-cn/install/nodejs
