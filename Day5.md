# Day5

## Vue2基本语法

+ Vue.js优点(体积小，运行效率更高，双向数据绑定，ui框架多)

+ 声明式渲染

  + Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

  ```html
  <div id="app">
    {{ message }}
  </div>
  ```

+ 条件与循环

  + 控制切换一个元素：

    ```html
    <div id="app-3">
      <p v-if="seen">现在你看到我了</p>
    </div>
    ```

    

+ 处理用户输入(用 `v-on` 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法：)

  ```html
  <div id="app-5">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转消息</button>
  </div>
  ```

  + Vue 还提供了 `v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定。

```html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```

+ 组件化应用构建

  > 组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用.

注册组件：

```html
<ol>
  <!-- 创建一个 todo-item 组件的实例 -->
  <todo-item></todo-item>
</ol>
```

+ vue实例

  ```vue
  var vm = new Vue({
    // 选项
  })
  ```

  当创建一个 Vue 实例时，你可以传入一个**选项对象**。

  一个 Vue 应用由一个通过 `new Vue` 创建的**根 Vue 实例**，以及可选的嵌套的、可复用的组件树组成。举个例子，一个 todo 应用的组件树可以是这样的：

```vu
根实例
└─ TodoList
   ├─ TodoItem
   │  ├─ TodoButtonDelete
   │  └─ TodoButtonEdit
   └─ TodoListFooter
      ├─ TodosButtonClear
      └─ TodoListStatistics

```

+ 数据与方法

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

```vue
// 我们的数据对象
var data = { a: 1 }

// 该对象被加入到一个 Vue 实例中
var vm = new Vue({
  data: data
})

// 获得这个实例上的 property
// 返回源数据中对应的字段
vm.a == data.a // => true

// 设置 property 也会影响到原始数据
vm.a = 2
data.a // => 2

// ……反之亦然
data.a = 3
vm.a // => 3
```

数据改变--重渲染

+ 实现生命周期钩子

(created是生命周期钩子，是一个函数，可以被调用)

比如 [`created`](https://cn.vuejs.org/v2/api/#created) 钩子可以用来在一个实例被创建之后执行代码：

```js
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```

也有一些其它的钩子，在实例生命周期的不同阶段被调用，如 [`mounted`](https://cn.vuejs.org/v2/api/#mounted)、[`updated`](https://cn.vuejs.org/v2/api/#updated) 和 [`destroyed`](https://cn.vuejs.org/v2/api/#destroyed)。生命周期钩子的 `this` 上下文指向调用它的 Vue 实例。

> 不要在选项 property 或回调上使用[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)，比如 `created: () => console.log(this.a)` 或 `vm.$watch('a', newValue => this.myMethod())`。因为箭头函数并没有 `this`，`this` 会作为变量一直向上级词法作用域查找，直至找到为止，经常导致 `Uncaught TypeError: Cannot read property of undefined` 或 `Uncaught TypeError: this.myMethod is not a function` 之类的错误。

生命周期：当前组件在创建到销毁经历的一系列过程。

+ 文本

数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

```html
<span>Message: {{ msg }}</span>
```

Mustache 标签将会被替代为对应数据对象上 `msg` property 的值。无论何时，绑定的数据对象上 `msg` property 发生了改变，插值处的内容都会更新。

通过使用 [v-once 指令](https://cn.vuejs.org/v2/api/#v-once)，你也能执行一次性地插值，当数据改变时，插值处的内容不会更新。但请留心这会影响到该节点上的其它数据绑定：

```html
<span v-once>这个将不会改变: {{ msg }}</span>
```

+ 原始HTML(v-html指令)

  ```html
  <p>Using mustaches: {{ rawHtml }}</p>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p
  ```

  

+ Attribute(v-bind指令)

  ```html
  <div v-bind:id="dynamicId"></div>
  ```

  > 如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` attribute 甚至不会被包含在渲染出来的 `<button>` 元素中。
  >
  > 对于布尔，存在即为true.

+ Javascript表达式

