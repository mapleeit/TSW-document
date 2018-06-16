# TSW远程调试

> TSW：表示TSW目录，如： /usr/local/services/TSW-1.0

## 准备工作

1、安装最新版chrome浏览器，e.g.63.0.3239.108（正式版本） （64 位）

2、登录到你的需要调试的机器上（TSW的启动和关闭需要root权限）

3、TSW启动和停止脚本

启动脚本位置：

	TSW/bin/proxy/startup.sh

停止脚本位置：

	TSW/bin/proxy/shutdown.sh

## 开启调试模式

1. 先用停止脚本把正在跑的TSW关闭
1. 调试模式启动：node --inspect-brk=0.0.0.0:8080 TSW
    ![调试模式启动](./debug-1.png)

## 连接远程调试

1. Chrome中打开地址： chrome://inspect

    ![chrome中打开地址](./debug-2.png)

1. IP和端口添加到调试列表

    ![IP和端口添加到调试列表](./debug-3.png)

1. 开始断点调试

    ![连接并开始断点调试](./debug-4.png)