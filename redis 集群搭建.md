### 主从
 在redis.conf 中修改 # slaveof <masterip> <masterport>,配置master ip和端口
 # masterauth <master-password> 配置master的密码

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
7. 


