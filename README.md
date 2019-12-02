# Hive
	hive --service metastore &
	hive --service hiveserver2 &

##### 建外部表
	create external table if not exists studenttable(
	name string comment 'name value',
	sex string comment 'sex value',
	age string comment 'age value')
	row format delimited
	fields terminated by '\t'
	lines terminated by '\n'
	stored as textfile;

##### 加载数据
	load data local inpath '/data/hive/test/data.txt' into table studenttable;

##### 插入数据
	insert into studenttable(name,sex,age) values('Jack','0','20');

# 分区表
	# 创建一个分区表，分区的单位时dt和国家名
	create table logs(ts bigint,line string) partitioned by (dt String,country string) row format delimited fields terminated by '\t' lines terminated by '\n';
	
	# 加载数据
	load data local inpath '/root/hive/file1.txt' into table logs partition (dt='2019-12-01',country='GB');
	load data local inpath '/root/hive/file2.txt' into table logs partition (dt='2019-12-01',country='GB');
	load data local inpath '/root/hive/file3.txt' into table logs partition (dt='2019-12-01',country='US');
	load data local inpath '/root/hive/file4.txt' into table logs partition (dt='2019-12-02',country='GB');
	load data local inpath '/root/hive/file5.txt' into table logs partition (dt='2019-12-02',country='US');
	load data local inpath '/root/hive/file6.txt' into table logs partition (dt='2019-12-02',country='US');
	
	# 查看分区结构
	show partitions logs;
	
	# 条件查询
	select ts,dt,line,country from logs where country='GB';
	select ts,dt,line,country from logs where dt='2019-12-02' and country='US';

# hadoop命令
	# 更改所有者
	sudo -u hdfs hadoop fs -chown root /user/hive/warehouse/path_to_file
	# 删除目录或文件
	hadoop fs -rm -r -skipTrash /path_to_file/file_name