这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```

> 模板表达式都被放在沙盒中，只能访问[全局变量的一个白名单](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9)，如 `Math` 和 `Date` 。你不应该在模板表达式中试图访问用户定义的全局变量。

+ 指令

> 指令是带有 `v-` 前缀的特殊 attribute。指令 attribute 的值预期是**单个 JavaScript 表达式** .
>
> 指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

```html
<p v-if="seen">现在你看到我了</p>
```

这里，`v-if` 指令将根据表达式 `seen` 的值的真假来插入/移除 `<p>` 元素。

+ 参数

  一些指令能够接收一个“参数”，在指令名称之后以冒号表示。

+ 动态参数

传入的参数的个数是动态的，可以是1个、2个到任意个，还可以是0个。. 在不需要的时候，你完全可以忽略动态函数，不用给它传递任何值.

+ 修饰符

修饰符是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

```html
<form v-on:submit.prevent="onSubmit">...</form>
```

+ v-bind缩写

```html
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>
```

+ v-on缩写

  ```html
  <!-- 完整语法 -->
  <a v-on:click="doSomething">...</a>
  
  <!-- 缩写 -->
  <a @click="doSomething">...</a>
  
  <!-- 动态参数的缩写 (2.6.0+) -->
  <a @[event]="doSomething"> ... </a>
  ```

  







## ES6+ 特性

+ let 和const

    可以把let看成var，只是它定义的变量被限定在了特定范围内才能使用，而离开这个范围则无效。const则很直观，用来定义常量，即无法被更改值的变量。

```javascript
for (let i=0;i<2;i++)console.log(i);//输出: 0,1
console.log(i);//输出：undefined,严格模式下会报错
```

+ 变量解构赋值

一.数组

1.**完全解构：**
let a = 1;
let b = 2;
let c = 3; 可以写成 let [a, b, c] = [1, 2, 3];
**不完全解构：**
等号左边的模式，只匹配一部分的等号右边的数组，解构依然成功

2、默认值：
解构解析允许指定默认值
如：let [x, y = ‘b’] = [‘a’]; // x=‘a’, y=‘b’

注意：只有当一个数组成员严格等于undefined，默认值才会生效；null不严格等于undefined

默认值可以引用解构赋值的其他变量，但该变量必须已经声明

二、对象
1、基本用法与数组一致

2、**不同点**在于：数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

三、字符串
字符串被转换成了一个类似数组的对象，如：

```javascript
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```

四.数值和布尔值(会被先转为对象)

五、圆括号的问题
1、圆括号不能用在声明语句，只能用在赋值语句
2、圆括号不能用在模式上（({ p: (d) } = {}); // 正确，其中p就是模式，d是变量）



+ 扩展和新增方法

1.字符串扩展

**遍历:for...of**

```javascript
 let foo=[{a:2},{b:3}]
        for(let temp of foo){
            console.log(temp);//{a:2},{b:3}
        }
