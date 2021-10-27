<b style="font-size: 2em">Docker</b>

---

# Dockerfile

```text
# 父镜像
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base

MAINTAINER YZQ <yinziqiang@chaoying.com.cn>

# 配置镜像环境变量
ENV {Key} {Value}

# 设置时间为中国上海（默认为UTC）
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 设置工作目录
WORKDIR /app

# 复制发布文件到/app下
COPY . /app

# 设置容器端口
EXPOSE 61000

# 使用{ProjectName}.dll来运行ASP.NET Core项目，注意大小写
ENTRYPOINT ["dotnet", "CySoft.WxAPI.dll"]
```

---

# 常用命令

```bash
# 构建镜像
# docker build -f {Dockerfile文件目录:Dockerfile} -t {镜像名称(限定小写)}:{版本号} .
> docker build -f Dockerfile_Release -t cysoft.wxapi:1.0.211019 .

# 启动容器，-d在后台以守护形式运行容器，-it交互形式运行容器
# docker run --name {容器名称} --network {网络模式:bridge/host/none} -it -p {对外端口}:{内部端口} {镜像名称(限定小写)}:{版本号}
> docker run --name CySoft.WxAPI.1 -it -p 61000:61000 cysoft.wxapi:1.0.211019
# 启动容器，使用host模式（仅支持Linux主机），不需要指定端口映射
> docker run --name CySoft.WxAPI.1 --network host -it cysoft.wxapi:1.0.211019
# 启动容器，挂载宿主机物理目录
> docker run -p 61111:80 -v /D/Conf_WxAPI:/app/Conf -v /D/Log_WxAPI:/app/Log --name CySoft.WxAPI.1 -itd --privileged=true cysoft.wxapi:1.0.211019

# 查看运行容器
> docker ps -a
```

---

# 常用镜像

``` bash
# Postgres SQL
> docker pull postgres
> docker run --name PostgresSQL -e POSTGRES_PASSWORD=123456 -p 5432:5432 -itd postgres

# nginx
> docker pull nginx

# Redis
> docker pull redis

# busybox【集成了三百多个最常用Linux命令和工具的软件】
> docker pull busybox

# RabbitMQ
> docker pull rabbitmq
> docker run -d --hostname yzq-rabbit --name RabbitMQ -p 15672:15672 rabbitmq:3-management

# Memcached
> docker pull memcached

# Mysql
> docker pull mysql

# Consul
> docker pull consul

# Ubuntu
> docker pull ubuntu

# Zookeeper
> docker pull zookeeper

# MongoDB
> docker pull mongo

# MSSQL【https://docs.microsoft.com/zh-cn/sql/linux/quickstart-install-connect-docker?view=sql-server-ver15&pivots=cs1-cmd】
> docker pull mcr.microsoft.com/mssql/server:2019-latest
> docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=123456" -p 1433:1433 --name MSSQL2019 -h DockerMsSQL -d mcr.microsoft.com/mssql/server:2019-latest
```

---

# 备注

* host网络模式仅支持Linux主机，并且不支持Docker for Mac，Docker for Windows或Docker EE for Windows Server。

---

# 相关资源

> 官网  
> <https://www.docker.com/>  
>
> Docker Hub  
> <https://hub.docker.com/>
>
> benjamin杨 博客园  
> <https://www.cnblogs.com/benjamin77/category/1186577.html>
>
> 菜鸟教程  
> <https://www.runoob.com/docker/docker-command-manual.html>
