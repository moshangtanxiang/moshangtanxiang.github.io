---
title: vue-router
date: 2020-05-15 15:58:43
tags:
- vue-router
categories:
- Vue
---


### vue-router实现原理：
&ensp;&ensp;&ensp;&ensp;vue-router实现单页面跳转，提供了三种方式：hash模式、history模式、abstract模式，根据mode参数决定采用哪种

### 路由模式：
vue-router 提供了三种运行模式：
+ hash: 使用 URL hash 值来作路由。默认模式。
+ history: 依赖 HTML5 History API 和服务器配置。
+ abstract: 支持所有 JavaScript 运行环境，如 Node.js 服务器端


#### 1. Hash模式
&ensp;&ensp;&ensp;&ensp;hash即浏览器url中#后面的内容，包含#。hash是URL中的锚点，代表的是网页中的一个位置，单单改变#后的部分，浏览器只会加载相应位置的内容，不会重新加载页面。
&ensp;&ensp;&ensp;&ensp;也就是说即#是用来指导浏览器动作的，对服务器端完全无用，HTTP请求中，不包含#。每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置。所以说Hash模式通过锚点值的改变，根据不同的值，渲染指定DOM位置的不同数据。

#### 2. History模式
&ensp;&ensp;&ensp;&ensp;HTML5 History API提供了一种功能，能让开发人员在不刷新整个页面的情况下修改站点的URL，就是利用 history.pushState API 来完成 URL 跳转而无须重新加载页面；由于hash模式会在url中自带#，如果不想要很丑的 hash，我们可以用路由的 history 模式，只需要在配置路由规则时，加入"mode: 'history'",这种模式充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。
有时，history模式下也会出问题：
```
eg:
hash模式下：xxx.com/#/id=5 请求地址为 xxx.com,没有问题。
history模式下：xxx.com/id=5 请求地址为 xxx.com/id=5，如果后端没有对应的路由处理，就会返回404错误；
```
为了应对这种情况，需要后台配置支持：
在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。

#### 3. abstract模式
&ensp;&ensp;&ensp;&ensp;abstract模式是使用一个不依赖于浏览器的浏览历史虚拟管理后端。
&ensp;&ensp;&ensp;&ensp;根据平台差异可以看出，在 Weex 环境中只支持使用 abstract 模式。 不过，vue-router 自身会对环境做校验，如果发现没有浏览器的 API，vue-router 会自动强制进入 abstract 模式，所以 在使用 vue-router 时只要不写 mode 配置即可，默认会在浏览器环境中使用 hash 模式，在移动端原生环境中使用 abstract 模式。 （当然，你也可以明确指定在所有情况下都使用 abstract 模式）。