```

**JSON.stringify()**

** UTF-8规定，0xD800到0xDFFF之间的码点，不能单独使用，必须配对使用）**

```javascript
JSON.stringify('\u{D834}') // ""\\uD834""
```

**模板字符串**

> ① 利用模板字符串可以以另一种方法解决字符串拼接的问题。模板字符串用反引号（`）标识，它可以当做普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量
>
> ② 如果使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中。若不想要头和尾的换行，可以用trim方法消除它
>
> ③当需要将反引号作为普通字符串输出时需要加`\`。
>
> ④ 在模板字符串中，大括号内部可以放入任意的javascript表达式，可以进行运算，以及引入对象属性。还可以调用函数。在进行运算时要注意将做运算的变量放到一个${}内，否则结果为字符串的运算。如果大括号中的值不是字符串，将按照一般的规则转为字符串。比如，大括号中是一个对象，将默认调用对象的toString方法。
> ⑤ 大括号内部实际是在执行js代码，故若大括号内部为一个字符串，则会原样输出
>
> ⑥ 模板字符串可以进行嵌套
>
> ⑦ 标签模板：模板字符串可以紧跟在一个函数名后面，该函数将被调用来处理这个模板字符串。这被称为“标签模板”功能。注意：当模板字符串中有变量时，会将字符串和变量拆分开，具体见下例
> ⑧ ==在向函数传参时，模板字符串中有变量时，若变量后面没有字符串，则会自动添加一个空字符串""，当变量后面有字符串时，则不会添加。所有字符串会被第一个参数接收集合成数组，而变量会被其他参数接收。第一个参数有一个raw属性，其中保存的是转以后的原字符串。==在下例中，raw中保存识别的\n不是换行符，而是\n字符串。这样可以通过raw属性获得转义之前的字符串。
> ⑨ 向函数传参时，若函数形参只有一个，则无法接收到模板字符串的变量值。但是可以通过arguments来获取（在arguments中，字符串数组为第一个元素，变量都以不同元素存储起来）
> ⑩ “标签模板”的一个重要应用，就是过滤 HTML 字符串，防止用户输入恶意内容。

字符串新增

**String.fromCodePoint()**

**String.raw()**

2.数值的扩展和新增

**Number.isFinite(), Number.isNaN()**
ES6在Number对象上，新提供了Number.isFinite()和Number.isNaN()两个方法
Number.isFinite()用来检查一个数值是否为有限的(finite)，即不是Infinity；
只要参数类型不是数字，则`Number.isFinite`一律返回`false`；
`Number.isNaN()`用来检查一个值是否为`NaN`



**Number.parseInt(), Number.parseFloat()**
ES6将全局方法`parseInt()`和`parseFloat()`,移植到`Number`对象上面，行为完全保持一致



**Number.isInterger()**

Number.isInterger()用来判断一个数值是否为整数

JavaScript 内部，整数和浮点数采用的是同样的储存方法，所以 25 和 25.0 被视为同一个值
如果参数不是整数值，`Number.isInterger()`返回`false`



**Math.trunc()**
Math.trunc()方法用于去除一个数的小数部分，返回整数部分

对于非数值，Math.trunc内部使用Number方法将其先转化为数值。

对于空值和无法截取整数的值，返回NaN。



**Math.sign()**
Math…sign()方法用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。
Math.sign()方法返回五种值

> 参数为正数，返回 **+1**
> 参数为负数，返回 **-1**
> 参数为0，返回 **0**
> 参数为-0，返回 **-0**
> 参数为其他值，返回 **NaN**

如果是非数值，会自动转为数值，对于无法转化为数值的值，会返回NaN。



**Math.cbrt()**
Math.cbrt()方法用于计算一个数的立方根。



**指数运算符**
ES2016中新增了一个指数运算符(`**`)

3.函数扩展和新增

+ 参数

允许为函数的参数设置默认值

**参数默认值**与**解构赋值的默认值**结合起来使用

+ 属性

  **length属性**

  length将返回**没有指定默认值的参数个数**
  `注意1：rest 参数也不会计入length属性`

```javascript
(function (a = 0, b, c) {}).length // 0
(function (a, b = 1, c) {}).length // 1
```



**name属性**

返回该函数的函数名

```javascript
var f = function () {};
// ES6
f.name // "f"

const bar = function baz() {};
bar.name // "baz"
```

*箭头函数*

使用“箭头”（=>）定义函数

```javascript
//单个参数时
var f = v => v;
// 等同于
var f = function (v) {
  return v;
};

// 多个参数时
var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};

