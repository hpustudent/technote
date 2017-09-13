#### 安装pm2
1. npm install pm2@latest -g
2. pm2 start app.js 启动进程, pm2 start app.js -i 数字，如果数字为0，则根据cpu核心数量启动，不是0，则根据你指定的数量启动,如果想要服务器重启时启动之前的应用，需要在pm2 start ...后使用 pm2 save命令
3. pm2 stop ... 停止运行进程
4. pm2 monit 查看监控信息
5. pm2 delete all 删除所有，delete + id number删除指定id
