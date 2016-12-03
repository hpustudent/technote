1. 使用morgan.token 定制token

        morgan.token('GMT8', function(req, res){
          return moment().format('YYYY-MM-DD HH:mm:ss.SSS');
        });
        
2. 使用express的use方法将中间价加入，加入格式为`:GMT8`

        app.use(morgan('[:GMT8] :status :remote-addr ":method :url HTTP/:http-version" ":referrer" ":user-agent"'));
