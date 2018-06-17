#WebSocket

> TSW已内置`WebSocket`

## WebSocket路由

> 只需在[config配置文件](./config)里实现`config.wsRouter`

## 编写处理模块

```js
//需实现的function

exports.onConnection = function(ws){//WebSocket连接建立的回调函数
    //ws.send('xxx');
    //ws.close();
};
exports.onMessage = function(ws, message) {//收到消息的回调函数

};
exports.onClose = function(ws, code, reason) {//WebSocket连接关闭时的处理函数
	
};
exports.onError = function(ws, err) {//WebSocket连接出错时的处理函数
	
};

```
##ws对象属性详解
- `ws.upgradeReq` -- node http连接中的`request`对象
	- `upgradeReq` -- `object` `ws`扩展属性
		- `upgradeReq.GET` -- `object` `WebSocket`请求`get`参数
		- `upgradeReq.headers` -- `object` `WebSocket`请求`cookie`对象
		- `upgradeReq.REQUEST` -- `object` `WebSocket`请求`url`解析后的对象
		- `upgradeReq.REQUEST.pathname` -- `string` `WebSocket`请求的`pathname`
- `ws.readyState` -- `number` `WebSocket`连接的状态，值为数字，只有`readyState`等于`1`时才能send消息
	- `0` -- `number` `WebSocket`连接还没有open
	- `1` -- `number` `WebSocket`连接已经open，并且可以收发消息了
	- `2` -- `number` `WebSocket`连接关闭中
	- `3` -- `number` `WebSocket`连接已关闭
- `ws.send('xxx')` -- 发送消息，支持二进制数据
- `ws.close()` -- 关闭`WebSocket`连接

## 加密WebSocket
http有加密通信https，同样，ws也有加密通信wss，无需单独部署，直接复用https证书

## WebSocket跨机器跨进程消息转发
每个`woker`都监听了一个私有port，从`global.TSW_HTTP_WORKER_PORT`得到，利用私有port转发消息


## 注意事项

> 如果TSW前面有类`nginx`接入层，需要在转发时保持`Upgrade`透传

```html
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "Upgrade";
```


##浏览器端连接demo
```js
const ws = new WebSocket('wss://tswjs.org/hello/world?aaa=xxx');
ws.onopen = function() {//连接建立
	ws.send('xxx');
	ws.close();
};
ws.onmessage = function(message) {};
ws.onclose = function() {};

```

