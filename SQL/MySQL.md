[toc]

### 列的数据类型

![avatar](D:/其他/图片/study/列的数据类型-数值.png)

![avatar](D:/其他/图片/study/列的数据类型-字符串.png)

![avatar](D:/其他/图片/study/列的数据类型-时间.png)

### 建表规范

![avatar](D:/其他/图片/study/建表规范.png)


### 数据库引擎

- InnoDB ：默认使用，安全性高，事务处理，多表多用户操作
- MyISAM ：早些年使用，节约空间，速度较快


- | MyISAM | InnoDB
--- | ---|---
事务支持 | 不支持 | 支持
数据行锁定 | 不支持【是表锁定】 | 支持
外键约束 | 不支持 | 支持
全文索引 | 支持 | 不支持
表空间的大小 | 较小 | 较大，约是2倍


### TRUNCATE命令

完全清空一个数据库表，表的结构和索引约束不会变


```
--清空student表
TRUNCATE 'student'
```

> delete VS TRUNCATE

- 相同点：都能删除数据，且不会删除表结构
- 不同：
  - TRUNCATE 重新设置自增列，计数器会归零
  - TRUNCATE 不会影响事务

### distinct关键字

- 去重

去除查询结果中重复的数据，重复的多条数据只显示一条


### 模糊查询、联表查询join..on  自连接、分页、函数、分组 过滤

![avatar](D:/其他/图片/study/select语法.png)

### MD5加密

MD5('123456')

> 保存加密后的密码，验证密码时，同加密后的验证对象进行比较即可


### 事务

**ACID原则**

- 原子性（Atomicity）
  - 要么都成功，要么都失败
- 一致性（Consistency）
  - 事务前后数据完整性一致
- 持久性（Durability）
  - 事务一旦提交则不可逆，被持久化到数据库中
- 隔离性（Isolation）
  - 多个用户并发访问数据库时，多个事务相互隔离，互不干扰


> 隔离所导致的一些问题：

脏读、不可重复读、幻读（虚读）

> 模拟转账


```
set autocommit = 0;  --关闭自动提交
start transaction    --开启一个事务

update account set .. where ..
update account set .. where ..

commit;             --提交事务，持久化到数据库
rollback;           --回滚

set autocommit = 0;  --恢复默认值

```

### 索引

> 这块内容比较多，《面试常问.md中有相关笔记》

> [参考好文](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)

定义：**索引（Index）是帮助MySQL高效获取数据的数据结构**

- 主键索引
- 唯一索引
- 常规索引
- 全文索引

索引在小数据量的时候，用处不大，但在大数据量时，区别十分明显~

> 索引原则

- 索引不是越多越好
- 不要对经常变动的数据加索引
- 小数据量的表不需要额外加索引
- 索引一般加在常用来查询的字段上

### 三大范式

- 第一范式（1NF）
  - 原子性：保证每一列不可再分
- 第二范式（2NF）
  - 前提：满足第一范式
  - 每张表只描述一件事情
- 第三范式（3NF）
  - 前提：满足第一范式 和 第二范式
  - 需要确保数据表中每一列数据都和主键直接相关，而不能间接相关

> 规范性 VS 性能

**关联查询的表不得超过三张**

- 如：
  - 故意增加冗余字段--》从多表查询变为单表查询
  - 故意增加一些计算列--》降低查询时的数据量

