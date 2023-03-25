# 配置日志

```properties
mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.stdoutImpl
```



# 主键生成策略

### 雪花算法



### 配置主键自增：

1. 实体类字段上`@tableId(type = Idtype.AUTO)`

2. 数据库字段一定要是自增！



其他

```java
public enum IdType {
	AUTO(0), // 数据库id自增
    NONE(1), // 未设置主键
    INPUT(2), // 手动输入
    ID_WORKER(3), // 默认的全局唯一id
    UUID(4), // 全局唯一id uuid
    ID_WORKER_STR(5) // ID_WORKER 字符串表示法
}
```



# 自动填充

创建时间、修改时间！这些个操作一遍都是自动化完成的，我们不希望手动更新！

阿里巴巴开发手册：所有的数据库表：gmt_create、gmt_modified,几乎所有的表都要配置上！而且需要自动化！



### 数据库级别

create_time/datetime

update_time/datetime



### 代码级别



# 乐观锁

version默认值为1

```java
@Version
private Integer version;
```



# 逻辑删除

> 物理删除：从数据库中直接移除
> 逻辑删除：再数据库中没有被移除，而是通过一个变量来让他失效！deleted = 0 => deleted = 1



管理员可以查看被删除的记录！防止数据的丢失，类似于回收站！

deleted默认值0

```java
@TableLogic
private Integer deleted;
```



# 条件构造器

QueryWrapper(LambdaQueryWrapper) 和 UpdateWrapper(LambdaUpdateWrapper)



# 代码自动生成器











