// 箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回
var calculate = (num1, num2) => { 
   let total = num1*num1 + num2*num2; 
   return total; 
}
```

箭头函数的注意点：

- `函数体内的this对象，就是定义时所在的对象`，而不是使用时所在的对象
- `本身无this对象，不可以当作构造函数`，也就是说，不可以使用new命令，否则会抛出一个错误
- `不可以使用arguments对象`，该对象在函数体内不存在。如果要用，可以用 rest 参数代替
- `不可以使用yield命令`，因此箭头函数不能用作 Generator 函数



4.数组的扩展和新增

**Array.from()**

> Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。
>
> 实际应用中，常见的类似数组的对象是 DOM 操作返回的 NodeList 集合，以及函数内部的arguments对象。Array.from都可以将它们转为真正的数组。
>
> 如果map函数里面用到了this关键字，还可以传入Array.from的第三个参数，用来绑定this。
>
> Array.from()可以将各种值转为真正的数组，并且还提供map功能。这实际上意味着，只要有一个原始的数据结构，你就可以先对它的值进行处理，然后转成规范的数组结构，进而就可以使用数量众多的数组方法。
> 

```javascript
Array.from({ length: 2 }, () => 'jack')
// ['jack', 'jack']
```

`Array.from()`的另一个应用是，将字符串转为数组，然后返回字符串的长度。因为它能正确处理各种 Unicode 字符，可以避免 JavaScript 将大于`\uFFFF`的 Unicode 字符，算作两个字符的 bug。

**Array.of()**

`Array.of()`方法用于将一组值，转换为数组。

```javascript
Array.of(15, 13, 8) // [15,13,8]
Array.of(15) // [15]
Array.of(15).length // 1
```

这个方法的主要目的，是弥补数组构造函数Array()的不足。因为参数个数的不同，会导致Array()的行为有差异。

Array.of()基本上可以用来替代Array()或new Array()，并且不存在由于参数不同而导致的重载。它的行为非常统一。

Array.of()总是返回参数值组成的数组。如果没有参数，就返回一个空数组。

**Copywithin()**

数组实例的`copyWithin()`方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。

```javascript
Array.prototype.copyWithin(target, start = 0, end = this.length)
```

它接受三个参数:

target（必需）：从该位置开始替换数据。如果为负值，表示倒数。
start（可选）：从该位置开始读取数据，默认为 0。如果为负值，表示从末尾开始计算。
end（可选）：到该位置前停止读取数据，默认等于数组长度。如果为负值，表示从末尾开始计算。
这三个参数都应该是数值，如果不是，会自动转为数值。

**Find()和FindIndex()**

数组实例的`find`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。

**扩展运算符**

扩展运算符（spread）是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

该运算符主要用于函数调用。

5.对象扩展和新增

对象的解构赋值用于从一个对象取值，相当于将目标对象自身的所有可遍历、但尚未被读取的属性，分配到指定的对象上面。所有的键和它们的值，都会拷贝到新对象上面

```javascript
let{x,y,...z} = {x:1,y:2,a:3,b；4};
x//1,
y//2,
z//{a:3,b:4}
```



+ Symbol

  **基本用法**

  ```javascript
          let s1 = Symbol([1,2]);
          let s2 = Symbol('bar');
  
          console.log(s1) // Symbol(1,2)
          console.log(s2) // Symbol(bar)
  ```

  还需要注意的是，Symbol不允许和其他数据类型的值进行运算，否则会报错，但是可以显示的转为字符串或者布尔值。

**作为属性名使用**

作为属性名使用时不能用点形式，必须放在方括号内，如果用点，声明的是普通属性名，并不是Symbol，如下代码所示：

```javascript
        let mySymbol = Symbol();

        let a = {};
        a.mySymbol="yes"
        a[mySymbol] = 'Hello!';  

        console.log(a["mySymbol"])//yes
        console.log(a[mySymbol])//hello

```

需要注意的是，作为属性名使用时，是不会被for...in、for...of、Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()返回的，但他并不是私有属性，用Object.getOwnPropertySymbols()这个方法，可以获取到所有的Symbol属性名，还有一个新API，就是Reflect.ownKeys，它返回所有键值，包括常规属性。


+ Set和Map数据结构

  1.Set

可以接受数组来初始化实际内部执行

set内部数据无法重复，所以可以用于数组去重，用Array.form可以转为数组

方法和遍历同Map

2.Map

键值对形式存储（键可以是任意数据类型，包括Object）

Map也可以接受一个二维数组作为参数

读取一个未知的值返回undefined

Map中的键是看的内存地址，内存地址不同则键视为不同

对于简单数据类型，两个值严格相等才视为同一个键，-0和0视为同一个键

NAN视为同一个键

四个操作方法
size
set(key,value)
get(key,value)
has(key)
delete(key)
clear()

遍历方法（3个返回遍历器，一个遍历方法）



+ Proxy和Reflect

> Proxy用于修改某些操作的默认行为，即对编程语言层面进行修改，属于“元编程”，Proxy意思为“代理”，即在访问对象之前建立一道“拦截”，任何访问该对象的操作之前都会通过这道“拦截”，即执行Proxy里面定义的方法。

ES6原生规定的Proxy的基本用法为:

```javascript
 let pro = new Proxy(target,handler);
