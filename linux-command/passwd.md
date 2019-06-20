## passwd ##

用来更改使用者的密码

### 补充说明 ###

**passwd命令** 用于设置用户的认证信息，包括用户密码、密码过期时间等。系统管理者则能用它管理系统用户的密码。只有管理者可以指定用户名称，一般用户只能变更自己的密码。


###  语法

	passwd(选项)(参数)

###  选项

	-d：删除密码，仅有系统管理者才能使用；
	-f：强制执行；
	-k：设置只有在密码过期失效后，方能更新；
	-l：锁住密码；
	-s：列出密码的相关信息，仅有系统管理者才能使用；
	-u：解开已上锁的帐号。

###  参数 

- 用户：组：指定所有者和所属工作组。当省略“：组”，仅改变文件所有者；
- 文件：指定要改变所有者和工作组的文件列表。支持多个文件和目标，支持shell通配符。


###  知识扩展

与用户、组账户信息相关的文件

存放用户信息：


/etc/passwd
/etc/shadow


存放组信息：


/etc/group
/etc/gshadow


用户信息文件分析（每项用`:`隔开）


例如：jack:X:503:504:::/home/jack/:/bin/bash
jack　　# 用户名
X　　# 口令、密码
503　　# 用户id（0代表root、普通新建用户从500开始）
504　　# 所在组
:　　# 描述
/home/jack/　　# 用户主目录
/bin/bash　　# 用户缺省Shell


组信息文件分析


例如：jack:$!$:???:13801:0:99999:7:*:*:
jack　　# 组名
$!$　　# 被加密的口令
13801　　# 创建日期与今天相隔的天数
0　　# 口令最短位数
99999　　# 用户口令
7　　# 到7天时提醒
*　　# 禁用天数
*　　# 过期天数


###  实例

### 1.	设置当前用户的密码
	#	passwd 
	系统会先提示输入当前密码，再提示输入新密码和确认输入，如果两次输入均无误，则密码设置成功。
    如果密码过于简单，系统会出错返回。

### 2.	设置指定用户的密码（此功能仅适用于超级用户）
	#	passwd testuser
	系统无需验证指定用户的当前密码而直接提示输入新密码，然后确认输入。输入无误后则密码设置成功。

### 3.	查看用户testuser的密码状态（此功能仅适用于超级用户）
	#	passwd -S testuser
	则系统显示出用户testuser的密码状态，其中“MD5 crypt”表示经过MD5加密。

### 4.锁定指定用户账户（此功能仅适用于超级用户）
	#	Passwd -l testuser
	这样用户toplinux就被锁定而失效。

### 5.	对锁定的用户账户进行解锁（此功能仅适用于超级用户）
	#	Passwd -u testuser
	用户testuser被解锁重新激活。



### 6. 如果是普通用户执行passwd只能修改自己的密码。如果新建用户后，要为新用户创建密码，则用passwd用户名，注意要以root用户的权限来创建。
	
	
	# passwd linuxde     # 更改或创建linuxde用户的密码；
	Changing password for user linuxde.
	New UNIX password:           # 请输入新密码；
	Retype new UNIX password:    # 再输入一次；
	passwd: all authentication tokens updated successfully.  # 成功；


### 7. 普通用户如果想更改自己的密码，直接运行passwd即可，比如当前操作的用户是linuxde。

	
	$ passwd
	Changing password for user linuxde.  # 更改linuxde用户的密码；
	(current) UNIX password:    # 请输入当前密码；
	New UNIX password:          # 请输入新密码；
	Retype new UNIX password:   # 确认新密码；
	passwd: all authentication tokens updated successfully.  # 更改成功；
	
	
	比如我们让某个用户不能修改密码，可以用`-l`选项来锁定：
	
	
	# passwd -l linuxde     # 锁定用户linuxde不能更改密码；
	Locking password for user linuxde.
	passwd: Success            # 锁定成功；
	
	# su linuxde    # 通过su切换到linuxde用户；
	$ passwd       # linuxde来更改密码；
	Changing password for user linuxde.
	Changing password for linuxde
	(current) UNIX password:           # 输入linuxde的当前密码；
	passwd: Authentication token manipulation error      # 失败，不能更改密码；

	
	
	# passwd -d linuxde   # 清除linuxde用户密码；
	Removing password for user linuxde.
	passwd: Success                          # 清除成功；
	
	# passwd -S linuxde     # 查询linuxde用户密码状态；
	Empty password.                          # 空密码，也就是没有密码；

