## es6语法
#### call 和 apply
语法：foo.call(this, arg1,arg2,arg3) == foo.apply(this, arguments) == this.foo(arg1, arg2, arg3);

apply：应用某一对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即A对象应用B对象的方法。 apply：最多只能有两个参数——新this对象和一个数组argArray。

call：调用一个对象的一个方法，以另一个对象替换当前对象。例如：B.call(A, args1,args2);即A对象调用B对象的方法。 call：它可以接受多个参数，第一个参数与apply一样，后面则是一串参数列表。


let 自带作用域，代替var,在同一作用域不可以重复声明,没有声明提升

const 常量，只能读不能写,可以改变对象内的属性，不可以直接改变定义的值

数组解构赋值，按下标严格匹配

对象的解构赋值，按照属性名匹配  `也是在声明变量`

定义对象的属性可以直接写定义的变量的名称，name等同于name:name,函数也可以直接写run(){}等同于run:function(){}
  ```js
  let name = 'tian';
  let age = '23';
  let say = function(){
    console.log('say');
  }
  let obj = {
    name,
    age,
    say,
    run(){
      console.log('run');
    }
  }
  ```


#### 箭头函数
函数体内的this对象就是定义时所在的对象，而不是使用时的对象
let 函数名 =(参数) => 返回值  let a = () =>8; 等同于：
```js
  var a = function(){
    return 8;
  }
```
```js
 let a = (num,num1) => num*num1;
 console.log(a(5,6));
```
如果多个操作,就需要return
```js
let a = (num,num1) => {
  num = ++num
  num1 = ++num1
  return num*num1
}
console.log(a(5,6));
```
如果返回的是一个对象，用()包起来 let a = (num,num1) => ({name:'a'})

setTimeout(()=> console.log(55),50)


#### 字符串拼接
用两个反引号包裹要拼接的字符串，${}内写定义的变量名,{}内还可以对变量进行运算,charAt返回与下标匹配的字符串
```js
let name = 'tian';
let age = '23';
let obj = {
  name:"aaa"
}
let str =`<p class="active">${obj.name}姓名:${name.charAt(2)},年龄:${age*2}</p>`;
document.body.innerHTML = str;
```

#### es6函数的默认值
可以在形参内定义一个默认值，如果不传入参数，等于默认值，传入参数等于所传的参数
```js
function sum(num=5){
  return ++num
}
console.log(sum(8));
```
也可以在参数进行结构赋值，下列代码拿到的是tian这个值
```js
function sum({name}){
  console.log(name)
}
sum({name:'tian'});
```

#### rest剩余参数
剩余的所有参数，语法: ...参数
```js
function restFunc(a,...rest){
  console.log(a); //1
  console.log(rest);  //[]
}
restFunc(1)

function restFunc(a,...rest){
  console.log(a);  //1
  console.log(rest);  //[2,3,4]
}
restFunc(1,2,3,4)
```

#### reduce
数组的方法，里面写一个函数，函数有四个参数，前两个是要操作的数，第三个参数是下标，第四个参数是数组，该方法必须有返回值，根据返回值来进行操作，第一次循环是从数组拿出两个数赋给前两个参数，第二次循环是把返回值当做第一个参数，从数组向下取一位赋给第二个参数
```js
[0,1,2,3,4].reduce(function(acc,cur,index,array){
  console.log(acc,cur);
  return acc + cur;
})
let arr = [12,65,23,15,9];
let max = arr.reduce ((acc,cur) => {
  return acc>cur? acc : cur
})
console.log(max);
```
#### 展开操作符
```js
let arr = [0,1,2,3];
let arr1 = [...arr,4,5];
console.log(arr1)

let obj = {a:{b:1}};
let {...x} = obj;
console.log(x);
```

#### 导入导出
let str = 'tian';
let obj = {age:23}

export {str,obj}  // 命名导出

import {str} from './test';  //导入

import {str `as` ccc} from './test.js';  //把str重命名为ccc

export default str; //默认导出   只能导出一个

import aaa from './test.js'  //导入，可以随便定义一个名称来导入默认导出的内容

#### 数组.filter()方法
```js
var filtered = [12, 5, 8, 130, 44].filter(function(value ,index ,array) {
  return value >= 10;  //把符合的留下，放在新的数组里
});
// filtered is [12, 130, 44]
```
#### 数组.map()函数
根据原有的数组生成一个新的数组，不破坏原有数组，生成的规则由函数内规定
```js
var numbers = [1, 4, 9, 15];
var doubles = numbers.map(function(item,index,array) {
  return item * 2;
});
var roots = numbers.map(item => `<p>${item}</p>`);
console.log(roots)
```
#### .forEach()
遍历数组，没有返回值
```js
let arr = [1, 4, 9, 15];
arr.forEach(item => {console.log(item);})

arr.forEach(function(item){
  console.log(item);
  })
```
#### .forin
没有返回值，遍历，可用obj[variable]获得值
```js
let obj = {name:"tian",age:23};
for (var variable in obj) {
  console.log(variable)
}
```
#### keys
有返回值，把返回的值存在数组内,返回其枚举自身属性的对象，可用obj[variable]获得值
```js
let obj = {name:"tian",age:23};
let names = Object.keys(obj);
console.log(names); //[name,age]
```
#### findIndex
遍历对象  得到符合条件的对象的下标
```js
let arr = [
  {name:'tian',age:23,id:45322},
  {name:'tian',age:24,id:453222},
  {name:'tian',age:13,id:4522},
  {name:'tian',age:32,id:453322}
]
let index = arr.findIndex(item =>item.age ===13)
console.log(index)
```
#### throw new Error 主动报错，抛出错误

#### class
语法  constructor(参数){私有属性}  首字母大写
```js
class Point {
  constructor(x, y) {
    // 属性全部放在这里
  }
  // 方法 不能用逗号隔开
  toString() {

  }
}
```
#### 继承关键字  extends  
把私有属性也会继承过来,子类必须要加super()
```js
class Po{
  constructor(x){
    this.x = x;
  }
  toString(){
    console.log('Po toString');
  }
}

class Po1 extends Po{
  constructor(a,b,x){
    super(x);
    this.a = a;
    this.b = b;
  }
  say(){
    console.log('Po1 say');
  }
}
var p = new Po1(5,6,7);
console.log(p);
p.toString();
p.say();
```

```js
class [name]{}  //定义类
class [name] extends [fathername]{}  //继承类
class [name] extends [fathername]{  //子类定义constructor必须先super()
  constructor(){
    super()
  }
}
class内只能写一个个的方法，方法与方法之间什么都不加，不可以有逗号
class的名字首字母大写
class内的方法内部就一切正常了，想写什么写什么
```

#### .assign
Object.assign方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）,Object.assign方法的第一个参数是目标对象，后面的参数都是源对象 ，如果有相同的属性，后面的会把前面的覆盖掉
```js
var target = { a: 1};
var source1 = { b : 2};
var source2 = { c : 3};
Object.assign(target, source1 , source2);
console.log(target); //Object {a: 1, b: 2, c: 3}
```

includes() 方法用来判断当前数组是否包含某指定的值，如果是，则返回 true，否则返回 false
```js
var a = [1, 2, 3];
a.includes(2); // true
a.includes(4); // false
```
