## 关闭Nginx进程
nginx默认创建一个工作进程

```shell
root      2713     1  0 07:56 ?        00:00:00 nginx: master process ../sbin/nginx
nobody    2714  2713  0 07:56 ?        00:00:00 nginx: worker process
```

* * *

启动nginx时候，我们通过更改配置，设置参数worker\_processes=10。来创建多个进程

```conf
#user  nobody;
worker_processes  10;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

pid        logs/nginx.pid;

events {
    worker_connections  1024;
}
```

* * *

```shell
fuhui@ubuntu:/usr/local/nginx$ ps -ef | grep 'nginx' 
root      2713     1  0 07:56 ?        00:00:00 nginx: master process ../sbin/nginx
nobody    2747  2713  0 08:00 ?

        00:00:00 nginx: worker process
nobody    2748  2713  0 08:00 ?        00:00:00 nginx: worker process
nobody    2749  2713  0 08:00 ?        00:00:00 nginx: worker process
nobody    2750  2713  0 08:00 ?        00:00:00 nginx: worker process
nobody    2751  2713  0 08:00 ?

        00:00:00 nginx: worker process
nobody    2752  2713  0 08:00 ?        00:00:00 nginx: worker process
nobody    2753  2713  0 08:00 ?

        00:00:00 nginx: worker process
nobody    2754  2713  0 08:00 ?

        00:00:00 nginx: worker process
nobody    2755  2713  0 08:00 ?
        00:00:00 nginx: worker process
nobody    2756  2713  0 08:00 ?        00:00:00 nginx: worker process
fuhui     2852  2332  0 08:29 pts/6    00:00:00 grep --color=auto nginx
```

* * *

开始删除掉正在运行的Nginx进程

方式1：
```shell
sudo kill ` ps -ef | grep 'nginx' | awk '{print  $2}' `
```

* * *

方式2：

```powershell
kill $(ps aux | grep '[n]ginx' | awk '{print $2}')
```

* * *