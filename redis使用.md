###redis两种使用场景  
1. 生产消费模式，一个产生消息，多个消费者监听队列，抢消息。一个消息被一个消费者所有。
2. 发布订阅模式：一个生产消息，监听队列消费者受到同一份消息。一个消息多个消费者收到的一样。

####生产消费
 使用redis的list结构实现，生产者调用redis的lpush往特定key中装入消息，消费者使用brpop（阻塞）监听该key。
####发布订阅
发布者调用publish往特定channel发送消息，订阅者在初始化订阅到channel，有消息会立即接受，否则阻塞。

###redis 安装
1. wget -c http://download.redis.io/releases/redis-3.2.5.tar.gz 断点续传下载安装包
2. tar -zxvf 解压
3. cd redis-3.2.5 后执行make编译
4. 编译完成后，可进入到src下，可以看到src下有redis-server、redis-cli,使用make install安装
5. 在/usr/local/redis3.2下建立etc和bin文件夹，用来存放配置文件和命令
6. 把src下边的mkreleasehdr.sh redis-benchmark redis-check-aof redis-check-dump redis-cli redis-server移动至bin下
7. 把redis.conf移动到/etc目录下
8. 启动时，要使用后台启动配置redis.conf中的daemonize为yes，使用./redis-server ***/redis.conf进行启动redis服务器
9. 关闭所有redis可以使用pkill redis-server杀死本机所有redis服务

