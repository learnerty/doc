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

#### 生命周期函数
`默认执行，不需要调用`  
##### 初始化,首次挂载
constructor() 获取默认属性  执行顺序最高,如果要从constructor中获得props，需要
```js
constructor(props){
  super(props);
}
```
componentWillMount()  首次渲染之前  
render() 渲染  必须写，必须有返回值，返回值为JSX节点   
componentDidMount()  首次渲染之后  

##### 更新
修改props,通过setState修改state会触发组件的更新阶段  
componentWillReceiveProps(nextProps)  组件将要收到新的props属性发生变化，就会触发更新(父级传入的props发生变化，而且必须是父级控制的state发生变化)   
shouldComponentUpdate(nextProps, nextState)  判断是否需要更新，必须返回一个布尔值 返回true更新，false阻止更新
componentWillUpdate(nextProps, nextState)   更新之前  nextState下一个状态   
render() 渲染  
componentDidUpdate(prevProps, prevState)   更新之后   prevState更新成功之前的状态  
##### 销毁
componentWillUnmount()



#### 表单
e.target  触发事件的目标
```js
constructor(){
  super();
  this.state={
    input:''
  }
}
handleSubmit(e){
  e.preventDefault()  //阻止跳转
  e.target.reset()    //清空表单数据,用状态控制无法清空
}
handleChange(e){
  console.log(e.target.value);
  this.setState({input:e.target.value})
}
<form onSubmit={this.handleSubmit.bind(this)}>
  <input placeholder='name' value={this.state.input} onChange={this.handleChange.bind(this)}/>
  <button>提交</button>
</form>
```
defaultValue 非受控的，只能通过设置ref获得值

文本域  下拉菜单
```js
textarea(e){
  this.setState({textarea:e.target.value})
}
<textarea value={this.state.textarea} onChange={this.textarea.bind(this)}/>

handleSelect(e){
  this.setState({select:e.target.value})
}
<select value={this.state.select} onChange={this.handleSelect.bind(this)}>
  <option value="gr">Gr</option>
  <option value="hr">Hr</option>
</select>

handleRadio(e){
  this.setState({radio:e.target.value})
}
男<input name="goodRadio" type="radio" value="boy" onChange={this.handleRadio.bind(this)}/>
女<input name="goodRadio" type="radio" value="gril" onChange={this.handleRadio.bind(this)} defaultChecked/>
```
多选
```js
handleCheck(e){
  this.setState({checkbox:e.target.checked})
}
<input type="checkbox" checked={this.state.checkbox} onChange={this.handleInput.bind(this)} name="checkbox"/>
```


声明一个对象时，属性名也可以是一个变量，用方括号包裹
```js
let prop = 'aaa';
let obj = {[prop] : 888}
let obj1[prop] = 888;
```

所以可以把上面的一堆方法整合
```js
handleSubmit(e){
  e.preventDefault();
}
handleInput(e){
  let target = e.target;
  console.log(target.name);
  let value = target.name==='checkbox' ? target.checked : target.value
  console.log(value);
  this.setState({
    [target.name] : value
  })
}
<form onSubmit={this.handleSubmit.bind(this)}>
  <input value={this.state.input} onChange={this.handleInput.bind(this)} name="text"/>
  <textarea value={this.state.textarea} onChange={this.handleInput.bind(this)} rows="5" cols="20" name="textarea"/>
  <select value={this.state.select} onChange={this.handleInput.bind(this)} name="select">
    <option value="gr">Gr</option>
    <option value="hr">Hr</option>
  </select>
  <br/>
  同意<input type="checkbox" checked={this.state.checkbox} onChange={this.handleInput.bind(this)} name="checkbox"/>
  <br/>
  男<input name="goodRadio" type="radio" value="boy" onChange={this.handleInput.bind(this)}/>
  女<input name="goodRadio" type="radio" value="gril" onChange={this.handleInput.bind(this)} defaultChecked/>
  <br/>
  <button>提交</button>
</form>
```

trim() 去掉字符串首尾的空格  
<input type='number'/>  只能输入数字  
<input type='range' max='100' min='10'/>  滑动条

#### JSON
JSON格式最后一项不能加括号，数据类型永远是字符串   
JSON.stringify() 把正常的js对象或数组转换成JSON字符串
```js
let obj = {name:'tian'};
console.log(JSON.stringify(obj));
```
JSON.parse()  把JSON对象转换成正常的js变量
```js
let jsonStr = '{"name":"tian"}';
let o = JSON.parse(jsonStr);
```
#### 本地缓存
`sessionStorage`关闭浏览器保存的信息清空`localStorage`一直存在
保存一个本地的储存
localStorage.aaa=‘ooo’  
localStorage.setItem('aaa','ooo')
获得本地储存的数据
localStorage.aaa   
localStorage.getItem('aaa')
删除本地缓存  
localStorage.removeItem('aaa')
## react-router-dom
## 路由
首先要在项目内装一个包  
npm install react-router-dom --save

function App(props){}默认传入一个props  
```js
function App({title,age}){
  return (
    <div>
      {title}{age}
    </div>
  )
}
<App title='tian' age={23}/>
```

`BrowserRouter as Router  把Ccc作为App来使用,Router代替BrowserRouter`  
`BrowserRouter 需要后台服务器支撑，需要服务器配合使用，HashRouter不需要服务器支撑，在页面路径前多了/#，表示在本页面跳转，两个都是找的一个html`   
import {BrowserRouter as Router, Route, Link} from 'react-router-dom';  
Router组件本身是一个容器，所有组件都放在<Router></Router>里,只能有一个children，不能有多个节点，Route写单条的路由规则:<Route path='地址' component={组件名} />   exact严格匹配
```js
<Router>
  <div>
  <Link to='/about'>about</Link>
  <Route exact path='/' component={Home} />
  <Route path='/about' component={About} />
  </div>
</Router>
```
可以嵌入一个变量，冒号表示变量,冒号后写变量名来写变量  path='/:变量名'  可以用{props.match.params.变量名}来拿到变量的值

#### 请求重定向
<Redirect from='/old' to='/new'/>  将old页面请求跳转到new页面

<Switch></Switch> 不加的话是所有符合的都会挂载上，加上后匹配规则变为，从上往下找，成功匹配到一条就不往下找了
```js
<Switch>
  <Route exact path='/' component={Home} />
  ...
</Switch>
```

不写path任何页面都能匹配到，用来写404页面，放在最底下
```js
<Switch>
  ...
  <Route component={Not} />
  最好用：
  <Route path='/404' component={NotFound} />
  <Redirect from='*' to='/404'/>
</Switch>
```

<NavLink></NavLink> 用作导航，在当前选中页有默认的class名：active，可以用activeClassName=""来更改默认的名称，也可以activeStyle={{...: '...'}}来写行内样式

`history方法`
```js
this.props.history.push('/work')  //跳转到
this.props.history.goBack();  //返回上一级
this.props.history.go(-2);  //往回倒两步
this.props.history.goForward();  //向前一步
```

挂载到root的组件默认会被注入props，但二级组件没有被注入props，需要
```js
import { withRouter } from 'react-router';
export default withRouter(Home)
```
