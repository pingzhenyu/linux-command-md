## chown ##

用来变更文件或目录的拥有者或所属群组

### 补充说明 ###

chown命令 改变某个文件或目录的所有者和所属的组，该命令可以向某个用户授权，使该用户变成指定文件的所有者或者改变文件所属的组。用户可以是用户或者是用户D，用户组可以是组名或组id。文件名可以使由空格分开的文件列表，在文件名中可以包含通配符。

只有文件主和超级用户才可以便用该命令。


###  语法

	chown(选项)(参数)

###  选项

	-c或——changes：效果类似“-v”参数，但仅回报更改的部分；
	-f或--quite或——silent：不显示错误信息；
	-h或--no-dereference：只对符号连接的文件作修改，而不更改其他任何相关文件；
	-R或——recursive：递归处理，将指定目录下的所有文件及子目录一并处理；
	-v或——version：显示指令执行过程；
	--dereference：效果和“-h”参数相同；
	--help：在线帮助；
	--reference=<参考文件或目录>：把指定文件或目录的拥有者与所属群组全部设成和参考文件或目录的拥有者与所属群组相同；
	--version：显示版本信息。

###  参数 

- 用户：组：指定所有者和所属工作组。当省略“：组”，仅改变文件所有者；
- 文件：指定要改变所有者和工作组的文件列表。支持多个文件和目标，支持shell通配符。

###  实例

### 1 改变文件的拥有者和群组
	# ll log1
	-rwxrwxr-x. 1 root root 0 Nov 20 18:53 log1
	# chown root:mail log1
	# ll log1
	-rwxrwxr-x. 1 root mail 0 Nov 20 18:53 log1
	
	将log1文件的拥有者设为root，群组设为mail

### 2. 改变文件拥有者和群组
	# ll log1
	-rwxrwxr-x. 1 root mail 0 Nov 20 18:53 log1
	# chown root: log1
	# ll log1
	-rwxrwxr-x. 1 root root 0 Nov 20 18:53 log1
	
	将log1文件的拥有者和群组均设为root

### 3. 改变文件群组

	# ll log1
	-rwxrwxr-x. 1 root root 0 Nov 20 18:53 log1
	# chown :mail log1
	# ll log1
	-rwxrwxr-x. 1 root mail 0 Nov 20 18:53 log1

	将log1文件的群组由root改为mail
	
###  4. 改变指定目录以及其子目录下的所有文件的拥有者和群组

	# ll dir2
	total 0
	-rwxr--r--. 1 root root 0 Nov 26 19:34 log2
	-rwxr--r--. 1 root root 0 Nov 26 19:33 log3
	# chown -R -v root:mail dir2
	changed ownership of ‘dir2/log3’ from root:root to root:mail
	changed ownership of ‘dir2/log2’ from root:root to root:mail
	changed ownership of ‘dir2’ from root:bin to root:mail
	# ll dir2
	total 0
	-rwxr--r--. 1 root mail 0 Nov 26 19:34 log2
	-rwxr--r--. 1 root mail 0 Nov 26 19:33 log3

###  5.	改变文件的属主用户。

	假设当前目录下有一文件abc，属主为root。将属主改变为ddf，为了查看设置是否成功
	#	ll abc
	#	chown -v ddf abc
	#	ll abc

###  6.	改变文件的属主用户和属组用户。
	假设当前目录下的文件abc，属主和属组为root，同时将属主和属组更改为ddf
	#	ll abc
	#	chown -v ddf:ddf abc
###  7.	改变文件的属主用户，并指定文件的属组用户为当前登陆账户的所属群组。
	假设当前目录下存在文件abc，其属主和属组都为ddf，将abc的属主设定为root。
	同时将其属组设定为当前登陆用户所在的群组。在命令提示符下输入：
	#	ll abc
	#	chown -v root: abc
	#	ll abc
