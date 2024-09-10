# influxdb笔记
## 常用命令
### tag查找measurements
```
select * from "emsdata_86-611230-001" where "sn" = '2-35100-002322-00080' limit 1
```
### 查找tag value
```
show tag values from "emsdata_86-611230-001" with key = "sn"
```
# hbase
## scan
```
scan 'svoltdata:emsdatav2_86-311200-001',{COLUMNS => 'data:CVa.DevEMS03.Data.P_PCSTotal',TIMERANGE => [1723046400000,1725984000000]}
```
```
scan 'svoltdata:emsdatav2_86-311200-001',{COLUMNS => ['data:CVa.DevEMS03.Data.P_PCSTotal:toString','data:CBa.DevBCMU.SOC.C101'],TIMERANGE => [1723046400000,1725984000000]}
```