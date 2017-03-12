### 使用morgan生成日志
1. 日志要素，一般包含请求时间，请求ip，请求状态，请求方式，请求url，请求浏览器等，morgan提供了很好的支持
2. 请求时间,使用`npm install --save moment` 安装moment模块，可以很方便的定制时间格式，使用moment定义一个时间token  


          logger.token('TIME', function(req, res){
            return moment().format('YYYY-MM-DD HH:mm:ss.SSS');
          });


3. 获取请求ip,如果需要获取ip的具体地址，可以使用淘宝地址转换接口`http://ip.taobao.com/service/getIpInfo.php?ip=****`



          logger.token('IPREGION', function(req, res) {
              return req.headers['x-forwarded-for']
                || (req.connection && req.connection.remoteAddress)
                || (req.connection && req.connection.socket && req.connection.socket.remoteAddress)
                || (req.socket && req.socket.remoteAddress)
                || undefined;
            });




4. 请求状态和其他的内容，morgan自带的有，可以直接使用，综上，添加中间件

        app.use(logger('[:TIME] :status :IPREGION ":method :url HTTP/:http-version" ":referrer" ":user-agent"'));
