# doris-docker-compose
deploy doris using docker-compose for dev


# quick start

## download doris
```bash
wget https://dist.apache.org/repos/dist/release/doris/要部署的版本
# 例如如下链接
wget https://dist.apache.org/repos/dist/release/doris/1.0/1.0.0-incubating/apache-doris-1.0.0-incubating-bin.tar.gz
```

如果用了其他版本，请自行修改 Dockerfile

## compose up
```bash
docker-compose up -d
```

## config be
connect doris use mysql client

default user is  root
password is empty


check backends config, is empty 
```sql
SHOW PROC '/backends';
```


config backends
```sql
ALTER SYSTEM ADD BACKEND "doris-docker-compose_doris-be_1:9050";
ALTER SYSTEM ADD BACKEND "doris-docker-compose_doris-be_2:9050";
ALTER SYSTEM ADD BACKEND "doris-docker-compose_doris-be_3:9050";
```

check backends config again, backends Alive value should be ture
```sql
SHOW PROC '/backends';
```

test sql
```sql
create database if not exists testdb;
drop table if exists testdb.test_table;
create table if not exists testdb.test_table(
       name varchar(100),
       value float
)
ENGINE=olap
UNIQUE KEY(name)
DISTRIBUTED BY HASH(name);

insert into testdb.test_table values ("nick", 1), ("nick2", 3);
select * from testdb.test_table;
```

## restart
因为 doris 使用文件存储 backends 的 ip 信息， docker-compose restart 后，可能会导致 backends ip 发生变化，导致 fe 启动失败。
可以清除 volume 数据，再重启即可

clear volume
```bash
docker-compose down -v
```

restart 
```bash
docker-compose up -d
```

Note: 因为数据会被清除，本项目 only for dev 