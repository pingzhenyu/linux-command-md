## tar ##

Linux下的归档使用工具，用来打包和备份

### 补充说明 ###

**tar命令** tar 是用来建立，还原备份文件的工具程序，它可以加入，解开备份文件内的文件。

首先要弄清两个概念：打包和压缩。打包是指将一大堆文件或目录变成一个总的文件；压缩则是将一个大的文件通过一些压缩算法变成一个小文件。为什么要区分这两个概念呢？这源于Linux中很多压缩程序只能针对一个文件进行压缩，这样当你想要压缩一大堆文件时，你得先将这一大堆文件先打成一个包（tar命令），然后再用压缩程序进行压缩（gzip bzip2命令）。


###  语法

	tar(选项)(参数)

###  选项

	-A或--catenate：新增文件到以存在的备份文件；
	-B：设置区块大小；
	-c或--create：建立新的备份文件；
	-C <目录>：这个选项用在解压缩，若要在特定目录解压缩，可以使用这个选项。
	-d：记录文件的差别；
	-x或--extract或--get：从备份文件中还原文件；
	-t或--list：列出备份文件的内容；
	-z或--gzip或--ungzip：通过gzip指令处理备份文件；
	-Z或--compress或--uncompress：通过compress指令处理备份文件；
	-f<备份文件>或--file=<备份文件>：指定备份文件；
	-v或--verbose：显示指令执行过程；
	-r：添加文件到已经压缩的文件；
	-u：添加改变了和现有的文件到已经存在的压缩文件；
	-j：支持bzip2解压文件；
	-v：显示操作过程；
	-l：文件系统边界设置；
	-k：保留原有文件不覆盖；
	-m：保留文件不被覆盖；
	-w：确认压缩文件的正确性；
	-p或--same-permissions：用原来的文件权限还原文件；
	-P或--absolute-names：文件名使用绝对名称，不移除文件名称前的“/”号；
	-N <日期格式> 或 --newer=<日期时间>：只将较指定日期更新的文件保存到备份文件里；
	--exclude=<范本样式>：排除符合范本样式的文件。

###  参数 

- 用户：组：指定所有者和所属工作组。当省略“：组”，仅改变文件所有者；
- 文件：指定要改变所有者和工作组的文件列表。支持多个文件和目标，支持shell通配符。


#### zip格式

压缩： zip -r [目标文件名].zip [原文件/目录名]  
解压： unzip [原文件名].zip  

-r参数代表递归  

#### tar格式（该格式仅仅打包，不压缩）

打包：tar -cvf [目标文件名].tar [原文件名/目录名]  
解包：tar -xvf [原文件名].tar  

c参数代表create（创建），x参数代表extract（解包），v参数代表verbose（详细信息），f参数代表filename（文件名），所以f后必须接文件名。  

#### tar.gz格式

方式一：利用前面已经打包好的tar文件，直接用压缩命令。

压缩：gzip [原文件名].tar  
解压：gunzip [原文件名].tar.gz  

方式二：一次性打包并压缩、解压并解包

打包并压缩： tar -zcvf [目标文件名].tar.gz [原文件名/目录名]  
解压并解包： tar -zxvf [原文件名].tar.gz  
注：z代表用gzip算法来压缩/解压。  

#### tar.bz2格式

方式一：利用已经打包好的tar文件，直接执行压缩命令：

压缩：bzip2 [原文件名].tar  
解压：bunzip2 [原文件名].tar.bz2  
方式二：一次性打包并压缩、解压并解包  

打包并压缩： tar -jcvf [目标文件名].tar.bz2 [原文件名/目录名]  
解压并解包： tar -jxvf [原文件名].tar.bz2  
注：小写j代表用bzip2算法来压缩/解压。  


###  实例


### 1.	将etc文件夹文件全部打包成tar包

```
tar -cvf etc.tar /etc 
tar -zcvf etc.tar.gz /etc
tar -jcvf etc.tar.bz2 /etc  
```

### 2.	查阅上述 tar包内有哪些文件
	命令：
	tar -ztvf log.tar.gz
	输出：
	# tar -ztvf log.tar.gz
	-rw-r--r-- root/root      3743 2018-11-30 09:51 1.log
	说明：
	由于我们使用 gzip 压缩的log.tar.gz，所以要查阅log.tar.gz包内的文件时，就得要加上 z 这个参数了。
### 3.	将tar 包解压缩
	# cd test2
	# ls
	# tar -zxvf /home/hc/test/log.tar.gz 
	1.log
	# ls
	1.log
	说明：
	在预设的情况下，我们可以将压缩档在任何地方解开的,比如此处就是在test2目录下解压了test目录下的log.tar.gz
