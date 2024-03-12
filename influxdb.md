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