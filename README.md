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
	
# hadoop命令
	# 更改所有者
	sudo -u hdfs hadoop fs -chown root /user/hive/warehouse/path_to_file
	# 删除目录或文件
	hadoop fs -rm -r -skipTrash /path_to_file/file_name
