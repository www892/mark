现代磁盘的缺陷：IO性能弱、稳定性差  

RAID（Redundant Array of Independent Disks）磁盘冗余阵列通过将多块磁盘通过RAID机制并行工作的方式来提高磁盘的性能和冗余性  

RAID评判标准：  
- 速度：读写速度的提升  
- 磁盘使用率：多磁盘的空间使用率  
- 冗余性： 能够支持几块磁盘损坏而不丢失数据  

RAID分为几种，用级别概念标识，常用RAID级别有：  
- RAID 0  提高读写性能
- RAID 1  提高读取性能性能及冗余性  
- RAID 5  提高读写性能及冗余性  
- RAID 6  提高读写性能及冗余性  

软件RAID是通过操作系统功能或特定软件来实现RAID机制，会占用系统资源，稳定性收操作系统影响    

硬件RAID是通过专有RAID设备实现RAID机制，硬件RAID较为独立，稳定性、速度不受上层系统影响  

Linux系统中通过mdadm程序实现软件RAID功能  
mdadm支持的RAID级别有：RAID0、RAID1、RAID4、RAID5、RAID6  
Linux系统中RAID信息保存在/proc/mdstat中  

通过mdadm命令创建一个RAID0：  
`mdadm -C /dev/md0 -a yes -l 0 -n 3 /dev/sdb /dev/sdc /dev/sdd`  
\-C  创建一个RAID
\-a  自动创建相应设备文件
\-l   指定RAID级�??
\-n   指定磁盘数量
\-x  指定一个备份磁盘

创建好RAID之后需要保存配置信息： 
`mdadm -D --scan > /etc/mdadm.conf`  

查看RAID信息：  
`mdadm -D /dev/md0`  
`cat /proc/mdstat`  

关闭一个RAID  
`mdadm -S /dev/md0`  

模拟一个磁盘故障：  
`mdadm /dev/md0 -f /dev/sdb`  

从一个RAID移出一个磁盘：
`mdadm /dev/md0 -r /dev/sdb`  

向一个RAID中添加一个磁盘：
`mdadm /dev/md0 -a /dev/sdc`  

硬件RAID是通过专有RAID设备实现RAID机制，硬件RAID较为独立，稳定性、速度不受上层系统影响    
