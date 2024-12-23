## 使用 HertzBeat快速监控 Nginx
HertzBeat 是一款我们开源的实时监控系统，无需Agent，性能集群，兼容Prometheus，自定义监控和状态页构建能力。https://github.com/dromara/hertzbeat
它支持对应用服务，应用程序，数据库，缓存，操作系统，大数据，中间件，Web服务器，云原生，网络，自定义等监控。
下面广告演示下如果使用 HertzBeat 快速监控 Nginx 服务状态。
1. 部署 HertzBeat
docker run -d -p 1157:1157 -p 1158:1158 --name hertzbeat tancloud/hertzbeat
2. 部署 Nginx
本地部署启动 Nginx, 默认监控 Nginx 可用性，若监控更多指标，则需启用 Nginx 的 ngx_http_stub_status_module 和 ngx_http_reqstat_module 监控模块
3. 在 HertzBeat 添加 Nginx 监控
访问 HertzBeat 控制页面，在 应用服务监控 -> Nginx服务器 添加对端 Nginx 监控，配置对端IP端口等参数。(对了 Docker 默认网络环境下localhost不通本地)

确认添加后就OK啦，后续我们就可以看到 Nginx 的相关指标数据状态，还可以设置告警阈值通知等，当 Nginx 挂了或者某个指标异常过高时，通过邮件钉钉微信等通知我们。
