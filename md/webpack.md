#### 安装webpack  
npm install -D webpack(项目内局部安装)  
npm install -g webpack(全局安装)

打包(全局安装webpack)  
webpack src/index.js build/bundle.js --- webpack 入口文件 出口文件  
(非全局)  
./node_modules/.bin/webpack 入口文件 出口文件

在packges.json配置,可以执行npm run bulid执行打包操作    --watch监听，更改后自动更新
```
"scripts":{
  "bulid": "./node_modules/.bin/webpack src/index.js build/bundle.js --watch"
}
```


### 用配置文件配置(推荐)
如果想要支持es6 和JSX 语法，首先要安装babel  
`npm install --save-dev babel-loader babel-core`  
使用es6语法需要装包babel-preset-env  
`npm install babel-preset-env --save-dev`  
使用JSX语法需要装包babel-preset-react  
`npm install --save-dev babel-preset-react`  
还要新建文件.babelrc  
```
{
  "presets": ["env","react"]
}
```
要导入css文件需要装两个包，如果安装了postcss-loader包，则不需要装css-loader包  
`npm i --save-dev style-loader css-loader`
#### packges.json
```
"scripts":{
  "bulid": "./node_modules/.bin/webpack"
}
```
#### webpack.config.js
```
const path = require('path');   nodejs的核心模块
var webpack = require('webpack');
const ExtractTextPlugin = require("extract-text-webpack-plugin");
module.exports = {   模块接口
  entry: './src/index.js',     要打包的文件，入口文件
  output: {     打包到哪里，出口文件
    path: path.resolve(__dirname,"build"),  __dirname代表webpack.config.js的绝对路径  拼接build文件夹，形成路径
    filename: "bundle.js",  文件名
    publicPath: 'build/'   公共路径，图片等打包后的路径是生成的文件名，需要添加公共路径来获得正确的路径
  },
  watch: true,    是否监听，true监听,false不监听
  devtool: "source-map",    报错报到源代码里
  module: {   模块
    rules: [   规则
      { test: /\.js$/, exclude: /node_modules/, use: "babel-loader" }, 打包以.js为结尾的,就用babel-loader处理，exclude排除node_modules文件夹
      {
        test: /\.css$/,
        use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: "postcss-loader"
        })
      },  把css单独生成文件,添加css前缀
      { test: /\.(jpe?g|png)$/, use: "file-loader" },  打包图片
      { test: /\.less$/,use: [ 'style-loader', 'postcss-loader','less-loader' ] }  less
    ]
  },
  plugins:[  插件
    new webpack.optimize.UglifyJsPlugin({
      compress: {
        warnings: false,   不要警告
        drop_console: false,    删掉注释
      }
    }),
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': '"production"',   生产环境
    }),
    new ExtractTextPlugin("styles.css"),   生成单独css文件存放位置，出口是output定义的出口
    new HtmlWebpackPlugin({
      template: 'template/index.html',   模板html文件参考地址
      filename: path.resolve(__dirname,'index.html')  生成模板的位置,webpack.config.js文件同级的index.html页面
    })
  ]
}
```

#### 添加css前缀
先装包   
`npm i -D  postcss-loader`  
`npm i -D autoprefixer`  
`npm i -D cssnano`  
新建postcss.config.js文件
```
module.exports = {
  plugins: [
    require('autoprefixer'),   导入autoprefixer，添加css前缀
    require('cssnano')  导入cssnano,压缩css样式
  ]
}
```
#### 打包图片
装包  
`npm install --save-dev file-loader`
#### 把css分离到一个单独的文件
装包  
`npm install --save-dev extract-text-webpack-plugin`
#### 自动生成一个html
装包  
`npm install --save-dev html-webpack-plugin`

### css预处理器
`less` 文件后缀是less  
装包
`npm i -D less less-loader`
1. 可以嵌套
2. 支持变量
事例,新建main.less
```
@blue: '#666';
@opac: 1;
.p{
  text-align: center;
}
.box{
  background-color: red;
  &:hover{
    background-color: #dd5555;
  }
  transition: all 1s;
  p{
    font-size: 22px;
    color: @blue;
    opacity: @opac*0.5;
    .p();
  }
}
```

`sass` 文件后缀是scss
