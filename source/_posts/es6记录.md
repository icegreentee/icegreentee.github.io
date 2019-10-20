---
title: es6记录
date: 2019-10-16 16:30:35
categories:
- 工具 
tags:
- javascript
- es6Object
---

## Object.values()

获取传入对象的值的数组

## Object.keys()

获取传入对象的键的数组

## Object.entries()

获取传入对象的数组形式的键值对

```javascript
const cars = {bmw:3, tesla:2, toyota:1}
const keys = Object.keys(cars)
const vals = Object.values(cars)
const entries = Object.entries(cars)
console.log(vals,keys)
console.log(entries)
```

[ 3, 2, 1 ]   [ 'bmw', 'tesla', 'toyota' ]
[ [ 'bmw', 3 ], [ 'tesla', 2 ], [ 'toyota', 1 ] ]

## 函数默认参数

es6开始，直接在参数行赋值默认参数

```javascript
function test(a=50,b=100){
    console.log(a,b)
}
test(5)
```

5 100

## 模板对象

```js
// OLD
var name = 'Your name is ' + first + ' ' + last + '.';
var url = 'http://localhost:3000/api/messages/' + id;

// ES6语法 `${NAME}` 不是引号哦 tab建上方
var name = `Your name is ${first} ${last}. `;
var url = `http://localhost:3000/api/messages/${id}`;
```

## 多行字符串

```js
var roadPoem = `Then took the other, as just as fair,
    And having perhaps the better claim
    Though as for that the passing there
    Had worn them really about the same,`;
