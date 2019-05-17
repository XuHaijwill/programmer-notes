# docker使用指南

docker仓库:https://hub.docker.com/

阿里云镜像仓库:https://cr.console.aliyun.com/cn-hangzhou/repositories

# 常用工具的安装

## tomcat安装
0. 可指定版本号 
`docker pull tomcat:7.0.94`
1. 后台运行，并指定主机代理端口
`docker run -d -p 8130:8080 tomcat:7.0.94`
1. 从主机复制到容器 
`docker cp dubbo-admin-2.5.9.war d58d827ff3d1:/usr/local/tomcat/webapps`

