## mount ##

用于挂载Linux系统外的文件

### 补充说明 ###

**mount命令** Linux mount命令是经常会使用到的命令，它用于挂载Linux系统外的文件。

###  语法

	mount [-hV]
	mount -a [-fFnrsvw] [-t vfstype]
	mount [-fnrsvw] [-o options [,...]] device | dir
	mount [-fnrsvw] [-t vfstype] [-o options] device dir

###  选项

	-V：显示程序版本
	-h：显示辅助讯息
	-v：显示较讯息，通常和 -f 用来除错。
	-a：将 /etc/fstab 中定义的所有档案系统挂上。
	-F：这个命令通常和 -a 一起使用，它会为每一个 mount 的动作产生一个行程负责执行。
		在系统需要挂上大量 NFS 档案系统时可以加快挂上的动作。
	-f：通常用在除错的用途。它会使 mount 并不执行实际挂上的动作，而是模拟整个挂上的过程。
		通常会和 -v 一起使用。
	-n：一般而言，mount 在挂上后会在 /etc/mtab 中写入一笔资料。
		但在系统中没有可写入档案系统存在的情况下可以用这个选项取消这个动作。
	-s-r：等于 -o ro
	-w：等于 -o rw
	-L：将含有特定标签的硬盘分割挂上。
	-U：将档案分割序号为 的档案系统挂下。-L 和 -U 必须在/proc/partition 这种档案存在时才有意义。
	-t：指定档案系统的型态，通常不必指定。mount 会自动选择正确的型态。
	-o async：打开非同步模式，所有的档案读写动作都会用非同步模式执行。
	-o sync：在同步模式下执行。
	-o atime、-o noatime：当 atime 打开时，系统会在每次读取档案时更新档案的『上一次调用时间』。
		当我们使用 flash 档案系统时可能会选项把这个选项关闭以减少写入的次数。
	-o auto、-o noauto：打开/关闭自动挂上模式。
	-o defaults:使用预设的选项 rw, suid, dev, exec, auto, nouser, and async.
	-o dev、-o nodev-o exec、-o noexec允许执行档被执行。
	-o suid、-o nosuid：
	允许执行档在 root 权限下执行。
	-o user、-o nouser：使用者可以执行 mount/umount 的动作。
	-o remount：将一个已经挂下的档案系统重新用不同的方式挂上。例如原先是唯读的系统，
		现在用可读写的模式重新挂上。
	-o ro：用唯读模式挂上。
	-o rw：用可读写模式挂上。
	-o loop=：使用 loop 模式用来将一个档案当成硬盘分割挂上系统。


###  实例

### 1. 将 /dev/hda1 挂在 /mnt 之下。

	#mount /dev/hda1 /mnt
### 2. 将 /dev/hda1 用唯读模式挂在 /mnt 之下。

	#mount -o ro /dev/hda1 /mnt
### 3. 将 /tmp/image.iso 这个光碟的 image 档使用 loop 模式挂在 /mnt/cdrom 之下。
	用这种方法可以将一般网络上可以找到的 Linux 光 碟 ISO 档在不烧录成光碟的情况下检视其内容。
	#mount -o loop /tmp/image.iso /mnt/cdrom

	挂载光盘镜像文件mydisk.iso, 可以先执行mkisofs命令将用户sheriff的主目录/home/sheriff下的资料建
	立成一个mydisk.iso的光盘镜像文件。
	#	mkisofs –r –J –V mydisk –o /root /mydisk.iso /home/sheriff

	然后，可以执行mount命令将已创建好的光盘镜像文件mydisk.iso挂载到新建的挂载点/mnt/vcdrom目录下。
	#	mount –o loop –t iso9660 /root/myd isk.iso /mnt/vcdrom
	最后查看/mnt/vcdrom目录下资料，证实挂载操作成功完成。
### 4.	挂载移动磁盘。
	第1步：对Linux系统而言，USB接口的移动磁盘被识别为SCSI设备。插入移动磁盘之前，应先用fdisk –l或
	more /proc/partitions查看系统的磁盘和磁盘分区情况。
	第2步：接好移动磁盘后，再用fdisk –l或more /proc/partitions查看系统的磁盘和磁盘分区情况。
	第3步：对比两次磁盘分区情况查看结果，应该可以发现多了一个SCSI磁盘/dev/sdb和它的三个磁盘分区/dev/sdb1，/dev/sdb2。
	其中/dev/sdb5是/dev/sdb2分区的逻辑分区。可以使用下面的命令挂载/dev/sdb1和/dev/sdb5。
	#	mkdir –p /mnt/usbhd1 
	#	mkdir –p /mnt/usbhd2 
	#	mount –t ntfs /dev/sdb1 /mnt/usbhd1 
	#	mount –t vfat /dev/sdb5 /mnt/usbhd2 
	对ntfs格式的磁盘分区应使用-t ntfs 参数，对fat32格式的磁盘分区应使用-t vfat参数。若汉字文件名显示
	为乱码或不显示，可以使用下面的命令格式。
	#	mount –t ntfs –o iocharset=cp936 /dev/sdc1 /mnt/usbhd1 
	#	mount –t vfat –o iocharset=cp936 /dev/sdc5 /mnt/usbhd2 
### 5.	挂载U盘。
	第1步：和USB接口的移动磁盘一样，在Linux系统中U盘也被当作SCSI设备。插入U磁盘之前，
	应先用fdisk –l或more /proc/partitions查看系统的磁盘和磁盘分区情况。
	第2步：接好U磁盘后，再用fdisk –l 或 more /proc/partitions查看系统的磁盘和磁盘分区情况。
	第3步：对比两次磁盘分区情况查看结果，应该可以发现多了一个SCSI磁盘/dev/sdd和它的一个磁盘分区
	/dev/sdb1，/dev/sdb1就是要挂载的U盘。
	#	mkdir –p /mnt/usb 
	#	mount –t vfat /dev/sdd1 /mnt/usb 
	若汉字文件名显示为乱码或不显示，可以使用下面的命令格式。
	#	mount –t vfat –o iocharset=cp936 /dev/sdd1 /mnt/usb 
### 6.	挂载Windows文件共享。
	Windows网络共享的核心是SMB/CIFS，在Linux下要挂载Windows的磁盘共享，就必须安装和使用samba软件包。
	现在流行的Linux发行版绝大多数已经包含了Samba软件包，如果安装Linux系统时未安装Samba，请首先安装Samba。
	当Windows系统共享设置好以后，就可以在Linux客户端挂载了，具体操作步骤如下：
	第1步，建立一个目录用来作挂载点(mount point)。
	#	mkdir –p /mnt/samba 
	第2步，挂载。
	#	mount -t smbfs -o username=adm inistrator, password=BEIBEI //192.168.1.100/c$ /mnt/samba 
	第3步，访问测试。
	#	cd /mnt/samba 
	#	ls 
	实例6：虚拟挂载/dev/sdb1磁盘的vfat文件系统。
	#	mount –fv –t vfat /dev/sdb1 /mnt/usb 
	参数-f表示虚拟挂载文件系统，实际上并未真实挂载文件系统。通过执行”ls /mnt/usb”命令，
	可以看到加载点下没有什么内容显示。
	实例7：列出当前已挂载的vfat文件系统。
	#	mount–t vfat 


