# 修改postgre的配置文件.conf
--需要重新启动postgresql

    关闭正在运行的 PostgreSQL 服务器。您可以使用以下命令来停止服务器：

sudo systemctl stop postgresql

这是针对使用 systemd 的 Linux 发行版的命令。如果您使用其他初始化系统，请使用适当的命令来停止 PostgreSQL 服务器。

    启动 PostgreSQL 服务器。使用以下命令来启动服务器：

sudo systemctl start postgresql

同样，这是针对使用 systemd 的 Linux 发行版的命令。如果您使用其他初始化系统，请使用适当的命令来启动 PostgreSQL 服务器。

    验证服务器是否成功启动。您可以使用以下命令来检查 PostgreSQL 服务器的状态：

sudo systemctl status postgresql

如果服务器成功启动，并且没有显示任何错误信息，那么您的新配置已经生效。

请注意，重启 PostgreSQL 服务器将中断正在进行的连接和事务。在执行重启操作之前，请确保没有重要的操作正在进行，并通知相关的用户和应用程序。

 ```
sudo su - postgres  #登陆到postgres(没有设置密码)
[sudo] password for tempo:
postgres@vm172-31-6-252:~$ psql
psql (14.9 (Ubuntu 14.9-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# \q    #退出postgres
# 创建新postgres用户和创建新数据库
postgres@vm172-31-6-252:~$ psql
psql (14.9 (Ubuntu 14.9-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# create user monitor with password 'monitor';  # 创建新用户'monitor'
CREATE ROLE

postgres=# create database monitorDB;  # 创建新表monitorDB
CREATE DATABASE
postgres=# grant all privileges on database monitorDB to monitor; # 授权
GRANT
postgres=# grant all privileges on all tables in schema public to monitor;  # 授权读写权限
GRANT
postgres=# \q
```
如果要单独一个权限以及单独一个表，则：`GRANT SELECT ON TABLE mytable TO testUser;`
```
postgres=# create user tempo with password 'tempo';  # 创建新用户'tempo'
CREATE ROLE
postgres=# grant all privileges on database monitorDB to tempo; # 授权
GRANT
```


查看所用用户及权限:
```
postgres@shortman:~$ psql
psql (14.9 (Ubuntu 14.9-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# \du
```

查看用户的所有库:
```
postgres@shortman:~$ psql
psql (14.9 (Ubuntu 14.9-0ubuntu0.22.04.1))
Type "help" for help.

postgres=# \l+
```
切换数据库
```
postgres=# \c exampledb
```
查看表
```
postgres=# \d
```
查看表结构
```
postgres=# \d user_tab1
```

查看表的内容
```
查询pg_tables表获取当前数据库中所有表的信息（pg_tables是系统视图）

select * from pg_tables

通常我们只关注public中的表，只需要加上以下查询条件即可

select tablename from pg_tables where schemaname='public'

```

常用控制台命令

\password           设置密码。
\q                  退出。
\h                  查看SQL命令的解释，比如\h select。
\?                  查看psql命令列表。
\l                  列出所有数据库。
\c [database_name]  连接其他数据库。
\d                  列出当前数据库的所有表格。
\d [table_name]     列出某一张表格的结构。
\du                 列出所有用户。
\e                  打开文本编辑器。
\conninfo           列出当前数据库和连接的信息。


### 设置idle_session_timeout
1. 查看该参数说明：
```sql
postgres=# select * from pg_settings where name = 'idle_session_timeout' \gx
```
出现的错误：
1.port 5432 failed: FATAL:  remaining connection slots are reserved for non-replication superuser connections
解决：


### 查看表的前10条：select * from shortman_tableinfo limit 10;
### 查看表的后10条：SELECT * FROM table_name ORDER BY column_name DESC LIMIT 10;
例如，假设有一个名为 `posts` 的表，其中包含 id、title 和 created_at 列，您可以使用以下查询来获取最新 10 条记录的 title 和 created_at 列数据：
sql

SELECT title, created_at FROM posts ORDER BY created_at DESC LIMIT 10;
### 查看表的所有行数：
要查看 PostgreSQL 数据库表中的行数，您可以使用以下查询：
sql

SELECT COUNT(*) FROM table_name;

在上面的查询语句中，将 table_name 替换为要查询的实际表名。这将返回表中的总行数。

例如，如果您要查看名为 users 的表的行数，可以执行以下查询：
sql

SELECT COUNT(*) FROM users;

### 删除表中的id范围的内容
DELETE FROM shortman_serverinfo
WHERE id BETWEEN 1 AND 36;


迁移数据：
INSERT INTO 目标表明 (time, guest, guest_nice, idle, iowait, irq, nice, softirq, steal, system, total_active, total_idle, "user", percent, free_physics, free_swap, processes, total_physics, total_swap, uptime, used_physics, used_swap, swap_percent, memory_percent, free, mount_point, total, used, disk_percent, name_id)
SELECT time, guest, guest_nice, idle, iowait, irq, nice, softirq, steal, system, total_active, total_idle, "user", percent, free_physics, free_swap, processes, total_physics, total_swap, uptime, used_physics, used_swap, swap_percent, memory_percent, free, mount_point, total, used, disk_percent, name_id
FROM 原表;
LIMIT 1000 OFFSET 1000;


删除指定列：
ALTER TABLE 待删除列的表名
DROP COLUMN guest,
DROP COLUMN guest_nice,
DROP COLUMN idle,
DROP COLUMN iowait,
DROP COLUMN irq,
DROP COLUMN nice,
DROP COLUMN softirq,
DROP COLUMN steal,
DROP COLUMN system,
DROP COLUMN total_active,
DROP COLUMN total_idle,
DROP COLUMN "user",
DROP COLUMN free_physics,
DROP COLUMN free_swap,
DROP COLUMN processes,
DROP COLUMN total_physics,
DROP COLUMN total_swap,
DROP COLUMN uptime,
DROP COLUMN used_physics,
DROP COLUMN used_swap,
DROP COLUMN swap_percent,
DROP COLUMN free,
DROP COLUMN mount_point,
DROP COLUMN total,
DROP COLUMN used;

## 查看数据库中所有表的行数：
SELECT n.nspname, c.relname, c.reltuples
FROM pg_class c
JOIN pg_namespace n ON n.oid = c.relnamespace
WHERE c.relkind = 'r';
在这个查询中：

    n.nspname 是模式的名称（在这个例子中，我们假设模式是monitordb）。
    c.relname 是表的名称。
    c.reltuples 是表中行的估计数量。这个值是由PostgreSQL的统计信息收集器估算的，通常通过执行ANALYZE命令来更新。请注意，这个值可能不是实时准确的，特别是在有大量数据变动的表上。
    ::BIGINT 是一个类型转换操作，将reltuples的值从它的原生类型（通常是整数）转换为BIGINT类型，以确保我们可以处理非常大的数字
