---
title: 页面缓存
date: 2019-11-15 17:45:39
tags: cookie
---

## localstorage缓存:
```
    // 缓存数据字典
      api.dictionary_get({type:'Gender'}).then(res=>{
          localStorage.setItem("Gender", JSON.stringify(res.data));
      })

 	localStorage.setItem("Gender", “data”);
 	localStorage.getItem("Gender");
```
    localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。同源可以读取并修改localStorage数据。

## cookie缓存（会话级别）：
### cookie设置
```
    //默认关闭浏览器就销毁
    setCookie(name,value){
        var exp = new Date();
        exp.setTime(exp.getTime() + 2*30*24*60*60*1000);
        document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString();
    },
```
### cookie获取
```
    getCookie(name){
        var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");
        if(arr=document.cookie.match(reg))
            return unescape(arr[2]);
        else
            return null;
    },
```
&ensp;&ensp;&ensp;&ensp;cookie：不设置存活时间 是**保存在浏览器内存中**，关闭浏览器则内存消失；如果设置保存时间，将保存在浏览器硬盘中，如果不超时就一直存在，超时则消失。
### （会话流程）
&ensp;&ensp;&ensp;&ensp;服务器创建session、cookie，服务器保存session信息，但有一个唯一标识符sessionid保存在cookie中发送给浏览器，再访问时根据sessionid找session信息。
* session销毁方式：
    + session默认存活时间只有三十分钟，超时即销毁；
    + 服务器非正常关闭，session即消失；


## sessionstorage缓存（会话级别）:
&ensp;&ensp;&ensp;&ensp;sessionStorage的清除时机是在会话结束，会话结束是在用户关闭标签页或者关闭窗口的时候；手动新开一个标签或窗口时，会新开会话，即使链接一样，也不会共享sessionStorage
&ensp;&ensp;&ensp;&ensp;使用方法同localstorage，**session保存在服务器端**。


## 三者的异同：
![funnel](/img/storage.png)
