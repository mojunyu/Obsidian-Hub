**安全停止一个正在运行的 Flink CDC 同步作业，并创建一个 Savepoint，以便后续可以从该断点精确恢复作业，确保数据不丢失、不重复。**


```bash

# 优雅地停止一个正在运行的 Flink 作业
# 并在停止前为它创建一个 Savepoint
# Savepoint存储路径：/opt/app/flink-1.20.1/savepoints
# 1e224732a96d1c0fde7af365db299fca 是Flink 作业的 Job ID
sudo /opt/app/flink-1.20.1/bin/flink stop -p /opt/app/flink-1.20.1/savepoints 1e224732a96d1c0fde7af365db299fca

# 使用 Flink CDC 从指定的 Savepoint 恢复一个数据同步作业
sudo -E bash -c "/opt/app/flink-cdc-3.5.0/bin/flink-cdc.sh  /opt/app/flink-cdc-3.5.0/conf/mysql-to-starrocks-stat.yaml  --jar=/opt/app/flink-1.20.1/lib/mysql-connector-java-8.0.27.jar  -s file:///opt/app/flink-1.20.1/savepoints/savepoint-文件名称"


# 执行 生成 快照 id ：savepoint-1e2247-e91c5201503d
sudo /opt/app/flink-1.20.1/bin/flink stop -p /opt/app/flink-1.20.1/savepoints 1e224732a96d1c0fde7af365db299fca

Suspending job "1e224732a96d1c0fde7af365db299fca" with a CANONICAL savepoint.
Triggering stop-with-savepoint for job 1e224732a96d1c0fde7af365db299fca.
Waiting for response...
Savepoint completed. Path: file:/opt/app/flink-1.20.1/savepoints/savepoint-1e2247-e91c5201503d


sudo -E bash -c "/opt/app/flink-cdc-3.5.0/bin/flink-cdc.sh  /opt/app/flink-cdc-3.5.0/conf/mysql-to-starrocks-stat.yaml  --jar=/opt/app/flink-1.20.1/lib/mysql-connector-java-8.0.27.jar  -s file:///opt/app/flink-1.20.1/savepoints/savepoint-1e2247-e91c5201503d"


```



```bash
# 增加表 
1. 直接加 
2. 如果starrock没有自动增加表，需要手动重启flink 
3. sudo /opt/app/flink-1.20.1/bin/flink stop -p /opt/app/flink-1.20.1/savepoints [job id] 
4. sudo -E bash -c "/opt/app/flink-cdc-3.5.0/bin/flink-cdc.sh /opt/app/flink-cdc-3.5.0/conf/mysql-to-starrocks-muttable.yaml --jar=/opt/app/flink-1.20.1/lib/mysql-connector-java-8.0.27.jar -s [file:///opt/app/flink-1.20.1/savepoints/savepoint-](file:///opt/app/flink-1.20.1/savepoints/savepoint-)文件名称"

# 增加字段
1. 直接加字段，但是不能写after！！

# 删除字段
1. 暂停flink job： sudo /opt/app/flink-1.20.1/bin/flink stop -p /opt/app/flink-1.20.1/savepoints [job id],会生成一个savepoint文件 
2. 在mysql和starrock中执行 ```ALTER TABLE `ad_agent` ADD `test1` INT NOT NULL;``` 
3. sudo -E bash -c "/opt/app/flink-cdc-3.5.0/bin/flink-cdc.sh /opt/app/flink-cdc-3.5.0/conf/mysql-to-starrocks-muttable.yaml --jar=/opt/app/flink-1.20.1/lib/mysql-connector-java-8.0.27.jar -s [file:///opt/app/flink-1.20.1/savepoints/savepoint-](file:///opt/app/flink-1.20.1/savepoints/savepoint-)文件名称"



```