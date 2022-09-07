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
一般是在/user 目录下，在对应的用户名下面
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
## flume
## flume1.9及以上连kafka
```
java.security.cert.CertificateException: No subject alternative names matching IP address 10.45.16.224 found
```
kafka高版本默认验证hostname,kafka需要如下字段置为空字符串跳过验证，但flume不支持配置文件是空的字符串，目前flume-1.9,1.10还没解决，是个bug。
```
kafka.consumer.ssl.endpoint.identification.algorithm=''
```
### flume写入hive
#### 缺少hive-hcatalog-streaming.jar
```
java.lang.NoClassDefFoundError: org/apache/hive/hcatalog/streaming/RecordWriter
```
#### 缺少hive-metastore.jar
```
java.lang.NoClassDefFoundError: org/apache/hadoop/hive/metastore/api/MetaException
```
#### 缺少hive-exec.jar
```
java.lang.ClassNotFoundException: org.apache.hadoop.hive.ql.session.SessionState
```
#### 缺少hive-cli.jar
```
java.lang.ClassNotFoundException: org.apache.hadoop.hive.cli.CliSessionState
```
#### 缺少hadoop-common.jar
```
java.lang.NoClassDefFoundError: org/apache/hadoop/conf/Configuration
```
#### 缺少hadoop-mapreduce-client-core.jar
```
java.lang.ClassNotFoundException: org.apache.hadoop.mapreduce.TaskAttemptContext
```
#### 缺少commons-io.jar
```
java.lang.ClassNotFoundException: org.apache.commons.io.Charsets
```
#### 缺少hive-hcatalog-core.jar
```
java.lang.ClassNotFoundException: org.apache.hive.hcatalog.common.HCatUtil
```
#### 缺少commons-configuration.jar
```
java.lang.ClassNotFoundException: org.apache.commons.configuration.Configuration
```
#### 缺少hadoop-auth.jar
```
java.lang.ClassNotFoundException: org.apache.hadoop.util.PlatformName
```
#### 缺少libfb303-0.9.3.jar
```
java.lang.ClassNotFoundException: com.facebook.fb303.FacebookService$Iface
```