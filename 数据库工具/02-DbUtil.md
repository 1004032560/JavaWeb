## 1、DBUtil

Apache 组织开发的开源的对 JDBC 进行简单封装的工具类库

作用：

1. 简化 JDBC 的开发，少写代码
2. 不影响性能
3. 可以使用数据库连接池技术（提高伸缩性，健壮性，性能指标）

DAO：Data Access Object：数据访问对象层





## 2、JDBC的弊端

1. 大量的重复劳动

2. 效率低，开发周期长

 

## 3、为什么使用Dbutils

封装了 JDBC，减少重复劳动，提高效率，开发周期短



## 4、DBUtils核心类3个

DbUtils：连接数据库的对象

QueryRunner：SQL 语句的操作对象

ResultSetHandler：封装数据的策略对象，将结果数据转换为另一个对象









调用BeanHandler，不用自己写回调方法，DBUtil中自带的方法，传参为：实体类.class；对象，反射机制