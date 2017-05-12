## 2 npm yarn
初始化node项目  
```bash
  npm init
  等同
  yarn init
```

npm install jquery --save  安装jquery插件  --save 向package.json记录  
等同yarn add jquery

npm install  安装配置文件package.json记录的所有依赖

用npm装的包，直接require('包名')，如果是自己的包，则require('相对路径/包名')

安装指定版本的最高版本 npm install jquery@3.0 --save-dev    一般用来安装开发所用的  
等同yarn add -D jquery@3.0

安装第三方模块
```js
npm install [packagename] [--save]
//安装到了node_modules
--save:记录到dependencies字段下
--save-dev:记录到devDependencies字段下
--global:缩写为 -g  全局安装,安装到我们的系统上，可以在任何位置使用
```

卸载模块
```bash
  npm uninstall [packagename] [-g]  不是全局不用加-g
  卸载后需要手动在package.json里删除依赖关系
```

npm install -g create-react-app 安装react开发环境  
create-react-app 名称  创建react环境  
create-react-app --version  查看版本  
create-react-app --help   查看帮助  
npm run start  运行  
npm list -g 查看全局装的包  
npm install yarn -g  安装yarg

#### yarn
```
开始新项目 yarn init
添加依赖包
yarn add [package]
yarn add [package]@[version]
yarn add [package]@[tag]
升级依赖包
yarn upgrade [package]
yarn upgrade [package]@[version]
yarn upgrade [package]@[tag]
移除依赖包
yarn remove [package]
安装项目的全部依赖
yarn或者yarn install
```
