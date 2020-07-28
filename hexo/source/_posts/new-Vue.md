title: new Vue
author: John Doe
date: 2020-06-12 11:48:49
tags:
---
Vue是一个类

在 src/core/instance/index.js 中

	function Vue (options) {
          if (process.env.NODE_ENV !== 'production' &&
            !(this instanceof Vue)
          ) {
            warn('Vue is a constructor and should be called with the `new` keyword')
          }
          this._init(options)
  	}
    
调用了this._init 方法，此方法在 src/core/instance/init.js 中，
主要是定义uid，合并配置，初始化生命周期、事件中心、渲染、data、props、computed、watcher等。

	Vue.prototype._init = function (options?: Object) {
        const vm: Component = this
        // a uid
        vm._uid = uid++

        let startTag, endTag
        /* istanbul ignore if */
        if (process.env.NODE_ENV !== 'production' && config.performance && mark) {
          startTag = `vue-perf-start:${vm._uid}`
          endTag = `vue-perf-end:${vm._uid}`
          mark(startTag)
        }

        // a flag to avoid this being observed
        vm._isVue = true
        // merge options
        if (options && options._isComponent) {
          // optimize internal component instantiation
          // since dynamic options merging is pretty slow, and none of the
          // internal component options needs special treatment.
          initInternalComponent(vm, options)
        } else {
          vm.$options = mergeOptions(
            resolveConstructorOptions(vm.constructor),
            options || {},
            vm
          )
        }
        /* istanbul ignore else */
        if (process.env.NODE_ENV !== 'production') {
          initProxy(vm)
        } else {
          vm._renderProxy = vm
        }
        // expose real self
        vm._self = vm
        initLifecycle(vm) // 生命周期
        initEvents(vm)	// 事件中心
        initRender(vm)	// 渲染
        callHook(vm, 'beforeCreate')
        initInjections(vm) // resolve injections before data/props
        initState(vm) 
        initProvide(vm) // resolve provide after data/props
        callHook(vm, 'created')

        /* istanbul ignore if */
        if (process.env.NODE_ENV !== 'production' && config.performance && mark) {
          vm._name = formatComponentName(vm, false)
          mark(endTag)
          measure(`vue ${vm._name} init`, startTag, endTag)
        }

        if (vm.$options.el) {
        	// 挂载,把模板渲染成DOM
          vm.$mount(vm.$options.el)
        }
  	}
    