```

## 结构赋值

 #### 对象解构

要求接受属性名和解构对象的属性一一对应

```js
let node = {
    type: "Identifier",
    name: "foo"
};
let { type, name } = node;
console.log(type); // "Identifier"
console.log(name); // "foo"
```

一定要用一对小括号包裹解构赋值语句，JS引擎将一对开放的花括号视为一个代码块。语法规定，代码块语句不允许出现在赋值语句左侧，添加小括号后可以将块语句转化为一个表达式，从而实现整个解构赋值过程

```js
let node = {
    type: "Identifier",
    name: "foo"
},
type = "Literal",
name = 5;
// 使用解构来分配不同的值
({ type, name } = node);
console.log(type); // "Identifier"
console.log(name); // "foo"
```

可以为变量设置默认值，如果它可能不存在node中

```js
let node = {
    type: "Identifier",
    name: "foo"
};
let { type, name, value = true } = node;
console.log(type); // "Identifier"
console.log(name); // "foo"
console.log(value); // true
```

为非同名变量赋值

```js
let node = {
    type: "Identifier",
    name: "foo"
};
let { type: localType, name: localName } = node;
console.log(localType); // "Identifier"
console.log(localName); // "foo"
```

为非同名变量设初始值

```js
let node = {
    type: "Identifier"
};
let { type: localType, name: localName = "bar" } = node;
console.log(localType); // "Identifier"
console.log(localName); // "bar"
```

#### 数组解构

数组解构与对象解构略有不同，数组解构按照位置进行解构,和对象不同，数组解构赋值不需要加括号

```js
let colors = [ "red", "green", "blue" ],
firstColor = "black",
secondColor = "purple";
[ firstColor, secondColor ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

变量交换，无需第三变量

```js
// 在 ES6 中互换值
let a = 1,
    b = 2;
[ a, b ] = [ b, a ];
console.log(a); // 2
console.log(b); // 1
```

设置默认值，同理

```
let colors = [ "red" ];
let [ firstColor, secondColor = "green" ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

不定元素

```js
let colors = [ "red", "green", "blue" ];
let [ firstColor, ...restColors ] = colors;
console.log(firstColor); // "red"
console.log(restColors); // [ 'green', 'blue' ]
```

数组复制

```js
// 在 ES6 中克隆数组
let colors = [ "red", "green", "blue" ];
let [ ...clonedColors ] = colors;
console.log(clonedColors); //"[red,green,blue]"
```

#### 字符串同样可以解构

```js
const [a, b, c, d, e] = 'hello';
console.log(a);//"h"
console.log(b);//"e"
console.log(c);//"l"
console.log(d);//"l"
console.log(e);//"o"
```

#### 字符串集合函数

查找字符串是否包含在另一个字符串中

- includes()：返回布尔值，表示是否找到了参数字符串。
- startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
- endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。

```js
let s = 'Hello world!';
console.log(s.startsWith('Hello')) // true
console.log(s.endsWith('!')) // true
console.log(s.includes('o')) // true

// 这三个方法都支持第二个参数，表示开始搜索的位置。
console.log(s.startsWith('world', 6)) // true
console.log(s.endsWith('d',11)) // true
console.log(s.includes('Hello', 6)) // false
```

#### repeat（）

返回一个新字符串，将一个字符串重复n次

```js
console.log("abc".repeat(3))  //abcabcabc
```

#### 空白填充

padStart() 和  padEnd()

```js
// 第一个参数用来指定字符串的最小长度，第二个参数是用来补全的字符串。
console.log('x'.padStart(5, 'ab')) // 'ababx'
console.log('x'.padEnd(5, 'ab')) // 'xabab'
// 补全字符串过长时，不全完毕多余的会去除
console.log('x'.padStart(5, 'abbbbbbb')) // 'abbbx'
console.log('x'.padEnd(5, 'abbbbbbbbb')) // 'xabbb'
```

#### promise

[参考文章](https://www.jianshu.com/p/82237a7ca6e5)

“承诺将来会执行”的对象在JavaScript中称为Promise对象。

resolve()   表示成功执行，执行时表示执行成功。可以传递参数，会执行.then的回调函数，且可以接受传递的参数

reject 表示执行失败。同理与resolve（）。由.catch（）进行接受。

```js
var promise = new Promise(function (resolve, reject) {
    var a = 2
    if (a== 0) {
        resolve(a)
    } else {
        reject("233")
    }
})
promise.then(function (value) {
    console.log(value);
}).catch(function (error) {
    console.log(error);
})
//1 
//2
```



then，catch的返回都是一个新的promise，可以做为下一个then或者catch的参数，执行没有错误后面的then会接受上一个then的参数，执行错误会由下面第一个catch方法来接受

```js
var promise = new Promise(function (resolve, reject) {
    resolve()
})
promise.then(function (value) { // 抛出错误
    console.log(1 / x)
}).then(function () { // 此方法不会执行
    console.log('This "then" method will not happend!')
}).catch(function (error) { // 接受错误，并打印出错误
    console.log('Have an error: ',error)
}).then(function () { // 此方法会执行
    console.log('This "then" method  will happend!')
})
```

Promise.all() 和 Promise.race()

都接受promise对象的数组。

Promise.all()当这个数组里的所有Promise对象全部变为resolve的时候，该方法才resolve

Promise.race()只要其中一个Promise对象变为Resolved或者Rejected状态，该方法才resolve

#### Async/Await

[参考文章](https://www.jianshu.com/p/1e75bd387aa0)

async/await是一个用同步思维解决异步问题的方案，等待awiat返回结果才会继续执行

async

- 自动将常规函数转换成Promise，返回值也是一个Promise对象

- 只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数

- 异步函数内部可以使用await

```js
//async 返回promise对象可以用then去捕获
async function doubleAndAdd(a,b) {
  return a + b
}

doubleAndAdd(1,2).then(res=>{console.log(res)})
```

awiat

- await 后面如果是promise那么等待promise对象resolve的值做为返回结果
- await后面如果不是promise那么同样会等待后面函数或者表达式执行完毕
- await只能在async函数内部使用,用在普通函数里就会报错

```js
async function doubleAndAdd(a,b) {
  a = await doubleAfterSec(a)
  b = await doubleAfterSec(b)
  return a + b
}

function doubleAfterSec(param) {
  return new Promise( resolve =>{
    setTimeout(()=> resolve(param*2) ,1000)
  })
}

doubleAndAdd(1,2).then(console.log)
```

Promise.all的使用,多个await命令不存在依赖关系，即后面的await不依赖前一个await的结果。使用promise.all只有当后面的两个promise对象都完成时，才会同时处理。使用promise.all相比单独的await命令运行更快。

```js
async function doubleAndAdd(a,b) {
  [a,b] = await Promise.all([doubleAfterSec(a), doubleAfterSec(b)]);
  return a + b
}

```

异常处理

async返回的是promise对象，通过catch捕获里面的reject异常

```js
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(() => { reject('error') }, ms);  //reject模拟出错，返回error
  });

}

async function asyncPrint(ms) {
  console.log('start');
  await timeout(ms)
  console.log('end');  //这句代码不会被执行了
}

asyncPrint(1000).catch(err => {
  console.log(err); // 从这里捕捉到错误
});
```

在async内部使用try/catch来捕获异常

```js
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(() => { reject('error') }, ms);  //reject模拟出错，返回error
  });
}

async function asyncPrint(ms) {
  try {
    console.log('start');
    await timeout(ms);  //这里返回了错误
    console.log('end');  //所以这句代码不会被执行了
  } catch (err) {
    console.log(err); //这里捕捉到错误error
  }
}

asyncPrint(1000);
```

提前截住错误。在await出拦截错误。

```js
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject('error')
    }, ms);  //reject模拟出错，返回error
  });
}

async function asyncPrint(ms) {
  console.log('start');
  await timeout(ms).catch(err => {  // 注意要用catch
    console.log(err)
  })
  console.log('end');  //这句代码会被执行
}

asyncPrint(1000);
```

