---
title: 私有化部署
tags:
---
# 私有化部署

> 如果你的团队有一定的运维能力，私有化部署是不错的选择。


## 准备工作

1. `Memcached`集群一个：用于状态保持和冷却池
1. 管理端服务器：用于开启`skyMode`管理端


## 实例

1. `config.js`增加`memcached`配置
1. 不需要配置`appid`和`appkey`，如果有，去掉即可
1. 示例如下
    ```js
    this.memcached = {
        host        : '127.0.0.1:11211',
        timeout     : 500,
        poolSize    : 20,
        retries     : 1,
        maxQueueSize: 1000
    };
    ```


## 开启管理端

1. `config.js`增加`memcached`配置，同上
1. `config.js`增加`skyMode`配置
1. 然后在浏览器直接访问即可
    ```js
    this.skyMode = true;
    this.memcached = {
        host        : '127.0.0.1:11211',
        timeout     : 500,
        poolSize    : 20,
        retries     : 1,
        maxQueueSize: 1000
    };
    ```


## 集成

> 因为私有化部署的网络特殊性，
> 管理端只提供了最基础的`抓包`、`测试环境`、`临时染色`能力，
> 其它能力需自行扩展，与已有运维系统集成。
> 可集成的能力如下：

1. `config.beforeReportLog(reportData)` -- 自定义日志上报，可与日志系统集成
1. `config.beforeReportApp(reportData)` -- 自定义指标上报，可与监控系统集成
1. `config.beforeRuntimeReport(reportData)` -- 自定义Runtime上报，可与告警推送集成


## 运维平台织云lite

> 如何高效安全的在生产环境对TSW进行快速批量部署、起停和升级等维护操作，得各个使用者自己去搞定，
如果没有一个称手的运维平台，还是有点费劲的，好马配好鞍，织云lite为TSW提供了一些列自动打包的脚本，
在您的生产环境部署了织云lite的前提下，一键执行脚本，就能将Nodejs、TSW在织云lite上打包，
带来下述维护上的便利：
详情请参阅 [《如何通过织云lite玩转TSW》](http://bbs.coc.tencent.com/forum.php?mod=viewthread&tid=63)

- 织云Lite 是一款轻量型服务管理平台，提供标准化的应用打包操作，可连接持续集成系统，完成线上程序分发，轻松实现进程管理。
    - 文件包组织：进程依赖的库、配置文件、工具脚本打成文件包。
    - 版本迭代管理：可视化管理文件包，及对应版本安装的机器列表。
    - 秒级发布回滚：每次版本变更只需增量传送变动文件，敏捷高效。
    - 集中式管理：收拢发布入口，避免操作冲突，方便协同操作。
    - 操作查询：统一查询入口，所有现网变更一目了然。
    - 进程管理：可以定制每个进程的启停方式，挂掉后自动拉起。
    - 织云lite的[安装部署传送门](http://bbs.coc.tencent.com/forum.php?mod=viewthread&tid=24)



