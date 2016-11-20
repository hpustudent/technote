### string list hash set zset
#### string
1. 设置 set, 取值get，删除del
2. setnx 如果不存在则设置，存在返回0
3. setex 设置过期，语法为：setex name expiredtime value
4. setrange 字符串替换
5. mset, mget 一次性获取设设置多个

#### list
1. 双向链表，可以做栈或队列
2. lpush 头部加入元素
3. rpush 尾部加入元素
4. linsert插入元素
5. lpop 头部取出元素
6. rpop 尾部取出元素
7. lrange key start end 取出从start到end的元素 如lrange person 0 -1 取出所有person的元素
8. lset 指定下标的元素替换
9. lrem 删除元素返回删除的个数
10. ltrim 保留指定范围内的数据

#### hash
1. hset key field value, hse一个键 一个域一个值
2. hget key field

3. 批量添加，hmset key field value [field value ...]
4. 判断是否存在，hexists key field
5. 返回键值对数量 hlen key
6. 返回所有的keys hkeys key
7. 返回所有的va hvals key
8. hgetall 返回所有的key和value

#### set 无顺序
1. sadd key member [member...]向集合key中添加多个成员
2. srem 删除集合元素
3. sdiff 返回两个集合的不同元素
4. smembers 返回所有集合元素
5. sdiffstore 将返回的不同元素存储到另外集合
6. sinter 交集
7. sinterstore 交集结果存放另外集合
8. sunion 并集
9. sunionstore 并集结果存放另外集合
10. smove 一个集合移动到另一个集合
11. scard 元素个数
12. sismember 判断元素是否在集合中
13. srandmember 随机返回一个元数

#### zset有序集合
1. zadd 向集合添加，如果存在更新顺序zadd key score member
2. zrange key start end 获取元素可以在最后添加withscores关键字会将score打印出来
3. zrem 删除zset中名字为key的成员
4. zincrby 以指定值递增
5. zrangebyscore 找到指定score区间范围的数据
6. zremrangebyrank 删除索引
7. zremrangebyscore 删除指定score区间的数据
8. zrank 返回排序索引，从小到大
9. zrevrank 从大到小降序
10. zcard 返回集合所有元素个数
11. zcount 返回集合中指定区间的数量

#### 其他命令
1. expire key 时间，设置超时时间
2. ttl key 查看剩余时间
3. persist 取消过期时间
4. select 选择数据库
5. randomkey 随机返回key
6. rename 重命名key
7. move key 将key从一个数据库移动到另外的数据库
8. dbsize 数据库中key数量
9. info 获取数据库信息
10. config get 某个参数，获取相关的配置信息 get * 获取所有
11. flushdb 清空当前数据库，flushall 清空所有数据库
12. 删除某个键 del key即可




