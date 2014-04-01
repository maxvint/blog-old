###安装和启动redis
####下载安装
windows下安装下载地址：<https://github.com/mythz/redis-windows>，下载后解压即可，例如	`G:\redis`。
解压后有以下几个文件：
* redis-server.exe：服务程序
* redis-check-dump.exe：本地数据库检查
* redis-check-aof.exe：更新日志检查
* redis-benchmark.exe：性能测试，用以模拟同时由N个客户端发送M个 SETs/GETs 查询

####运行redis
启动redis服务：

	G:\redis>
	$ redis-server.exe redis.conf

设置客户端：

	G:\redis>
	$ redis-cli.exe -h 127.0.0.1 -p 6379

####测试一下

	$ ./redis-cli set mykey somevalue
	OK
	$ ./redis-cli get mykey
	somevalue

性能测试

	G:\redis>redis-benchmark.exe -h 127.0.0.1 -p 6379 -n 100000 -c 50

####redis管理工具
推荐一个redis的管理工具：phpRedisAdmin:<https://github.com/ErikDubbelboer/phpRedisAdmin>，用过phpMyAdmin的人懂得（需要安装php的redis扩展）。

###安装php_redis扩展
下载对应的php_redis扩展包，放到php的ext目录，再在php.ini中增加

	extension=php_redis.dll

重启apache或者iis查看phpinfo中是否有redis扩展信息。

####php-redis测试

	<?php
		$redis = new Redis();                   //redis对象
		$redis->connect('192.168.60.6', '6379'); //连接redis服务器
		$redis->set('test', 'Hello World');      //set字符串值
		echo $redis->get('test');               //获取值
	?>

###redis+mysql实现缓存写入



