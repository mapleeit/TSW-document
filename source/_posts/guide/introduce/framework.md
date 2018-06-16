#开源框架的集成

##示例代码

参考配置文件 `TSW/examples/framework/config.js`

## express

> 如果你已经基于`express`开发代码了，那么将`express`集成进`TSW`是不错的选择

1. 注释掉`app.listen()`的调用
1. 编写模块，导出`app`
1. 将编写好的模块挂载到TSW路由上

> Example

```js
"use strict";

const express = require('express');
const app = express();

//http://127.0.0.1/express
app.all('/express',function(req, res){
	res.end('hello express~');
});

//app.listen(80);
//划重点
module.exports = app;
```

>`TSW`内置自动解析常用的`POST`请求，`express`中要去掉对应的中间件，`TSW`支持的列表如下

1. text/plain
2. application/x-www-form-urlencoded
3. application/json


## koa

> 如果你已经基于`koa`开发代码了，那么将`koa`集成进`TSW`是不错的选择

1. 注释掉`app.listen()`的调用
1. 编写模块，导出`app`
1. 将编写好的模块挂载到TSW路由上

```js
"use strict";

const koa = require('koa');
const app = new koa();

//http://127.0.0.1/koa
app.use(ctx => {
	ctx.body = 'Hello Koa';
});

//app.listen(80);
//划重点
module.exports = app;
```

>`TSW`内置自动解析常用的`POST`请求，`koa`中要去掉对应的中间件，`TSW`支持的列表如下

1. text/plain
2. application/x-www-form-urlencoded
3. application/json


## hapi
> 如果你已经基于hapi开发代码了，那么将hapi集成进TSW是不错的选择


1. 空参数启动`hapi`的`server`
1. 编写处理请求的模块，通过`server.connections[0].listener.emit('request',req,res)`调用`hapi`
1. 将编写好的模块挂载到TSW路由上

```js
"use strict";

const Hapi = require('hapi');
const server = new Hapi.Server();
const logger = plug('logger');

server.connection();
server.start();

//http://127.0.0.1/hapi
server.route({
	method: 'GET',
	path:'/hapi',
	handler: function (request, reply) {
		logger.debug('hello hapi');
		return reply('hello hapi~');
	}
});



/**
 * 业务处理模块，通过config.js路由过来
 */
module.exports = function(req,res){
	logger.debug('hello hapi');
	//全转给hapi去处理
	server.connections[0].listener.emit('request',req,res);
};
```

## VueSSR
> 如果你需要使用`Vue`的服务器端渲染，也可以很轻易地集成进去

```javascript
if (typeof window !== 'undefined') {
	window.disable()
}

const { createBundleRenderer } = require('vue-server-renderer')
const bundle = require('this/is/your/vue-ssr-server-bundle.json')
const clientManifest = require('this/is/your/vue-ssr-client-manifest.json')

module.exports = (req, res) => {
	let renderer = createBundleRenderer(bundle, {
		template: `
			<html>
				<head>
					<meta charset="utf-8">
					<title>{{title}}</title>
				</head>
				<body>
					<div id="app">
						<!--vue-ssr-outlet-->
					</div>
				</body>
			</html>
		`,
        clientManifest
	})
	
	renderer.renderToString({
		title: 'Vue SSR - demo'
	}, (error, html) => {
		if (error) {
			res.end(`Error: ${JSON.stringify(error)}`)
			return 1
		}
		res.end(html)
		return 0
	})
}
```

这里有一个地方需要特别注意：
```javascript
if (typeof window !== 'undefined') {
	window.disable()
}
```
__使用`VueSSR`的时候，需要将全局变量[`window`](//tswjs.org/doc/api/global)禁用掉__。原因是`Vue`使用了`window`来作为判断是否是浏览器环境中的标准，导致判断环境错误，执行出错。