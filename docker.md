# docker笔记

### 列出所有的容器
```
docker container ls --all
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
