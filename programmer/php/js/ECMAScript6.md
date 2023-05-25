## ES6

一. 简介

* ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准



二. 语法

### let

* 变量不能重复声明. var可以

* 块级作用域

    * 锁声明的变量只在let所在代码块有效, `for`循环的计数器，就很合适使用`let`命令。


````
```
  javascript
  {
    let a = 10;
    var b = 1;
  }

  a // ReferenceError: a is not defined.
  b // 1
  
```

* for 循环中. 变量`i`是`let`声明的，当前的`i`只在本轮循环有效. 而var 是全局的, 类似引用传递
````

* 不存在变量提升

    ```javascript
    // var 的情况
    console.log(foo); // 输出undefined
    var foo = 2;
    
    // let 的情况
    console.log(bar); // 报错ReferenceError
    let bar = 2;
    ```

* 不影响作用域链



### const

* 定义时赋初值
* 定义后不能修改
* 对常量定义的数组或者对象的元素修改不算对常量的修改





### 变量解构赋值

* 数组

  ```javascript
  let [a, b, c] = [1, 2, 3];
  ```

* 对象

  ```javascript
  let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
  foo // "aaa"
  bar // "bbb"
  ```

let和const

变量的解构赋值

数组的扩展

Promise对象

async函数

class的基本语法