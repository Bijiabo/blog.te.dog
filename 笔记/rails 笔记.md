---
date: 2016-09-17 02:02
status: public
title: 'Rails 笔记'
---

最近看下 Rails 5 版本。
# 部署
设置生产环境：
```
RAILS_ENV=production  
```
------
生产模式界面 `500` 错误，查看日志有这么一行：
```
ActionView::Template::Error (SQLite3::SQLException: no such table: ...
```
应该是生产环境下忘记初始化数据库了，执行：
```
rails db:create RAILS_ENV=production
rails db:migrate RAILS_ENV=production
```
编译文件
```
rails assets:precompile RAILS_ENV=production
```
------
使用 capistrano 部署时在 bindle:install 步骤出现报错：
```
Your bundle is locked to rake (11.2.2), but that version could not be found in any of the sources listed in your Gemfile. If you haven't changed sources, that means the…
```
应该是 rake 版本不对，服务端执行 `sudo gem install rake -v 11.2.2` 安装 `11.2.2` 版本 rake

------
```
$ rvm env --path
passenger-config --ruby-command 
```

------
通过 `rvmsudo passenger-install-nginx-module` 配置 `nginx` 后，通过 ` sudo service nginx start ` 启动 `nginx` 会提示找不到命令。需要通过这条命令来启动：
```
sudo /opt/nginx/sbin/nginx
```
杀死 Nginx:
```
$ ps auxw | grep nginx
root     25817  0.0  0.1  43248  1172 ?        S    Jan01   0:00 nginx: master process /opt/nginx/sbin/nginx
www-data 25818  0.0  0.3  44240  3484 ?        S    Jan01   0:02 nginx: worker process
```
```
sudo kill 25817
```
or
```
sudo kill $(cat /opt/nginx/logs/nginx.pid)
```
------
获取 Passenger path: 
```
echo `passenger-config --root`/bin
```
设置