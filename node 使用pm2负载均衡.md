#### ecosystem 启动
`pm2 ecosystem`

`pm2 start ecosystem.config.js --env production`


#### 安装pm2
1. npm install pm2@latest -g
2. pm2 start app.js 启动进程, pm2 start app.js -i 数字，如果数字为0，则根据cpu核心数量启动，不是0，则根据你指定的数量启动,如果想要服务器重启时启动之前的应用，需要在pm2 start ...后使用 pm2 save命令，使用--name 指定名字
3. pm2 stop ... 停止运行进程
4. pm2 monit 查看监控信息
5. pm2 delete all 删除所有，delete + id number删除指定id
6. pm2 flush 更新代码后必须使用这个命令刷新，否则加载错误
7. pm2 开机自启动  
（1） pm2 save 保存当前状态  
（2）pm2 startup 生成命令  
（3）systemctl enable pm2-root,启用开机自动启动    
