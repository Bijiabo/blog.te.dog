---
date: 2015-12-24 21:41
status: public
title: 'Passenger(+Nginx) deploy Ghost'
---

前90％步骤参考[Passenger官方说明](https://www.phusionpassenger.com/library/walkthroughs/deploy/)即可（部署Node.js程序）。

只不过最后一步设定nginx的.conf文件时做部分调整,`[Ghost file path]`即为Ghost程序路径。

```
server {
    listen 80;
    server_name yourDomain.com;

    # Tell Nginx and Passenger where your app's 'public' directory is
    root /[Ghost file path]/core/shared;

    # Turn on Passenger
    passenger_enabled on;
    # Tell Passenger that your app is a Node.js app
    passenger_app_type node;
    passenger_startup_file ../index.js;
}
```

------