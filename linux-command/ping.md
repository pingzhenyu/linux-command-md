## ping ##

测试主机之间网络的连通性

### 补充说明 ###

**ping命令** 用来测试主机之间网络的连通性。执行ping指令会使用ICMP传输协议，发出要求回应的信息，若远端主机的网络功能没有问题，就会回应该信息，因而得知该主机运作正常。

###  语法

	ping(选项)(参数)

###  选项

	-d：使用Socket的SO_DEBUG功能；
	-c<完成次数>：设置完成要求回应的次数；
	-f：极限检测；
	-i<间隔秒数>：指定收发信息的间隔时间；
	-I<网络界面>：使用指定的网络界面送出数据包；
	-l<前置载入>：设置在送出要求信息之前，先行发出的数据包；
	-n：只输出数值；
	-p<范本样式>：设置填满数据包的范本样式；
	-q：不显示指令执行过程，开头和结尾的相关信息除外；
	-r：忽略普通的Routing Table，直接将数据包送到远端主机上；
	-R：记录路由过程；
	-s<数据包大小>：设置数据包的大小；
	-t<存活数值>：设置存活数值TTL的大小；
	-v：详细显示指令的执行过程。




###  实例

### 1.	查看www.google.cn连通性。
	
	#	ping www.google.cn
	PING www.google.cn (203.208.41.144) 56(84) bytes of data.
	64 bytes from 203.208.41.144: icmp_req=1 ttl=55 time=34.0 ms
	64 bytes from 203.208.41.144: icmp_req=2 ttl=55 time=35.3 ms

### 2.	查看网关的连通性，网关ip地址为192.168.1.1。
	#	ping 192.168.1.1
	PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
	64 bytes from 192.168.1.1: icmp_req=1 ttl=64 time=1.88 ms
	64 bytes from 192.168.1.1: icmp_req=2 ttl=64 time=11.3 ms
	64 bytes from 192.168.1.1: icmp_req=3 ttl=64 time=1.66 ms
	64 bytes from 192.168.1.1: icmp_req=4 ttl=64 time=5.46 ms
