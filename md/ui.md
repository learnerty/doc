## material-ui
1. 装包 yarn add material-ui
2. 装包 yarn add react-tap-event-plugin
3. 在入口文件添加
```
import injectTapEventPlugin from 'react-tap-event-plugin';
injectTapEventPlugin();
```
4. 导入 import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider' 只需导入一次
5. 把用到的ui组件挂载到 MuiThemeProvider  只能有一个子节点，所以要用div包起来
```
<MuiThemeProvider>
  <div>
    <RaisedButton label="Default" />
  </div>
</MuiThemeProvider>
```
