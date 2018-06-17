#router

> 可用于实现多级路由

## 指定url

```js
const router = plug('router');
router.route('https://tswjs.org/login');
```



## 指定路由名字

```js
const router = plug('router');
router.route(null,'login');
```

## API
- `router.route(url,[name])`
	- `url` -- `string` 重新指定url，如果url不变，填null即可
	- `name` -- `string` 路由的名字，可省略

