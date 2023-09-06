---
title: mysql库表备份与恢复
date: 2023-09-06 16:00:11
categories:
- MySQL
tags:
- MySQL
- backup
---

### 执行环境

Centos7.9

MySQL

## 备份



```mysql
mysqldump -uroot -p'dream' -h 127.0.0.1 -P 3306 \
    --routines --events --triggers --no-data \
    --add-drop-database --add-drop-table --all-databases \
    > backup.sql
```

`mysqldump`命令有很多其他参数，可以根据需要进行使用。以下是一些常用的参数：

- `-h` 或 `--host`：指定要连接的MySQL服务器的主机名或IP地址。
- `-P` 或 `--port`：指定要连接的MySQL服务器的端口号。
- `-u` 或 `--user`：指定要连接的MySQL服务器的用户名。
- `-p` 或 `--password`：指定要连接的MySQL服务器的密码。注意，在指定密码时，不要在参数后面留有空格，否则可能导致密码不被正确识别。
- `--databases`：指定要备份的多个数据库，使用空格分隔。
- `--tables`：指定要备份的特定表，使用逗号分隔。
- `--single-transaction`：在备份过程中使用单个事务，以确保数据的一致性。
- `--lock-tables`：在备份过程中锁定所有要备份的表，以确保数据的一致性。
- `--no-create-db`：在备份过程中不包括创建数据库的语句。
- `--no-create-info`：在备份过程中不包括创建表的语句。
- `--add-drop-database`：在备份过程中包括删除数据库的语句。
- `--add-drop-table`：在备份过程中包括删除表的语句。
- `--compress`：在备份过程中使用压缩来减小备份文件的大小。
- `--verbose`：在备份过程中显示详细的输出信息。
- `--routines`：导出备份时包括存储过程。
- `--events`：导出备份时包括事件。
- `--triggers`：导出备份时包括触发器。
- `--no-data`：导出备份时不包括实际数据，只包括数据库结构。

这只是一小部分常用的`mysqldump`参数，可以通过查阅`mysqldump`的官方文档或使用`mysqldump --help`命令来获取更多详细的参数信息。

## 恢复

执行导出的备份sql文件

```
mysql -uroot -pdream < backup.sql
```

