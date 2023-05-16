# Hive

## 基本架构

* UI 提供查询窗口
* Driver：接受查询组件请求，实现session句柄，提供jdbc、odbc模型化api
* Compiler：根据元数据进行语法解析
* MetaStore：存放表、分区等结构化数据信息
* Execution Engine：执行编译器创建的执行计划

## 常规优化

* 表设计
  * 分区表
  * 列存
* 数据存储格式
  * 行存（textfile，sequenceFile）
  * 列存（parquet、orc）
    * 相同点
      * 支持二进制存储、行组、列块
      * 基本类型+复杂类型
      * 支持压缩
      * 支持谓词下推、映射下推
    * parquet
      * 支持嵌套（json），orc不支持，需要用复杂类型表达
      * 对spark非常友好
    * ORC
      * 比 parquet 压缩效率高
      * 对hive友好
      * 支持事务ACID
      * 支持不同的索引机制，查询效率更快
        * row group index（行组索引）
        * bloom filter
  * Hive数据压缩
    * 压缩格式| 是否支持切片| 解压缩速度| 压缩率
    * snappy | no|最快 | 很差
    * lzo| yes | 很快| 很高
    * Bzip2 | yes | 最慢 | 最高
    * gzip | no | 一般 | 很高
  * MR 属性优化
    * 开启本地模式
    * 开启JVM重用
    * 开启stage并行执行
    * 开启关联优化
  * 表之间的优化
    * 含有小表走map join
    * 都是大表走bucket join
  * sql 优化
    * from ... insert 带起 union all
    * group by 代替 count(distict)
    * 谓词下推
      * left join，右侧表过滤条件写在on后，左侧表写在where后
      * join，on == where后
      * full join， 写在where后，on后不下推

## 参考文档

[Hive架构](https://blog.csdn.net/github_39577257/article/details/98958568)

[Hive 优化参考](https://blog.csdn.net/qq_43192537/article/details/102161058)