### 4. 只解压tar包里的部分文件
	# cd ../test
	# ls
	1.log  2.log  3.log  log.tar  log.tar.bz2  log.tar.gz
	# tar -zcvf log123.tar.gz 1.log 2.log 3.log 
	1.log
	2.log
	3.log
	# ll
	total 36
	-rw-r--r-- 1 root root  3743 Nov 30 09:51 1.log
	-rw-r--r-- 1 root root  3743 Nov 30 09:51 2.log
	-rw-r--r-- 1 root root  3743 Nov 30 09:51 3.log
	-rw-r--r-- 1 root root  1943 Nov 30 10:07 log123.tar.gz
	-rw-r--r-- 1 root root 10240 Nov 30 10:01 log.tar
	-rw-r--r-- 1 root root  1810 Nov 30 10:01 log.tar.bz2
	-rw-r--r-- 1 root root  1817 Nov 30 10:01 log.tar.gz
	# cd ../test2
	# ls
	1.log
	# tar -ztvf /home/hc/test/log123.tar.gz 
	-rw-r--r-- root/root      3743 2018-11-30 09:51 1.log
	-rw-r--r-- root/root      3743 2018-11-30 09:51 2.log
	-rw-r--r-- root/root      3743 2018-11-30 09:51 3.log
	# tar -zxvf /home/hc/test/log123.tar.gz 2.log
	2.log
	# ls
	1.log  2.log
	说明：
	此处是只解压出了log123.tar.gz包里的2.log文件，我们可以通过 tar -ztvf 来查阅 tar 包内的文件名称
### 5. 在文件夹当中，比某个日期新的文件才备份
	命令：
	tar -N "2018/11/30" -zcvf log11.tar.gz .
	输出：
	# ll
	total 0
	-rw-r--r-- 1 root root 0 Nov 30 10:23 1.log
	-rw-r--r-- 1 root root 0 Nov 30 10:23 2.log
	-rw-r--r-- 1 root root 0 Nov 30 10:23 3.log
	# tar -N "2018/11/30" -zcvf log11.tar.gz ./*
	tar: Option --after-date: Treating date `2018/11/30' as 2018-11-30 00:00:00
	./1.log
	./2.log
	./3.log
	# tar -N "2018/12/30" -zcvf log12.tar.gz ./*
	tar: Option --after-date: Treating date `2018/12/30' as 2018-12-30 00:00:00
	tar: ./1.log: file is unchanged; not dumped
	tar: ./2.log: file is unchanged; not dumped
	tar: ./3.log: file is unchanged; not dumped
	tar: ./log11.tar.gz: file is unchanged; not dumped
	# ll
	total 8
	-rw-r--r-- 1 root root   0 Nov 30 10:23 1.log
	-rw-r--r-- 1 root root   0 Nov 30 10:23 2.log
	-rw-r--r-- 1 root root   0 Nov 30 10:23 3.log
	-rw-r--r-- 1 root root 128 Nov 30 10:56 log11.tar.gz
	-rw-r--r-- 1 root root  45 Nov 30 10:57 log12.tar.gz
	# tar -tzvf log11.tar.gz 
	-rw-r--r-- root/root         0 2018-11-30 10:23 ./1.log
	-rw-r--r-- root/root         0 2018-11-30 10:23 ./2.log
	-rw-r--r-- root/root         0 2018-11-30 10:23 ./3.log
	# tar -tzvf log12.tar.gz 
	# 
	将当前目录下的更新时间比2018-11-30 00:00:00新的文件或目录进行压缩备份
### 6. 备份文件夹内容时排除部分文件
	# ls
	1.log  2.log  3.log  log11.tar.gz  log12.tar.gz
	# tar --exclude ./log12.tar.gz  -zcvf test.tar.gz ./*
	./1.log
	./2.log
	./3.log
	./log11.tar.gz
	# tar -tzvf test.tar.gz 
	-rw-r--r-- root/root         0 2018-11-30 10:23 ./1.log
	-rw-r--r-- root/root         0 2018-11-30 10:23 ./2.log
	-rw-r--r-- root/root         0 2018-11-30 10:23 ./3.log
	-rw-r--r-- root/root       128 2018-11-30 10:56 ./log11.tar.gz
	
### 7. 把/etc目录包括其子目录全部做一归档文件，归档文件名为etcbackup.tar。
	因为要创建归档文件，所以主选项选择-c。-v选项可以显示该命令在处理每个文件的时候显示详细的处理过程。
	以etcbackup.tar做为归档文件的名字，则需要-f选项。
	#	tar -cvf etcbackup.tar /etc
### 8. 查看实例一中生成etcbackup.tar备份文件的内容，并在标准输出设备上分屏显示。
	对于备份在其他存储介质上的归档文件，用户可能不清楚其具体文件内容，但是用户又不愿将其所有内容从
	归档文件中提取出来。此时，可以利用tar工具的-l选项查看归档文件的具体内容。
	#	tar -tvf etcbackup.tar |more
### 9. 将打印机假脱机文件整理归档并压缩，并命名为spoolfile.tar.gz。
	假设打印机假脱机文件文件位于/var/spool中，不仅要创建归档文件还要对归档文件进行压缩，因此需要-z选项，
	同时需要-f选项。如果用户需要查看归档文件处理过程的报告信息，可以加上-v选项。
	#	tar czvf spoolfile.tar.gz /var/spool
