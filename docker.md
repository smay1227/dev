# docker笔记
## 常用命令
### 列出所有的容器
```
docker container ls --all
docker ps -a
```
```
CONTAINER ID   IMAGE                                         COMMAND                  CREATED          STATUS          PORTS                                                                                NAMES
6d03375c33d8   xsxx.docker.repo:11844/history:latest         "java -jar -Duser.ti…"   4 minutes ago    Up 4 minutes    8083/tcp, 0.0.0.0:8086->8086/tcp, 0.0.0.0:20883->20880/tcp                           history
e7ca31835f9d   xsxx.docker.repo:11844/rcs:latest             "java -jar -Duser.ti…"   13 minutes ago   Up 13 minutes   0.0.0.0:8084->8084/tcp, 0.0.0.0:20884->20880/tcp                                     rcs
1e2a6c60ca61   xsxx.docker.repo:11844/sms:latest             "java -jar -Duser.ti…"   13 hours ago     Up 13 hours     0.0.0.0:8000->8000/tcp, 0.0.0.0:8085->8085/tcp, 8083/tcp, 0.0.0.0:20881->20880/tcp   sms
2f9db21847d6   xsxx.docker.repo:11844/base:latest            "java -jar -Duser.ti…"   14 hours ago     Up 14 hours     0.0.0.0:8083->8083/tcp, 0.0.0.0:20880->20880/tcp                                     base
3547bc2480f4   xsxx.docker.repo:11844/real:latest            "java -jar -Duser.ti…"   15 hours ago     Up 15 hours     8083/tcp, 0.0.0.0:8087->8087/tcp, 0.0.0.0:20882->20880/tcp                           real
6cbfb7e82ae2   xsxx.docker.repo:11844/sms-platform:latest    "/docker-entrypoint.…"   17 hours ago     Up 17 hours     0.0.0.0:9090->80/tcp                                                                 sms-platform
c9f5b6a67309   xsxx.docker.repo:11844/base-platform:latest   "/docker-entrypoint.…"   18 hours ago     Up 18 hours     0.0.0.0:8080->80/tcp                                                                 base-platform
```
### 进入到某个容器里面
```
docker exec -it real /bin/bash
```
### 查看某个容器服务的控制台日志
```
docker logs -f sms
```
### inspect pid
```
docker inspect 4afd890c3552 |grep Pid
"Pid": 2241212,
"PidMode": "",
"PidsLimit": 0,
```
### 使用docker里的网络
```
nsenter -n -t pid
```
### docker跳过证书认证
在/etc/docker中daemon.json(没有就新建)中追加如下，之后重启docker, systemctl restart docker
```
{
  "insecure-registry": ["harbor.svoltcloud.com"]
}
```
### 启动容器
```
docker run -itd --name basepro alpinepro:2.0 /bin/sh
```
### 停止容器
```
docker stop containerId
```
### 删除镜像文件
```
docker rmi IMAGE:TAG
```
### 删除运行（过）容器
```
docker rm containerId
```
### 镜像拉取
```
docker pull harbor.xxx.com/power/main/java:1.0.0
```

## 给容器打字体
### 进入需打字体的容器
```
# 更新源
apk update
# 安装font-adobe-100dpi软件
apk add font-adobe-100dpi
# 创建文件
mkdir /usr/share/fonts/win
```
### 将字体复制到docker容器中
```
docker cp xxxx.ttc containerId:/usr/share/fonts/win
```
### 对文件赋权限
```
chmod 777 /usr/share/fonts/win/xxxx.ttc
```
### 刷新 查看
```
# 刷新
fc-cache -f
# 查看所有字体
fc-list
```
### 制作镜像
```
docker commit -a "author" -m "comment" containerId image:tag
```
### 镜像私服推送
```
# 登录
docker login ip:port
# 打tag
docker tag SOURCE_IMAGE[:TAG] ip:port/power/IMAGE[:TAG]
# 推镜像
docker push ip:port/power/IMAGE[:TAG]
# 退出登录
docker logout
```

# k8s
### get nodes
```
kubectl get nodes --show-labels
```
### 描述节点
```
kubectl describe nodes
```
