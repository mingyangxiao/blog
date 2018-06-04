---
layout: post
title: MySQL使用frm及ibd文件恢复表结构和数据
excerpt: MySQL使用frm及ibd文件恢复表结构和数据
tags: MySQL 运维
---

> 本方法仅适用于启用了 innodb_file_per_table = 1 (独立表空间)的数据库

> 恢复所用数据库版本尽可能与原数据库版本保持一致

假设待恢复的文件为 demo.frm demo.ibd

1. 创建临时数据库 test
2. 创建表demo(与demo.frm保持一致), 添加任意字段(在不知道原表字段情况下)
3. 停止服务，使用demo.frm覆盖掉test数据库中的demo.frm
4. 在[mysqld]项下增加以下参数innodb_force_recovery=6，启动服务
5. 查看表结构，此时会提示 Table 'test2.attachment' doesn't exist 
6. 查看日志会发现 `[Warning] InnoDB: table test/demo contains 1 user defined columns in InnoDB, but 9 columns in MySQL.` 提示，即表中有9列数据，但我们只定义了一列
7. 注释innodb_force_recovery=6，重启服务
8. 重建demo表，任意添加9个字段
9. 重复步骤4，此时已能查看表结构，导出表定义语句
10. 重复步骤7，删除demo表，使用导出的表定义重建
11. 卸载表空间 `alter table demo discard tablespace;`,停止服务 
12. 使用demo.idb覆盖test数据库中demo.idb，启动服务
13. 关联表空间 `alter table variety import tablespace;`


