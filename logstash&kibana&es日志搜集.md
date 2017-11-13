### 安装java
1. 执行命令 `yum install java-1.8.0-openjdk`

### 安装es
1. 下载安装包 `wget -c https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.4.tar.gz`
2. 解压 `tar -zxvf elasticsearch-5.6.4.tar.gz`
3. 运行 `bin/elasticsearch` 即可启动es
4. 由于elasticsearch 命令自带的不包含停止等命令，所以可以安装servicewrapper插件解决，通过`https://github.com/elasticsearch/elasticsearch-servicewrapper/archive/master.zip`下载解压后，将service文件夹放到elasticsearch的bin目录下
5. 配置servicewrapper，在service目录下找到elasticsearch.conf文件，配置前两行：`ES_HOME`及`ES_HEAP_SIZE`
6. 接下来就可以使用`bin/service/elasticsearch start | stop | restart | install | remove | console | condrestart | status`控制es的状态了

