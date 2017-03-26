---
title: postmassege
date: 2017-03-01 12:34:55
tags: html5
---


# postmessage 兼容性

{% asset_img 兼容.png %}

## 跨文档消息传输；

```html
<!--postMessage.ejs-->
<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
    <script>
      window.addEventListener('message',function(e){
        console.log(e);
        console.log(e.data)
      },false);
      function hello (){
        var iframe = window.frames[0];
        var obj = {name:"parent"};
        var message = JSON.stringify(obj);
        iframe.postMessage(message,'http://127.0.0.1:3000/iframe');
        console.log(1);
      }
    </script>
  </head>
  <body>
    <h1>postmessage</h1>
    <iframe width="400" src="http://127.0.0.1:3000/iframe" onload="hello()"></iframe>
  </body>
</html>
```

```html
<!--iframe.ejs-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script>
        window.addEventListener('message',function(e){
            console.log(e.origin);
            // 获得发送信息的源窗口 e.source;
            console.log(JSON.parse(e.data))
            console.log('这里是子窗口',this.location,e.origin)
            e.source.postMessage('你好,父窗口，我是子窗口',e.origin);
        })
    </script>
</head>
<body>
    hh
</body>
</html>
```