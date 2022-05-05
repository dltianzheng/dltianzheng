### docker修改端口映射

端口映射 -p localport:container_port

### 一 通过docker的下container配置文件

/var/lib/docker/containers/container_id/hostconfig.json

修改PortBindings 

修改config.v2.json

在 config.v2.json 里面添加一个配置项 "ExposedPorts":{"80/tcp":{}} , 将这个配置项添加到 "Tty": true, 前面

最后重启 docker的守护进程 service docker restart

### 二 重新运行







