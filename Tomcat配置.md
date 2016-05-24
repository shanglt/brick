# Tomcat 6 配置
## Tomcat并发优化
```
<Connector port="8080" protocol="HTTP/1.1"
	connectionTimeout="20000"
	redirectPort="8443"
	maxThreads="800" 
	acceptCount="1000"/>
```

**maxThreads** 最大任务数，即同时处理的任务个数，默认200；

**acceptCount** 当tomcat启动的线程数达到最大时，接受请求排队的个数，默认100；

> 接收一个请求，此时的tomcat启动的线程数已经到达maxThreads，等待队列中的请求个数也到达acceptCount，此时tomcat会直接拒绝此次请求，返回connection refused。

