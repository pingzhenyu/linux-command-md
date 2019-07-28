## grep ##

强大的文本搜索工具

### 补充说明 ###

**grep** （global search regular expression(RE) and print out the line，全面搜索正则表达式并把行打印出来）是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。用于过滤/搜索的特定字符。可使用正则表达式能多种命令配合使用，使用上十分灵活。

grep的工作方式是这样的，它在一个或多个文件中搜索字符串模板。如果模板包括空格，则必须被引用，模板后的所有字符串被看作文件名。搜索的结果被送到标准输出，不影响原文件内容。

grep可用于shell脚本，因为grep通过返回一个状态值来说明搜索的状态，如果模板搜索成功，则返回0，如果搜索不成功，则返回1，如果搜索的文件不存在，则返回2。我们利用这些返回值就可进行一些自动化的文本处理工作。

###  语法

	cat(选项)(参数)

###  选项
	-a --text  # 不要忽略二进制数据。
	-A <显示行数>   --after-context=<显示行数>   # 除了显示符合范本样式的那一行之外，并显示该行之后的内容。
	-b --byte-offset                           # 在显示符合范本样式的那一行之外，并显示该行之前的内容。
	-B<显示行数>   --before-context=<显示行数>   # 除了显示符合样式的那一行之外，并显示该行之前的内容。
	-c --count    # 计算符合范本样式的列数。
	-C<显示行数> --context=<显示行数>或-<显示行数> # 除了显示符合范本样式的那一列之外，并显示该列之
                                                前后的内容。
	-d<进行动作> --directories=<动作>  # 当指定要查找的是目录而非文件时，必须使用这项参数，
                                        否则grep命令将回报信息并停止动作。
	-e<范本样式> --regexp=<范本样式>   # 指定字符串作为查找文件内容的范本样式。
	-E --extended-regexp             # 将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则
                                       表达式。
	-f<范本文件> --file=<规则文件>     # 指定范本文件，其内容有一个或多个范本样式，让grep查找符合范本
                                     条件的文件内容，格式为每一列的范本样式。
	-F --fixed-regexp   # 将范本样式视为固定字符串的列表。
	-G --basic-regexp   # 将范本样式视为普通的表示法来使用。
	-h --no-filename    # 在显示符合范本样式的那一列之前，不标示该列所属的文件名称。
	-H --with-filename  # 在显示符合范本样式的那一列之前，标示该列的文件名称。
	-i --ignore-case    # 忽略字符大小写的差别。
	-l --file-with-matches   # 列出文件内容符合指定的范本样式的文件名称。
	-L --files-without-match # 列出文件内容不符合指定的范本样式的文件名称。
	-n --line-number         # 在显示符合范本样式的那一列之前，标示出该列的编号。
	-q --quiet或--silent     # 不显示任何信息。
	-R/-r  --recursive       # 此参数的效果和指定“-d recurse”参数相同。
	-s --no-messages  # 不显示错误信息。
	-v --revert-match # 反转查找。
	-V --version      # 显示版本信息。   
	-w --word-regexp  # 只显示全字符合的列。
	-x --line-regexp  # 只显示全列符合的列。
	-y # 此参数效果跟“-i”相同。
	-o # 只输出文件中匹配到的部分。
	-m <num> --max-count=<num> # 找到num行结果后停止查找，用来限制匹配行数

### grep正则表达式元字符集


####	字符匹配：
	. ：匹配任意单个字符；
	[]：匹配指定范围内的任意单个字符；
	[^]：匹配指定范围外的任意单个字符；
	
	标准的字符类名称如下：
	[:alnum:] - 字母数字字符
	[:alpha:] - 字母字符
	[:digit:] - 数字: '0 1 2 3 4 5 6 7 8 9'
	[:lower:] - 小写字母: 'a b c d e f g h i j k l m n o p q r s t u v w x y z'
	[:upper:] - 大写字母: 'A B C D E F G H I J K L M N O P Q R S T U V W X Y Z'
	[:blank:] - 空字符: 空格键符 和 制表符
	[:space:] - 空格字符: 制表符、换行符、垂直制表符、换页符、回车符和空格键符
