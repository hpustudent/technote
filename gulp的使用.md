### gulp简介
    gulp是基于流的自动化构建工具，基于nodejs运行，可以完成css，js，图片的压缩

### gulp安装
    1. 使用npm -version 检测系统是否已经安装了nodejs环境
    2. 创建项目文件夹，使用npm init ，初始化package.json文件
    3. 使用npm install --save gulp 安装gulp模块，为了可以在控制台直接使用gulp，一般在全局也安装gulp，使用命令 sudo npm install -g gulp-cli
    4. 新建gulp主文件gulpfile.js,即可在glupfile.js定义自动化任务
    5. 使用npm install 安装 gulp-uglify模块，此模块用于对js文件进行压缩
    6. 使用npm install 安装 gulp-minify-css模块，此模块用于对css文件压缩
    7. 使用npm install --save gulp-babel babel-preset-es2015安装babel模块，此模块用于对es6代码转换为es5
    8. npm install gulp-rename安装rename模块，比如在压缩时输出.min.js版本
    
### gulp api
    1. gulp.task 用来定义任务，第一个参数指定任务名称，第二个参数为函数实现，使用gulp执行时，会调用入口任务名字为default的任务，此任务可以指定多个
    其他的任务
        gulp.task('default',['css', 'js'], function(){
          console.log('task done');
        });
    2. gulp.src(path) 传入要压缩的文件路径，gulp.dest(path)传入输出路径
    3. 添加es6到es5转换插件
        	.pipe(babel({
            presets:['es2015']
          }))
    4. 对js代码进行压缩
        .pipe(uglify())
    5. 同时输出压缩版js和未压缩版js
        gulp.task('js', function(){
          return gulp.src('src/js/my.js')
            .pipe(babel({
              presets:['es2015']
            }))
            .pipe(gulp.dest('dist/js/'))
            .pipe(uglify())
            .pipe(rename({extname:'.min.js'}))
            .pipe(gulp.dest('dist/min/js/'));
        });
    
