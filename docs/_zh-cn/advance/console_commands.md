---
title:       "贡献代码"
lastChanged: "2019/02/04"
---

# 命令行指令 {docsify-ignore-all}

?> ***这是一个占位符***.
   <br><br>
   请您帮助ioBroker完善这篇文章。  
   请注意[ioBroker风格指南][]，
   这样可以更容易地合并您的提交。

ioBroker命令行指令可以执行启动，停止或更新等操作。
下面是对这些命令的详细描述。

?> 注意:  
  所有以`iobroker`开头的命令，都可以在任何目录中调用。
  而`npm install`命令必须从ioBroker根目录调用。

下面是所有可以执行的命令：

- [命令行指令 {docsify-ignore-all}](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%8C%87%E4%BB%A4-docsify-ignore-all)
  - [npm install iobroker.adapterName](#npm-install-iobrokeradaptername)
  - [iobroker start](#iobroker-start)
  - [iobroker stop](#iobroker-stop)
  - [iobroker restart](#iobroker-restart)
  - [iobroker isrun](#iobroker-isrun)
  - [iobroker start adapterName.instance](#iobroker-start-adapternameinstance)
  - [iobroker stop adapterName.instance](#iobroker-stop-adapternameinstance)
  - [iobroker restart adapterName.instance](#iobroker-restart-adapternameinstance)
  - [iobroker add adapterName](#iobroker-add-adaptername)
  - [iobroker install adapterName](#iobroker-install-adaptername)
  - [iobroker upload adapterName](#iobroker-upload-adaptername)
  - [iobroker setup](#iobroker-setup)
  - [iobroker setup custom](#iobroker-setup-custom)
  - [iobroker del adapterName](#iobroker-del-adaptername)
  - [iobroker del adapterName.instance](#iobroker-del-adapternameinstance)
  - [iobroker update](#iobroker-update)
  - [iobroker upgrade](#iobroker-upgrade)
  - [iobroker upgrade self](#iobroker-upgrade-self)
  - [iobroker upgrade adapterName](#iobroker-upgrade-adaptername)
  - [iobroker object get](#iobroker-object-get)
  - [iobroker object chmod](#iobroker-object-chmod)
  - [iobroker object chown](#iobroker-object-chown)
  - [iobroker object list](#iobroker-object-list)
  - [iobroker set](#iobroker-set)
  - [iobroker state get](#iobroker-state-get)
  - [iobroker state getplain](#iobroker-state-getplain)
  - [iobroker state getvalue](#iobroker-state-getvalue)
  - [iobroker state set](#iobroker-state-set)
  - [iobroker state del](#iobroker-state-del)
  - [iobroker message](#iobroker-message)
  - [iobroker clean](#iobroker-clean)
  - [iobroker backup](#iobroker-backup)
  - [iobroker restore](#iobroker-restore)
  - [iobroker host](#iobroker-host)
  - [iobroker host set](#iobroker-host-set)
  - [iobroker host remove](#iobroker-host-remove)
  - [iobroker list](#iobroker-list)
  - [iobroker adduser](#iobroker-adduser)
  - [iobroker deluser](#iobroker-deluser)
  - [iobroker passwd](#iobroker-passwd)
  - [iobroker chmod](#iobroker-chmod)
  - [iobroker chown](#iobroker-chown)
  - [iobroker file read](#iobroker-file-read)
  - [iobroker file write](#iobroker-file-write)
  - [iobroker version](#iobroker-version)
  - [iobroker uuid](#iobroker-uuid)
  - [iobroker status](#iobroker-status)
  - [iobroker repo](#iobroker-repo)
  - [iobroker info](#iobroker-info)

?> 注意:  
   超时参数`--timeout 5000`，可用于上述所有指令。
   它设定连接到数据库的超时时间（以毫秒为单位）。

## npm install iobroker.adapterName

此命令必须从ioBroker的根目录（通常是`/opt/iobroker`或`C:\Program Files\ioBroker`）调用。
此命令使用npm管理器来安装或更新给定的`适配器`或`js-controller`。
此命令不依赖于ioBroker的任何代码，即使`admin`或`js-controller`存在问题也可以执行。

用法示例：

- `npm install iobroker.admin`
  - 更新或安装`admin`适配器
- `npm install iobroker.js-controller`
  - 更新或安装`js-controller`
- `npm install https://github.com/husky-koglhof/ioBroker.hmm/tarball/master/`
  - 直接从github或其他地方安装适配器。
    地址文件**必须**是ZIP或GZ压缩包，并且压缩包内必须包含`package.json`文件。

在调用`npm install ..`安装了适配器之后，
应该重新启动指定的适配器或整个js-controller，以激活新的适配器。  
重启这可以通过`iobroker restart adapterName`或者`iobroker restart`来完成。
有关详细信息，请参见[此处](#iobroker-restart)。

?> 注意:  
   只能安装名称以`ioBroker`为前缀的软件包，比如**ioBroker.zzz**。

## iobroker start

以守护进程方式启动iobroker。如果ioBroker已经启动，您将收到警告：

```bash
ioBroker controller daemon already running. PID: xx
```

?> Windows注意事项：  
   通常Windows系统中的ioBroker作为服务启动。
   而此命令希望启动第二个ioBroker实例，这将导致与自动启动的ioBroker服务冲突。  
   所以在Windows系统中，需要在ioBroker目录中使用`serviceIoBroker.bat start`命令，
   而不是`iobroker start`命令。
   在执行命令前，您应该首先拥有管理员权限来启动服务。

## iobroker stop

停止以守护进程运行的iobroker服务。如果ioBroker未启动，您将收到警告：

```bash
ioBroker controller daemon is not running
```

?> Windows注意事项：  
   通常Windows系统中的ioBroker作为服务启动。
   此命令无效。
   所以在Windows系统中，需要在ioBroker目录中使用`serviceIoBroker.bat stop`，
   而不是`iobroker stop`命令。
   在执行命令前，您应该首先拥有管理员权限来启动服务。

## iobroker restart

此命令是`iobroker stop`和`iobroker start`连续命令顺序执行。详细请参考上述两条命令。

## iobroker isrun

获取ioBroker服务是否在运行的真实状态。如果服务没有运行，返回值为`100`。

用法和`iobroker status`相同。

## iobroker start adapterName.instance

通过此命令使某个`适配器实例`自动启动，并且立即启动该适配器实例。  
如果此适配器实例正在运行，则会重新启动该适配器实例。  
用法：

- `iobroker start email.0`
  - 为`ioBroker.email.0`适配器实例设置为启动并自动启动。

?> 注意:  
   可以通过`iobroker start all`命令启动所有处于`disabled`状态的适配器实例。

## iobroker stop adapterName.instance

通过此命令使某个`适配器实例`停止并取消自动启动。  
用法：

- `iobroker stop email.0`
  - 停止`ioBroker.email.0`适配器实例并取消自动启动。

## iobroker restart adapterName.instance

通过此命令重启某`适配器实例`。
如果该适配器实例处于`disabled`状态，此命令会使该适配器实例状态变为`enabled`。

## iobroker add adapterName

此命令完整的语法是：

```bash
iobroker add adapterName [desiredInstanceNumber] [--enabled] [--host \<host\>] [--port \<port\>]
```

安装并新建一个`适配器实例`。如果适配器实例编号已被占用，则使用之后一个可以用的适配器实例编号。

此命令有几个参数可以设置：

- enabled: 适配器实例将在创建后自动启用，否则将使用适配器预定义值。
- host: 将适配器实例安装到指定ioBroker宿主机上。
  可以通过`iobroker list hosts`命令来获取当前局域网内可用的宿主机列表。
- port: 如果适配器配置项中有native.port字段，则在安装后将其设置为此参数的值。
- desiredInstanceNumber: 通过此参数指定实例的编号。

用法：

- `iobroker add dwd`
  - 安装并创建dwd`适配器实例`.
- `iobroker add admin --enabled --port 80`
  - 创建一个新的（通常为第二个）admin`适配器实例`。并且将web页面端口号设置为80。

如果此命令不起作用，您可以始终使用`npm install iobroker.adapterName`命令强制更新或安装。
此命令不会创建实例。
您在执行上述命令后还需要再调用`iobroker add iobroker.adapterName`命令创建适配器实例。

## iobroker install adapterName

仅在ioBroker中安装`适配器`并且不创建任何实例。如果已安装适配器，您将收到以下警告：  
`adapter "admin" yet installed. Use "upgrade" to install newer version.`

## iobroker upload adapterName

将`适配器`的`www`和`admin`文件夹中的网页源码文件上传到ioBroker文件存储
（`iobroker-data`）中。
开发人员通常使用它来更新配置页面或“www”页面上所做的更改。
您不能直接修改`iobroker/iobroker-data/adapter/file`中的文件。  
开发人员可以通过配置配置文件`iobroker-data/iobroker.json`的`objects.noFileCache`项，
用于禁用文件的缓存。
当将此标志设置为true（当然，配置文件更改后需要新启动）之后，
`iobroker-data`目录中的更改将直接在Web网页上生效，
就不需要再输入`iobroker upload adapterName`命令了。

?> 注意:  
   可以通过`iobroker upload all`命令更新所有的适配器。

## iobroker setup

如果ioBroker不是通过npm或windows安装程序安装的（例如，只是从github下载并解压缩），
则必须调用此命令。
此命令创建默认配置文件并准备数据目录。

您可以使用参数“first”调用此命令，以确保在配置已经存在时，不会覆盖任何内容。

用法：

- `iobroker setup first`
  - 当配置文件不存在时创建配置文件。

## iobroker setup custom

如果要要启用多主机配置，则必须调用此命令。  
调用此命令必须根据情况设置以下几个参数：

<pre><code>
`对象`数据库的类型[file，couch，redis]，默认是[file]：
`对象`数据库的`宿主机`，默认是[127.0.0.1]：输入主服务器的IP地址
`对象`数据库的`端口`，默认为[9001]：
`状态`数据库的类型[file，couch，redis]，默认是[file]：
`状态`数据库的`宿主机`，默认是[127.0.0.1]：输入主服务器的IP地址
`状态`数据库的`端口`，默认为[9000]：
状态类型DB [file，redis]，默认[file]：
状态主机DB（文件），默认[ip]：
状态端口DB（文件），默认[9000]：
</code></pre>

您只需按回车键即可将配置所有参数为\[\]中显示的默认值。

?> 注意:  
   1.目前仅支持*file*数据库。  
   2.除非您是专家，十分了解您的修改并且能够解决遇到的问题，否则请不要修改端口号。  
   3.请确认主服务器的防火墙允许已定义的端口（9000/9001）的访问。  

## iobroker del adapterName

从ioBroker中完全删除此`适配器`的所有`实例`和`状态`，并将其从磁盘上删除。  
删除后无法恢复适配器实例的设置。

用法：

- `iobroker del dwd`
  - 从ioBroker中删除dwd适配器的所有实例和代码。

## iobroker del adapterName.instance

仅从ioBroker中删除此指定的`适配器实例`，而**不是**从磁盘中删除`适配器`。  
删除后无法恢复适配器实例的设置。

用法：

- `iobroker del dwd.0`
  - 从ioBroker中删除dwd.0适配器实例。

## iobroker update

此命令完整语法是：`iobroker update \[repository url\]`

从配置好的ioBroker`适配器库`中读取`适配器`信息。
如果设置了`\repository url\`，则将从此链接的`适配器库`中读取`适配器`信息。  
此命令不做任何更改，只更新有关可用适配器版本的内部信息并显示它。  
要仅显示可更新的适配器，请使用参数“--updatable”。

用法:

- `iobroker update`
  - 列出已配置（通常为本地）`适配器库`的可用版本。
- `iobroker update https://raw.githubusercontent.com/ioBroker/ioBroker.js-controller/master/conf/sources-dist.json`
  - 列出指定URL的`适配器库`的可用版本。

实例输出如下：

```bash
>./iobroker.js update
Cannot get version of "virtual".
Cannot get version of "geofency".
update done
Adapter    "zwave"         : 0.1.0
Adapter    "yr"            : 0.1.2    , installed 0.1.2
Adapter    "web"           : 0.2.6    , installed 0.2.6
Adapter    "vis"           : 0.2.9    , installed 0.2.9
Adapter    "virtual"
Adapter    "sonos"         : 0.1.5    , installed 0.1.4 [Updateable]
Adapter    "rickshaw"      : 0.2.1    , installed 0.2.1
Adapter    "pushover"      : 0.1.0
Adapter    "onkyo"         : 0.0.4
Adapter    "telnet"        : 0.0.0
Adapter    "socketio"      : 0.2.3    , installed 0.2.3
Adapter    "simple-api"    : 0.0.3    , installed 0.0.3
Adapter    "sayit"         : 0.3.0    , installed 0.3.0
Adapter    "ping"          : 0.1.3    , installed 0.1.3
Adapter    "node-red"      : 0.1.5    , installed 0.1.5
Adapter    "mqtt"          : 0.1.6    , installed 0.1.5 [Updateable]
Adapter    "mobile"        : 0.0.2
Adapter    "legacy"        : 0.1.12
Adapter    "knx"           : 0.0.1
Controller "js-controller" : 0.5.14   , installed 0.5.14
Adapter    "javascript"    : 0.2.3    , installed 0.2.3
Adapter    "ical"          : 0.0.2    , installed 0.0.1 [Updateable]
Adapter    "hmm"           : 0.0.15   , installed 0.0.16
Adapter    "hue"           : 0.2.0    , installed 0.2.0
Adapter    "hm-rpc"        : 0.3.5    , installed 0.3.4 [Updateable]
Adapter    "hm-rega"       : 0.1.17   , installed 0.1.17
Adapter    "history"       : 0.1.3    , installed 0.1.3
Adapter    "highcharts"    : 0.0.0
Adapter    "graphite"      : 0.1.0
Adapter    "geofency"
Adapter    "example"       : 0.1.1    , installed 0.1.1
Adapter    "email"         : 0.1.0
Adapter    "dwd"           : 0.1.7    , installed 0.1.7
Adapter    "cul"           : 0.0.2    , installed 0.0.3
Adapter    "b-control-em"  : 0.1.1
Adapter    "artnet"        : 0.0.3
Adapter    "admin"         : 0.3.21   , installed 0.3.20 [Updateable]
```

## iobroker upgrade

此命令完整语法是：`iobroker upgrade \[repository url\]`

升级**所有**适配器（不包括js-controller）到指定版本，该版本将在存储库中找到。

用法：

- `iobroker upgrade`
  - 升级所有适配器。
- `iobroker upgrade https：// raw.githubusercontent.com / ioBroker / ioBroker.js-controller / master / conf / sources-dist.json`
  - 将所有适配器版本升级至指定URL`适配器库`中指定的版本

## iobroker upgrade self

此命令完整语法是：`iobroker upgrade self \[repository url\]`

此命令将升级ioBroker的`js-controller`到指定版本，该版本将在存储库中找到。

?> 注意:  
   如果指定的存储库中配置的版本低于当前版本，则会降级本地的js-controller。

用法：

- `iobroker upgrade self`
  - 升级`js-controller`到已配置的存储库中配置的版本。
- `iobroker upgrade self https://raw.githubusercontent.com/ioBroker/ioBroker.js-controller/master/conf/sources-dist.json`
  - 升级`js-controller`到指定URL的存储库中配置的版本。

## iobroker upgrade adapterName

此命令完整语法是：`iobroker upgrade adapterName \[repository url\]`

升级**指定**`适配器`到指定版本，该版本将在存储库中找到。

?> 注意:  
   如果指定的存储库中配置的版本低于当前版本，则会降级本地的适配器版本。

用法：

- `iobroker upgrade email`
  - 升级`ioBroker.email适配器`到已配置的存储库中配置的版本。
- `iobroker upgrade email https://raw.githubusercontent.com/ioBroker/ioBroker.js-controller/master/conf/sources-dist.json`
  - 升级`ioBroker.email适配器`到指定URL的存储库中配置的版本。

## iobroker object get

此命令完整语法是：`iobroker get objectId`

获取对象的描述信息，结果以json格式返回。

?> 注意:  
   默认情况返回值并不会被格式化，如果需要格式化请加`--pretty`参数。

用法：

- `iobroker object get system.adapter.admin.0.uptime`
  - 获取对象`system.adapter.admin.0.uptime`的描述信息，结果可能如下
    ```json
    {
      "_id":"system.adapter.admin.0.uptime",
      "type":"state",
      "common":{"name":"admin.0.uptime","type":"number","role":"indicator.state","unit":"seconds"},
      "native":{}
    }
    ```

## iobroker object chmod

此命令完整语法是：`iobroker object chmod <object-mode> [state-mode] <id>`

ID可以是带有`*`通配符。`*`只能在末尾使用。

## iobroker object chown

此命令完整语法是：`iobroker object chown <user> <group> <id>`

ID可以是带有`*`通配符。`*`只能在末尾使用。

## iobroker object list

此命令完整语法是：`iobroker object list <id>`

列出对象的权限信息。  
ID可以是带有`*`通配符。`*`只能在末尾使用。

用法：

- `iobroker object list system.adapter.admin.*`
  - 输出可能如下：
    ```bash
    ObjectAC | StateAC |     User     |     Group    | ID
    ---------+---------+--------------+--------------+--------------
    rw-r--r-- rw-r--r--          admin  administrator system.adapter.admin.0.uptime
    rw-r--r-- rw-r--r--          admin  administrator system.adapter.admin.0.memRss
    rw-r--r-- rw-r--r--          admin  administrator system.adapter.admin.0.memHeapTotal
    rw-r--r-- rw-r--r--          admin  administrator system.adapter.admin.0.memHeapUsed
    rw-r--r-- rw-r--r--          admin  administrator system.adapter.admin.0.connected
    rw-r--r-- rw-r--r--          admin  administrator system.adapter.admin.0.alive
    rw-r--r--                    admin  administrator system.adapter.admin.0
    ```

## iobroker set

此命令完整语法是：`iobroker set <instance> [--port value] [--enabled true|false] [--ip address] [--auth true|false] [--ssl true|false] [—-ttl value]`

通过此命令以命令行方式修改实例设置。可以修改以下设置：

- port：更改实例绑定的端口
- enabled：启用/禁用实例（也可以使用`iobroker start | stop <instance>`来完成
- ip：更改绑定的IP地址
- auth：启用或禁用身份验证
- ssl：打开或关闭SSL协议
- ttl：设置登录超时时间（以秒为单位）

## iobroker state get

此命令完整语法是：`iobroker state get stateId`

获取状态的值，结果以json格式返回。

?> 注意:  
   默认情况返回值并不会被格式化，如果需要格式化请加`--pretty`参数。

用法：

- `iobroker state get system.adapter.admin.0.uptime`
  - 获取状态`system.adapter.admin.0.uptime`的值，结果可能如下
    ```json
    {"val":496,"ack":true,"ts":1425925626,"from":"system.adapter.admin.0","lc":1425925626}
    ```

## iobroker state getplain

此命令完整语法是：`iobroker state getplain stateId`

获取状态的值，只返回状态的值。

用法：

- `iobroker state getplain system.adapter.admin.0.uptime`
  - 获取状态`system.adapter.admin.0.uptime`的值，结果可能如下
    ```bash
    571
    true
    system.adapter.admin.0
    1425925701
    1425925701
    ```

## iobroker state getvalue

此命令完整语法是：`iobroker state getvalue stateId`

获取状态的值，只返回状态的值。

用法：

- `iobroker state getvalue system.adapter.admin.0.uptime`
  - 获取状态`system.adapter.admin.0.uptime`的值，结果可能如下
    ```bash
    571
    ```

## iobroker state set

此命令完整语法是：`iobroker state set stateId newValue ack`

此命令用来设置状态的值。`ack`默认是`false`。  
如果ID错误，不会有错误log输出。

用法：

`iobroker state set sayit.0.tts.text “你好”`  
`iobroker state set adapter.0.states.temperature 28.5 true`

## iobroker state del

此命令完整语法是：`iobroker state del stateId`

移除状态。

## iobroker message

此命令完整语法是：`iobroker message adapter.instance command message`

如果未设置实例参数，则向**所有**的`适配器实例`发送消息。
如果设定了实例参数，则向指定的`适配器实例`发送消息。

## iobroker clean

清除ioBroker的所有设置。**如果调用此命令，则无法恢复设置。**

用法：

- `iobroker clean yes`
  - 清除所有ioBroker的设置，结果可能如下：
    ```bash
    Deleted 205 objects.
    Restarting ioBroker...
    ```

## iobroker backup

将ioBroker的设置备份成zip压缩文件。

## iobroker restore

此命令完整语法是：`iobroker restore <backup name or path>`

使用此命令恢复`iobroker backup`创建的备份压缩包。
如果您调用不带参数，您将获得可用备份列表。

在恢复之前的备份配置之后，除`admin`适配器外，所有适配器状态均为`已禁用`状态。
要立即启用所有适配器，可以调用`iobroker start all`。
如果某些适配器未上传，您可以调用`iobroker upload all`立即上传所有适配器的文件。

用法：

- `iobroker restore`
  - 获取可用备份列表，结果可能如下：
    ```bash
    Please specify one of the backup names:
      2015_07_18-12_20_28_backupIoBroker.tar.gz or 2015_07_18-12_20_28 or 0
      2015_07_17-21_54_01_backupIoBroker.tar.gz or 2015_07_17-21_54_01 or 1
    ```
- `iobroker restore 0`
  - 将最新的备份恢复到当前ioBroker配置。

## iobroker host

更改`对象`中的主机名。你必须在此之前停止ioBroker。

有时，将iobroker数据从一个系统移动到另一个系统，需要更改主机名。
此时需要使用此命令可以执行此操作。

要将数据库中的某些特定主机名更改为当前主机名，可以调用`iobroker host oldHostName`。  
要更改任何主机名（必须只是单个主机系统，而不是多个主机），可以调用`iobroker host this`。

## iobroker host set

您可以将主机名更改为某些特定的名字（而不是计算机名）。
为此你必须写：`iobroker host set newHostName`。

## iobroker host remove

此命令用于删除主机名，请谨慎执行此命令。

## iobroker list

使用此命令可以显示ioBroker系统的不同类型的对象和状态。

用法：

- `iobroker list objects hm-rega.0`或`iobroker l o hm-rega.0`
  - 显示hm-rega.0实例的所有对象。
- `iobroker list states hm-rega.0`或`iobroker l s hm-rega.0`
  - 显示hm-rega.0实例的所有状态
- `iobroker list files vis.0`或`iobroker l f vis.0`
  - 显示vis.0实例的所有文件
- `iobroker list instances`或`iobroker l i`
  - 显示所有的实例
    此命令还可以使用下面几个参数作为实例的过滤规则：
    - enabled：显示所有已启用的实例
    - disabled：显示所有已禁用的实例
    - port：显示所有使用端口的实例
    - ip：显示所有可以被其他IP绑定的实例
    - ssl：显示所有可以启用ssl的实例
- `iobroker list adapters`或`iobroker l a`
  - 显示所有适配器
- `iobroker list users`或`iobroker l u`
  - 显示所有用户
- `iobroker list groups`或`iobroker l g`
  - 显示所有用户组
- `iobroker list enums`或`iobroker l e`
  - 显示所有枚举
- `iobroker list hosts`或`iobroker l h`
  - 显示所有宿主机

## iobroker adduser

此命令用于创建新用户。

默认情况下，新用户属于“管理员”组。
可以使用参数“--ingroup”定义一个新的组。  
如果未指定密码，则必须已交互式方式输入密码。  

例如。 在组“user”中创建用户“martin”：

## iobroker deluser

此命令用于删除现存用户。

## iobroker passwd

此命令用于修改用户的密码。

## iobroker chmod

更改文件权限。

## iobroker chown

更改文件所有者。

## iobroker file read

从ioBroker数据库文件读取文件并保存到当前文件系统中。

命令中`file`和`read`可以缩写为`f`和`r`。

用法：

- `iobroker file read <fileToRead> [storeFile]`

## iobroker file write

将当前文件系统中的文件写入ioBroker数据库文件。

命令中`file`和`write`可以缩写为`f`和`w`。

用法：

- `iobroker file write <fileToRead> <storeFile>`

## iobroker version

获取`适配器`或`js-controller`版本号。

用法：

- `iobroker version`或`iobroker -v`或`iobroker --version`
  - 获取`js-controller`版本号。
- `iobroker version admin`或`iobroker admin -v`或`iobroker admin --version`
  - 获取admin`适配器`版本号。

## iobroker uuid

显示当前安装的ioBroker的UUID。

## iobroker status

获取当前ioBroker的运行状态

## iobroker repo 

- 显示已经配置的`适配器库`文件。
- 选择某一个已经配置的`适配器库`文件。

用法：

- `ioBroker repo`
  - 显示已经配置的`适配器库`文件，可能显示如下：
    ```bash
    default: conf/sources-dist.json
    online: https://raw.githubusercontent.com/ioBroker/ioBroker.js-controller/master/conf/sources-dist.json
    fast: http://download.iobroker.net/sources-dist.json

    Active repo: fast
    ```
- `ioBroker repo default`
  - 选择default`适配器库`文件为当前的`适配器库`文件

## iobroker info

显示有关此主机的信息。

输出可能如下：
```bash
Platform       : Windows
Architecture   : x64
CPUs           : 4
Speed          : 2496 MHz
Model          : Intel(R) Core(TM) i7-7660U CPU @ 2.50GHz
RAM            : 15.9 GB
System uptime  : 13d. 13:18:04
Node.js        : v8.11.1
adapters count : 176
Disk size      : 949.9 GiB
Disk free      : 813.3 GiB
NPM            : v5.8.0
```

[ioBroker风格指南]: _zh-cn/community/styleguidedoc
