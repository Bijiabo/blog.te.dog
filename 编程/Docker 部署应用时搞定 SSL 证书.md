title: Docker 部署应用时搞定 SSL 证书
最近做的一些小项目和 demo 都使用 Docker 来部署了。一台主机目前跑了十来个容器，目前使用 nginx-proxy 来做反向代理，以实现每个容器对应的站点都可以用 80 端口来访问。

这个周末想给站点加上 SSL 证书，本想直接用 Certbot 申请 Let’s Encrypt 证书搞定，但是似乎 Docker 不是这么玩的。搜索了一下，看到 [nginx-proxy](https://github.com/jwilder/nginx-proxy) 官方文档里面有提到相关支持：
> SSL Support using letsencrypt
> letsencrypt-nginx-proxy-companion is a lightweight companion container for the nginx-proxy. It allow the creation/renewal of Let's Encrypt certificates automatically.

使用 [letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion) 即可解决我的需求。

按照官网文档，首先启动 nginx-proxy 容器：
```shell
$ docker run -d -p 80:80 -p 443:443 \
    --name nginx-proxy \
    -v /path/to/certs:/etc/nginx/certs:ro \
    -v /etc/nginx/vhost.d \
    -v /usr/share/nginx/html \
    -v /var/run/docker.sock:/tmp/docker.sock:ro \
    --label com.github.jrcs.letsencrypt_nginx_proxy_companion.nginx_proxy=true \
    jwilder/nginx-proxy
```
然后启动 letsencrypt-nginx-proxy-companion：
```shell
$ docker run -d \
    -v /path/to/certs:/etc/nginx/certs:rw \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    --volumes-from nginx-proxy \
    jrcs/letsencrypt-nginx-proxy-companion
```
这样就算是基本设定好反向代理以及自动 SSL 证书了。

接下来，在需要添加 HTTPS 支持的容器中，设定全局变量：
- LETSENCRYPT_HOST // 用于申请证书的域名，多个域名用逗号隔开
- LETSENCRYPT_EMAIL // 用于申请证书的邮箱
- VIRTUAL_HOST // 告诉 nginx-proxy 当前容器要绑定什么域名，多个域名用逗号隔开

大功告成。