### 自带的zkCli.sh 使用
1. 查看： ls + 路径，查看路径下的节点
2. 添加节点：ceate + 路径 + 值
3. 删除指定节点：delete + 路径
4. 获取节点的值：get + 路径
5. 设置节点的值：set + 路径 + 值
6. 递归删除节点：rmr + 路径

### apache cautor使用
1. 引入curator依赖，引入下边的依赖，会自动依赖client、zookeeper、framework

         <dependency>
          <groupId>org.apache.curator</groupId>
          <artifactId>curator-recipes</artifactId>
          <version>2.11.0</version>
          <exclusions>
              <exclusion>
                  <groupId>org.slf4j</groupId>
                  <artifactId>slf4j-api</artifactId>
              </exclusion>
          </exclusions>
      </dependency>
2. 创建客户端使用CuratorFrameworkFactory.builder()方法，将返回一个构造者对象，传入，连接字符串、超时时间，重试策略可以构造一个CuratorFramework  
对象：

          CuratorFramework curatorFramework = CuratorFrameworkFactory.builder()
                          .connectString(CONNECTADDR)
                          .sessionTimeoutMs(SESSIONTIMEOUT)
                          .retryPolicy(retryPolicy)
                          .build();

这里重试策略一般选择ExponentialBackoffRetry，指定初次连接时间和重试次数，这种策略重试间隔是分散的不是固定的。  
3. 节点创建(withAcl做验证身份用)
`curatorFramework.create().withAcl().creatingParentsIfNeeded().withMode(CreateMode.PERSISTENT).forPath("***", bytes);`
4. 节点删除delete
5. 节点修改setData
6. 节点查找checkExists
7. 节点取值getData
8. watcher的监听，使用NodeCacheListener和PathChildrenCacheListener实现监听节点或子节点的变化

