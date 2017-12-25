### 安装java
1. 执行命令 `yum install java-1.8.0-openjdk`

### 安装es
1. 下载安装包 `wget -c https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.4.tar.gz`
2. 解压 `tar -zxvf elasticsearch-5.6.4.tar.gz`

        2.1 由于es不能使用root下启动，需要创建用户组和添加用户
        2.2 groupadd es创建用户组
        2.3 useradd es -g es -p 123456创建用户es并加入组es，设置密码
        2.4 chown -R es:es elasticsearch-5.6.4/将目录下所有内容改变为es组es用户
        2.5 su es切换为es用户，在执行下边的命令

3. 运行 `bin/elasticsearch` 即可启动es
4. 由于elasticsearch 命令自带的不包含停止等命令，所以可以安装servicewrapper插件解决，通过`https://github.com/elasticsearch/elasticsearch-servicewrapper/archive/master.zip`下载解压后，将service文件夹放到elasticsearch的bin目录下
5. 配置servicewrapper，在service目录下找到elasticsearch.conf文件，配置前两行：`ES_HOME`及`ES_HEAP_SIZE`
6. 接下来就可以使用`bin/service/elasticsearch start | stop | restart | install | remove | console | condrestart | status`控制es的状态了
7. 启动成功后，使用`curl http://localhost:9200/`测试服务是否正常

#### 错误1：max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536]
root用户下vi /etc/security/limits.conf，添加如下：

        * soft nofile 65536
        * hard nofile 65536
        root soft nofile 65536(ubuntu中需要设置)
        root hard nofile 65536(ubuntu中需要设置)
        
修改后如果要生效，需要重新登录，不用重启电脑

#### 错误2：max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
root用户下vi /etc/sysctl.conf 添加如下：

        vm.max_map_count=262144

修改后使用命令` sysctl -p` 重新加载配置即可

### 查询状态接口
1. http://192.168.56.111:9200/_cluster/health   查询集群健康状态
2. http://192.168.56.111:9200 查看节点信息
3. http://192.168.56.111:9200/_cat/nodes?v 查看节点列表

### 集群配置
1. es目录下的config目录中有`elasticsearch.yml`文件,主要用于对集群、节点、索引以及持久化和集群发现机制等进行参数设置

        cluster.name: YourClusterName //相同集群名在多播模式下自动加入统一集群
        node.name: YourNodeName //区分节点，统一集群下节点名需要唯一
        bootstrap.memory_lock=true //避免将内存数据交换到硬盘上，因为太耗时，可能会使GC时间变长
        network.host: 192.168.1.11 //当前节点绑定地址
        http.port: 9200 //http绑定的端口
       
        discovery.zen.ping.unicast.hosts: ["11.11.11.11"] //各个服务器地址，多写几个万一某一个节点不在了呢，单播部署在局域网内部
        discovery.zen.minimum_master_nodes:  //选择主节点过程中最少的节点数，节点数/2+1
        discovery.zen.ping.timeout: 5s //节点通信超时时间
        node.master: true //设置节点为主节点
        node.data: true //设置节点为数据节点
        
        http.cors.enabled: true //允许跨域请求
        http.cors.allow-origin: "*" //设置跨域REST来自何处，*代表所有
