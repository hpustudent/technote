1. 使用morgan.token 定制token

        morgan.token('GMT8', function(req, res){
          return moment().format('YYYY-MM-DD HH:mm:ss.SSS');
        });
        
2. 使用express的use方法将中间价加入，加入格式为`:GMT8`

        app.use(morgan('[:GMT8] :status :remote-addr ":method :url HTTP/:http-version" ":referrer" ":user-agent"'));

3. http访问时将会有log出现

        [2016-12-03 18:46:46.927] 200 ::ffff:127.0.0.1 "GET /pageinfo?url=****.htm HTTP/1.1" "-" "******(Macintosh; OS X/10.11.0) GCDHTTPRequest"
