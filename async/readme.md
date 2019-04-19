# JavaScript异步解决方案 #
***
| Author  | ripple |
| :---:  | ------ |

## 简介 ##

主要介绍JavaScript在解决异步放上上的历史演变

## 大纲


- 回调函数
- 事件监听
- Promises对象
- Generator
- 使用async函数
- 借助流程控制库
- 使用Web Workers
- 对比（案例）

##### 回调函数
```js

function f1(callback){
    setTimeout(function(){
        //f1的任务代码
        callback();
    },1000);
}
f1(f2);

```

##### 事件监听
```js

function f1(callback){
    setTimeout(function(){
        //f1的任务代码
        callback();
    },1000);
}
f1(f2);

```

##### promise对象

Promise.all

```js

var p1 = new Promise(function(resolve,reject){resolve('one')})
var p2 = new Promise(function(resolve,reject){resolve('two')})
Promise.all([p1,p2]).then((res) =>{console.log(res)})

//["one", "two"]

```

```js

var p1 = Promise.resolve(1)
var p2 = Promise.reject(2)
var p3 = Promise.reject(3)
Promise.all([p1,p2,p3]).then((res) =>{console.log(res)}).catch((e) =>{console.log(e)})

//2 

```

##### Generator
```js

 function* gen() {    
        yield 1;    
        yield 2;    
        return 1;
      }
      var g = gen();
      gen.next() // {value:1,done:false}
      gen.next() // {value:2,done:false}
      gen.next() // {value:3,done:true}

```

##### async函数

```js
async function fn(){
	//	过程
	let a = await Promise.resolve(1)
	let b = await 3
    let c = await new Promise((resolve) =>{resolve(a+b+1)})
	
    //结果
    return c //return 出来的值为函数执行后得到的promise的值
}

fn()


```


参考网站
***
- https://www.jianshu.com/p/2f5d72703c46 （*Javascript异步解决方案的发展历程*）