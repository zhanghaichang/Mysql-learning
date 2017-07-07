# EXPLAIN你的查询语句  
* EXPLAIN 关键字能够让你知道索引的使用,如何搜索数据的,扫描行数等等,可以帮助你分析你SELECT 语句的瓶颈。因此可以优化你的SELECT语句,选择一个复杂的sql语句。

![EXPLAIN截图](http://images2015.cnblogs.com/blog/825922/201512/825922-20151202213920533-1374552881.png)
* select_type: 有三个参数(simple,primary, union,dependent union,union result)  simple 它表示简单的select,没有union和子查询(这里只介绍simple)
* table : 出自哪一张表
* type :显示的访问类型,从性能最好到最坏以此是 system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL
表中只有一行;

*1)const类型的特例  
2)const:  表中最有有一行匹配,const用户比较primary key或者unique索引,因为只有一行,所以很快  
3)eq_ref :   mysql手册是这样说的:"对于每个来自于前面的表的行组合，从该表中读取一行。这可能是最好的联接类型，除了const类型。它用在一个索引的所有部分被联接使用并且索引是UNIQUE或PRIMARY KEY"。即比较带索引的列  
4)ref : 对于每个来自于前面的表的行组合，所有有匹配索引值的行将从这张表中读取。这里的索引不包括 primary和unique.  
5)rang : 给定范围内的索引,如 EXPLAIN SELECT * FROM user WHERE id IN (1,5) 或者是 BETWEEN  
6)ALL : 全表扫描*  

* possible_key : 显示 使用的哪个索引在该表中找到行 

* key : 该查询时所用到的索引

* key_len : 使用索引的长度

* ref : ref列显示使用哪个列或常数与key一起从表中选择行。

* rows : 显示查询时扫描的行数,值越大越不好,所以根据这个可以判断mysql语句的好坏以及建立索引优化

* extra: 额外的信息

可以根据EXPLAIN你SELECT的查询语句 进行相关的优化
