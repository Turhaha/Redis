# kafka安装部署

	1. 单机模式
		一台机器，一个Broker
	2. 伪分布式集群
		一台机器启动多个Broker服务
	3. 完全分布式集群
		多台机器，每台机器启动一个Broker服务
    
### Kafka基于Scala语言框架，使用的时候，需要编译，制定scala语言版本

1. 官网下载scala版本和kafka版本
2. 解压与配置（tar.gz）
3. 创建kafka logs存储目录
4. 启动Broker（进入bin目录下）
5. 创建topic（参考官网给的命令行）
6. 进行生产者的发送
7. 确认几台消费者都接受到了订阅的消息
