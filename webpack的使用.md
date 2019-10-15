1、webpack是将依赖不同类型的模块依赖文件打包为静态文件  
2、webpack可以将es6转换为es5  
3、在根目录创建webpack.config.js

    module.exports = {
        entry: './src/index.js',
        output: {
            path: path.join(__dirname, 'dist'),
            filename: "bundle.js"
        },
        mode: 'production'
    }

4、entry就是要打包的文件，output是经过webpack编译后的文件输出的文件位置  
5、在项目package.json中添加scripts，里边添加webpack键值对方便使用`npm run ***`直接启动  
6、如果是多入口则entry需要改为对象，entry改为对象的时候，output也要同步改,可以用占位符确保名称唯一

    entry: {
            home:'./src/index.js',
            news:'./src/news.js'
        },
        output: {
            path: path.join(__dirname, 'dist'),
            filename: "[name].js"
        }
7、webpack默认处理js和json，如果处理vue这种则需要用loaders去支持转换,使用test指定规则use指定loader名称

    module:{
            rules:[{
                test: /\.css$/, use:'css-loader'
            }]
        }

8、plugin是用来拓展webpack功能的，在整个构建过程中都会起作用，loader是处理文件的，plugin不直接操作文件，但是对整个构建起作用，使用`plugins`
关键字进行指定  

9、mode可以指定当前构建的环境可以用`production` `development` `none`,默认是production，一旦mode设置为development，那么
process.env.NODE_ENV的值就为development，同样的mode为production也会设置，设置为none的时候什么都不会设置  

10、webpack解析es6和vue，解析es6主要是通过babel-loader转换，在module的rules中添加，babel-loader是依赖babel的，需要增加.babelrc配置文件
并增加preset配置，`npm i @babel/core @babel/preset-env babel-loader --save-dev`安装babel

    {
        test: /\.js$/, use:'babel-loader'
    }
    
.babelrc的配置为

    {
      "presets": [
        "@babel/preset-env"
      ]
    }

11、webpack解析css，css-loader用来加载css文件并且转换成commonjs对象，style-loader将样式通过style标签插入到head中`npm i css-loader style-loader --save-dev`,这里要先写style-loader后写css-loader，执行顺序是从右到左的否则会有问题

    {
      test: /\.css$/, use:['style-loader', 'css-loader']
    }

12、webpack使用热更新，在package.json中，修改scripts，添加`"dev":"webpack-dev-server --open"`,并在在webpack.config中把mode改为
development，而且需要在webpack.config中配置plugin

    plugins: [new webpack.HotModuleReplacementPlugin()],
    devServer: {
        contentBase: './dist',
        hot:true
    },
    mode: 'development'
    
13、webpack生成资源指纹,指纹只能在发布版时才可以使用，配置package.json的scripts脚本  

    "build": "webpack --config webpack.pro.js",
    "dev":"webpack-dev-server --config webpack.dev.js --open"

14、webpack 对不同机型分辨率的转换，使用rem相对单位，`px2rem-loader`可以将px自动转换为rem

        {
            loader:"px2rem-loader",
            options:{
                remUnit:75, //一个rem=75px
                remPrecision:8
            }
        }
        
然后使用阿里的lib-flexible 自动计算根元素宽度  

15、将资源内联到代码中，使用raw-loader,`npm i raw-loader@0.5.1 -D`  

16、多页面打包，将每个页面以及资源都用文件夹进行分类，每个文件夹内部的文件命名及结构统一

    src
        index
            index.html
            index.js
            index.css

        news
            index.html
            index.js
            index.css

