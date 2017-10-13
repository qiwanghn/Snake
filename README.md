## Abstract
  怎么知道web api被调用的频率了？
  如何分析各时段web api各接口方法的调用次数？
  如何获取web api接口方法的调用失败频次？
  如何分析web api接口方法耗时异常？

  Snake是基于C#开发的实时api监控平台，包括api压力监控和调用异常监控。  
  是基于RESTFul api风格开发的.net web api微服务应用集群，实时的接口调用监控为系统开发者提供了有利的分析数据。  
  Snake是为此而生的安静而平顺监控系统，它通过Filter实现监控嵌入，异步发送监控日志消息，通过基于RabbitMQ  
  实现的企业服务总线平顺处理消息，最终将监控日志数据输入存储到Mongodb中。

## Requirements
  * Windows 7 以上操作系统  
  * IIS 7 +  
  * .NET Framework 4.6  
  * [RabbitMQ 3.6.5](http://www.rabbitmq.com)  
  * [Mongodb 3.2.1](https://www.mongodb.com)  
  
## Quick Started
1. 编译并发布Snake.Api到IIS站点  
2. 编译Snake.ApiTrackService项目，修改配置文件App.config配置项，如下：
	  <appSettings>
		<add key="MongoConnectionString" value="mongodb://snake:snake@localhost:27017/SnakeDbTest/?MaximumPoolSize=500;socketTimeoutMS=2000;MinimumPoolSize=1;waitQueueTimeoutMS=300;waitQueueMultiple=10;ConnectionLifetime=30000;ConnectTimeout=30000;Pooled=true" />
	  </appSettings>
  
	  <!--************************** snake.Service Settings ********************** -->
	  <snake.service>
		<add key="snake.serviceName" value="SnakeConsumer" />
		<add key="snake.serviceDisplayName" value="Snake Consumer Server" />
		<add key="snake.serviceDescription" value="Snake Consumer Server" />
	  </snake.service>

	  <!--************************* RabbitMQ Connection Settings ****************** -->
	  <RabbitMQ.Connection>
		<add key="RabbitMQ.HostName" value="localhost" />
		<add key="RabbitMQ.Port" value="5672" />
		<add key="RabbitMQ.UserName" value="snake" />
		<add key="RabbitMQ.Password" value="snake" />
		<add key="RabbitMQ.VirtualHost" value="snakeTest" />
		<add key="RabbitMQ.QueueName" value="q_snake_apitrack" />
		<!--`消费者个数-->
		<add key="RabbitMQ.ConsumerNum" value="4" />
		<!--重试次数-->
		<add key="RabbitMQ.UseRetryNum" value="3" />
	  </RabbitMQ.Connection>

## Reference

## Copyright and license
