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
5. 如果不用监控程序，则配置daemonize yes，修改logfile文件位置，报错时有log可以参考

4. 修改各个端口号，port ****
5. 修改bind服务器ip bind **.**.**.**

6. 指定数据文件存放目录，dir /usr/local/***/****
7. 开启aof  appendonly yes由于是集群所以不需要alaway，默认的就可以, 修改allkeys-lru allkeys-lru 以免系统内存不足

8. 使用redis-server /usr/local/***/***.conf 启动各个redis服务器
9. 使用redis-trib.rb 脚本的create命令创建集群，由于这个脚本是ruby脚本，需要先做一下
    1. ruby -v 查看ruby是否安装如果没有
    2. apt-get install ruby进行安装ruby
    3. 安装后，执行./redis-trib.rb脚本查看是否有错，如果提示redis没有安装，要使用gem install redis 安装ruby的redis模块
    4. ruby安装好后，执行./redis-trib.rb create --replicas 1 你的ip1 port1 你的ip2 port2 你的ip3 port3 你的ip4 port4 你的ip5 port5 你的ip6 port6 创建集群，--replicas 1代表1主从比例，这里设置为1，表示一主一从， 1：1
    5.  执行后给出提示 >>> Creating cluster....[OK] All 16384 slots covered.集群就创建成功了
    6. 若需要授权配置成功后使用  
      - config set masterauth abc  
      - config set requirepass abc  
      - config rewrite  
      
10. 使用redis-cli -c -h **.**.**.** -p ** 指定-c选项进入集群中，执行客户端命令行后，输入cluster nodes，查看集群状况 ，输入cluster info 查看集群信息，有密码时指定-a，-p是指定的端口
11. 添加redis节点，./redis-trib.rb add-node 指定新ip:port 指定已存在集群的某个ip:port,加入集群
12. 加入后需要重新分片 使用./redis-trib.rb reshard ip:port

[http://blog.csdn.net/qq_37595946/article/details/77800147]! redis安装出错解决

13. 遇到错误'Asynchronous AOF fsync is taking too long (disk is busy?). Writing the AOF buffer without waiting for fsync to complete, this may slow down Redis.'的处理：`echo "vm.dirty_bytes=33554432" >> /etc/sysctl.conf` 执行`sysctl -p`使配置生效

14. 遇到错误'WARNING overcommit_memory is set to 0! Background save may fail under low memory condition. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.' 使用`echo 'vm.overcommit_memory=1' >> /etc/sysctl.conf` 设置允许程序分配所有本机物理内存，执行`sysctl -p`生效

15.  MISCONF Redis is configured to save RDB snapshots,but it is currently not able to persist on disk. Commands that may modify the data set are disabled, because this instance is configured to report errors during writes if RDB snapshotting fails (stop-writes-on-bgsave-error option). Please check the Redis logs for details about the RDB error.，使用`config set stop-writes-on-bgsave-error no` 即可
