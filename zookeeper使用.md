### 有什么用
1. 高可用分布式管理协调服务，基于zab(原子消息广播协议)实现。
2. 集群管理
3. 保证顺序一致性
4. 保证原子性，所有请求的处理结果，所有机器上的应用情况一样
5. 单一视图，服务器端数据模型一样

### 组成部分
三种组成，leader，follower，observer,znode维护一个状态stat结构（包含数据变化的版本号，ACL：Access Control List变化，时间戳），每当节点数据内容变化，会多一个版本号，
节点的内容以原子方式读写。

### 应用
配置的管理，日志搜集，分布式锁，集群的管理，发布订阅，数据库切换

### 安装
1. wget -c http://mirror.bit.edu.cn/apache/zookeeper/stable/zookeeper-3.4.9.tar.gz 下载安装包
2. 将zookeeper目录配置为ZOOKEEPER_HOME变量，导出bin目录到path下
3. 在zookeeper安装目录的conf目录下，复制zoo_sample.cfg 命名为zoo.cfg
4. 编辑zoo.cfg，修改dataDir目录到安装目录下自定义目录中，用以存放数据
5. 配置通信端口  
        server.0=*.*.*.*:3000:3999 (server.serverid=ip地址：FL通信端口：选举端口)  
        server.1=*.*.*.*:3000:3999  
        server.2=*.*.*.*:3000:3999  
6. 配置服务器标示
  在dataDir所指定的目录中，创建节点标识文件myid,写入serverid到文件中
7. 使用zkServer.sh start 启动zookeeper
8. 使用zkServer.sh status 查看状态（需要关闭防火墙服务，service iptables stop）
