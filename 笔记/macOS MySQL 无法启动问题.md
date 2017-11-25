title: macOS MySQL 无法启动问题
`系统偏好设置/MySQL` 点击`Start MySQL Server`无反应，下方提示文字：
```
Warning the user/local/mysql/data directory is not owned by the mysql user
```

在 [Stack Overflow](https://stackoverflow.com/questions/5527676/warning-the-user-local-mysql-data-directory-is-not-owned-by-the-mysql-user) 上找到解决方法：

```bash
sudo chown -RL root:mysql /usr/local/mysql
sudo chown -RL mysql:mysql /usr/local/mysql/data
sudo /usr/local/mysql/support-files/mysql.server start
```
