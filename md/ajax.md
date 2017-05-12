## js原生AJAX  
#### GET
```js
var xml = new XMLHttpRequest();    //创建 XMLHttpRequest 对象
xml.onreadystatechange=function(){  //存储函数,每当readyState属性改变时,就会调用该函数
  if(xml.readyState===4&&xml.status===200){  //readyState=4代表请求以完成且响应已就绪，status=200表示请求成功
    console.log(xml.responseText);   //responseText获得字符串形式的响应数据
  }
}
xml.open('GET','https://api.github.com/users/learnerty',true);   //打开
xml.open('请求方式','地址',是否异步(true或false));
xml.send();   //发送
```
readyState
```
存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。
0: 请求未初始化
1: 服务器连接已建立
2: 请求已接收
3: 请求处理中
4: 请求已完成，且响应已就绪
```
请求包括请求头和请求体，响应包括响应头和相应体，头包含客户端或服务器端的配置信息，体包括发送或返回的具体数据

#### POST
```js
xml.open('POST','路径',true)
xml.setRequestHeader("Content-type","application/json");  //添加请求头，设置为json格式
let data = {   //要传的数据
  名称: '数据'
}
xml.send(JSON.stringify(data));   //转成json格式发送
```


## jqAJAX
```js
$.ajax({
  type:'GET',//默认为GET jq版本高于1.9新增了method
  url:'https://cnodejs.org/api/v1/topics',  //路径
  success:function(data){  //success成功后，会自动把后台返回的json转换成对象
    console.log(data);
  }
  error:function(error){  //失败
    console.log(error);
  }
})
```
#### 链式操作+POST
```js
$.ajax({
  method:'POST',  //提交方式
  dataType:'json',  //期望后台返回的数据类型
  contentType:'application/json', //发往后台的数据类型
  url:'https://cnodejs.org/api/v1/accesstoken',   //提交地址
  data:JSON.stringify({accesstoken: '3f77acb1-d753-4393-b784-44913190e6a8'})   //发给后台的数据
}).done(function(data){   //.done  成功执行
  console.log(data);
}).fail(function(err){   //.fail  失败执行
  console.log(err);
}).always(function(){    //.always  无论成功失败都执行
  console.log('ajax');
})
```

AJAX不能够实现跨域请求，为了能够实现跨域请求，一般需要后台进行蛇者，但还是有些需要前台进行设置，在jq中，需添加
```js
dataType:'jsonp',
jsonp:'callback'
```

#### fetch
es6的语法 成功 .then,失败 .catch
```js
fetch('地址',method:'POST',body:'数据')
fetch('https://api.github.com/users/learnerty')  //请求完成
  .then(function(response) {   //拿到后台返回的响应
    return response.json()    //转换成json数据
  }).then(function(json) {
    console.log('parsing json', json)  
  }).catch(function(ex) {   //失败
    console.log('parsing failed', ex)
  })
```

#### axios
装包 `npm install axios`
```js
axios.get('https://api.github.com/users/learnerty')
  .then(res => console.log(res))
  .catch(err => alert(err))
axios.post('https://cnodejs.org/api/v1/accesstoken',{accesstoken:token})
```
