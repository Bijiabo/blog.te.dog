这两天编写的 OfficeServiceBot 基本有个雏形了，明天到办公室尝试部署到树莓派上面试试。查了一下如何后台运行，比预想的要简单一些，使用 nohup 命令即可，比如入口文件是 `main.py`，如果要后台运行，只需要执行：

```shell
nohup python main.py
```

程序欢快的跑起来之后，如果要杀掉它，首先要找到对应的 PID，执行：
```shell
ps -ef | grep python
```

输入结果如下：
```
503 82193     1   0  5:06下午 ??         0:00.26 python main.py
503 82204 82193   0  5:06下午 ??         0:02.38 /Users/developer/Code/Python/OfficeServiceBot/botEnv/bin/python main.py
503 82917 82223   0  5:12下午 ttys000    0:00.00 grep --color=auto --exclude-dir=.bzr --exclude-dir=CVS --exclude-dir=.git --exclude-dir=.hg --exclude-dir=.svn python
```
使用 kill 命令杀死进程即可：
```shell
kill 82193
```

明天试试，希望程序比较实用。
