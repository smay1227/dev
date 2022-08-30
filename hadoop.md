# hadoop
## hadoop 文件操作
### 查找文件
```
./hadoop fs -ls /hive/click_20220309
```
### 删除文件
```
./hadoop fs -rm /hive/click_20220309/0_20220309_0_1646809008.orc
```
### presto 连接
```
./prestoClient --server localhost:8080 --catalog hive --schema default
```
## beeline
###
在装有beeline的机器上直接输入
```
beeline
```
进入beeline, 连接hive
```
!connect jdbc:hive2://hwy-bms-data02.xxxx.com:2181,hwy-bms-data01.xxxx.com:2181,hwy-bms-data03.xxxx.com:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2
```