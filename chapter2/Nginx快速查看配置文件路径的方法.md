## 查看nginx服务路径
```bash
ps aux|grep nginx
```
输入如下：
```bash
root      66635  0.0  0.0  13136  1148 pts/0    S+   00:05   0:00 grep --color=auto nginx
root      88067  0.0  0.3 134172  6552 ?        Ss   Sep08   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_p 
```

nginx的路径为：/usr/sbin/nginx

## 查看nginx配置文件路径
使用nginx的 `-t` 参数进行配置检查，即可知道实际调用的配置文件路径及是否调用有效。

```bash
/usr/sbin/nginx -t
# 或者
nginx -t
```
输出如下：
```bash
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
nginx的配置文件路径为：/etc/nginx/nginx.conf。

## nginx配置文件include其他配置文件

nginx 的配置很灵活,支持`include`配置文件,如果配置内容过多， 这个文件就会比较乱, 也影响管理和阅读.所以直接拆分出来,分成不同的配置文件；怎么实现呢 ？直接include：

```bash
include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites/pstest.conf;
```