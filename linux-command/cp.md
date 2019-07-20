## cp ##

将源文件或目录复制到目标文件或目录中

### 补充说明 ###

**cp命令** 用来将一个或多个源文件或者目录复制到指定的目的文件或目录。它可以将单个源文件复制成一个指定文件名的具体的文件或一个已经存在的目录下。cp命令还支持同时复制多个文件，当一次复制多个文件时，目标文件参数必须是一个已经存在的目录，否则将出现错误。


###  语法

	cp [OPTION]... [-T] SOURCE DEST
	cp [OPTION]... SOURCE... DIRECTORY
	cp [OPTION]... -t DIRECTORY SOURCE...


###  选项
	-a：此参数的效果和同时指定"-dpR"参数相同；
	-d：当复制符号连接时，把目标文件或目录也建立为符号连接，并指向与源文件或目录连接的原始文件或目录；
	-f：强行复制文件或目录，不论目标文件或目录是否已存在；
	-i：覆盖既有文件之前先询问用户；
	-l：对源文件建立硬连接，而非复制文件；
	-p：保留源文件或目录的属性；
	-R/r：递归处理，将指定目录下的所有文件与子目录一并处理；
	-s：对源文件建立符号连接，而非复制文件；
	-u：使用这项参数后只会在源文件的更改时间较目标文件更新时或是名称相互对应的目标文件并不存在时，才复制文件；
	-S：在备份文件时，用指定的后缀“SUFFIX”代替文件的默认后缀；
	-b：覆盖已存在的文件目标前将目标文件备份；
	-v：详细显示命令执行的操作。

###  参数

*   源文件：制定源文件列表。默认情况下，cp命令不能复制目录，如果要复制目录，则必须使用 -r 选项；
*   目标文件：指定目标文件。当“源文件”为多个文件时，要求“目标文件”为指定的目录。

###  实例

###  目录结构
	../test/
	├── dir2
	├── dir3
	│   ├── dir1
	│   ├── file2.txt
	│   ├── log2
	│   └── log2~
	└── log1
### 1. 复制文件到指定目录
	
	# cp log1 dir2 （目标文件存在时，会覆盖,加上参数 -i会询问是否覆盖，-f强制覆盖）
	
### 2.	将指定文件复制到当前目录，当前在dir2目录
	# cp ../dir3/log2 .
	
### 3.	将文件log2复制到目录/usr/local/src下，并改名为file1
	cp log2 /usr/local/src/file1

### 4.	将目录/etc目录下的所有文件及其子目录复制到目录dir2中
	cp -r /etc dir2
        -R, -r, --recursive copy directories recursively
### 5. 复制整个目录
	# cp -a dir3 dir2  
	-a, --archive same as -dR --preserve=all
        -d     same as --no-dereference --preserve=links
### 6. 为log1文件建立一个链接文件log_link.log
	# cp -s log1 log1_link

### 7. 若 ~/.bashrc 比 dir2/bashrc 新才复制过来
	# cp -u ~/.bashrc dir2/bashrc
	-u 是在目标文件与来源文件有差异时，才会复制的。
	
### 8. 拷贝目录下的隐藏文件如 .babelrc
	cp -r aaa/.* ./bbb
	将 aaa 目录下的，所有`.`开头的文件，复制到 bbb 目录中。

	cp -a aaa ./bbb/ 
	记住后面目录最好的'/' 带上 `-a` 参数
### 9. 将当前目录中的所有内容备份到/backup（假设该目录存在）目录下，并保持源文件的符号连接链接。
	由于要备份当前目录中的所有内容，当前目录下可能包含目录，因此应该开启-r选项，备份子目录下的所有内容。	
	同时要求保持源文件的链接，所以开启-a
	#	cp –iar . /backup
### 10. 备份当前目录下的一文件abc，到目录/backup/study目录中
	#	cp -i abc /backup/study
### 11.	备份链接文件，并保持源文件的属性和链接
	假设当前目录下存在一链接到一个目录的链接文件lndir，备份到/backup目录下并重命名为lndir.backup
	#	cp -iav lndir /bacup/lndir.backup
### 12.备份一文件到目标目录只保持其属主和访问权限属性
	假设当前目录下存在一文件abc，将其备份到目录/backup下并保持属主和访问权限
	#	cp -iv --preserve=mode,ownership abc /backu
