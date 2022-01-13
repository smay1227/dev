# java线程分析
## 查看最占cpu的线程
### 用top找出最占cpu的进程
```
top
top - 16:37:32 up 8 days,  6:27,  3 users,  load average: 22.96, 25.22, 23.11
Tasks: 187 total,   1 running, 186 sleeping,   0 stopped,   0 zombie
%Cpu(s): 82.4 us,  7.8 sy,  0.0 ni,  7.6 id,  0.0 wa,  0.0 hi,  2.2 si,  0.0 st
KiB Mem :  8009268 total,   121996 free,  7253480 used,   633792 buff/cache
KiB Swap:  4194300 total,  3845628 free,   348672 used.   457240 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND                                                                                                                                                  
31852 root      20   0   13.3g   2.4g 168476 S 306.9 31.9  96:34.37 java   
```
### 查看该进程最占cpu的线程
```
top -Hp 31852
top - 16:14:08 up 8 days,  6:04,  1 user,  load average: 29.13, 21.33, 12.17
Threads: 1184 total,   3 running, 1181 sleeping,   0 stopped,   0 zombie
%Cpu(s): 83.5 us,  7.3 sy,  0.0 ni,  7.7 id,  0.0 wa,  0.0 hi,  1.5 si,  0.0 st
KiB Mem :  8009268 total,   129764 free,  6873224 used,  1006280 buff/cache
KiB Swap:  4194300 total,  3767036 free,   427264 used.   828308 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                                                                                                                                   
32201 root      20   0   14.2g   2.3g 314428 S 63.1 29.9   1:52.74 java                                                                                                                                                      
32363 root      20   0   14.2g   2.3g 314428 S 19.2 29.9   0:11.55 java                                                                                                                                                      
31864 root      20   0   14.2g   2.3g 314428 S 17.9 29.9   1:16.38 java                                                                                                                                                      
32362 root      20   0   14.2g   2.3g 314428 S 16.0 29.9   0:18.66 java                                                                                                                                                      
 1792 root      20   0   14.2g   2.3g 314428 S 15.7 29.9   1:01.17 java                                                                                                                                                      
32364 root      20   0   14.2g   2.3g 314428 S  8.7 29.9   0:16.11 java                                                                                                                                                      
 1880 root      20   0   14.2g   2.3g 314428 S  5.8 29.9   0:19.85 java                                                                                                                                                      
 1879 root      20   0   14.2g   2.3g 314428 S  5.4 29.9   0:19.67 java                                                                                                                                                      
 1878 root      20   0   14.2g   2.3g 314428 S  5.1 29.9   0:19.56 java                                                                                                                                                      
31856 root      20   0   14.2g   2.3g 314428 R  4.5 29.9   0:13.69 java                                                                                                                                                      
31854 root      20   0   14.2g   2.3g 314428 S  4.2 29.9   0:13.35 java                                                                                                                                                      
31855 root      20   0   14.2g   2.3g 314428 S  4.2 29.9   0:13.51 java                                                                                                                                                      
31857 root      20   0   14.2g   2.3g 314428 R  3.8 29.9   0:13.67 java
```
### 打印出该线程的十六进制数
```
printf '%x\n' 32201
7dc9
```
### 使用jstack找出7dc9是哪个线程
```
jstack 31852 | grep 7dc9
"Log4j2-TF-32-AsyncLoggerConfig-9" #196 daemon prio=5 os_prio=0 tid=0x00007fc5a2012800 nid=0x7dc9 runnable [0x00007fc363025000]
```
## jstat打印jvm使用情况
```
jstat -gc -h3 pid 1000 10
```
gc情况，每隔1000ms打印一次记录，打印10次停止，每3行后打印指标头部
## 查看线程情况
```
ps -mp pid -o THREAD,tid,time
```
## iostat
```
iostat -x 1
Linux 3.10.0-957.el7.x86_64 (localhost.localdomain) 	12/30/2021 	_x86_64_	(4 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           2.41    0.00    0.96    0.00    0.00   96.63

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda               0.00     0.02    0.13    2.51    22.40   127.50   113.67     0.00    0.62    2.52    0.52   0.32   0.09
dm-0              0.00     0.00    0.13    2.53    22.34   127.48   112.94     0.00    0.64    2.57    0.54   0.32   0.09

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          87.75    0.00   10.75    0.00    0.00    1.50

Device:         rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
sda               0.00     0.00    0.00   66.00     0.00  8127.50   246.29     0.02    0.36    0.00    0.36   0.33   2.20
dm-0              0.00     0.00    0.00   66.00     0.00  8127.50   246.29     0.02    0.36    0.00    0.36   0.35   2.30
```