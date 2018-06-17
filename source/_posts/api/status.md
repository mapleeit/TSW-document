# TSW指标


> `SUM`开头表示是累计型，聚合时求和

> `AVG`开头表示是时刻值，聚合时求平均值

## CPU ##

- AVG_TSW_CPU_USED -- 当前CPU使用率，`0-100`

## 内存 ##

- AVG_TSW_MEMORY_RSS -- 当前内存RSS使用量，单位Bit
- AVG_TSW_MEMORY_HEAP -- 当前内存HEAP使用量，单位Bit
- AVG_TSW_MEMORY_EXTERNAL -- 当前内存EXTERNAL使用量，单位Bit

## HTTP

- SUM_TSW_HTTP_20X -- 返回200的次数，包含`200`和`206`等
- SUM_TSW_HTTP_302 -- 返回重定向的次数，包含`301`、`302`、`303`和`307`
- SUM_TSW_HTTP_304 -- 返回304的次数
- SUM_TSW_HTTP_403 -- 返回403的次数
- SUM_TSW_HTTP_404 -- 返回404的次数
- SUM_TSW_HTTP_404GY -- 404公益返回次数
- SUM_TSW_HTTP_418 -- 返回418的次数，我是茶壶
- SUM_TSW_HTTP_419 -- 返回419的次数，Love For One Night
- SUM_TSW_HTTP_666 -- 返回666的次数，同200
- SUM_TSW_HTTP_501 -- 返回501的次数
- SUM_TSW_HTTP_508 -- 返回508的次数，不是我的域名
- SUM_TSW_HTTP_500 -- 返回50X的次数，包含500，503，513等，不包含以上已知的错误
- SUM_TSW_HTTP_OTHER -- 返回未知的次数，不在以上统计范围内的算未知
- SUM_TSW_HTTP_TST -- 安全扫描器的请求次数
- SUM_TSW_XSS_BLOCK -- XSS防御器生效次数
- SUM_TSW_CC_LIMIT -- CC防御生效次数
- SUM_TSW_BAD_COOKIE -- COOKIE格式不严格，自动纠正的次数

## 健康状况

- SUM_TSW_OVERLOAD_REJECT -- 过载保护生效次数
- AVG_TSW_ST0_X10 -- `setTimeout(fn,0)`测量得到的延迟，放大10倍方便观察，单位1/10ms
- AVG_TSW_IP_STD_X10 -- IP访问次数加权方差，放大10倍方便观察
- SUM_TSW_IP_BLOCK -- 命中黑名单IP的次数
- SUM_TSW_IP_EMPTY -- 空IP阻挡次数，收包过程中断连或高负载的情况下会出现
- SUM_TSW_ROUTE_EXCEED -- 疑似循环转发，拒绝次数
- SUM_TSW_CD_CHECK -- CD冷却API调用次数

## 日志

- SUM_TSW_LOG_FAIL  -- 包含逻辑失败的流水次数
- SUM_TSW_LOG_FORCE -- 强制上报的流水次数
- SUM_TSW_LOG_ERROR -- 包含错误的流水次数
- SUM_TSW_LOG_ALPHA -- 染色流水次数，即云抓包次数
- SUM_TSW_LOG_WEB   -- 来自浏览器端的流水上报次数
- SUM_TSW_LOG_TST   -- 安全扫描器产生的流水次数
- SUM_TSW_REPORT_LOG -- 流水落地的次数
- SUM_TSW_ERROR_LOG_DROP -- `warn`或`error`级别日志，丢弃的条数
- AVG_TSW_ERROE_LOG_5S -- `warn`或`error`级别日志发生频率，统计粒度5秒


## 文件读写

- SUM_TSW_FILECACHE_WRITE -- 文件缓存API写调用次数
- SUM_TSW_FILECACHE_READ -- 文件缓存API读调用次数
- SUM_TSW_FILE_SYNC -- 文件API同步方式调用次数，不包含异步方式调用

## WEBSOCKET

- SUM_TSW_WEBSOCKET_CONNECT -- `WebSocket`连接建立次数
- SUM_TSW_WEBSOCKET_MESSAGE -- `WebSocket` 消息接收次数
- SUM_TSW_WEBSOCKET_ERROR -- `WebSocket` 错误事件触发次数
- SUM_TSW_WEBSOCKET_CLOSE -- `WebSocket` 关闭事件触发次数
- SUM_TSW_WEBSOCKET_TIMEOUT -- `WebSocket` 请求/响应模型下，响应超时次数
- SUM_TSW_WEBSOCKET_RESPONSE -- `WebSocket` 请求/响应模型下，成功响应次数
- SUM_TSW_WEBSOCKET_PUSH -- `WebSocket` 消息推送次数


## CDN
- SUM_TSW_CDN_CSS -- 从CDN获取CSS的次数
- SUM_TSW_CDN_JS -- 从CDN获取JS的次数

## WEBSO

- SUM_TSW_WEBSO_OK -- `WEBSO`请求次数
- SUM_TSW_WEBSO_LIMIT -- `WEBSO`命中柔性次数
- AVG_TSW_WNSDIFF_SIZE -- `wnsdiff`体积，单位Bit
- AVG_TSW_WNSDIFF_COST -- `wnsdiff`耗时，单位ms


