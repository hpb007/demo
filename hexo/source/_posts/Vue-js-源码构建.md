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
	
    script 字段为npm的执行脚本,不同命令可以打包不同版本的vue
    
1. scripts/build.js

	
    先从配置文件(./config.js)读取配置，再通过命令行参数对构建配置过滤，构建出不同用途的vue.js
    
2. scripts/config.js

	
    都是vue.js构建的配置，entry表示构建的入口js文件地址，dest表示构建后的js文件地址，format表示构建的格式，cjs表示构建出来的文件遵循CommonJS规范，es表示构建出来的文件遵循ESModule规范，umd表示构建出来的文件遵循UMD规范。

三、Runtime Only VS Runtime + Compiler

1. Runtime Only

	
    在使用Runtime Only版本的vue.js使，通常需要借助如webpack的vue-loader工具把.vue文件编译成Javascript，因为是在编译阶段做的，所以只包含运行时的vue.js代码，因此代码体积会更轻量
    
2. Runtime + Compiler


	我们如果没有对代码做预编译，但又使用了template属性并传入一个字符串，则需要在客户端编译模板，如下所示：
    
	// 需要编译器的版本
    new Vue({
    	template: '<div>{{ hi }}</div>'
    })

    // 不需要
    new Vue({
    	render(h){
        	return h('div', this.hi)
        }
    })
    
    因为在vue.js 2.0中，最终渲染都是通过render函数，如果写template属性，则需要编译成render函数，那么这个编译过程会发生时，就需要带有编译器的版本。很明显，这个编译过程对性能有一定损耗，所以通常我们更推荐使用Runtime-Only的Vue.js
    

    
    
