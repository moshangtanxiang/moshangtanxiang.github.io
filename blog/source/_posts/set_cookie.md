---
title: 页面缓存
date: 2019-11-15 17:45:39
tags: cookie
---
前端页面常用缓存，具体设置哪种根据项目需求而定
## cookie缓存：
### cookie设置
```
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
## localstorage缓存:
// 缓存数据字典
      api.dictionary_get({type:'Gender'}).then(res=>{
          localStorage.setItem("Gender", JSON.stringify(res.data));
      })
// 单一死数据
 	localStorage.setItem("Gender", “data”);

 	localStorage.getItem("Gender");