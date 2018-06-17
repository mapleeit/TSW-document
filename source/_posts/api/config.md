#配置文件

> TSW全局配置文件，业务逻辑挂载点，也是一个模块~。

## 加载顺序

>配置文件`config.js`加载顺序如下，`{TSW}`表示安装目录

1. `/etc/tsw.config.js`
1. `/usr/local/node_modules/config.js`
1. `/data/release/node_modules/config.js`
1. `{TSW}/conf/config.js`


> Example

```js
const config = plug('config');
```

## 开放平台
- `appid` -- `string` `tswjs.org`颁发的`appid`，默认`null`
- `appkey` -- `string` `tswjs.org`颁发的`appkey`，默认`null`
    ```js
    this.appid = 'tsw007';
    this.appkey = 'FuiFsFwe3asdF12sdwvkshk8';
    ```

## 基础配置
- `devMode` -- `boolean` 开发者模式 ，本地代码修改后可立即生效，有损性能，默认`false`
- `httpAdminPort` -- `number` http管理端口，只监听本地回路`127.0.0.1`，默认值`12701`
	- `reload` -- `curl 127.0.0.1:12701/reload`
- `runAtThisCpu` -- `array|string` worker启动数量和cpu分配策略，默认值`auto`
	- `'auto'` -- `string` 自动分配，核数x1
	- `[0,1]` -- `array[number]` 手动分配，启动两个worker，分别绑定到cpu0和cpu1上
- `workerUid` -- `string` worker运行时用户，默认值`'nobody'`
- `alphaFile` -- `string` 指定`alpha`文件位置，用于固定的白名单，默认值`null`
- `alphaFileUrl` -- `string` 指定`alpha`文件的网络位置，默认值`null`
- `blackIpFile` -- `string` 指定`blackIp`文件位置，默认值`null`
- `blackIpFileUrl` -- `string` 指定`blackIp`文件的网络位置，默认值`null`
- `cpuLimit` -- `number` CPU使用限制，默认值`85`，每个worker独立生效，超过限制自动开启过载保护。
- `memoryLimit` -- `number` 内存使用限制，默认值`768MB`，每个worker独立生效，超过限制自动淘汰。
- `CCIPLimit` -- `number` CC检测预警阈值，默认值`400`,即聚集度达到`400‰`判定为恶意。
    - `-1` -- 表示关闭检测
- `CCIPLimitAutoBlock` -- `boolean` CC检测，启用自动拉黑，默认值`false`。`1.1.3`新增
- `logger` -- `object` 日志级别
	- `logLevel` -- `{'debug':10,'info':20,'warn':30,'error':40,'off':50}['info']`
- `httpProxy` -- `object` 全局http代理设置，为fiddler设计，对在win7下开发比较有用
	- `ip` -- `string` 默认值`'127.0.0.1'`
	- `port` -- `number` 默认值`8888`
	- `enable` -- `boolean` 是否启用，默认值`false`
- `timeout` -- `object` 全局超时控制，单位`ms`
	- `post` -- `bumber` `post like`请求处理超时，默认值30000
	- `get` -- `bumber` `get like`请求处理超时，默认值10000
	- `socket` -- `bumber` `socket`超时设置，默认值30000
	- `keepAlive` -- `bumber` `keepAlive`超时设置，默认值0
        ```js
        this.timeout = {
            socket: 30000,
            post: 30000,
            get: 10000,
            keepAlive: 10000,
            dns: 3000
        }
        ```
- `beforeStartup(cpu)` -- `function` 启动完成前的回调
    - `cpu` -- `number` 当前工作进程对应的`cpu`编号
- `ajaxDefaultOptions` -- `object` `ajax`全局设置，默认值`null`
- `afterStartup(cpu)` -- `function` 启动完成后的回调
    - `cpu` -- `number` 当前工作进程对应的`cpu`编号
- `extendMod` -- `object` 支持重新定义TSW里部分方法的实现
	- `getUid(request)` -- `function` 重新定义从`request`解析`UID`的实现
	- `isTST(request)` -- `function` 重新定义TST（安全扫描器）请求

## HTTP/HTTPS
- `httpAddress` -- `string` http网卡，推荐`'0.0.0.0'`
- `httpPort` -- `number` http端口，默认`80`或者你喜欢的数字
- `workerPortBase` -- `number` worker起始端口，默认`12801`。比如`worker/7`对应的端口为`12801+7=12808`
    - 消息分发 -- `websocket`场景下发送消息到指定worker里
