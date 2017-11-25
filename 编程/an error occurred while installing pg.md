---
date: 2015-12-25 21:49
status: public
title: 'An error occurred while installing pg ...'
---

Ubuntu部署Ruby on Rails时遇到报错：
```
An error occurred while installing pg (0.18.3), and Bundler cannot continue.  
Make sure that `gem install pg -v '0.18.3'` succeeds before bundling.  
```

解决：
```
sudo apt-get install libpq-dev  
gem install pg  
```