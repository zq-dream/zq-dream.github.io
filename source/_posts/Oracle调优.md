---
title: Oracle调优
date: 2022-05-25 14:02:45
categories:
- 性能调优
tags:
- Oracle
---
# Oracle技能增强培训

## 高频inseter优化
使用hash分区表

## 联合索引
对重复索引的优化

## 外键字段无索引
非必要情况不要使用外键
优化方案：
- 在外键字段上建索引
如果满足以下三个条件，则不用建索引
- 不会删除父表记录
- 不会更新父表主键字段
- 不会关联父表和子表，或者谓词中没有使用外键字段过滤数据

## 避免整个批量过程只有一个大事务
问题场景：
- 一个大批量的commit，要么全部成功，要么全部失败  

优化方案：
- 根据实际跑批逻辑分为多阶段的小事务分别commit

例子
```sql
for i in 1..24 loop
  select * from t_tab 
  where time between add_months(sysdate,-1*i) and add_months(sysdate,-1*i+1)
  commit;
end;



```

## LOB字段不能设置为nologging
优化方案：
- 对应的表及LOB对象设置为logging

## 不建议使用varchar2/char/number存储时间类型的字段
优化方案：
- 时间字段使用date/timestamp类型

## 行专列函数的使用
不建议使用WM_CONCAT，12以后的版本不支持
优化方案：
- 

## 避免字符类型隐式转换
问题场景：

优化方案：


## 大表分区存储

