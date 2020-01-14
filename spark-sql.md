# Spark SQL

SQL on Hadoop

Spark SQL as a distributed SQL engine.

{% embed url="https://spark.apache.org/docs/latest/sql-distributed-sql-engine.html" %}

Thrift JDBC/ODBC server根据HiveServer2实现。所以连接字符串也是一套规范。

```text
jdbc:hive2://localhost:10002/default;httpPath=/;principal=hive/hdp-team.example.com@EXAMPLE.COM
```



### 本地开发环境

#### Hadoop

```text
# 参考文档配置一个伪集群
# https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html#Pseudo-Distributed_Operation


# hdfs(namenode, datanode)启停
# NameNode - http://localhost:9870/

sbin/start-dfs.sh
sbin/stop-dfs.sh

# yarn(resourcemanager, nodemanager)启停
# ResourceManager - http://localhost:8088/

sbin/start-yarn.sh
sbin/stop-yarn.sh

# 合并脚本
sbin/start-all.sh
sbin/stop-all.sh
```

#### Hive

```text
# 参考文档启动JDBC服务
# https://cwiki.apache.org/confluence/display/Hive/GettingStarted

bin/schematool -dbType derby -initSchema

$HIVE_HOME/bin/hiveserver2
# Hive Session ID = N次出现后，才能被beeline连接。

$HIVE_HOME/bin/beeline -n jiahua -u jdbc:hive2://localhost:10000

```

python通过JDBC连接hiveserver2

```text
# 依赖包安装
pip install thrift_sasl
pip install pyhive

# 参考sqlalchemy的SQL方言支持
# https://docs.sqlalchemy.org/en/13/dialects/
```

MapReduce太慢了！一个COUNT花了好久，都要超时了。

Spark SQL thriftserver（目前碰到了不少问题，可能需要试试Impala）

Spark SQL就用它来清洗数据吧。

```text
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop

# 与Hive集成
# hive metastore server
$HIVE_HOME/bin/hive --service metastore
# 会读取本地的metastore_db文件夹。

# 启停thriftserver
$SPARK_HOME/sbin/start-thriftserver.sh \
  --master yarn
$SPARK_HOME/sbin/stop-thriftserver.sh

# beeline
$SPARK_HOME/bin/beeline -n jiahua -u jdbc:hive2://localhost:10000

CREATE TABLE movielens (
  userid INT,
  movieid INT,
  rating INT,
  unixtime STRING)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
STORED AS TEXTFILE;

LOAD DATA LOCAL INPATH '/Users/jiahua/opt/hive/ml-100k/u.data'
OVERWRITE INTO TABLE movielens;



```

