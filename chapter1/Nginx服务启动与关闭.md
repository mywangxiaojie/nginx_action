## 启动Nginx服务

### 启动Nginx服务有两种方式：

1. 通过命令行启动：进入Nginx可执行目录（通常是/usr/local/nginx/sbin/），然后输入命令./nginx即可启动Nginx服务。
2. 使用系统服务管理工具：大多数Linux发行版都提供了系统服务管理工具，如systemd或init.d。你可以使用这些工具来启动Nginx服务。例如，在systemd系统中，可以使用命令sudo systemctl start nginx来启动Nginx服务。

## 重启Nginx服务
### 重启Nginx服务也有两种方式：
1. 进入Nginx可执行目录（通常是/usr/local/nginx/sbin/），然后输入命令./nginx -s reload来重启Nginx服务。这个命令会重新加载Nginx的配置文件，而不会中断当前的连接。
2. 使用系统服务管理工具。在systemd系统中，可以使用命令sudo systemctl restart nginx来重启Nginx服务。

## 停止Nginx服务
Nginx默认创建一个工作进程。启动nginx时候，我们通过更改配置，设置参数worker\_processes=10。来创建多个进程。
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



### 停止Nginx服务也有三种方式：
1. 进入Nginx可执行目录（通常是/usr/local/nginx/sbin/），然后输入命令./nginx -s stop来停止Nginx服务。这个命令会立即停止Nginx服务。
2. 使用系统服务管理工具。在systemd系统中，可以使用命令sudo systemctl stop nginx来停止Nginx服务。
3. 直接杀死进程。首先需要查找Nginx的进程号，可以使用命令ps -ef | grep nginx来查找。然后使用命令kill -QUIT [进程号]（从容停止）、kill -TERM [进程号]（快速停止）或kill -INT [进程号]（强制停止）来停止Nginx服务。
4. 批量删除正在运行的worker进程,如下：

方式1：
```shell
sudo kill ` ps -ef | grep 'nginx' | awk '{print  $2}' `
```

* * *

方式2：

```powershell
kill $(ps aux | grep '[n]ginx' | awk '{print $2}')
```


## 设置开机自启动
如果你希望在系统启动时自动启动Nginx服务，可以使用以下方法：
1. 将Nginx加入到系统服务管理工具中。例如，在systemd系统中，可以使用命令`sudo systemctl enable nginx`来将Nginx添加到开机自启动列表中。在init.d系统中，可以将Nginx的启动脚本添加到相应的目录中（如/etc/rc.d/rc3.d/）。
2. 将Nginx加入到chkconfig管理列表中。使用命令chkconfig --add /etc/init.d/nginx来将Nginx添加到chkconfig管理列表中。然后使用命令chkconfig nginx on来设置Nginx在开机时自动启动。
3. 将Nginx加入到rc.local文件中。使用编辑器打开 /etc/rc.local 文件，添加一行 /etc/init.d/nginx start 来在系统启动时自动启动Nginx。