```

其中 new Proxy相当于创建了一个Proxy实例，target为所要拦截的目标对象，handler也是一个对象，里面定义的是对拦截对象所要进行的拦截方法。

> 1、Reflect对象与Proxy对象一样，都是ES6对操作对象设计的API
> 2、对于我个人的理解而言，Reflect设计的目的是为了优化Object的一些操作方法以及合理的返回Object操作返回的结果，对于一些命令式的Object行为，Reflect对象可以将其变为函数式的行为



+ Promise和async/await异步编程

**Promise**

> Promise 是异步编程的一种解决方案，比传统的解决方案，回调函数和事件——更合理和更强大，Promise 是一个对象，从它可以获取异步操作的消息，Promise构造函数接受一个函数作为参数，该函数的两个参数分别是`resolve`和`reject,`基本样例：

```javascript
const promise = new Promise((resolve, reject)=>{
        ses.sendEmail(params, function(err, data) {
            if (err) {
                reject (err);
            } else {
                resolve(data);
            } 
        });
 }); 
```

Promise实例生成以后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回调函数。

```javascript
promise.then(function(value) {
  resolved(value);
}, function(error) {
  rejected(error);
});
```

但是一般不要在then方法里面定义reject状态的回调函数，强烈建议使用catch的方式进行处理，上面的写法可以改写为下面这种更加合理：

```javascript
promise.then(function(data) {    
    resolved(value);
}).catch(function(err) {
    console.log(error)
});
```

**async/await**

> `async`表示函数里有异步操作，`await`表示紧跟在后面的表达式需要等待结果。

async有很多种使用形式：

```javascript
// 函数声明
async function foo() {}
 
// 函数表达式
const foo = async function () {};
 
// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)
 
// Class 的方法
class Storage {
  constructor() {
    this.cachePromise = caches.open('avatars');
  }
 
  async getAvatar(name) {
    const cache = await this.cachePromise;
    return cache.match(`/avatars/${name}.jpg`);
  }
}
 
const storage = new Storage();
storage.getAvatar('jake').then(…);
 
// 箭头函数
const foo = async () => {};
```



+ Generator函数异步编程

> Generator 函数是ES6提供的一种异步编程解决方案，语法行为与传统函数完全不同。
>
> Generator 函数有多种理解角度。语法上，首先可以把它理解成，Generator 函数是一个状态机，封装了多个内部状态。
>
> 执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。
>
> 形式上，Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield表达式，定义不同的内部状态。
> 

```javascript
    function* helloWorldGenerator() {
      yield 'hello';
      yield 'world';
      return 'ending';
    }
    
    var hw = helloWorldGenerator();

```

调用 Generator 函数，返回一个遍历器对象，代表 Generator 函数的内部指针。以后，每次调用遍历器对象的next方法，就会返回一个有着value和done两个属性的对象。value属性表示当前的内部状态的值，是yield表达式后面那个表达式的值；done属性是一个布尔值，表示是否遍历结束。

```javascript
    hw.next()
    // { value: 'hello', done: false }
    
    hw.next()
    // { value: 'world', done: false }
    
    hw.next()
    // { value: 'ending', done: true }
    
    hw.next()
    // { value: undefined, done: true }
```

Generator函数写法:

```javascript
    function * foo(x, y) { ··· }
    function *foo(x, y) { ··· }
    function* foo(x, y) { ··· }
```



+ Class类

在ES6以前，定义一个类如下：

```javascript
function Foo(x,y){
    this.x = x;
    this.y = y;
}
Foo.prototype.sayX = function(){
    console.log(this.x);
}
```

而用`class`改写之后如下：

```javascript
class Foo{
    constructor(x, y){
        this.x = x;
        this.y = y;
    }
    
