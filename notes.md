# 开发笔记
## redis操作
### 登录集群中某一台机器
```
redis-cli -h 192.168.200.56 -p 7002 -a "pass" -c
```
### 随机一个key
```
RANDOMKEY
```
### 查看某个key所占内存大小
```
memory usage "q9o.cn/D1SJRu"
```
### 查看hset里面的数据
```
hgetall  "q9o.cn/D1SJRu" 
```
### 查看redis信息
```
info
```
### 查看redis实列大小
```
dbsize
```
### 查看集群主备信息
```
cluster nodes
```
### 删除某个实例的数据
```
flushdb
flushall
```
1. flushAll 清空数据库并执行持久化操作，也就是RDB文件会发生改变,变成76个字节大小(初始状态下为76字节)，所以执行flushAll之后数据库真正意义上清空了。

2. flushDB 清空数据库,但是不执行持久化操作,也就是说RDB文件不发生改变.而redis的数据是从RDB快照文件中读取加载到内存的,所以在flushDB之后,如果想恢复数据库,则可以直接kill掉redis-server进程,然后重新启动服务,这样redis重新读取RDB文件,数据恢复到flushDB操作之前的状态.
<p>
注意:要直接kill 掉redis-server服务,因为shutdown操作会触发持久化.
lsof -i:6379 命令查看redis-server的进程号,然后kill即可
</p>

## 长链接
### 断开某个长链接
```
安装tcpkill
yum install dsniff -y
tcpkill -i em1 host 119.3.44.14
```
### 查看连接数
```
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
```
### 抓包命令
```
tcpdump -n -i bond0 src 106.14.3.99 or dst 106.14.3.99 and port 7890 and tcp -w 1127.cap
```
## linux命令
### 修改主机名
centos7中用
```
hostnamectl set-hostname xxxx
```
### 安装jdk
```
rpm -ivh jdk-8u144-linux-x64.rpm
```
### 动态查看服务器时间
```
watch -n 1 -d date
watch -n 1 "date +%T"
```
