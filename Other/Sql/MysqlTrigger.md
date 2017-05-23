# Mysql 触发器
1. 起因：一次作业中，需要使用事务，结果在过程中发现`mysql`竟然不支持`check`约束，好吧，不是不支持只是你设置了之后`mysql`会忽略他，所以并没有什么用，官网的解释是说为了更好的兼容性。在找资料的过程中发现，在`mysql`中可以使用**触发器**来实现检查约束的效果，所以就简单的总结一下触发器的使用。
2. 简介：
>创建语法

```
create trigger trigger_name
trigger_time
trigger_event on tbl_name
for each row
trigger_stmt
```
>其中:

```
trigger_name:标识触发器名称，用户自行指定；
trigger_time:标识触发时机，取值为before或after;
trigger_event:标识触发时间，取值为insert、update或delete;
tbl_name:标识建立触发器表名;
trigger_stmt:触发器程序体，可以是一句SQL语句，或者使用begin和end包含多条语句。
```
>可以建立6种触发器，即：before|after insert、before|after update、before|after delete。
>**不允许在同一个表上建立两个相同类型的触发器，所以一个表上最多建立6个触发器**
3. trigger_event
Mysql 除了对`insert`, `update`, `delete`基本操作进行定义外，还定义了`loda data`, `replace`语句，这两种语句也能触发上述触发器。
`load data`语句用于将一个文件装入到一个数据表中，相当于一系列`insert`操作。
`replace`语句和`insert`很像，在表中有主键约束或者唯一性约束时，会先删除原来的数据，然后增加一条新数据，就是一条`replace`有时等价于一条`insert`有时又等价与`insert + delete`
```
触发条件:
    INSERT型触发器：插入某一行时激活，可能通过`insert,load data,replace`触发。
    UPDATE型触发器：更改某一行时激活，可能通过`update`触发。
    DELETE型触发器：删除某一行时激活，可能通过`delete，replace`触发。
```
**delimiter new_delemiter命令**
>可以改变在mysql命令行模式下的分隔符。

4. new与old解释
```
在insert型触发器中，new用来表示将要(before)或已经(after)插入的新数据;
在update型触发器中，old用来表示将要或已经被修改的原数据，new用来表示将要或已经修改为的新数据;
在delete型触发器中，old用来表示将要或者已经被删除的原数据;
```
>先记录这么多，以备后用。
