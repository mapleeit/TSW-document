# 快速开始
> hello world

## 环境要求

- 操作系统: Windows/Mac/Linux
- Node.js: 8.0.0+

## 开始

1. 需先安装 [Node.js](https://nodejs.org/en/download/)，并且Node.js的版本需不低于8.0.0。
1. 安装 -- `git clone https://github.com/Tencent/TSW.git`
1. 切换工作目录 -- `cd TSW`
1. 补全依赖 -- `npm install --no-optional`
1. 启动 --  `node --inspect index.js`
    - 注意：80端口通常需要`root`权限才可监听，监听失败，尝试切换到`root`用户或`sudo`
1. 预览 -- 打开浏览器，访问 `http://127.0.0.1/` 即可

## 示例代码

参考配置文件 `TSW/examples/framework/config.js`

## 开始使用开放平台

1. 在应用中增加配置`config.appid`、`config.appkey`。`appid`和`appkey`获取方式参见[开放平台](//tswjs.org/guide/introduce/cloud)
    ```js
    this.appid = 'tsw007';
    this.appkey = 'ABCDEFFsFwe3asdF12sdwvkshk8';
    ```
1. 其它保持不变，重启让其生效
1. 然后就可以在tswjs.org上使用，染色、抓包、测试环境和监控等基础能力


## 进一步了解

1. 开源框架的集成 [了解一下？](//tswjs.org/guide/introduce/framework)