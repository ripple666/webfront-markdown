# 前端笔记

***
| Author  | ripple |
| :---:  | ------ |
| E-mail | 651632406@qq.com |

## 简介

该文件用来记录前端一些基本的知识和用法，包括CSS、js的基本语法，npm,nodejs,webpack，canvas，svg,vue，react,等等一系列的相关知识点






## JavaScript必备知识点
- 内置类型
	- 原始（Primitive）类型
	- 对象（Object）类型
	- 类型转换
	- 四则运算符
- 原型以及原项链
- new
- this
- instanceof
- 执行上下文


### 内置类型
#### 原始（Primitive）类型
- js有6种原始类型，boolean，null，undefined，number，string，symbol
- NaN 也属于 number 类型，并且 NaN 不等于自身
- null === null
- 首先原始类型存储的都是值，是没有函数可以调用的，比如 undefined.toString()
![](https://i.imgur.com/nFoGBtV.png)
- typeof null 会输出 object，但是这只是 JS 存在的一个悠久 Bug。在 JS 的最初版本中使用的是 32 位系统，为了性能考虑使用低位存储变量的类型信息，000 开头代表是对象，然而 null 表示为全零，所以将它错误的判断为 object 。虽然现在的内部类型判断代码已经改变了，但是对于这个 Bug 却是一直流传下来。
```js
typeof 1 // 'number'
typeof '1' // 'string'
typeof undefined // 'undefined'
typeof true // 'boolean'
typeof Symbol() // 'symbol'
typeof null // 'object'
```

#### 对象（Object）类型
- 原始类型存储的是值,对象类型存储的是地址（指针）。当你创建了一个对象类型的时候，计算机会在内存中帮我们开辟一个空间来存放值
- typeof 对于对象来说，除了函数都会显示 object
```js
typeof [] // 'object'
typeof {} // 'object'
typeof console.log // 'function'

```
- 如果我们想判断一个对象的正确类型，这时候可以考虑使用 instanceof
```js
const Person = function() {}
const p1 = new Person()
p1 instanceof Person // true

var str = 'hello world' 
str instanceof String // false

var str1 = new String('hello world') //这里的string是对象类型，String {"hello world"}
str1 instanceof String // true
```

- 对于常量 a 来说，假设内存地址（指针）为 #001，那么在地址 #001 的位置存放了值 []，常量 a 存放了地址（指针） #001
```js
const a = []
```

- 当我们将变量赋值给另外一个变量时，复制的是原本变量的地址（指针），也就是说当前变量 b 存放的地址（指针）也是 #001，当我们进行数据修改的时候，就会修改存放在地址（指针） #001 上的值，也就导致了两个变量的值都发生了改变。
```js
const a = [];
const b = a;
b.push(1)
```

```js
function test(person) {
  person.age = 26  //指的是#001这个地址
  person = { //新分配 #002新的地址，person 拥有了一个新的地址（指针）
    name: 'yyy',
    age: 30
  }

  return person
}
const p1 = { //分配 #001地址
  name: 'yck',
  age: 25
}
const p2 = test(p1)
console.log(p1) // {name: "yck", age: 26}
console.log(p2) // {name: "yyy", age: 30}
```

#### 类型转换
	
- 一般可以通过 Object.prototype.toString.call(xx)获取一个变量的正确类型。得到的结果为 [object Type] 的字符串。
- 常见类型转换有三种：
	- 转换为布尔值
	- 转换为数字
	- 转换为字符串

| 原始值  | 转换目标 | 结果    |
|-------|:---:|-----------|
| 0,NaN,undefine、null,""  | 布尔值 | false |
| 数组  | 字符串   | [1,2] => '[1,2]' |
| 对象  | 字符串   | {name: "yck", age: 26} => "[object Object]" |
| []、null、''、false | 数字   | 0 |
| 除了空数组的引用类型，undefine  | 数字   | NaN |
| ture | 数字   | 1 |

- 对象在转换类型的时候，会调用内置的 [[ToPrimitive]] 函数,该函数的算法逻辑:
	- 如果已经是原始类型了，那就不需要转换了
	- 调用 x.valueOf()，如果转换为基础类型，就返回转换的值
	- 调用 x.toString()，如果转换为基础类型，就返回转换的值
	- 如果都没有返回原始类型，就会报错
当然你也可以重写 Symbol.toPrimitive ，该方法在转原始类型时调用优先级最高。
```js
let a = {
  valueOf() {
    return 0
  },
  toString() {
    return '1'
  },
  [Symbol.toPrimitive]() {
    return 2
  }
}
1 + a // => 3
```

#### 四则运算符
- 只有当加法运算时，其中一方是字符串类型，就会把另一个也转为字符串类型,然后做字符串拼接。
- 其他运算（*、/、-、%）只要其中一方是数字，那么另一方就转为数字。
```js
1 + '1' // '11'
4 + [1,2,3] //  "41,2,3"
'a' + + 'b' // 先算+ 'b' 为 NaN,然后因为加法中有字符串，就将NaN转"NaN",字符串拼接 "aNaN"
true + true // 2
```

### 原型以及原项链
- 每个函数都有 prototype 属性，除了 Function.prototype.bind()，该属性指向原型。
- 每个对象都有 __proto__ 属性，指向了创建该对象的构造函数的原型。其实这个属性指向了 [[prototype]]，但是 [[prototype]] 是内部属性，我们并不能访问到，所以使用 _proto_ 来访问。
- 对象可以通过 __proto__ 来寻找不属于该对象的属性，__proto__ 将对象连接起来组成了原型链。
- Object,Function,Array,Date,RegExp都是函数，Function.prototype是个函数属性存储了 Function 的原型对象。
![foo.__proto__ === Object.__proto === Function.prototype](https://i.imgur.com/TXzRpWV.png '')

### new
- 使用new创建函数是创建在堆中的，必须要程序员手动的去管理该对象的内存空间，生成一个新的对象。Object,Array,RegExp,Date都是函数。
- 普通定义的对象的内存空间是在栈中的，其作用范围只是在函数内部，函数执行完成后就会调用析构函数，删除该对象，
- new一个函数一般会经历4个过程：
	- new Object()
	- __proto__ = Fun.prototype
	- apply(Obj)绑定this，让新对象拥有
	- 将对象返回出去
```js
function create() {
    // 创建一个空的对象
    let obj = new Object()
    // 获得构造函数
    let Con = [].shift.call(arguments)
    // 链接到原型
    obj.__proto__ = Con.prototype
    // 绑定 this，执行实例的时候其实在执行构造函数
    let result = Con.apply(obj, arguments) 
    // 确保 new 出来的是个对象
    return typeof result === 'object' ? result : obj
}
```

### instanceof

### 执行上下文

### this

- 对于直接调用 foo 来说，不管 foo 函数被放在了什么地方，this 一定是 window
- 对于 obj.foo() 来说，我们只需要记住，谁调用了函数，谁就是 this，所以在这个场景下 foo 函数中的 this 就是 obj 对象
- 对于 new 的方式来说，this 被永远绑定在了 c 上面，不会被任何方式改变 this
- 箭头函数其实是没有 this 的，箭头函数中的 this 只取决包裹箭头函数的第一个普通函数的 this。
```js
function foo() {
  console.log(this.a)
}
var a = 1 
foo()//结果是1，a是window下的变量

const obj = {
  a: 2,
  foo: foo
}
obj.foo() //结果是2，此时函数绑定了，this指向调用该函数的对象

const c = new foo() //结果是2
```