#### 匹配次数：
用在要指定其出现的次数的字符的后面，用于限制其前面字符出现的次数；默认工作于贪婪模式；

	*：匹配其前面的字符任意次；0,1,多次；
	.*：匹配任意长度的任意字符
	\?：匹配其前面的字符0次或1次；即其前面的字符是可有可无的；
	\+：匹配其前面的字符1次或多次；即其面的字符要出现至少1次；
	\{m\}：匹配其前面的字符m次；
	\{m,n\}：匹配其前面的字符至少m次，至多n次；
	\{0,n\}：至多n次
	\{m,\}：至少m次

#### 位置锚定：
	^：行首锚定；用于模式的最左侧；
	$：行尾锚定；用于模式的最右侧；
	^PATTERN$：用于PATTERN来匹配整行；
	^$：空白行；
	^[[:space:]]*$：空行或包含空白字符的行；
	\< 或 \b：词首锚定，用于单词模式的左侧；
	\> 或 \b：词尾锚定，用于单词模式的右侧；
	\<PATTERN\>：匹配完整单词；
	单词：非特殊字符组成的连续字符（字符串）都称为单词；

####  分组及引用
	\(\)：将一个或多个字符捆绑在一起，当作一个整体进行处理；
		    \(xy\)*ab
	Note：分组括号中的模式匹配 到的内容会被正则表达式引擎自动记录于内部的变量中，这些变量为：
	\1：模式从左侧起，第一个左括号以及与之匹配的右括号之间的模式所匹配到的字符；
	\2：模式从左侧起，第二个左括号以及与之匹配的右括号之间的模式所匹配到的字符；



###  grep命令常见用法
	在文件中搜索一个单词，命令会返回一个包含 “match_pattern” 的文本行：
	
	grep match_pattern file_name
	grep "match_pattern" file_name
	在多个文件中查找：
	
	grep "match_pattern" file_1 file_2 file_3 ...
	输出除之外的所有行 -v 选项：
	
	grep -v "match_pattern" file_name
	标记匹配颜色 --color=auto 选项：
	
	grep "match_pattern" file_name --color=auto
	使用正则表达式 -E 选项：
	
	grep -E "[1-9]+"
	# 或
	egrep "[1-9]+"
	只输出文件中匹配到的部分 -o 选项：
	
	echo this is a test line. | grep -o -E "[a-z]+\."
	line.
	
	echo this is a test line. | egrep -o "[a-z]+\."
	line.
	统计文件或者文本中包含匹配字符串的行数 -c 选项：
	
	grep -c "text" file_name
	输出包含匹配字符串的行数 -n 选项：
	
	grep "text" -n file_name
	# 或
	cat file_name | grep "text" -n
	
	#多个文件
	grep "text" -n file_1 file_2
	打印样式匹配所位于的字符或字节偏移：
	
	echo gun is not unix | grep -b -o "not"
	7:not
	#一行中字符串的字符便宜是从该行的第一个字符开始计算，起始值为0。选项  **-b -o**  一般总是配合使用。
	搜索多个文件并查找匹配文本在哪些文件中：
	
	grep -l "text" file1 file2 file3...
	grep递归搜索文件
	在多级目录中对文本进行递归搜索：
	
	grep "text" . -r -n
	# .表示当前目录。
	忽略匹配样式中的字符大小写：
	
	echo "hello world" | grep -i "HELLO"
	# hello
	选项 -e 制动多个匹配样式：
	
	echo this is a text line | grep -e "is" -e "line" -o
	is
	line
	
	#也可以使用 **-f** 选项来匹配多个样式，在样式文件中逐行写出需要匹配的字符。
	cat patfile
	aaa
	bbb
	
	echo aaa bbb ccc ddd eee | grep -f patfile -o
	在grep搜索结果中包括或者排除指定文件：
	
	# 只在目录中所有的.php和.html文件中递归搜索字符"main()"
	grep "main()" . -r --include *.{php,html}
	
	# 在搜索结果中排除所有README文件
	grep "main()" . -r --exclude "README"
	
	# 在搜索结果中排除filelist文件列表里的文件
	grep "main()" . -r --exclude-from filelist
	使用0值字节后缀的grep与xargs：
	
	# 测试文件：
	echo "aaa" > file1
	echo "bbb" > file2
	echo "aaa" > file3
	
	grep "aaa" file* -lZ | xargs -0 rm
	
	# 执行后会删除file1和file3，grep输出用-Z选项来指定以0值字节作为终结符文件名（\0），
     xargs -0 读取输入并用0值字节终结符分隔文件名，然后删除匹配文件，-Z通常和-l结合使用。
	

