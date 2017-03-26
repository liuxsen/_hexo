---
title: mockJS笔记
date: 2017-03-01 19:28:10
tags: 前端库
---


# mockjs 实战 （nodejs 集成 mock.js）

{% asset_img mockjs.png %}


> mockjs 可以做什么

+ 根据数据模板生成模拟数据
+ 模拟ajax请求 生成并返回模拟数据
+ 基于html 模板生成模拟数据

> 为什么要用mock.js

+ 开发时，后端还没有完成数据输出，前端只能写静态模拟数据
+ 将模拟数据写在js文件里面；数据太长了；
+ 后端完成后，挨个改接口api url
+ 写模拟数据太累；需要收集很多的资源，图片，地址，随机数，ip等；

> 如何使用mock.js 安装

+ npm i mock.js

> mockjs 语法规范



### 数据模板

> 属性值

+ string 重复value
    - 'name | min-max':'value'
    - 'name | count':'value'
    - 'name | nunber+1':"value"


提供jsonp来请求；

```js
//express
router.get('/mockapi', function(req, res, next) {
    var callback = req.query.callback;
    var Mock = require('mockjs');
    var data = Mock.mock({
        // 属性 list 的值是一个数组，其中含有 1 到 10 个元素
        'list|1-10': [{
            // 属性 id 是一个自增数，起始值为 1，每次增 1
            'id|+1': 1
        }]
    })
    var ret = JSON.stringify(data, null, 4);
    console.log(ret);
    ret = callback + "(" + ret + ")";
    res.send(ret);
});
```

# mock 进阶 mock-server

[puer-mock](https://github.com/ufologist/puer-mock);

```json
{
    "api": {
        "GET /api/users": {
            "response": {
                "users|10-30": [{
                    "id": "@id"
                }]
            }
        },
        "GET /api/lists": {
            "response": {
                "lists|2-5": [{
                    "id": "@id",
                    "name": "@cname",
                    "title": "@title"
                }]
            }
        }
    }
}
```
> 操作步骤

+ npm install puer -g
+ cd yourprojectrootdir
+ npm install puer-mock --save-dev
+ copy node_modules/puer-mock/example files to your project root directory
+ cd yourprojectrootdir
+ puer -a _mockserver.js
+ 添加npm 命令 在packege.json 中添加
+ "mock": "puer -a _mockserver.js"
+ npm run mock
+ 查看api localhost:8000/api/users