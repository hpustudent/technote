### 主从
 在redis.conf 中修改 # slaveof <masterip> <masterport>,配置master ip和端口即可  
 为了防止数据丢失，可以打开持久化，开启aof后rdb数据文件就不见了（rdb是快照保存数据的save 900 1表示900s内至少一个键修改就保存，aof是可以自己配置保存方式，二者只能开启一种）
    1. appendonly yes
    2. appendfsync always
    3. redis-check-aof 可以恢复aof中的数据
    
### 哨兵
1. 监控，不断检查主从是否正常
2. 某个redis服务器故障，哨兵向管理员或其他应用发送通知
3. 故障转移，主故障，从顶上。

4. 配置哨兵，将sentinel.conf拷贝到etc下
    1. 修改配置 sentinel monitor mymaster 127.0.0.1 6379 2 含义为：名称，ip ,端口, 选举次数
    2. 修改配置 sentinel down-after-milliseconds mymaster 30000 哨兵多久查看一次，30秒检测不到就说明挂了，可以选举新master了
    3. 修改配置 sentinel failover-timeout mymaster 180000 
    4. 修改配置 sentinel parallel-syncs mymaster 1
5. 启动哨兵， redis-server sentinel.conf --sentinel & 后台启动哨兵程序
6. 查看哨兵信息，redis-cli -h **** -p 26379 info Sentinel

### 集群
1. 修改配置 # cluster-enabled yes
2. 修改配置 # cluster-config-file nodes-***.conf
3. 指定节点超时 cluster-node-timeout ***

4. 指定pid, pidfile /var/run/redis_*.pid
5. 如果不用监控程序，则配置daemonize yes

4. 修改各个端口号，port ****
5. 修改bind服务器ip bind **.**.**.**

6. 指定数据文件存放目录，dir /usr/local/***/****
7. 开启aof  appendonly yes由于是集群所以不需要alaway，默认的就可以

8. 使用redis-server /usr/local/***/***.conf 启动各个redis服务器
9. 使用redis-trib.rb 脚本的create命令创建集群，由于这个脚本是ruby脚本，需要先做一下
    1. ruby -v 查看ruby是否安装如果没有
    2. apt-get install ruby进行安装ruby
    3. 安装后，执行./redis-trib.rb脚本查看是否有错，如果提示redis没有安装，要使用gem install redis 安装ruby的redis模块
    4. ruby安装好后，执行./redis-trib.rb create --replicas 1 **.**.**.** port1 **.**.**.** port2 **.**.**.** port3 **.**.**.** port4 **.**.**.** port5 **.**.**.** port6 创建集群，--replicas 1代表1主从比例，这里设置为1，表示一主一从， 1：1
    5.  执行后给出提示 >>> Creating cluster....[OK] All 16384 slots covered.集群就创建成功了
    
