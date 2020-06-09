title: Vue.js 源码构建
author: John Doe
date: 2020-06-09 13:55:42
tags:
---
基于Rollup构建

一、为何使用Rollup

    webpack更强大，会将img、css、js等静态资源都编辑成js
    Rollup只处理js，更轻量，编译后的代码更友好，适合使用在js库。

二、package.json
	
    script 字段为npm的执行脚本