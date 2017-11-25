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