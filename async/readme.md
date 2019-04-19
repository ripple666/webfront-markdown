# JavaScript异步解决方案 #
***
| Author  | ripple |
| :---:  | ------ |

## 简介 ##

主要介绍JavaScript在解决异步放上上的历史演变

## 大纲


- 回调函数
- 事件监听
- 发布/订阅（观察者模式）
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

参考网站
***
- https://www.jianshu.com/p/2f5d72703c46 （*Javascript异步解决方案的发展历程*）