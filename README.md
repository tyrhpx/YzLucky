# Lucky(大吉)
 

 ## 注意：基于gdy666的Lucky_V1.4.10源码，定义为V1.0.0版本，后续进行改造升级。
 

<!-- TOC -->
- [Lucky(大吉)](#)
  - [特性](#特性)
  - [一键安装](#一键安装)
  - [OpenwrtIPK包安装](#OpenwrtIPK包安装)
  - [使用](#使用)
  - [Docker中使用](#docker中使用)
  - [后台界面](#后台界面)

  - [开发编译](#开发编译)
  - [更新日志](#更新日志)
  - [使用注意与常见问题](#使用注意与常见问题)

<!-- /TOC -->


## 特性

Lucky 的核心程序完全采用 Golang 实现，具有高效、稳定、跨平台等优点。其后台前端则采用 Vue3.2 技术进行开发，具有良好的用户体验和响应速度。此外，Lucky 的管理后台采用前后端分离的架构，第三方开发者也可以自由使用OpenToken轻松调用Lucky的各种功能接口。



## 功能模块

目前已经实现/集成的主要功能模块有
  - 端口转发
  - 动态域名(DDNS)
  - Web服务
  - Stun内网穿透
  - 网络唤醒
  - 计划任务
  - ACME自动证书
  - 网络存储



### 端口转发
  1. 主要用于实现公网 IPv6 转内网 IPv4 的 TCP/UDP 端口转发。
  2. 支持界面化的管理转发规则，用户可以通过 web 后台轻松地进行规则的添加、删除、修改等操作。
  3. 单条转发规则支持设置多个转发端口，这样可以实现多个内网服务端口的转发。
  4. 提供了一键开关和定时开关功能，用户可以根据自己的需求设置转发规则的开启和关闭时间，还可以使用计划任务模块进行定时开关。
  5. 单条规则支持黑白名单安全模式切换，用户可以根据需要选择使用白名单模式或黑名单模式。
  6. 白名单模式可以让没有安全验证的内网服务端口稍微安全一点暴露到公网，提高服务可用性。
  7. 实时记录最新的访问日志，方便用户了解转发情况。
  8. 规则列表日志一目了然，用户可以方便地追踪转发异常，及时进行排查和处理。



### 动态域名(DDNS)
  1. 支持接入多个不同的 DNS 服务商。
  2. 支持全功能自定义回调（Callback），包括设置 BasicAuth，方便接入任意 DNS 服务商。
  3. Webhook 支持自定义 headers。
  4. 内置常用免费 DNS 服务商设置模板（每步、No-IP、Dynv6、Dynu），通过自定义回调进行快速接入，仅需修改相应用户密码或 token 即可一键填充。


### Web服务
  1. 支持反向代理、重定向和 URL 跳转。
  2. 支持 HTTP 基本认证。
  3. 支持 IP 黑白名单模式。
  4. 支持 UserAgent 黑白名单。
  5. 规则日志清晰易懂，便于追踪异常。
  6. 支持一键开关规则和定时开关规则。


### Stun内网穿透
  1. 实现内网穿透，无需公网IPv4地址。
  2. 适合于国内运营商级NAT1宽带网络. 

### 网络唤醒
  1. 支持远程控制唤醒和关机操作
  2. 支持接入第三方物联网平台(点灯科技 巴法云),可通过各大平台的语音助手控制设备唤醒和关机.

### 计划任务
  1. 不依赖 Linux 系统的 Cron，支持 Windows 系统。
  2. 操作简便，可视化编辑。
  3. 可操作控制 Lucky 框架内的其他模块开关。

###  ACME自动证书
  1. 支持 ACME 自动证书的申请和续签。
  2. 支持 Cloudflare、阿里云和腾讯云三大 DNS 服务商。


### 网络存储
  1. 网络存储模块是一个应用范围广泛的模块，它提供了将本地存储、WebDAV和阿里云盘挂载到Lucky内部的各个文件类服务功能。
  2. 通过网络存储模块，你可以将添加的存储挂载到Web服务的文件服务、WebDAV、FTP和FileBrowser模块，实现更加便捷的文件管理和访问。





## 一键安装

- [一键安装详看这里](https://github.com/gdy666/lucky-files)


## OpenwrtIPK包安装

- [Openwrt IPK包](https://github.com/gdy666/luci-app-lucky)


## 使用
    

- 默认后台管理地址 http://<运行设备IP>:16601
  默认登录账号: 666
  默认登录密码: 666

- 常规使用请用 -cd <配置文件夹路径> 指定配置文件夹的方式运行 
    ```bash
    #仅指定配置文件夹路径(如果配置文件夹不存在会自动创建),建议使用绝对路径
    lucky -cd luckyconf

    ```




## Docker中使用

- 不挂载主机目录, 删除容器同时会删除配置

  ```bash
  # host模式, 同时支持IPv4/IPv6, Liunx系统推荐
  docker run -d --name lucky --restart=always --net=host gdy666/lucky
  # 桥接模式, 只支持IPv4, Mac/Windows推荐,windows 不推荐使用docker版本
  docker run -d --name lucky --restart=always -p 16601:16601 gdy666/lucky
  ```

- 在浏览器中打开`http://主机IP:16601`，修改你的配置，成功
- [可选] 挂载主机目录, 删除容器后配置不会丢失。可替换 `/root/luckyconf` 为主机目录, 配置文件夹为lucky

  ```bash
  docker run -d --name lucky --restart=always --net=host -v /root/luckyconf:/goodluck gdy666/lucky
  ```












## 后台界面
![规则设置](./previews/relayruleset.png)
![规则列表](./previews/relayrules.png)
![](./previews/whitelistset.png)
![](./previews/whitelist.png)
#### 动态域名服务

![](./previews/ddnslist.png)


![](./previews/iphistroy.png)

![](./previews/webhookhistroy.png)

![](./previews/domainsync.png)

#### Http反向代理
![](./previews/reverseproxy.png)

#### 网络唤醒

![](./previews/wol001.png)

![](./previews/wol002.png)




#开发编译


    ```bash
    go build -v -tags "adminweb nomsgpack" -ldflags="-s -w"
    ```


# 更新日志
    2024-01-15 V1.0.0
        1.对应lucky的v1.4.10版本。
        




















。


## 使用注意与常见问题

 - 不同于防火墙端口转发规则,不要设置没有用上的端口,会增加内存的使用.

 - 小米路由 ipv4 类型的80和443端口被占用,但只设置监听tcp6(ipv6)的80/443端口转发规则完全没问题.

 - 如果需要使用白名单模式,请根据自身需求打开外网访问后台管理页面开关.

 - 转发规则启用异常,端口转发没有生效时请登录后台查看日志.

