### 自带的zkCli.sh 使用
1. 查看： ls + 路径，查看路径下的节点
2. 添加节点：ceate + 路径 + 值
3. 删除指定节点：delete + 路径
4. 获取节点的值：get + 路径
5. 设置节点的值：set + 路径 + 值
6. 递归删除节点：rmr + 路径
### apache cautor使用
1. 引入curator依赖  

              <dependency>
                  <groupId>org.apache.curator</groupId>
                  <artifactId>curator-client</artifactId>
                  <version>3.2.1</version>
              </dependency>

              <dependency>
                  <groupId>org.apache.curator</groupId>
                  <artifactId>curator-framework</artifactId>
                  <version>3.2.1</version>
              </dependency>

              <dependency>
                  <groupId>org.apache.curator</groupId>
                  <artifactId>curator-recipes</artifactId>
                  <version>3.2.1</version>
              </dependency>
