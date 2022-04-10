
# flinkwindowapp使用说明
##概述
   *本demo基于flink1.13.2版本开发，演示了flink窗口计算的完整流程，通过消费kafka集群数据，进行滚动窗口聚合后将结果通过分布式事务2pc方式写入mysql，最终迟到数据通过侧输出流进行处理，侧数据流中数据达到一定时间，或记录数达到一定数量就会以批量方式写入mysql，连接池为druid。
## kafka测试数据格式
```json
{"tradeNo":"flinktest00001","tradeName":"测试交易","trandeAme":323.12,"userId":12133,"createTime":"2022-04-10 11:12:12"}
```
## mysql建表
```sql
CREATE TABLE `transtarget` (
  `userid` int DEFAULT NULL,
  `totalame` double DEFAULT NULL,
  `starttime` varchar(255) DEFAULT NULL,
  `endtime` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `transflow` (
  `tradeno` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci DEFAULT NULL,
  `tradename` varchar(255) DEFAULT NULL,
  `trandeame` double DEFAULT NULL,
  `userid` double DEFAULT NULL,
  `createtime` varchar(255) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```
## 修改配置信息后编译打包
     需要根据自己环境修改mysql和kafka连接信息。
## 上传jar包到flink集群
     注意根据自己环境指定启动配置文件路径
![](vx_images/571214816231888.png)

##运行和测试
![164958066333](vx_images/84675316249768.png)