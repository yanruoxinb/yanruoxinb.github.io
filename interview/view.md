
# 易错题整理
## 转换
1. 比较
```js 
"" == false      //true
![] == ""       //true
3+"2" == 5      //false
[5<6<3,3<2<4]   //[true,true]
(2<3)||(3<2)    // true

// ( && ) 的优先级高于逻辑“或”运算符( || ) 的优先级
console.log(true||false&&false, true&&false||true)   
//true true

[ 'a', ,'b', ,].length      // 4
1 + - + + + - + 1           // 2 
[] +  {}                    // '[object Object]'
{} + []                     // 0
[] == false                 // true
NaN == false                // false
NaN == true                 // false
```

2. 数值转换

```js
console.log([“0x1“, “0x2“, “0x3“].map(parseInt));
// [1,NaN,0]
console.log(['1','2','3']).map(parseInt);
// [1,NaN,NaN]
```
## this
```js
//1 => 对象
a = 1;
function foo() {
    console.log(this.a); 
}
const obj = {
    a: 10,
    bar() {
        foo(); 
    }
}
obj.bar();  //1


// 2 => 函数内执行
    var a = 1
    function outer () {
    var a = 2
    function inner () { 
        console.log(this.a) // 1
    }
    inner()
    }
    outer()
```
箭头函数
```js
    function foo() {
        // 返回一个箭头函数
        return (a) => {
            // this继承自foo()
            console.log( this.a );
        };
    }

    var obj1 = {
        a: 2
    };

    var obj2 = {
        a: 3
    }

    var bar = foo.call( obj1 );
    bar.call( obj2 ); // 2，不是3！
```
```js
    function foo() {
        var self = this; // lexical capture of this
        setTimeout( function() {
            console.log( self.a ); 
            // self只是继承了foo()函数的this绑定
        }, 100 );
    }

    var obj = {
        a: 2
    };

    foo.call(obj); // 2
```
```js
    var num = 1;
    var myObject = {
        num: 2,
        add: function() {
            this.num = 3;
            (function() {
                console.log(this.num);
                this.num = 4;
            })();
            console.log(this.num);
        },
        sub: function() {
            console.log(this.num)
        }
    }
    myObject.add();
    console.log(myObject.num);
    console.log(num);
    var sub = myObject.sub;
    sub();
```
```js
var name = 'window'

function Person (name) {
  this.name = name;
  this.show1 = function () {
    console.log(this.name)
  }
  this.show2 = () => console.log(this.name)
  this.show3 = function () {
    return function () {
      console.log(this.name)
    }
  }
  this.show4 = function () {
    return () => console.log(this.name)
  }
}

var personA = new Person('personA')
var personB = new Person('personB')

personA.show1() //personA
personA.show1.call(personB) //personB

personA.show2() // personA
personA.show2.call(personB) //personA

personA.show3()() // window
personA.show3().call(personB) // personB
personA.show3.call(personB)() // window

personA.show4()()  // personA
personA.show4().call(personB) // windoA
personA.show4.call(personB)() //personB
```
```js
var name = 'window'

var person1 = {
  name: 'person1',
  show1: function () {
    console.log(this.name)
  },
  show2: () => console.log(this.name),
  show3: function () {
    return function () {
      console.log(this.name)
    }
  },
  show4: function () {
    return () => console.log(this.name)
  }
}
var person2 = { name: 'person2' }

person1.show1() // person1
person1.show1.call(person2) // person2

person1.show2() // window
person1.show2.call(person2) // window

person1.show3()()  // window
person1.show3().call(person2) //person2
person1.show3.call(person2)() // window

person1.show4()() // person1
person1.show4().call(person2) // person1
person1.show4.call(person2)() // person2
```

## 作用域
```js
  console.log(foo); //会打印函数，而不是 undefined 。
  function foo(){
      console.log("foo");
  }
  var foo = 1;
```
## 变量对象

> 变量提升
```js
foo;  // undefined
var foo = function () {
    console.log('foo1');
}

foo();  // foo1，foo赋值

var foo = function () {
    console.log('foo2');
}

foo(); // foo2，foo重新赋值
```

> 函数提升
```js
foo();  // foo2
function foo() {
    console.log('foo1');
}

foo();  // foo2

function foo() {
    console.log('foo2');
}

foo(); // foo2
```
> 声明优先级： 函数 > 变量
```js
foo();  // foo2
var foo = function() {
    console.log('foo1');
}

foo();  // foo1，foo重新赋值

function foo() {
    console.log('foo2');
}

foo(); // foo1
```

## 内存空间管理
```js
var a = {n: 1};
var b = a;
a.x = a = {n: 2};

a.x 	// 这时 a.x 的值是多少
b.x 	// 这时 b.x 的值是多少

// b={n:1,x:{n:2}} ;a={n:2} ;a===b.x //true

```

结果： a.x：undefined b.x:{n；2}

```html
<script>
    console.log(fun)
    console.log(person)
</script>

<script>
    console.log(person)
    console.log(fun)
    var person = "Eric";
    console.log(person)

    function fun() {
        console.log(person)
        var person = "Tom";
        console.log(person)
    }
    fun()
    console.log(person)
</script>

```




