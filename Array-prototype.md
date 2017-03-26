---
title: Array.prototype
date: 2017-03-02 21:17:21
tags: js基础
---

```js
  Array.prototype.indexOf
  Array.prototype.lastIndexOf
  Array.prototype.every
  Array.prototype.some
  Array.prototype.forEach
  Array.prototype.map
  Array.prototype.filter
  Array.prototype.reduce
  Array.prototype.reduceRight
```

1、indexOf

> indexOf()方法返回在该数组中第一个找到的元素位置，如果它不存在则返回-1。

```js
var arr = ['apple','orange','pear'];  
console.log("found:", arr.indexOf("orange") != -1); // "found" true
```

2、lastindexOf

> lastIndexOf() 方法返回在该数组中最后一个找到的元素位置，和 indexof相反。


3、every()

> evety()可是检测数组中的每一项是否符合条件

```js
var ary = [12,23,-24,42,1];
var result = ary.every(function(item, index){
  return item > 0
})
console.log(result) // false;
```


4、some()

> some()可以检测数组中是否有某一项符合条件

```js
var ary = [12,23,-24,42,1];
var result = ary.some(function(item, index){
  return item < 0
})
console.log(result); // true
```

5、 forEach() 


> forEach为每个元素执行对应的方法

**forEach是用来替换for循环的**

```js
var arr = [1,2,3,4,5,6,7,8];

arr.forEach(function(item,index){
  console.log(item);
});
// 1,2,3,4,5,6,7,8
```

6、 map()

> map()对数组的每个元素进行一定操作（映射）后，会返回一个新的数组， 

```js
var oldArr = [{first_name:"Colin",last_name:"Toh"},{first_name:"Addy",last_name:"Osmani"},{first_name:"Yehuda",last_name:"Katz"}];

function getNewArr(){
  return oldArr.map(function(item,index){
    item.full_name = [item.first_name,item.last_name].join(" ");
    return item;
  });

}
console.log(getNewArr());
// [{first_name:"Colin",last_name:"Toh",full_name:Colinlast_name}]
//  map()是处理服务器返回数据时是一个非常实用的函数。
```

### forEach 与map的区别：

> forEach：用来遍历数组中的每一项；这个方法执行是没有返回值的，对原来数组也没有影响；数组中有几项，那么传递进去的匿名回调函数就需要执行几次；每一次执行匿名函数的时候，还给其传递了三个参数值：数组中的当前项item,当前项的索引index,原始数组list；理论上这个方法是没有返回值的，仅仅是遍历数组中的每一项，不对原来数组进行修改；但是我们可以自己通过数组的索引来修改原来的数组；

**forEach方法中的this是ary,匿名回调函数中的this默认是window；**

```js
var ary = [12,23,24,42,1];
var res = ary.forEach(function (item,index,input) {
  input[index] = item*10;
})
console.log(res);//-->undefined;
console.log(ary);//-->会对原来的数组产生改变；// [120,230,240,420,10];
```
> 区别：map的回调函数中支持return返回值；return的是啥，相当于把数组中的这一项变为啥（并不影响原来的数组，只是相当于把原数组克隆一份，把克隆的这一份的数组中的对应项改变了）；

```js
var ary = [12,23,24,42,1];
var res = ary.map(function (item,index,input) {
  return item*10;
})
console.log(res);//-->[120,230,240,420,10];
console.log(ary);//-->[12,23,24,42,1]；
```

7、 filter
> 该filter()方法创建一个新的匹配过滤条件的数组。

**使用 filter()：**

```js
var arr = [
  {"name":"apple", "count": 2},
  {"name":"orange", "count": 5},
  {"name":"pear", "count": 3},
  {"name":"orange", "count": 16},
];
var newArr = arr.filter(function(item){
  return item.name === "orange";
});
console.log("Filter results:",newArr);
// [{"name":"orange", "count": 5},{"name":"orange", "count": 16}]
```

8、 reduce()

> reduce()可以实现一个累加器的功能



