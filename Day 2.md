# Day 2

## JavaScript学习

1.基本语法

+ 书写位置(行内式，内嵌式，外链式)

+ 注释( // or /* */)

+ 变量

+ 关键字

  

2.数据类型

+ 字符串型（String）
+ 数值型（Number）
+ 布尔型（Boolean）
+ undefined型（Undefined）
+ null型（Null）
+ 除以上外都称为Object型



3.数据类型转换

+ 转换为String
  + 方法一：
    - 调用被转换数据类型的toString（）方法
    - 该方法不会影响原变量，它会将转换的结果**返回**
    - 但是注意：null和undefined这两个值没有toString（）方法，如果调用他们的方法会报错。

+ + 方法二:

    + 调用String（）函数，并将被转换的数据作为参数传递给函数
    + 使用String（）函数做强制类型转换时，对于Number和Boolean实际上就是调用的toString（）方法。但是对于null和undefined就不会调用toString（）方法，它会将null直接转换为“null”；将undefined直接转换为“undefined”
      

    

- ###### 转换为Number

  > 使用Number（）函数，使用方法同toString（）函数 字符串转数字字符串转数字



**字符串转数字**

*如果是纯数字的字符串，直接转换为数字*

*如果字符串中有非数字的内容 则转换为NaN*

*如果字符串是一个空串或者全是空格的字符串，则转为0*



 **布尔转数字**

*true转成1*

*false转成0*



**null转数字**

*结果为0*



**underfined转数字**

*结果为NaN*



> 这种方式专门用来对付***字符串\***
>
> parseInt() 把一个字符串转换为一个整数
> parseFloat（）把一个字符串转换为一个浮点数

+ parseInt()可以将一个字符串中的有效的整数内容取出来，然后转换为Number，从左往右读，读到非整数就停止：

```javascript
a = "18px";
a = parseInt(a);
console.log(typeof a);
console.log(a);
```

结果为18。



+ 其他进制的数字

  > 在js中 如果需要表示16进制的数字，则需要以0x开头
  >
  > 如果需要表示8进制的数字，则需要以0开头 如果要表示2进制的数字，则需要以0b开头，但不是所有浏览器都支持

+ 转换为boolen

  > 数字转布尔，除了0和NaN，其余都是true
  >
  > 字符串转布尔，除了空串，其余都是true
  >
  > null和undefined都会转换为false
  >
  > 对象也会转换为true



4.函数

+ 函数的声明(普通的函数声明  or  使用变量初始化函数  or  使用function构造函数)

  > 必须有名字，会函数提升，在预解析阶段就已经创建，声明前后都可以调用

```javascript
//函数声明
//定义函数名
function fn(){
     console.log(123);
}
fn()
```

+ 函数表达式

  > 一种变量赋值，函表达式可以没有名字（匿名函数）,没有函数提升。

```javascript
//将函数赋值给一个变量，可以是匿名函数
var fn = function(){
    hi: function(){  }, //方法
};
//调用
fn()
//调用方法
fn.hi()
```

+ 匿名函数(自调用函数)

> 函数表达式可以 "自调用"。
>
> 如果表达式后面紧跟 () ，则会自动调用。
>
> 通过添加括号，来说明它是一个函数表达式：
>
> 如果需要执行匿名函数，在匿名函数后面加上一个括号即可立即执行。

```javascript
(function (){
    //此时会输出a
    console.log("a"); 
})()
 
//以上函数实际上是一个 匿名自我调用的函数 (没有函数名)。
```

+ 构造函数(初始化对象，和new一起使用，首字母大写)
  + 对构造函数使用new运算符,就能生成实例,并且this变量会绑定在实例对象上。

```javascript
function Person(name,age){
  this.name = name
  this.age = age                 
}
 
let p1 = new Person('张三','18')
```

+ 箭头函数
  + 语法比较简洁，并且没有自己的this，arguments，super或new.target。
  + 更适用于那些本来需要匿名函数的地方，并且它不能用作构造函数。

> ```javascript
> (参数1, 参数2, …, 参数N) => { 函数声明 }
> 
> (参数1, 参数2, …, 参数N) => 表达式(单一)
> // 相当于：(参数1, 参数2, …, 参数N) =>{ return 表达式; }
> ```

```javascript
    //多个参数
     const fn = (a, b) => {
            let result = a + b;
            console.log(result);//3
        }
        fn(1, 2)
 
    //只有一个参数
        var fn2 = c => {
            console.log(c); //davina
        }
        fn2(‘davina‘);
 
    //没有参数
        let fn3 = () => {
            console.log(‘123‘);
        }
        fn3(); //123
```

