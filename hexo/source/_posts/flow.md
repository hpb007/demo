title: Flow
author: John Doe
tags: []
categories: []
date: 2020-06-09 10:54:00
---
工作方式：

  1 类型推断<br>
    根据变量的上下文推断出变量类型，然后检查类型
    
    例： 
    /*@flow*/
    
    function getStr(str){
    	return str.split('-')
    }
    
    getStr('asd-f'); // true
    getStr(55); // false
    
    
    function add(a, b){
    	return a + b;
    }
    
    add('11', 5); // true
    add(11, 5); // true
    
    
  2 类型注释<br>
 	事先注释类型，基于注释判断
    
    例：
    
    /*@flow*/
    
    function add(a:number, b:number){
    	return a + b;
    }
    
    add('11', 5); // false
    add(11, 5); // true
    
    class Bar {
    	x: string | number;
        y: Array<string>;
        z: boolean;
        
        constructor(x: string | number, y: Array<string>, z: boolean | void){  //void 表示非必传
        	this.x = x;
            this.y = y;
            this.z = z
        }
    }
    
    var bar = Bar('zhang', [1,2,3]);  // false
    var bar = Bar(14, ['1','2','3']);  // true
    var bar = Bar('zhang', ['1','2','3'], true);  // true
    
    // 如果任意类型T可以为null或者undefined，需写成?T的格式
    var foo: ?string = null;
    
    var foo = 'adf';  // true;
    var foo;  // true;
    

    
    