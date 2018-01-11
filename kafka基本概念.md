# Kafka:A distributed streaming platform（Scala语言编写）

## 大数据基本一个流程
Flume/SDK  ->   Kafka   ->     spark/storm     ->    Redis/HBase

## Kafka使用场景
数据源： 应用系统A 产生的 用户访问数据和订单数据 为10000 条/秒

数据处理:Spark，处理的数据能力为1000条/秒

问题:产生的数据〉数据量

解决方法：引入消息队列（分布式需要可靠的消息系统）

## Kafka三大功能
1. 分布式消息系统（发布/订阅功能）

2. connector API(将Kafka topic中的数据保存到RDBMS中)

3. Stream compute（可以对kafka中的数据进行流式计算处理）


## Kafka 特点
* 消息系统，存储数据（提交日志格式文件）
* 分布式(有多台机器)
* Topic（存储某一类的数据）
    存储数据类似HDFS
	* 按照分区partition存储

  	    文件夹/文件
	* 分区数据有多个副本

	    Replications
      
## Kafka与前后框架的集合


###  Kafka与Flume
Flume框架实时收集数据，并不是存储数据，收集的数据要给存储系统

    1. KAFKA作为sink  --  最多

        接收数据并存储

    2. KAFKA作为Soure

        作为数据的提供者

    3. KAFKA作为Channel

        数据收集中的管道缓冲


###  KAFKA与Spark集成

1. 方式一： push

  Flume/KAFKA 将数据推送给Spark，就需要Receivers接受数据，被动性，推送
  
此种方式存在问题：Receivers进行接收数据，给spark进行处理，blocks存储在Ececutors内存中，副本数
问题，当接收的blocks数据没有被处理完，整个spark应用停止，当再次启动应用的时候，未处理的和当时处理完成的blocks数据丢失了。（除非将blocks也进行checkpoint到文件系统进行容灾备份WAL）

2. 方式二：pull

     Spark主动到Flume Agent sink中或者kafka Topic中拉取数据，主动性，拉取
     
此种情况就没有Receivers Task，不会出现数据未处理或者多出力
比如：从KAFKATopic中获取数据
Pull拉取数据，进行数据处理，处理完成以后，应用本身管理更新offset。调用的KAFKA，底层的消费者API。主流
