# react
## react demo
首先，必须导入

import React from 'react';
import ReactDOM from 'react-dom';


ReactDOM.render 把写的东西渲染到浏览器

ReactDOM.render(渲染什么东西,渲染到哪里)


querySelector  和$用法一样，代替$，找到匹配到的第一个

querySelectorAll  返回所以元素，找到的是一个数组，用[ ]来找

#### JSX语法
是对语法的拓展，不是一个新的语法

例如：`let hello = <p>hello world</p>` 就是一个JSX语法

JSX语法需要babel进行编译，转为这个方法 React.createElement();
```js
var hello = React.createElement(
  "p",
  null,
  "hello world"
);
```

Adjacent JSX elements must be wrapped in an enclosing tag 相邻的JSX元素必须包裹在一个闭合标签内  
每一个标签必须闭合Unterminated JSX contents  
class要写成className  for写成htmlFor

标签区分大小写

在JSX语法中可以嵌入变量或者求值表达式,可以写js语法，用一对大括号包裹即可,不可以写js语句


#### React组件(3种)
当做自定义标签使用，定义的组件名称首字母必须大写，渲染的时候也要首字母大写，一般组件都是写成直观闭的 < /> 组件可以嵌套组件
1. React.createClass
```js
let Hello = React.createClass({
  render:function(){
    return (
      <div>
        <h1>我是第一种组件的创建方式，即将废弃</h1>
      </div>
    )
  }
})
// ReactDOM.render(<Hello></Hello>, document.querySelector('#root'))
ReactDOM.render(<Hello />, document.querySelector('#root'),function(){console.log('回调函数');})
```
2. function(){}
```js
function World() {
  return(
    <h2>我是 hello World</h2>
  )
}
function Hello() {
  let x = 666;
  return(
    <div>
      <h1>我是第二种组{x}件的创建方式，必须有返回值，而且返回值必须是 JSX elements</h1>
      <World></World>
    </div>
  )
}
ReactDOM.render(<Hello />, document.querySelector('#root'))
```
3. class 组件名 extends React.Component{render(){}}
```js
class Hello extends React.Component{
  render(){
    return(
      <div>
        <h1>我是第三种组件的创建方法</h1>
      </div>
    )
  }
}
```
render(){} === render:function(){}

引入本地图片也和引入模块一样，把图片当做模块引入 例如：import img from './avater.jpg' 网上的图片直接写图片地址


引入css文件可以直接引入  `import './xxx.css'`

#### 行内样式
style = {{}}  
style = 一个对象 {属性名:'属性值',属性名:'属性值'}，因为对象是js语句，JSX语法不能写js语句，所以在对象外面用一对大括号包裹起来，遵循驼峰命名法，如fontSize

三种写行内样式的方法,还可以在外部导入变量
```js
import {red, style} from './style'
class Main extends React.Component{
  getStyles(){
    return ({
      textAlign: 'center'
    })
  }
  render(){
    let styles = {
      textAlign: 'center'
    }
    return (
      <div>
        <h2 style = {{textAlign:'center',color:red}}>我是身体1</h2>
        <h2 style = {styles}>我是身体2</h2>
        <h2 style = {this.getStyles()}>我是身体3</h2>
        <h2 style = {style}>我是导入的样式</h2>
      </div>
    )
  }
}
```

在JSX语法中，写注释要用大括号包起来  `{/* */}` ctrl + / 快捷键

对象合并  
Object.assign({},styles.common,styles.spec)  
创建一个新的对象，把后面的所有的对象的属性赋值给空对象，相同的属性，后面的会覆盖前面的



#### 状态
state  是一个异步操作，不会阻断进程  
名称必须是state,与setstate对应，state是一个对象，setstate()是一个方法  bind(this)绑定一个this
```js
class App extends React.Component{
  constructor(){
    super();
    this.state = {
      num:0
    }
  }
  handleClick(num){
    this.setState({
      num: this.state.num + num
    })
  }
  render(){
    return (
      <div className='app'>
        <p>数量是: {this.state.num}</p>
        <button onClick={this.handleClick.bind(this,1)}>+1</button>
        <button onClick={this.handleClick.bind(this,-1)}>-1</button>
      </div>
    )
  }
}
```

#### 计时器
用this.interval代替let interval  
clearInterval(this.interval)  
this.interval=setInterval(()=> this.setState({num:this.state.num+1}),1000)


#### vw可视窗口的宽度 vh可视窗口的高度
100vw 100%可视窗口的宽度    100vh 100%可视窗口的高度

#### 垂直居中
```css
.play{
  display: flex;   //变成弹性盒子
  align-items: center;   //垂直居中
}
.play>div{
  flex-grow: 1;   //加在子元素上
}
```

#### 下面的也是if判断
let cc = 6;  
cc && cc==6 && alert('aaa');console.log('qqq')
## react props
#### props
组件之间沟通，只能父子之间，父组件向子组件传数据，父组件在子组件的标签上写要自定义属性的，子组件用this.props接收，组件内部在任何地方都可以拿到
```js
父组件
<Btn title='注册' pad={13} bg='red'/>
子组件
<button style={{border:'none',padding:`${this.props.pad}px`,background:this.props.bg,color:'#fff'}}>
  {this.props.title}
</button>

在子组件里写，组件默认的属性
Btn.defaultProps = {
  title:'我是默认的标题',
  bg:'blue',
  pad:21
}
```
#### 检测传入的props的数据类型
首先安装检测类型的包 npm install prop-types  
```js
import PropTypes from 'prop-types';
Btn.propTypes = {
  title: PropTypes.string
}
```

#### children
特殊的props，写在标签中间
```js
<Child>
  <p style={{fontSize:'20px'}}>ddddddddd</p>
</Child>
{this.props.children}
```
