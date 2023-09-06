---
title: left join on 和 where 条件放置的区别
date: 2023-09-06 17:07:40
categories:
- MySQL
tags:
- MySQL


---

# left join on 和 where 条件放置的区别

总结：

1. **对于left join，不管on后面跟什么条件，左表的数据全部查出来，因此要想过滤需把条件放到where后面。**
2. **对于inner join，满足on后面的条件表的数据才能查出，可以起到过滤作用。也可以把条件放到where后面。**

数据库在通过连接两张或多张表来返回记录时，都会生成一张中间的临时表，然后再将这张临时表返回给用户。

在使用 `left join` 时，`on` 和 `where` 条件的区别如下：

1. `on` 条件是在生成临时表时使用的条件，它不管 `on` 中的条件是否为真，都会返回**左边表**中的记录。

2. **`where` 条件是在临时表生成好后，再对临时表进行过滤的条件**。这时已经没有 `left join` 的含义（必须返回左边表的记录）了，条件不为真的就全部过滤掉。

eg.

表1：`select * from tab1;`

| id   | size |
| ---- | ---- |
| 1    | 10   |
| 2    | 20   |
| 3    | 30   |
| 4    | 11   |

表2：`select * from tab2;`

| size | name |
| ---- | ---- |
| 10   | aaa  |
| 20   | bbb  |
| 20   | ccc  |

分析下面两条 sql：

```
select * from tab1 left join tab2 on (tab1.size = tab2.size) where tab2.name='aaa';
```

[!sql1](/img/MySQL/leftjoinon_where1.jpg)

```
select * from tab1 left join tab2 on (tab1.size = tab2.size and tab2.name='aaa');
```

[!sql2](/img/MySQL/leftjoinon_where2.jpg)

其实以上结果的关键原因就是 `left join`, `right join`, `full join` 的特殊性，**不管 `on` 上的条件是否为真都会返回 `left` 或 `right` 表中的记录**，`full` 则具有 `left` 和 `right` 的特性的并集。 而 `inner join` 没这个特殊性，则条件放在 `on` 中和 `where` 中，返回的结果集是相同的。