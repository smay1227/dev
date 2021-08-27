# 开发笔记
## redis操作
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