###  实例


### 1. 查找指定进程
	# ps -ef|grep uwsgi
	除最后一条记录外，其他的都是查找出的进程；最后一条记录结果是grep进程本身，并非真正要找的进程。

### 2. 查找指定进程时，不显示grep 本身进程
	# ps aux | grep uwsgi | grep -v "grep"
	# ps aux|grep [u]wsgi 
	# ps aux|grep /[u]wsgi 

### 3. 查找指定进程个数
	# ps -ef|grep uwsgi -c
	# ps -ef|grep -c uwsgi

### 4. 从文件中读取关键词进行搜索
	# cat 3.log | grep -f 4.log 

	# cat 3.log 
	1
	2
	3
	# cat 4.log 
	1
	12
	5
	43
	# cat 3.log | grep -f 4.log 
	1
	# cat 4.log | grep -f 3.log 
	1
	12
	43
	
	cat 3.log | grep -f 4.log 从3.log文件中匹配出含有4.log中关键字的行并输出
	cat 4.log | grep -f 3.log 从4.log文件中匹配出含有3.log中关键字的行并输出
	如：4.log中的关键字有1,12,5,43四个，在3.log中无论是完全匹配还是部分匹配只能匹配到1，并输出
	在 3.log中关键字为1,2,3, 所以在4.log中匹配3时，能完全匹配到含有1,2,3的行，并把匹配部分着色表示输出

### 5. 从文件中读取关键词进行搜索 且显示行号
	# cat 4.log | grep -nf 3.log
	输出4.log文件中含有从3.log 文件中读取出的关键词的内容行，并显示每一行的行号,冒号（:）左边是行号，右边是匹配的内容

### 6. 从文件中查找关键词
	# grep "1" 4.log 
	有无引号，或者单双引号 效果是一样的，但是加上引号可读性好一点。另外如果要查询带引号的内容，需要用\进行转义

### 7. 从多个文件中查找关键词
	# grep '1' 3.log 4.log 
	多文件时，输出查询到的信息内容行时，会把文件的命名放在在行的最左边输出并且加上":"作为标示符分隔，
	如果用了-n展示行号，则第二个：的左边是行号，最右边的是匹配内容

### 8.找出以1开头的行内容
	# cat 4.log |grep ^1
### 9.找出非1开头的行内容
	# cat 4.log |grep ^[^1]
### 10.找出以3结尾的行内容
	# cat 4.log |grep 3$
### 11.在当前目录中，查找后缀有 log 字样的文件中包含 1 字符串的文件，并打印出该字符串的行
	# grep 1 *log

### 12 . 以递归的方式查找符合条件的文件
	# grep -r 仅此一条 /home/hc
	查找指定目录/home/hc 及其子目录（如果存在子目录的话）下所有文件中包含字符串"仅此一条"的文件，
	并打印出该字符串所在行的内容


###  grep 查找源码

###  1. 递归查找并显示行号
这个是最基本的查找了。

grep -rn memcpy

在当前目录查找可以使用：
不指定目录：”grep -rn memcpy”
用”.“指定当前目录：”grep -rn memcpy .”
其实这两者查找结果一样，但在输出格式上是有区别的，具体留给你去比较好了。

###  2. 查找不区分大小写
grep -rni memcpy

选项”-i“或略大小写，这样除了匹配“memcpy”外，还可以匹配一些宏定义如”MEMCPY“和”Memcpy“等

###  3. 排除指定文件的搜索结果
搜索结果的第一列会显示搜索结果位于哪个文件中，所以可以通过对搜索结果第一列的过滤来排除指定文件。

例如：编译时生成的*.o.cmd文件中带了很多包含memcpy.h的行，如：

可以在搜索结果中用反向匹配”-v“排除*.o.cmd文件的匹配：

grep -rn memcpy | grep -v .o.cmd

如果想排除多个生成文件中的匹配，包括”*.o.cmd，*.s.cmd，*.o，*.map“等，有两种方式：

使用多个-v依次对上一次的结果进行反向匹配：

grep -rn memcpy | grep -v .o.cmd | grep -v .s.cmd | grep -v .o | grep -v .map

使用-Ev一次进行多个反向匹配搜索：
grep -rn memcpy | grep -Ev '\.o\.cmd|\.s\.cmd|\.o|\.map'

