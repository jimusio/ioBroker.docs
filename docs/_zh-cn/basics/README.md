---
title:       "基本概念"
lastChanged: "2019/02/02"
---

# 基本概念 {docsify-ignore-all}

?> ***这是一个占位符***.
   <br><br>
   请您帮助ioBroker完善这篇文章。  
   请注意[ioBroker风格指南][]，
   这样可以更容易地合并您的提交。

@@@  
本章节文档主要描述“是什么”，而不是“如何做”。  
每一个名词通过简短（2-4行）而清晰的文字来解释。如果有必要，为此名词新建一个小节。  
阅读完本章节文档后，用户应该能够初步了解各种ioBroker的专业术语。  
@@@

# 名词解释


Host：安装ioBroker的设备
Adapter：ioBroker的模块或插件，例如，用于与硬件通信
无法启动
每个主机只能有一个适配器
Instanz：适配器的可执行副本
执行适配器提供的代码
可以启动和停止
可以有设置
必须安装适配器才能具有适配器的实例
Objekt：可以存储数据的字段
大多数情况下，在创建channel上
an channel是充当文件夹的对象
Aufzählung：包含例如房间列表
Log：累积错误的日志
可过滤事件的严重性，实例等
Ereignisse：对象的所有更改列表

为了给刚刚接触ioBroker的用户提供解更多帮助，以下是ioBroker相关的最重要的术语。

| 中文名词 | 英文名词 | 解释 |
|---|---|---|
`Host`|`Host`|安装ioBroker的设备
`适配器`|`Adapter`|ioBroker的模块或插件。常用于连接某类设备、实现实用功能和连接云平台。
`实例`|`Instanz`|基于适配器的可执行的副本。用于运行适配器的代码、配置适配器。
`对象`|`Objekt`|用于存储数据的字段。一般情况下，实例都会创建一个`channel`。
`channel`|`channel`|对象的集合
`Aufzählung`|`Aufzählung`|保存一些特定的对象，例如房间
`日志`|`Log`|记录ioBroker和其适配器运行时的信息，比如错误信息。
`Ereignisse`|`Ereignisse`|记录对象的历史变化信息的列表

[ioBroker风格指南]: _zh-cn/community/styleguidedoc
