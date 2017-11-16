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

### 集群配置
1. es目录下的config目录中有`elasticsearch.yml`文件,主要用于对集群、节点、索引以及持久化和集群发现机制等进行参数设置

