# 启动和停止 nginx 以及重新加载其配置，配置文件的结构，提供静态内容，配置为代理服务器


nginx有一个主进程和多个工作进程。主进程的主要作用是读取和评估配置文件，并维护工作进程。工作进程负责实际处理请求。nginx采用基于事件的模型和操作系统依赖的机制，有效地将请求分配给工作进程。工作进程的数量在配置文件中定义，可以为给定的配置固定数量，也可以根据可用的CPU核心数自动调整

nginx及其模块的工作方式由配置文件决定。默认情况下，配置文件名为nginx.conf，位于/usr/local/nginx/conf、/etc/nginx或/usr/local/etc/nginx目录下。

## 启动、停止和重载配置
nginx -s signal
- stop —— 快速关闭
- quit —— 优雅关闭
- reload —— 重新加载配置文件
- reopen —— 重新打开日志文件

当主进程收到重载配置的信号时，它会检查新配置文件的语法是否有效，并尝试应用配置。如果成功，主进程将启动新的工作进程，并向旧的工作进程发送消息，要求它们关闭。否则，主进程会回滚更改，并继续使用旧配置。旧的工作进程接收到关闭命令后，停止接受新连接，并继续处理当前请求，直到所有请求都处理完毕。之后，旧的工作进程退出。

使用kill控制nginx主进程的进程ID默认写入nginx.pid文件，该文件位于/var/run目录中


## 配置文件的结构
nginx由多个模块组成，这些模块通过在配置文件中指定的指令来控制。
指令分为简单指令和块指令。简单指令由名称和由空格分隔的参数组成，并以分号（;）结尾。

如果块指令中可以包含其他指令，则该块被称为上下文（例如：events、http、server和location）。

配置文件中，未包含在任何上下文中的指令被视为在主上下文。


## 提供静态内容服务
root用于与location拼接

## 设置简单的代理服务器
接收客户端请求，转发请求到代理服务器，接收代理服务器的响应并将其发送给客户端。
proxy_pass http://localhost:8080/;