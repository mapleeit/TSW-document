#AJAX

> AJAX，用法同jQuery.ajax()


## 使用Deferred

>Example

```js
const ajax = plug('ajax');

ajax.proxy(request,response).request({
      url:url,
      dataType: 'json',
      data: data
}).done(function(d){
   const json = d.result;
});
```

## 使用async/await

> Example

```js
const ajax = plug('ajax');

(async function(){

    const json = await ajax.proxy(request,response).request({
          url:url,
          dataType: 'json',
          data: data
    }).toES6promise().then((d)=>{
        return d.result;
    }).catch(()=>{
        return null;
    });

})();
```

## 创建代理服务器

> Example

```js
const ajax = plug('ajax');

ajax.proxy(request,response).request({
      url:url,
      dataType: 'proxy'
}).fail(function(d){
   response.end();
});
```

## 更多用法

- `Ajax.proxy(req,res)` -- 返回一个新的`Ajax`实例
- `Ajax.request(opt)` -- 发起一次http请求
	- `Ajax.proxy(req,res).request(opt)` -- 代理模式，自动继承`req.headers`
	- `Ajax.request(opt)` -- 非代理模式，空`headers`
	- `return` -- `Deferred`实例，可以通过`.toES6promise()`转为`ES6 Promise`对象

## 请求参数

- `opt`
	- `devIp` -- `string` 开发者模式下，覆盖ip
	- `devPort` -- `number` 开发者模式下，覆盖port
	- `ip` -- `string` 目标ip
	- `port` -- `number` 目标port，默认80
	- `host` -- `string` 目标域名
	- `useIPAsHost` -- `boolean` 使用IP覆盖`headers.host`，默认`false`
	- `type` -- `"GET"|"POST"`，忽略大小写
	- `url` -- `string` 目标url，优先覆盖host、port、path
	- `path` -- `string` 目标path
	- `headers` -- `object` 要发送的headers
	- `timeout` -- `number` 超时时间，默认值3000ms
	- `retry` -- `number` 重试次数，默认值1
	- `data` -- `object` 要发送的数据，GET请求追加到url后在，POST请求转为body
	- `body` -- `string|Buffer` http body
	- `encodeMethod` -- `string` 格式化参数时的编码函数，默认`encodeURIComponent`
	- `success` -- `function` 成功回调
	- `error` -- `function` 失败回调
	- `response` -- `function(response)` `response`事件回调
        - `response` -- 请求对应的`response`对象
        - `返回值` -- 返回`false`可中断`ajax`处理流程
	- `formatCode` -- `function(obj,opt){return {isFail: 0,code:0}}` 格式化返回码
		- `obj` -- 原始data，类型与dataType对应
		- `isFail` -- 0:成功，1:失败，2:逻辑失败
		- `code` -- 翻译后的返回码
	- `dataType` -- `string|number` 指定返回值类型，默认值html
		- `html` -- 以string形式处理回包，gzip自动解压
		- `text` -- 以string形式处理回包，gzip自动解压
		- `buffer` -- 以Buffer形式处理回包，gzip不会自动解压
		- `json` -- 以string形式处理回包，并转成json，gzip自动解压
		- `jsonp` -- 以string形式处理回包，并转成json，gzip自动解压
		- `302` -- `response.statusCode` 为302时触发成功，忽略回包
		- `404` -- `response.statusCode` 为404时触发成功，忽略回包
		- `proxy` -- 用于透明代理，自动处理返回结果到`response`里，只需处理`error`回调即可
	- `jsonpCallback` -- `string` 用于指定jsonp回调的名字
	- `useJsonParseOnly` -- `boolean` 强制使用`JSON.parse`解析回包，默认值false，请求不受信任数据来源时建议开启
	    - `false` -- 不强制，此时可以请求jsonp和不严格的json
	    - `true`  -- 强制，这样更安全，同时要求JSON严格按标准套路来
	- `send` -- `function(request)` 自定义发送内容，覆盖body
		- 用于自定义的流式内容发送
		- 需手动调用request.end()结束发送
	- `enctype` -- `string` POST时指定body的编码方式
		- `application/x-www-form-urlencoded` -- 默认值
		- `application/json`
		- `multipart/form-data`
    - `keepAlive` -- `boolean` 是否启用长连接，默认false

## 返回值

- `data`
	- `opt` -- `object` 即原始`opt`
	- `buffer` -- `buffer` 原始响应内容
	- `result` -- `buffer|string|json` 根据`dataType`转换后的结果
	- `responseText` -- `string` 原始响应内容
	- `hasError` -- `boolean` 请求过程中是否发生网络错误或超时
	- `code` -- `number` 错误码，出错时填写
	- `msg` -- `string` 出错信息
	- `response` -- `object` 原始`response`对象
	- `times` -- `object` 各种测速打点
		- `start` -- `Date` 开始请求
		- `response` -- `Date` `response`事件触发
		- `end` -- `Date` `end`事件触发


## 错误码

- `data.code`
    - `508` -- `Parse json error`
    - `502` -- 建立`tcp`出错，对端原因
    - `600` -- `window.response`提前关闭
    - `60X` -- `600+`剩余重试次数
    - `513` -- 超时
    - `51X` -- `513+`剩余重试次数

