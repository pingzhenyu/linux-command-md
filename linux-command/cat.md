## cat ##

显示出文件的全部内容


### 补充说明 ###

**cat命令** 连接文件并打印到标准输出设备上，cat经常用来显示文件的内容，类似于下的type命令。

注意：当文件较大时，文本在屏幕上迅速闪过（滚屏），用户往往看不清所显示的内容。因此，一般用more等命令分屏显示。为了控制滚屏，可以按Ctrl+S键，停止滚屏；按Ctrl+Q键可以恢复滚屏。按Ctrl+C（中断）键可以终止该命令的执行，并且返回Shell提示符状态。


###  语法

	cat [OPTION]... [FILE]... 

###  选项

	-n或--number：从1开始对所有输出的行数编号；
	-b或--number-nonblank：和-n相似，只不过对于空白行不编号；
	-s或--squeeze-blank：当遇到有连续两行以上的空白行，就代换为一行的空白行；
	-A：显示不可打印字符，行尾显示“$”；
	-e：等价于"-vE"选项；
	-t：等价于"-vT"选项；


###  实例
### 1.	利用cat创建一新文件file1
	#cat file1
	
### 2. 显示file1中的内容
	# cat file1
	同时显示文件file1和file2的内容
	# cat file1 file2 
	
### 3. 将file1的文档内容覆盖到file2中
	不带行号覆盖内容
	# cat file1 > file2
	
### 4. 将file1的内容追加到file2的内容中
	# cat file1 >> file2

### 5. 清空file1文档内容
	# cat /dev/null > file1
	# cat file1

### 6.	查看系统文件系统的情况
	# cat /etc/fstab
