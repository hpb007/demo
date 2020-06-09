title: Vue.js 源码目录设计
author: John Doe
date: 2020-06-09 13:43:31
tags:
---
src目录结构<br>
  把功能模块拆分的非常清楚，相关的逻辑放在一个独立的目录下维护，把可复用的代码也抽成一个独立目录，使代码的可维护性和阅读性都变强。

    src
    ├── compiler        # 编译相关 
    ├── core            # 核心代码 
    ├── platforms       # 不同平台的支持
    ├── server          # 服务端渲染
    ├── sfc             # .vue 文件解析
    ├── shared          # 共享代码
    
compiler
	
    包含vue.js所有编译相关的代码。包括把模板解析成ast语法树，ast语法树优化，代码生成等功能
    
core

	包含vue.js的核心代码，包括内置组件、全局API封装、vue实例化、观察者、虚拟dom、工具函数等

platform

	包含web和weex(native客户端)两个目录

server
	
    包含所有服务端渲染相关的逻辑，这部分是跑在服务端的node.js，不是浏览器端。
    
sfc

	这部分会把.vue文件内容解析成一个javascript对象
    
shared

	定义一些工具方法，浏览器端的vue.js和服务端的node.js共享
	