由于这里使用了正则表达式”-E“，所以需要用”\“将”.“字符进行转义

另外，也可以使用”--exclude=GLOB“来指定排除某些格式的文件，如不在“*.cmd”，“*.o”和“*.map”中搜索：

grep -rn --exclude=*.cmd --exclude=*.o --exclude=*.map memcpy

跟“--exclude=GLOB”类似的用法有“--include=GLOB”，从指定的文件中搜索，如只在“*.cmd”，“*.o”和“*.map”中搜索：

grep -rn --include=*.cmd --include=*.o --include=*.map memcpy

“--include=GLOB”在不确定某些函数是否被编译时特别有用。 
例如，不确定函数rpi_is_serial_active是否有被编译，那就查找“*.o”文件是否存在这个函数符号：

grep -rn --include=*.o rpi_is_serial_active

显然，从结果看，这个函数是参与了编译的，否则搜索结果为空。

如果想知道函数rpi_is_serial_active最后有没有被链接使用，查询生成的u-boot*文件就知道了：

grep -rn --include=u-boot* rpi_is_serial_active
Binary file out/rpi_3_32b/u-boot matches

可见u-boot文件中找到了这个函数符号。

###  4. 不在某些指定的目录查找memcpy
如果指定了u-boot编译的输出目录，例如输出到out，则可以直接忽略对out目录的搜索，如：

grep -rn --exclude-dir=out memcpy

忽略多个目录（“out”和“doc”）：

grep -rn --exclude-dir=out --exclude-dir=doc memcpy

###  5. 查找精确匹配结果
通常的“memcpy”查找结果中会有一些这样的匹配：“MCD_memcpy”，“zmemcpy”，“memcpyl”，“memcpy_16”等，如果只想精确匹配整个单词，则使用-w选项：

grep -rnw memcpy .

###  6. 查找作为单词分界的结果
“作为单次分界“这个表述不太准确，例如，希望“memcpy”的查找中，只匹配“MCD_memcpy”，“memcpy_16”，而不用匹配“zmemcpy”，“memcpyl”这样的结果，也就是memcpy以一个完整单词的形式出现。

一般这种查询就需要结合正则表达式了，用正则表达式去匹配单词边界，例如：

grep -rn -E "(\b|_)memcpy(\b|_)"

关于正则表达式“(\b|_)memcpy(\b|_)”

“\b“匹配单词边界
“_“匹配单个下滑下
所以上面的表达式可以匹配：memcpy，memcpy_xxx，xxx_memcpy和xxx_memcpy_xxx等模式。（可能匹配的还有函数memcpy_，_memcpy和_memcpy_）

###  7. 查看查找结果的上下文
想在结果中查看匹配内容的前后几行信息，例如想看宏定义“MEMCPY”匹配的前三行和后两行：

ygu@guyongqiangx:u-boot-2016.09$ grep -rn -B 3 -A 2 MEMCPY
1
选项B/A： 
-B 指定显示匹配前（Before）的行数 
-A 指定显示匹配后（After）的行数

###  8. grep和find配合进行查找
find针是对文件级别的粗粒度查找，而grep则对文件内容的细粒度搜索。 
所以grep跟find命令配合，用grep在find的结果中进行搜索，能发挥更大的作用，也更方便。

例如，我想查找所有makefile类文件中对CFLAGS的设置。 
makefile类常见文件包括makefile，*.mk，*.inc等，而且文件名还可能是大写的。

可以通过find命令先找出makefile类文件，然后再从结果中搜索CFLAGS：

ygu@guyongqiangx:u-boot-2016.09$ find . -iname Makefile -o -iname *.inc -o -iname *.mk | xargs grep -rn CFLAGS
1
这里由于涉及到find命令，所以整个查找看起来有点复杂了，也可以只用grep的--include=GLOB选项来实现：

ygu@guyongqiangx:u-boot-2016.09$ grep -rn --include=Makefile --include=*.inc --include=*.mk CFLAGS .
1
比较上面的两个搜索结果，是一样的，但是有一点要注意：

grep命令的--include=GLOB模式下，文件名是区分大小写的，而且没有方式指定忽略文件名大小写
刚好这里搜索的Makefile只有首字母大写的形式，而不存在小写的makefile，所以这里碰巧是结果一致而已，否则需要指定更多的--include=GLOB参数。
