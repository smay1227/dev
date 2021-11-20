# 记一次线程挂掉生产事故
## 线程未捕获异常
```
Exception in thread "long-msg-receive-11" Exception in thread "long-msg-receive-4" java.lang.ArrayIndexOutOfBoundsException: err
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.takeSms(CmppMergeServiceImpl.java:111)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.access$000(CmppMergeServiceImpl.java:37)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl$ReceiveThread.run(CmppMergeServiceImpl.java:69)
java.lang.ArrayIndexOutOfBoundsException: err
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.takeSms(CmppMergeServiceImpl.java:111)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.access$000(CmppMergeServiceImpl.java:37)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl$ReceiveThread.run(CmppMergeServiceImpl.java:69)
Exception in thread "long-msg-receive-18" java.lang.ArrayIndexOutOfBoundsException: err
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.takeSms(CmppMergeServiceImpl.java:111)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.access$000(CmppMergeServiceImpl.java:37)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl$ReceiveThread.run(CmppMergeServiceImpl.java:69)
```
以上线程挂掉了11，4，18,还剩下如下线程：
```
"long-msg-receive-19" #281 daemon prio=5 os_prio=0 tid=0x00007f0e40486800 nid=0x1ac waiting on condition [0x00007f0c5c7c6000]
"long-msg-receive-17" #279 daemon prio=5 os_prio=0 tid=0x00007f0e40809800 nid=0x1aa waiting on condition [0x00007f0c5c9c8000]
"long-msg-receive-16" #278 daemon prio=5 os_prio=0 tid=0x00007f0e40808800 nid=0x1a9 waiting on condition [0x00007f0c5cac9000]
"long-msg-receive-15" #277 daemon prio=5 os_prio=0 tid=0x00007f0e40dc1800 nid=0x1a8 waiting on condition [0x00007f0c5cbca000]
"long-msg-receive-14" #276 daemon prio=5 os_prio=0 tid=0x00007f0e40dc0000 nid=0x1a7 waiting on condition [0x00007f0c5cccb000]
"long-msg-receive-13" #275 daemon prio=5 os_prio=0 tid=0x00007f0e40a15800 nid=0x1a6 waiting on condition [0x00007f0c5cdcc000]
"long-msg-receive-12" #274 daemon prio=5 os_prio=0 tid=0x00007f0e40a13800 nid=0x1a5 waiting on condition [0x00007f0c5cecd000]
"long-msg-receive-10" #272 daemon prio=5 os_prio=0 tid=0x00007f0e40a11000 nid=0x1a3 waiting on condition [0x00007f0c5d0cf000]
"long-msg-receive-9" #271 daemon prio=5 os_prio=0 tid=0x00007f0e413fb800 nid=0x1a2 waiting on condition [0x00007f0c5d1d0000]
"long-msg-receive-8" #270 daemon prio=5 os_prio=0 tid=0x00007f0e413f9800 nid=0x1a1 waiting on condition [0x00007f0c5d2d1000]
"long-msg-receive-7" #269 daemon prio=5 os_prio=0 tid=0x00007f0e413f8800 nid=0x1a0 waiting on condition [0x00007f0c5d3d2000]
"long-msg-receive-6" #268 daemon prio=5 os_prio=0 tid=0x00007f0e41264000 nid=0x19f waiting on condition [0x00007f0c5d4d3000]
"long-msg-receive-5" #267 daemon prio=5 os_prio=0 tid=0x00007f0e41262000 nid=0x19e waiting on condition [0x00007f0c5d5d4000]
"long-msg-receive-3" #265 daemon prio=5 os_prio=0 tid=0x00007f0e41444000 nid=0x19c waiting on condition [0x00007f0c5d7d6000]
"long-msg-receive-2" #264 daemon prio=5 os_prio=0 tid=0x00007f0e41442000 nid=0x19b waiting on condition [0x00007f0c5d8d7000]
"long-msg-receive-1" #263 daemon prio=5 os_prio=0 tid=0x00007f0e41688000 nid=0x19a waiting on condition [0x00007f0c5d9d8000]
"long-msg-receive-0" #262 daemon prio=5 os_prio=0 tid=0x00007f0e41a4e800 nid=0x199 waiting on condition [0x00007f0c5dad9000]
```
## 线程捕获异常输出如下
```
java.lang.ArrayIndexOutOfBoundsException: err
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.takeSms(CmppMergeServiceImpl.java:111)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.access$000(CmppMergeServiceImpl.java:37)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl$ReceiveThread.run(CmppMergeServiceImpl.java:69)
java.lang.ArrayIndexOutOfBoundsException: err
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.takeSms(CmppMergeServiceImpl.java:111)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.access$000(CmppMergeServiceImpl.java:37)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl$ReceiveThread.run(CmppMergeServiceImpl.java:69)
java.lang.ArrayIndexOutOfBoundsException: err
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.takeSms(CmppMergeServiceImpl.java:111)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl.access$000(CmppMergeServiceImpl.java:37)
	at com.o2o.cmpp.merge.service.CmppMergeServiceImpl$ReceiveThread.run(CmppMergeServiceImpl.java:69)

```
捕获异常的线程没有挂掉，jstack查看线程是正常的
```
jstack 7996 | grep "long-msg-receive"

"long-msg-receive-19" #281 daemon prio=5 os_prio=0 tid=0x00007f07a8ff6000 nid=0x2051 waiting on condition [0x00007f05bfdfc000]
"long-msg-receive-18" #280 daemon prio=5 os_prio=0 tid=0x00007f07a8ff4000 nid=0x2050 waiting on condition [0x00007f05bfefd000]
"long-msg-receive-17" #279 daemon prio=5 os_prio=0 tid=0x00007f07a8ff2000 nid=0x204f waiting on condition [0x00007f05bfffe000]
"long-msg-receive-16" #278 daemon prio=5 os_prio=0 tid=0x00007f07a8445800 nid=0x204e waiting on condition [0x00007f05c41c0000]
"long-msg-receive-15" #277 daemon prio=5 os_prio=0 tid=0x00007f07a8444000 nid=0x204d waiting on condition [0x00007f05c42c1000]
"long-msg-receive-14" #276 daemon prio=5 os_prio=0 tid=0x00007f07a8442800 nid=0x204c waiting on condition [0x00007f05c43c2000]
"long-msg-receive-13" #275 daemon prio=5 os_prio=0 tid=0x00007f07a8f66000 nid=0x204b waiting on condition [0x00007f05c44c3000]
"long-msg-receive-12" #274 daemon prio=5 os_prio=0 tid=0x00007f07a8f64800 nid=0x204a waiting on condition [0x00007f05c45c4000]
"long-msg-receive-11" #273 daemon prio=5 os_prio=0 tid=0x00007f07a8f63000 nid=0x2049 waiting on condition [0x00007f05c46c5000]
"long-msg-receive-10" #272 daemon prio=5 os_prio=0 tid=0x00007f07a8b41000 nid=0x2048 waiting on condition [0x00007f05c47c6000]
"long-msg-receive-9" #271 daemon prio=5 os_prio=0 tid=0x00007f07a8b3f000 nid=0x2047 waiting on condition [0x00007f05c48c7000]
"long-msg-receive-8" #270 daemon prio=5 os_prio=0 tid=0x00007f07a8b3d800 nid=0x2046 waiting on condition [0x00007f05c49c8000]
"long-msg-receive-7" #269 daemon prio=5 os_prio=0 tid=0x00007f07a914a000 nid=0x2045 waiting on condition [0x00007f05c4ac9000]
"long-msg-receive-6" #268 daemon prio=5 os_prio=0 tid=0x00007f07a9148000 nid=0x2044 waiting on condition [0x00007f05c4bca000]
"long-msg-receive-5" #267 daemon prio=5 os_prio=0 tid=0x00007f07a9146800 nid=0x2043 waiting on condition [0x00007f05c4ccb000]
"long-msg-receive-4" #266 daemon prio=5 os_prio=0 tid=0x00007f07a96b3000 nid=0x2042 waiting on condition [0x00007f05c4dcc000]
"long-msg-receive-3" #265 daemon prio=5 os_prio=0 tid=0x00007f07a96b1000 nid=0x2041 waiting on condition [0x00007f05c4ecd000]
"long-msg-receive-2" #264 daemon prio=5 os_prio=0 tid=0x00007f07a96af800 nid=0x2040 waiting on condition [0x00007f05c4fce000]
"long-msg-receive-1" #263 daemon prio=5 os_prio=0 tid=0x00007f07a97c5800 nid=0x203f waiting on condition [0x00007f05c50cf000]
"long-msg-receive-0" #262 daemon prio=5 os_prio=0 tid=0x00007f07a97f7000 nid=0x203e waiting on condition [0x00007f05c51d0000]

```