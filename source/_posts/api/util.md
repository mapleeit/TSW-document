#常用工具


## 内网IP

```js
const serverInfo = plug('serverInfo');
serverInfo.intranetIp;	//服务器内网IP

```


## 判断win7/mac环境


```js
const isWindows = plug('util/isWindows');
isWindows.isWin32Like; //true | false

```

## 染色标记
> alpha工具类

```js
const alpha = plug('util/alpha');

//当前请求
alpha.isAlpha();

//指定uid
alpha.isAlpha(uid);
```


## Deferred
> 基于jQuery.Deferred源码

```js
const Deferred = plug('util/Deferred');
const defer1 = Deferred.create();
const defer2 = Deferred.create();

defer1.done(function(ret){
    //xxx
}).fail(function(ret){
    //xxx
});

Deferred.when(defer1,defer2).done(function(ret1,ret2){
    //xxx
});

//转为Promise对象
defer1.toES6Promies().then(function(){
    //xxx
});
```


## gzip+chunked
> 用于流式回包

```js
const gzipHttp = plug('util/gzipHttp');
const gzip = gzipHttp.create();

gzip.write(chunked1,function(){
    this.flush();
});

gzip.write(chunked2,function(){
    this.flush();
});

gzip.end();
```

- gzipHttp.create([opt]) -- 返回一个gzip流。
	- `opt` -- `object`
		- `request` -- 默认`window.request`
		- `response` -- 默认`window.response`
		- `code` -- `bumber` 响应代码，默认`200`
		- `etag` -- `string` Etag，默认`null`
		- `offline` -- `string` 是否离线，`webso`下有效，决定`cache-offline`的值，默认`false`
			- `true` -- 离线，并立即更新`webview`
			- `store` -- 仅存储
			- `false` -- 不离线
		- `cache` -- `string` 对应Cache-Control，默认`no-cache`
		- `contentType` -- `string` 默认`text/html; charset=UTF-8`



## http工具
> http相关的工具类

```js
const httpUtil = plug('util/http');
const userIp = httpUtil.getUserIp();
const reqStr = httpUtil.getRequestHeaderStr();
const resStr = httpUtil.getResponseHeaderStr();
const isSent = httpUtil.isSent();
const isInner = httpUtil.isInnerIP('127.0.0.1');
```

- `httpUtil.getUserIp([request])` -- 获取用户IP
	- `request` -- 请求，缺省值为`window.request`
- `httpUtil.getRequestHeaderStr([request])` -- 获取请求头字符串
	- `request` -- 请求，缺省值为`window.request`
- `httpUtil.getResponseHeaderStr([response])` -- 获取响应头字符串
	- `response` -- 请求，缺省值为`window.response`
- `httpUtil.isSent([response])` -- 判断响应头是否已发送
	- `response` -- 请求，缺省值为`window.response`
- `httpUtil.isInnerIP(ip)` -- 是否内网ip
	- `ip` -- `string` 要判断的ip







