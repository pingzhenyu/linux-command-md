## cat ##

连接文件并打印到标准输出设备上

### 补充说明 ###

**cat命令** 连接文件并打印到标准输出设备上，cat经常用来显示文件的内容，类似于下的type命令。

注意：当文件较大时，文本在屏幕上迅速闪过（滚屏），用户往往看不清所显示的内容。因此，一般用more等命令分屏显示。为了控制滚屏，可以按Ctrl+S键，停止滚屏；按Ctrl+Q键可以恢复滚屏。按Ctrl+C（中断）键可以终止该命令的执行，并且返回Shell提示符状态。


###  语法

	cat(选项)(参数)

###  选项

	-n或--number：从1开始对所有输出的行数编号；
	-b或--number-nonblank：和-n相似，只不过对于空白行不编号；
	-s或--squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行；
	-A：显示不可打印字符，行尾显示“$”；
	-e：等价于"-vE"选项；
	-t：等价于"-vT"选项；

###  参数 

文件列表：指定要连接的文件列表。

###  实例

### 1. 将file1的文档内容覆盖到file2中
	不带行号覆盖内容
	# cat file1 > file2
	
	带行号覆盖内容
	# cat -n file1 > file2

### 2. 将file1的内容追加到file2的内容中
	# cat file1 >> file2

### 3. 清空file1文档内容
	# cat file1
	     1  我是file2的第一行
	     2  我是file2的第6行
	     3  我是file1的第一行
	     4  我是file1的第二行
	# cat /dev/null > file1
	# cat file1

### 4. 倒序输出file2中的内容

	# cat file2
	我是file2的第一行
	我是file2的第6行
	我是file1的第一行
	我是file1的第二行
	# tac file2
	我是file1的第二行
	我是file1的第一行
	我是file2的第6行

### 5. 设m1和m2是当前目录下的两个文件

	1. 在屏幕上显示文件m1的内容
	# cat m1 
	
	2. 同时显示文件m1和m2的内容
	# cat m1 m2 
	
	3. 将文件m1和m2合并后放入文件file中
	# cat m1 m2 > file 

### 6.	利用cat创建一新文件hhwork
	#	cat >hhwork

### 7.	查看系统文件系统的情况
	文件/etc/fstab记录系统中文件系统的信息，Linux在启动时候，通过读取该文件来决定挂载那些文件系统。	
	#	cat /etc/fstab
