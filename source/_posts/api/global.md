#全局变量

## 加载TSW内置模块

> `plug`用来加载server内置模块，用法同`require(id)`

```js
const logger = plug('logger');
const ajax = plug('ajax');
const config = plug('config');

```

## 上下文对象context

- 特性
    1. 供TSW内部使用，生命周期与`request`绑定
    1. `context` 等价与 `global.context`
    1. 同一个`request`生命周期内只能访问自己的`context`对象

- context
	- `context.window` -- `window`对象
	- `context.autoParseBody` -- `boolean` 为`false`时可关闭TSW自带的body解析
	    - 设置时机 -- `config.router.name()`



## 上下文对象window

- 特性
    1. 供业务使用，生命周期与`request`绑定
    1. `window` 等价与 `global.window`
    1. 同一个`request`生命周期内只能访问自己的`window`对象

- window
    - `window.disable()` -- 禁用全局变量`window`
        - 禁用后，可以通过 `context.window`来访问`window`
    - `window.enable()` -- 启用全局变量`window`
	- `window.onerror = fn` -- 定制错误页
	- `window.response` -- `response`原始对象
	- `window.request` -- `request`原始对象
		- `request.cookies` -- `cookie`的解析结果
		- `request.REQUEST` -- `request.url`的解析结果
		- `request.params` -- 默认值`{}`
		- `request.GET` -- GET参数
		- `request.POST` -- POST参数
            - `application/x-www-form-urlencoded` -- 自动解析，字符集`UTF-8`
            - `application/json` -- 自动解析，字符集`UTF-8`
            - `multipart/form-data` -- 因涉及二进制流式收包，不会自动解析
		- `request.param(key,[defaultValue])`
			- 按照优先级`params > GET > POST > defaultValue`返回非`null`值
	- `window.websocket` -- 触发`message`事件的`websocket`对象，详情查看[websocket对象](https://tswjs.org/doc/api/websocket)


## 当前核CPU使用率

- cpuUsed
	- 取值范围：0-100
	- 更新周期：5秒

## 其它

- TSW_HTTP_WORKER_PORT
    - 当前worker对应的私有端口，可用于websocket转发消息等场景
