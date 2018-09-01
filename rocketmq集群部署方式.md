### 多个master模式
无slave，节点全为master，单个master挂掉无影响，性能最高，一般的应用推荐的模式。
### 多master多slave，异步复制
每个master配置一个slave，采用异步复制，主备有短暂消息延迟。性能和多master几乎一样。master挂掉，磁盘损坏时，会丢失部分消息。
### 多master多slave，同步双写
每个master配置一个slave，同步双写是，主备都写成功的时候，才向应用返回成功。性能比异步复制稍低，但是服务可用性与数据可用性最高。交易相关的业务推荐。

### 部署
