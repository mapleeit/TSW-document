# 测试环境

> 用户维度切换测试环境

## 添加

增加如下配置项，重启，测试环境列表里会自动出现

```js
this.isTest = true;
this.testInfo = {
    "name"      : "神秘商店",
    "group"     : "TSW",
    "groupName" : "TSW团队",
    "desc"      : "没有人能知道这里在售卖什么",
    "order"     : 30,
    "owner"     : "TSW"
};
```

## 切换

1. 开放平台切换
    1. 登录`https://tswjs.org`
    1. 选择要切换的应用
    1. 点击测试环境，进行切换
1. 私有化部署切换
    1. 直接访问`http://${host}/group`
        - `host` -- 表示实际部署的管理端域名或IP
    1. 选择分组，进行切换

## 注意事项
1. 生效时间 -- 切换测试环境后，1分钟后全网生效
1. 有效期 -- 测试环境当天有效，0点自动失效
1. 用户标识 -- 在请求周期内可以设置用户`UID`用来染色，但对测试环境联动只有以下两种途径
    1. 在路由的`name`阶段，设置`UID`
    1. 在`config.js`中，重新定义从`request`解析`UID`的实现
        ```js
        this.extendMod = {
            getUin: function(request){
                const uid;
                 //code...
                return uid;
            }
        }
        ```

## 原理

1. TSW会维护一个`UID`到测试环境`IP+PORT`的路由表
1. 命中路由表的请求，流式转发给测试环境

## 故障排除

- 配置测试环境后，未出现在测试环境列表里时，排查清单
    1. 确认是Linux环境
    1. 确认`config.isTest`是否为`true`
        - 可使用工具`TSW/bin/proxy/dump.config.sh`查看目前生效的配置文件对象
    1. 排查`TSW/log/run.log.0`日志中是否有错误日志
    1. 排查`openapi.tswjs.org`域名是否连通，特别是`443`端口
    1. 确认`appid+appkey`无误，并重启使其生效
    1. 如果以上还不能解决，直接联系TSW协助排查



