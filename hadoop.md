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
### 删除文件夹
```
hadoop fs -rm -r /data/dw/ods/ods
```
### 复制文件夹
将源文件夹下的文件复制到目标文件夹下
```
hadoop fs -cp /user/hive/.Trash/Current/data/dw/ods/* /data/dw/ods
```
### trash 回收站
配置在core-site.xml中
```
<property>  
    <name>fs.trash.interval</name>  
    <value>1440</value>  
    <description>Number of minutes after which the checkpoint gets deleted. If zero, the trash feature is disabled.</description>  
</property>  

<property>  
    <name>fs.trash.checkpoint.interval</name>  
    <value>0</value>  
    <description>Number of minutes between trash checkpoints. Should be smaller or equal to fs.trash.interval. If zero, the value is set to the value of fs.trash.interval.</description>  
</property>
```
| 属性 | 说明 |
| ---- | ---- |
| fs.trash.interval  | 分钟数，当超过这个分钟数后检查点会被删除。如果为零，回收站功能将被禁用。 |
| fs.trash.checkpoint.interval  | 检查点创建的时间间隔(单位为分钟)。其值应该小于或等于fs.trash.interval。如果为零，则将该值设置为fs.trash.interval的值。 |
### 回收站目录
```
/user/${username}/.Trash/current
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