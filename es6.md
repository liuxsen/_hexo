---
title: ECMAScript6
date: 2017-03-01 19:24:52
tags: js
---

{% asset_img es6.jpg %}

```javascript
// let有  块作用域 var没有
// const 定义常量  定义一次就不再改变
/*
let firstname = "haha";
let lastname = 'heheh';
console.log(`my name is ${firstname} ${lastname}`)*/

/*
let person = {
    firstName :'haha',
    lastName: 'hehe',
    sayName(){
        console.log(`my name is ${this.firstName} ${this.lastName}`)
    }
}
person.sayName()*/

/*var add =(a,b) =>{
    return a+b; 
}*/
/*var add =(a,b) =>a+b;
console.log(add(2,3))*/

/*
let numbers = [2,3,4,5,6.7];
let doubled = numbers.map(function(n){
    return n*2;
})
console.log(doubled)*/


/*let numbers = [2,3,4,5,6.7];
// let doubled = numbers.map((n)=>n*2)
let doubled = numbers.map(n=>n*2)
console.log(doubled)*/


/*let person = {
    name: 'liu',
    sayName: function (){
        console.log(`hi i am ${this.name}`);
    }
}*/
/*let person = {
    name: 'liu',
    hobbies: ['haha','hehe'],
    sayName(){
        console.log(`hi i am ${this.name}`);
    },
    showHobbies: function (){
        var that = this;
        this.hobbies.forEach(function(h){
            console.log(`${that.name} likes ${h}`)
        })
    }
}*/
/*let person = {
    name: 'liu',
    hobbies: ['haha','hehe'],
    sayName(){
        console.log(`hi i am ${this.name}`);
    },
    showHobbies: function (){
        this.hobbies.forEach((h)=>{
            console.log(`${this.name} likes ${h}`)
        })
    }
}
person.sayName()
person.showHobbies()*/


//-----------------------
/*let sum = function(){
    console.log(arguments);
}
sum(2,3,4,5)*/

/*let sum = function(){
    return Array.prototype.reduce.call(arguments,(pre,cur)=>{
        console.log('pre---'+pre,'cur---'+cur)
        return pre+cur;
    })
}
console.log(sum(1,2,3))*/
/*
let sum = function(...args){
    // console.log(args)
    return args.reduce((pre,cur)=>pre + cur)
}
console.log(sum(2,3,4))*/

//----------------------
/*let mutiply = (mul, ...numbers)=>{
    console.log(mul,numbers);
    return numbers.map((n)=>{
        return mul*n;
    })
}
let result = mutiply(2,2,3,4,5)
console.log(result)*/

//----------

/*
let max = Math.max(2,3,4,5);
console.log(max)*/

/*let numbers = [4,6,5,6,20];
let max = Math.max.apply(null, numbers);
console.log(max)*/

/*let numbers =[12,3,4,5];
let max = Math.max(...numbers);
console.log(max)*/

/*let numbers = [2,3,4];
let newNumbers = [3,4,55];
let concatArray = newNumbers.concat(numbers);
console.log(concatArray)*/

/*let numbers = [2,3,4];
let newNumbers = [3,4,55];
let concatArray = [...numbers,...newNumbers];
console.log(concatArray)*/


/*------------destructuring----------------*/
//object 解构

/*let person = {
    name: 'liu',
    age: 30,
    location: "jianhui",
};
person.age; //30
person['age']; //30
// 定义的变量是value 值是 key
let {age: personAge,name: personName,location: personLocation} = person;
console.log(personAge);
console.log(personName);
console.log(personLocation);*/

//数组解构
/*let numbers = [1,2,3,4];
let first = numbers[0];
let second = numbers[1];*/

/*let numbers = [1,2,3,4];
let [first,second,,fourth] = numbers;
console.log(first,second,fourth) // 1,2,4
*/

/*let numbers = [1,2,3,4];
let [first,second,...therest] = numbers;
console.log(first,second,therest)  // 1,2,[3,4]*/


/*--------promise---------------*/
'use strict'

let mypromise = new Promise((resolve,reject)=>{
    // 异步resolve操作
    setTimeout(()=>{
        resolve('good to go!')
    },1000)
    //异步reject操作
    // setTimeout(()=>{
    //  reject('uh oh')
    // },500)
})

/*mypromise.then((res)=>{
    console.log(res)
},(err)=>{
    console.log(err)
})
console.log('good haha')*/
// 同等于下面
/*mypromise.then((res)=>{
    console.log(res)
}).catch((err)=>{
    console.log(err)
})
console.log('good haha')*/

// 多个promise
/*let myPromise2 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
        resolve('promise 2 - the promise')
    },1500)
})
Promise.all([mypromise,myPromise2])
    .then((data)=>{
        console.log(data)
    })
    .catch((err)=>{
        console.log(err)
    })*/



//api http://api.icndb.com/jokes/random/10
// fetch 资料 https://github.com/camsong/blog/issues/2
/*fetch('http://api.icndb.com/jokes/random/10')
    .then((res)=>{
        // res.json 返回的是promise
        res.json().then((data)=>{
            console.log(data);
        })
    })
    .catch((err)=>{
        console.log(err)
    })*/

//  pokeapi.co
```