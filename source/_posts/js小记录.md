---
title: js小记录
date: 2019-10-16 15:33:15
categories:
- 工具 
tags:
- javascript
---

## foreach方法遍历数组

相对与for循环来遍历数组，更快捷的写法

```javascript
let a = [1, 2, 3, 4, 5, 6, 7, 8, 9,"151" , 10]

a.forEach((value, index ,self) => { 
    console.log(value,index,self) }
)
```

结果为

1 0 [ 1, 2, 3, 4, 5, 6, 7, 8, 9, '151', 10 ]
2 1 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
3 2 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
4 3 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
5 4 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
10 5 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
7 6 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
8 7 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
9 8 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
151 9 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]
10 10 [ 1, 2, 3, 4, 5, 10, 7, 8, 9, '151', 10 ]

foreach方法

传入一个回调函数，回调函数参数为 值，序号，数组本身

* foreach方法没有返回值

* foreach方法会忽略数组中undefine的值

## map方法

与foreach方法类似

```javascript
let a = [1, 2, 3, 4, 5, 6, 7, 8, 9, , 10]

let b = a.map((value, index ,self) => { 
    return [value,index] }
)
console.log(b)
```

[ [ 1, 0 ],
  [ 2, 1 ],
  [ 3, 2 ],
  [ 4, 3 ],
  [ 5, 4 ],
  [ 6, 5 ],
  [ 7, 6 ],
  [ 8, 7 ],
  [ 9, 8 ],
  <1 empty item>,
  [ 10, 10 ] ]

不同的是map方法有返回值，map方法会遍历数组，return的结果最后会被组合成为一个新的数组返回。且map方法不会跳过空白值。

## for  in遍历数组

主要用于对象，用于数组可能不是按数组内部顺序进行遍历，for in遍历数组的索引值。主要用于普通对象。

## for of 遍历数组

相较于for in，for of遍历数组的值，相较于foreach，for of可以使用break，continue等。可应用maps，set，array等可迭代对象，以及类数组对象。但是一般对象无法使用。要想遍历所有对象，搭配object.keys（）来使用。

```javascript
const iterable = [1,,8,454];
 
for(let i of iterable){
    console.log(i)
}
```

1
undefined
8
454

```javascript
const iterable = new Map([['one', 1], ['two', 2]]);
 
for (const [key, value] of iterable) {
  console.log(`Key: ${key} and Value: ${value}`);
}
```

Key: one and Value: 1
Key: two and Value: 2





  