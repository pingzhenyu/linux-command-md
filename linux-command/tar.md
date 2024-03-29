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
```
tar -ztvf log.tar.gz
```

### 3.	将tar 包解压缩
```
tar -cvf etc.tar /etc 
tar -zcvf etc.tar.gz /etc
tar -jcvf etc.tar.bz2 /etc  

tar -zcvf etc.tar.gz /etc -C /home

```
在预设的情况下，我们可以将压缩档在任何地方解开的，-C 这个选项用在解压缩，若要在特定目录解压缩，可以使用这个选项。
### 4. 只解压tar包里的部分文件
```	
tar -jxvf etc.tar.bz2 etc/ucf.conf
```
此处是只解压出了etc.tar.bz2包里的etc/ucf.conf文件，可以通过 tar -ztvf 来查阅 tar 包内的文件名称
### 5. 在文件夹当中，比某个日期新的文件才备份
```
tar -N "2018/11/30" -zcvf log11.tar.gz .
```


### 6. 查看实例一中生成etcbackup.tar备份文件的内容，并在标准输出设备上分屏显示。
```
tar -tvf etcbackup.tar |more
```
