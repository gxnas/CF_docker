# CF-docker：Docker仓库镜像代理工具

这个项目是一个基于 Cloudflare Workers 的 Docker 镜像代理工具。它能够中转对 Docker 官方镜像仓库的请求，解决一些访问限制和加速访问的问题。本代码在[CM大佬](https://github.com/cmliu/CF-Workers-docker.io/blob/main/_worker.js) 的源码基础上修改得来。

## 部署方式

- **Workers** 部署：复制 [_worker.js](https://raw.githubusercontent.com/gxnas/CF_docker/refs/heads/main/_worker.js) 代码，`保存并部署`即可
- **Pages** 部署：`Fork` 后 `连接GitHub` 一键部署即可


## 变量说明
| 变量名 | 示例 | 必填 | 备注 | 
|--|--|--|--|
| URL302 | https://t.me/CMLiussss |❌| 主页302跳转 |
| URL | https://www.baidu.com/ |❌| 主页伪装(设为`nginx`则伪装为nginx默认页面) |
| UA | netcraft |❌| 支持多元素, 元素之间使用空格或换行作间隔 |


## 如何使用？ [视频教程](https://www.youtube.com/watch?v=l2jwq9CagNQ)

#### 一、使用该work 设定为注册表仓库。

优点：可以直连打开注册表，并下载镜像。

缺点：

1、缺点搜索结果有所缺失（没有收藏数星标 拉取只有latest版本下载）。

2、work上不能设定URL URL302变量来伪装主页防止滥用和爬虫访问？可以设置UA变量 但目前效果不明。

3、同时下载的映像会有该仓库地址的前置标识。

上述缺点不知是否可改进代码解决，个人感觉收藏数和拉取版本是可代码修复的。其他的则是我的知识盲区，感觉是不行

#### 二、使用该work 设定为官方仓库的注册表镜像

优点：pull拉取无问题。因为可以用URL URL302变量，藏起自己的镜像地址。无需担心免费超额

缺点：无法直接打开注册表。需要代理注册表仓库地址

上述缺点可通过在群晖上.控制面板-网络-代理服务器-填入自己的代理来访问 这里有详细解答 可以在只需要访问注册表的时候临时打开，并不会中断nas的网络。

或者在dsm上架设一个透明代理 只代理docker.io等域名来无痕解决。目前我个人是这样，还挺方便的（因为本来就有需求要给某个docker代理特定链接）

而且这样的使用方式比上面用代理服务器的方式更好，上面的方式会短暂的让群晖的ddns失效，而透明代理这个不会

（我人使用方法是在docker开一个host网络的v2rayA。补齐dsm的iptables模块（使用tproxy的前提），然后开启透明代理为规则端口分流一致，实现方式为tproxy。规则端口为RoutingA 里面设定只代理docker相关，其他直连或自己写。）供参考

 另外说下 在shell下也可以使用
 
 docker search dockpull.你的镜像.com/mysql 来搜索
 
 然后拉取的时候建议设好镜像设定 （这样可以避免上述在dsm注册表设定为仓库那样的缺点3
 
 就可以直接用docker pull 映像名 来拉取而不带你的镜像域名地址（像官方那样
 
 但是缺点也是CF的work不能设定URL URL302变量




# 第三方 DockerHub 镜像服务

**注意:**
- 以下内容仅做镜像服务的整理与搜集，未做任何安全性检测和验证。
- 使用前请自行斟酌，并根据实际需求进行必要的安全审查。
- 本列表中的任何服务都不做任何形式的安全承诺或保证。

| DockerHub 镜像仓库 | 镜像加地址 |
| ------------------ | ----------- |
| [bestcfipas镜像服务](https://t.me/bestcfipas/1900) | `https://docker.registry.cyou` |
|  | `https://docker-cf.registry.cyou` |
| [zero_free镜像服务](https://t.me/zero_free/80) | `https://docker.jsdelivr.fyi` |
|  | `https://dockercf.jsdelivr.fyi` |
|  | `https://dockertest.jsdelivr.fyi` |
| [docker proxy](https://dockerpull.com/) | `https://dockerpull.com` |
| [docker proxy](https://dockerproxy.cn/) | `https://dockerproxy.cn` |
| [Docker镜像加速站](https://hub.uuuadc.top/) | `https://hub.uuuadc.top` |
|  | `https://docker.1panel.live` |
|  | `https://hub.rat.dev` |
| [DockerHub 镜像加速代理](https://docker.anyhub.us.kg/) | `https://docker.anyhub.us.kg` |
|  | `https://docker.chenby.cn` |
|  | `https://dockerhub.jobcher.com` |
| [镜像使用说明](https://dockerhub.icu/) | `https://dockerhub.icu` |
| [Docker镜像加速站](https://docker.ckyl.me/) | `https://docker.ckyl.me` |
| [镜像使用说明](https://docker.awsl9527.cn/) | `https://docker.awsl9527.cn` |
| [镜像使用说明](https://docker.hpcloud.cloud/) | `https://docker.hpcloud.cloud` |
| [DaoCloud 镜像站](https://github.com/DaoCloud/public-image-mirror) | `https://docker.m.daocloud.io` |
| [AtomHub 可信镜像仓库平台](https://atomhub.openatom.cn/) (只包含基础镜像，共336个) | `https://atomhub.openatom.cn` |



# 公益Docker镜像地址
1、`https://dockerpull.com/`

2、`https://dockerproxy.cn/`

3、`https://dockerpull.com/`

4、`https://dockerproxy.cn/`

5、`https://docker.actima.top/`

6、`https://dockerproxy.github.io/`

7、`https://dh.jiasu.in/`
