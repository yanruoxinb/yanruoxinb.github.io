
### `Script`
1. defer
- 脚本会被延迟到整个页面都解析完毕后再运行，会在`DOMContentLoaded`事件之前执行，规范要求脚本应该按照他们出现的顺序执行
2. async
- 不必等脚本下载和执行完成后再加载页面，同样不必等该异步脚本下载和执行后再加载其它脚本。异步脚本不应该在加载期间修改DOM

### 文档模式
1. 混杂模式
2. 标准模式


### `let` 和 `var` 的区别
 1. 变量提升
```js
    // name 会被提升 
    console.log(name); // undefined 
    var name = 'Matt';
    // ----------
    // age 不会被提升
    console.log(age);  // ReferenceError:age 没有定义 
    let age = 26;
```

2. 全局声明
- `let` 在全局作用域中声明的变量不会成为`window`对象的属性（`var`声明的变量则会）
```js
    var name = 'Matt';
    console.log(window.name); // 'Matt'
    let age = 26;
    console.log(window.age); // undefined
```
3. 条件声明
- 在使用 var 声明变量时，由于声明会被提升，JavaScript 引擎会自动将多余的声明在作用域顶部合 并为一个声明。因为 let 的作用域是块，所以不可能检查前面是否已经使用 let 声明过同名变量，同 时也就不可能在没有声明的情况下声明它
```HTML
<script>
    var name = 'Nicholas';
    let age = 26;
</script>
<script>
    // 假设脚本不确定页面中是否已经声明了同名变量
    // 那它可以假设还没有声明过
    var name = 'Matt';
    // 这里没问题，因为可以被作为一个提升声明来处理, 不需要检查之前是否声明过同名变量
    let age = 36;
    // 如果 age 之前声明过，这里会报错
 </script>
```
> tips1: 在函数内定义变量是省略 `var` 操作符,可以创建一个全局变量
> tips2: `let` 不允许同一个块作用域中出现冗余声明
```js
    var name;
    var name;
    let age;
    let age; //SyntaxError;标识符age已经声明过了
```
> tips3: 对声明冗余报错不会因混用 let 和 var 而受影响。这两个关键字声明的并不是不同类型的变量， 它们只是指出变量在相关作用域如何存在
```js
    var name;
    let name; // SyntaxError
    let age;
    var age; // SyntaxError
```


### 判断数据类型

1. `typeof` 
- 返回值包括以下几种：`undefined`, `number`,`string`, `symbol` ,`object`, `function` ,`boolean`
```js
    // 需要注意的地方 
    typeof null; // object
    console.log(undefined == null) //true

```
2. `instanceof`
-  instanceof 操作符判断左操作数对象的原型链上是否有右边这个构造函数的 prototype 属性，就是说指定对象是不是某个构造函数的实例
> 只适用于对象，不适应原始类型的值

3. constructor
- 可以知道某个实例对象，到底是哪一个构造函数产生的

4. Object.prototype.toString.call

```js
    Object.prototype.toString.call('') ;   // [object String]
    Object.prototype.toString.call(1) ;    // [object Number]
    Object.prototype.toString.call(true) ; // [object Boolean]
    Object.prototype.toString.call(undefined) ; // [object Undefined]
    Object.prototype.toString.call(null) ; // [object Null]
    Object.prototype.toString.call(new Function()) ; // [object Function]
    Object.prototype.toString.call(new Date()) ; // [object Date]
    Object.prototype.toString.call([]) ; // [object Array]
    Object.prototype.toString.call(new RegExp()) ; // [object RegExp]
    Object.prototype.toString.call(new Error()) ; // [object Error]
    Object.prototype.toString.call(document) ; // [object HTMLDocument]
    Object.prototype.toString.call(window) ; //[object Window]

```

### new 函数的作用以及实现
> new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。

- 创造一个全新的对象
- 这个对象会执行[Prototype]连接,将这个新对象的[Prototype](__proto__)链接到这个构造函数.prototype所指向的对象
- 这个新对象会绑定到函数调用的this
- 执行构造函数内部代码
- 如果函数没有返回其它对象，那么 new 表达式中的函数调用会自动返回这个新对象


### 数值转换

1. 布尔值：`true` 转换为 1，`false`转换为 0 
2. 数值：直接返回
3. null：返回 0
4. undefined：返回 `NaN`
5. 字符串

- 如果是空字符串（不包含任何字符），返回0
- 如果字符串包含数值字符，包括数值字符前面带加、减号的情况，则转换为一个十进制数值。 因此，Number("1")返回 1，Number("123")返回 123，Number("011")返回 11(忽略前面 的零)。
- 如果字符串包含有效的浮点值格式如"1.1"，则会转换为相应的浮点值(同样，忽略前面的零)。
- 如果字符串包含有效的十六进制格式如"0xf"，则会转换为与该十六进制值对应的十进制整
数值。
> 如果字符串包含除上述情况之外的其他字符，则返回 NaN。

6. 对象
- 调用 valueOf()方法，并按照上述规则转换返回的值。如果转换结果是 NaN，则调用 toString()方法，再按照转换字符串的规则转换。

### 垃圾回收
- 标记清除
> 标记内存中存储的所有变量（记住，标记方法有很多种）。然后，它会将所有在上下文中的变量，以及被在上下文中的变量引用的变量的标记去掉。在此之后再被加上标记的变量就是待删除的了，原因是任何在上下文中的变量都访问不到它们了。随后垃圾回收程序做一次内存清理，销毁带标记的所有值并收回它们的内存。

- 引用计数

### 创建对象
1. 工厂模式
```js
    function createPerson(name, age, job) {
        let o = new Object();
        o.name = name;
        o.age = age;
        o.job = job;
        o.sayName = function() {
            console.log(this.name);
        };
        return o;
    }
    let person1 = createPerson("Nicholas", 29, "Software Engineer");
    let person2 = createPerson("Greg", 27, "Doctor");
```

2. 构造函数模式
```js
    function Person(name, age, job){
        this.name = name;
        this.age = age;
        this.job = job;
        this.sayName = function() {
            console.log(this.name);
        };
    }
    let person1 = new Person("Nicholas", 29, "Software Engineer");
    let person2 = new Person("Greg", 27, "Doctor");
    person1.sayName(); // Nicholas
    person2.sayName(); // Greg

```
3. 原型模式

