# VLESS Heroku

## 概述

用于在 Heroku 上部署 vless+websocket+tls  vless 性能更加优秀，占用资源更少。

## 镜像

经测试本镜像不会因为大量占用资源而被封号。

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/cyao2q/heroku-vless-1/tree/master)

注：失效问题

上方一键部署已失效，刚看到有朋友说heroku检测到代码违反服务协议，估计使用的人太多或被人举报仓库被heroku封了。

解决方法

a.这里建议你fork本代码后，在github里设置为私有，然后绑定你github到heroku部署使用，推荐这个。

b.或者也可以fork代码后，修改下面链接rptec为你自己账户名，通过链接部署。

https://dashboard.heroku.com/new?template=https://github.com/修改为自己的/heroku-vless-1/tree/master

免费服务，且用且珍惜。

## 注意

Address: yourAppName.herokuapp.com   
Port: 443   
id: Your entered id   
Flow: xtls-rprx-direct   
encryption: none   
Transport: ws   
TLS: tls      

## 流量中转

可以使用cloudflare的workers来`中转流量`，配置为：  https://dash.cloudflare.com/login
```
addEventListener(
    "fetch",event => {
        let url=new URL(event.request.url);
        url.hostname="xx.xxxx.xx";//你的heroku域名
        let request=new Request(url,event.request);
        event.respondWith(
            fetch(request)
        )
    }
)
```

```
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     if (new Date().getDate()%2==0) {
       url.hostname="first.herokuapp.com";//你的heroku域名
     } else {
       url.hostname="second.herokuapp.com";//你的heroku域名
     }
     let request=new Request(url,event.request);
     event.respondWith(
       fetch(request)
     )
  }
)
```

### 客户端软件推荐v2rayN
https://github.com/2dust/v2rayN/releases/tag/4.20
