
1. 安装jdk,这里不能使用openjdk，需要下载并配置环境变量

2. `wget -c http://mirrors.shu.edu.cn/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz` 下载maven，并配置bin路径

3. 修改程序数据库 `/usr/local/cachecloud/cachecloud-open-web/src/main/swap/online.properties`

        cachecloud.db.url = jdbc:mysql://127.0.0.1:3306/cachecloud
        cachecloud.db.user = 用户名
        cachecloud.db.password = 密码
        cachecloud.maxPoolSize = 20

        isClustered = true
        isDebug = false
        spring-file=classpath:spring/spring-online.xml
        log_base=/usr/local/cachecloud/logs
        web.port=8585
        log.level=WARN

4. 切换到cachecloud目录，执行命令`mvn clean compile install -Ponline`

5. 将编译好的包拷贝到/opt/cachecloud-web目录下

        拷贝war包(cachecloud-open-web/target/cachecloud-open-web-1.0-SNAPSHOT.war)到/opt/cachecloud-web下
        拷贝配置文件(cachecloud-open-web/src/main/resources/cachecloud-web.conf)到/opt/cachecloud-web下，并改名为cachecloud-open-web-1.0-SNAPSHOT.conf（spring-boot要求，否则配置不生效）

6. 拷贝启动脚本(cachecloud根目录下script目录下的start.sh和stop.sh)到/opt/cachecloud-web下

        sh start.sh #如果机器内存不足，可以适当调小:-Xmx和-Xms(默认是4g),需要先创建logs目录，以免找不到
        sh stop.sh


