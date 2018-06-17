#全局命令

TSW：表示TSW所在目录，如： /usr/local/services/TSW-1.0

## 本地开发(win7/Linux/Mac)

1. 命令行启动(前台模式) -- `node --inspect TSW`
1. 本地调试 -- `node --inspect-brk TSW`
    - 调试工具 -- `chrome://inspect`
1. 远程调试 -- `node --inspect-brk=0.0.0.0:8080 TSW`
    - 调试工具 -- `chrome://inspect`
1. 在WebStorm里调试 -- `javaScript file` 填入 `TSW/index.js`

## 生产环境(Linux)

1. 启动(后台模式) -- `TSW/bin/proxy/startup.sh`
1. 追加启动参数 -- `/etc/node_args.ini`，一行，顶格写,`1.1.1`新增
    ```
    --icu-data-dir=/home/some --no-deprecation
    ```
1. 停止 -- `TSW/bin/proxy/shutdown.sh`
1. 重启 -- `TSW/bin/proxy/restart.sh`
1. 热重启(shell)-- `TSW/bin/proxy/reload.sh`
1. 热重启(任意用户) -- `curl 127.0.0.1:12701/reload`
1. 收集1000个请求，并生成报告 -- `TSW/bin/proxy/top100.sh`
1. config对象快照到文件 -- `TSW/bin/proxy/dump.config.sh`
1. global对象快照到文件 -- `TSW/bin/proxy/dump.global.sh`

## Docker
```js
# build
docker build -t tsw .
# run
docker run -v configure_dir:/data/release/node_modules -p 8080:80 tsw
```




