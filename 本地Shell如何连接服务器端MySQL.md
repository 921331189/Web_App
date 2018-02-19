# 将 Python、服务器端的 MySQL 编码格式都改为 utf8
1. 本地：在/usr/lib/python2.7/site-packages/目录下添加一个sitecustomize.py文件，内容如下：
	import sys
	sys.setdefaultencoding('utf-8')
	
2. 登录 DMS 的命令窗口，输入：
	show variables like '%character%';  # 你会看到一堆 gbk
	set names 'utf8';   # 同时设置character_set_client，character_set_connection,character_set_results的编码
	alter database hdm334229313_db character set utf8;   # hdm334229313_db是我的数据库名字；设置数据库编码
	
	但 character_set_server 的编码还是 gbk
	
3. 由于阿里云虚拟主机 Linux 系统的 MySQL 版本是 5.1.73，而某个解决方案说：
		[  服务器端默认字符集设置，在[mysqld]下面添加： 
		5.5.19版本的是：  character_set_server 
		之前的版本的是：  default-character-set  ]

# 测试连接
1. 已将 db.py 中 create_engine 函数参数设为：
host='hyu4095090001.my3w.com',port=3306,user='hdm334229313',password='··········',database='hdm334229313_db'
所以之后所有涉及连接服务器参数的地方都不用填了！

2. 注：db.py最后有个测试代码，即创建一个表：包含条目（id， name, email, passwd, last_modified）

3. 第一种玩法：
在 Shell 中进入 db.py 所在的文件夹 C:\Python27\Scripts\projects\blog-python-app-master\www\transwarp
打开 Python 交互界面
输入 import db

4. 第二种玩法，利用 db.py 最后的测试代码：
进入 db.py 所在的文件夹 C:\Python27\Scripts\projects\blog-python-app-master\www\transwarp
输入 python db.py
