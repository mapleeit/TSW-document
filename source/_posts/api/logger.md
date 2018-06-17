# 日志

## 开始使用日志模块

```js
const logger = plug('logger');

logger.debug(`test ${tag}`);
logger.info(`test ${tag}`);
logger.warn(`test ${tag}`);
logger.error(`test ${tag}`);

```

- logger.js
    - `logger.setKey(uid)` -- 设置`uid`
        - `uid` -- `string` 用户标识，将与以下功能联动
            - 染色 -- `response.writeHead()`前设置有效
            - 抓包 -- `response.writeHead()`前设置有效
            - log上报 -- `response.writeHead()`前设置有效
            - 测试环境 -- `config.router.name()`阶段设置有效
    - `logger.getKey()` -- 获取`uid`
    - `logger.setGroup(group)` -- 设置分组
        - `group` -- `string` 分组名称
    - `logger.getGroup()` -- `string` 获取分组
    - `logger.report([uid])` -- 强制上报，并指定`uid`
    - `logger.drop([dropAlpha])` -- 丢掉当前请求的log
        - `dropAlpha` -- 是否丢掉alpha用户的log，默认`false`
    - `logger.isReport()` -- `boolean` 是否需要上报
    - `logger.getSN()` -- `number` 获取流水号
    - `logger.getText()` -- `string` 获取当前流水，返回一个文本



