```
#更新root用户密码
#ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456'; 
```


```
mysql -u root  -p root_password

# 登陆后进行授权远程连接
GRANT ALL ON *.* TO 'root'@'%';

# 刷新权限
flush privileges;

#更改加密规则
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;


# 刷新权限
flush privileges;

```