    sayX(){
        console.log(this.x);
    }
}
```

`Foo`这个类中的`constructor`方法便是构造方法，它对应旧的写法中的`Foo`函数。

除了构造函数，`Foo`类中还定义了一个`sayX`方法，**定义方法的时候前面不需要加入“function”，加了是会报错的。方法与方法之间也不需要加逗号，加了也会报错**

使用`class`定义的类使用时前面必须加`new`关键字，否则会报错。

> JavaScript中函数表达式，即`let foo = function(){}`这样的形式。而类也同样能用表达式的形式定义。

```ja
let newClass = class self{
    getNmae(){
        return self.name;
    }
}
```

**注：类名亦可省略，若内部不需要指向自己**



**类的静态方法**

在很多语言中，在方法前面加个`static`就会使该方法变为静态，**成为只能通过类来调用的类方法。**

而在ES6中也加入了类似的特性，例如：

```javascript
class Foo{
    static test(){
        console.log(this === Foo);
    }
}
```

上面代码中定义了一个名为`test`的静态方法，该方法的执行结果是输出了`true`。这说明了，**在静态方法内部的`this`指向的是类自己。**

静态方法不会被实例继承，如果实例去调用静态方法则会报错。



+ Module模块

> 在ES6前， 实现模块化使用的是 RequireJS 或者 seaJS（分别是基于 AMD 规范的模块化库， 和基于 CMD 规范的模块化库）。
>
> ES6 引入了模块化，其设计思想是在编译时就能确定模块的依赖关系，以及输入和输出的变量。
>
> ES6 的模块化分为导出（export)与导入（import）两个模块。

> 特点
> ES6 的模块自动开启严格模式，不管你有没有在模块头部加上 use strict;。
>
> 模块中可以导入和导出各种类型的变量，如函数，对象，字符串，数字，布尔值，类等。
>
> 每个模块都有自己的上下文，每一个模块内声明的变量都是局部变量，不会污染全局作用域。
>
> 每一个模块只加载一次（是单例的）， 若再去加载同目录下同文件，直接从内存中读取。

> export 与 import基本用法:
> 模块导入导出各种类型的变量，如字符串，数值，函数，类。
>
> 1、导出的函数声明与类声明必须要有名称（export default 命令另外考虑）。
> 2、不仅能导出声明还能导出引用（例如函数）。
> 3、export 命令可以出现在模块的任何位置，但必需处于模块顶层。
> 4、import 命令会提升到整个模块的头部，首先执行。

```javascript
/-----export [test.js]-----/
let myName = “Tom”;
let myAge = 20;
let myfn = function(){undefined
return “My name is” + myName + “! I’m '” + myAge + “years old.”
}
let myClass = class myClass {undefined
static a = “yeah!”;
}
export { myName, myAge, myfn, myClass }
/-----import [xxx.js]-----/
import { myName, myAge, myfn, myClass } from “./test.js”;
console.log(myfn());// My name is Tom! I’m 20 years old.
console.log(myAge);// 20
console.log(myName);// Tom
console.log(myClass.a );// yeah!
```

**as的用法**
export 命令导出的接口名称，须和模块内部的变量有一一对应关系。

导入的变量名，须和导出的接口名称相同，即顺序可以不一致。



使用 as 重新定义导出的接口名称，隐藏模块内部的变量.

```javascript
/-----export [test.js]-----/
let myName = “Tom”;
export { myName as exportName }
/-----import [xxx.js]-----/
import { exportName } from “./test.js”;
console.log(exportName);// Tom
```



不同模块导出接口名称命名重复， 使用 as 重新定义变量名.

```javascript
/-----export [test1.js]-----/
let myName = “Tom”;
export { myName }
/-----export [test2.js]-----/
let myName = “Jerry”;
export { myName }
/-----import [xxx.js]-----/
import { myName as name1 } from “./test1.js”;
import { myName as name2 } from “./test2.js”;
console.log(name1);// Tom
console.log(name2);// Jerry
```

