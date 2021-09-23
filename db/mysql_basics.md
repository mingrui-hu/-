

## SQL CLI

```mysql
show database;

# select a db
use mysql;

show tables;

show columns from TABLE;

show index from TABLE;

```



```mysql
create database test;
drop databse test;
```

MR_950919

### 数据类型

1. 数值型
   - INTEGER(INT), SMALLINT, DECIMAL(DEC), NUMERIC
   - FLOAT, REAL, DOUBLE PRECISON
   - BIT
   - TINYINT, MEDIUMINT, BIGINT
2. 日期和时间
   - DATETIME, DATE, TIMESTAMP, TIME, YEAR
   - 每个类型有一个有效值范围和一个零值(无效值)
   - TIMESTAMP有自动更新特性
3. 字符串类型
   - CHAR， VARCHAR, BINARY, VARBINARY, BLOB, TEXT, ENUM, SET
   - CHAR&VARCHAR： 存储和检索方式不同

## 基本操作

```mysql
create database data_school;
use data_school;
show tables;
```

```mysql
CREATE TABLE IF NOT EXISTS `python_class` (
    `id` INT UNSIGNED AUTO_INCREMENT,
    `number` INT(10) NOT NULL, 
    `name` VARCHAR(50) NOT NULL,
    `class_name` VARCHAR(50) NOT NULL,
    PRIMARY KEY (`id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

![image-20210825112933519](D:\笔记\db\mysql_basics.assets\image-20210825112933519-16298621752721.png)

- 注意： 

  1. 表名和列名格式: 不是单引号, 是反引号

  comment中才使用' '

  2. 最后ENGINE和前面括号之间没有空格
  3. 主键可以用多列定义， 列之间以逗号分隔

- 删除表

  `drop tables TABLE_NAME`

- 查询

```mysql
insert into python_class (number, name, class_name) values (1003, "小强", "python快乐学习班");
```

```mysql
select column_name, column_name from table_name;
```

- where语句

```mysql
select field1, field2, ..., fieldN from table_name1, table_name2 
[where condition1 [and [or]] condition2];

select * from python_class where name="小智";
```

- update子句

```mysql
update table_name set field1=new_value1, field2=new_value2 [where clause]
```

- Delete子句

  ```mysql
  delete from table_name [where]
  ```

  - 没有where子句， 表中所有记录将被删除

- Like子句

  - 

