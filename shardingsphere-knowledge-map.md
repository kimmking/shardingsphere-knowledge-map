# ShardingSphere Knowledge Map

## 功能

### 分库/分表/分库分表

- Sharding策略

	- Inline表达式/Groovy
	- Precise精确分片
	- Range范围分片
	- Complex复合分片
	- Hint强制分片

### 读写分离

- Master-Slave

	- 负载均衡
	- 线程内数据一致性

### 分布式主键

- UUID/Snowflake/Leaf

### 数据加解密

- AES/MD5

### 影子表压测

- 生产环境灰度压测

### 分布式事务

- XA/Seata/Saga

	- 2PC
	- BASE/TCC/AT

### 弹性迁移

- ShardingSphere-Scaling

	- 数据复制/异构扩容
	- 历史数据/增量数据

## 接入端

### ShardingSphere-JDBC

- 支持任意数据库
- Java/JDBC/支持基于JVM语言
- 支持原生JDBC/Yaml/Spring/SpringBoot
- 支持JPA/ORM框架Hibernate/MyBatis

### ShardingSphere-Proxy

- 支持MySQL/PostgreSQL
- 支持任意客户端或类库
- 以代理Server方案独立启动
- 支持控制语句

### ShardingSphere-Sidecar(TODO)

- 结合ServiceMesh

## 数据源

### 数据库

- MySQL(重点支持)
- PostgreSQL
- SQLServer
- Oracle

### 连接池

- Hikari(默认使用)
- C3P0
- DBCP
- Druid
- Proxool

## 性能

### 场景

- 延迟

	- JDBC多一步解析，延迟影响较小
	- Proxy额外多一跳，延迟增加几毫秒
	- 复杂的长SQL首次解析较慢，重复调用有缓存

- 吞吐

	- 简单查询分片数近线性提升
	- 随数据规模增大，对于单库优势明显增加
	- 全路由写操作下性能低于单库情况

### 优化

- 调整连接数和线程数
- 优化SQL日志和元数据加载
- 使用简单、带分片键和主键的SQL，避免全路由

## 治理

### 配置中心

- 启动参数
- 治理规则

	- 变动实时生效

- 元数据

### 注册中心

- 节点状态
- 从库禁用

### 支持Zookeeper/etcd，部分支持Nacos/Apollo

### 可观测性

- Trace

	- OpenTracing/Skywalking/APM

- Metrics

	- Prometheus/Grafana

### UI控制台

- Node/Vue

## 架构

### 设计机制

- 微内核/可插拔架构/SPI
- 以SQL解析(Antlr)+JDBC为基础
- 规则按LogicSchema组织
- 使用Guava Eventbus作为事件通知机制

### 核心流程

- 解析/路由/重写/执行/归并