- `httpsAddress` -- `string` https网卡，推荐`'0.0.0.0'`，默认空
- `httpsPort` -- `number` https端口，默认空
- `httpsOptions` -- `object` https证书之类的，透传给`Node.js`
- `page404` -- `string` 404公益页面路由
- `page419` -- `string` 419页面路由
- `router` -- `module` HTTP路由，需实现以下方法
    - `name(req)` -- `function` 负责`req.url`向`name`映射，让`url`收敛
    - `find(name,req,res)` -- `function` 负责`name`向`module`映射，返回处理模块
        - `module` -- `function` http逻辑处理模块，`module.exports`需导出个函数
- `allowArrayInUrl` -- `boolean` url解析参数时是否输出数组
    - `默认值` -- `false`
	- `false` -- 重复元素只取第一个
	- `true` -- 重复元素装在数组里
- `allowHost` -- `array[string|regex|object]` 对非法域名返回`508`，对内网IP无影响
    - `默认值` -- `[]`，空数组表示无限制
	- `string` -- 字符串类型全匹配
	- `regex` -- `regex`类型调用`regex.test(host)`方法匹配
	- `object` -- `object`类型调用`object.test(host)`方法匹配

## websocket
- `wsRouter` -- `module` websocket路由，需实现以下方法
    - `name(ws)` -- `function` 负责`ws.url`向`name`映射
    - `find(name,ws)` -- `function` 负责`name`向`WebSocket module`映射
        - `module` -- `module` websocket逻辑处理模块，需实现以下方法
            - `onConnection(ws)` -- 连接建立的回调函数
            - `onMessage(ws,message)` -- 收到消息的回调函数
            - `onClose(ws,code,reason)` -- 连接关闭时的处理函数
            - `onError(ws,err)` -- 连接出错时的处理函数

## 测试环境
- `isTest` -- `boolean` 测试环境标识 ，默认`false`，为`true`时自动发现
- `testInfo` -- `object` 测试环境信息
	- `name` -- `string` 名称
	- `group` -- `string` 分组名，测试环境会根据分组自动聚合。
	- `groupName` -- `string` 分组名称。
	- `desc` -- `string` 测试环境描述
	- `order` -- `number` 用于排序
	- `owner` -- `string` 测试环境负责人
        ```js
        this.isTest = true;
        this.testInfo = {
            "name"      : "神秘商店",
            "group"     : "TSW",
            "groupName" : "TSW团队",
            "desc"      : "没有人能知道这里在售卖什么",
            "order"     : 30,
            "owner"     : "TSW"
        };
        ```

## 开放平台OPENAPI
- `logReportUrl` -- `string` 染色日志上报，保持默认即可
- `h5testSyncUrl` -- `string` 测试环境同步，保持默认即可
- `utilCDUrl` -- `string` CD冷却池，保持默认即可
- `appReportUrl` -- `string` 指标上报，保持默认即可
- `runtimeReportUrl` -- `string` runtime告警，保持默认即可

## 私有化部署
- `skyMode` -- `boolean` 天空模式 ，私有化部署时管理端标识，默认`false`
    ```js
    this.skyMode = true;
    ```
- `memcached` -- `object` 私有化部署时`memcached`地址声明，默认值`null`
    ```js
    this.memcached = {
        host : '127.0.0.1:11211',
        timeout : 500,
        poolSize : 20,
        retries : 1,
        maxQueueSize : 1000
    };
    ```
- `beforeReportLog(reportData)` -- `function` 自定义日志上报
    - `reportData` -- `object` 包含上报信息的对象，具体字段可打印出来观看
    - `返回值` -- `boolean` 返回`false`会中断TSW的默认上报逻辑
- `beforeReportApp(reportData)` -- `function` 自定义指标上报
    - `reportData` -- `object` 包含上报信息的对象，具体字段可打印出来观看
    - `返回值` -- `boolean` 返回`false`会中断TSW的默认上报逻辑
- `beforeRuntimeReport(reportData)` -- `function` 自定义Runtime上报
    - `reportData` -- `object` 包含上报信息的对象，具体字段可打印出来观看
    - `返回值` -- `boolean` 返回`false`会中断TSW的默认上报逻辑
