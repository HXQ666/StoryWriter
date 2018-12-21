> 前言：什么是ES6？ECMAScript 6（简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。其中相比较于ES5新增了诸多的特性，并且ES6可转换为ES5的语法。->[在线ES6转换为ES5工具](http://google.github.io/traceur-compiler/demo/repl.html#%0A)。  
> 本系列学习随笔参考了阮一峰老师的[《ES6标准入门》](http://es6.ruanyifeng.com/)。

## 一、let关键字
#### 1、解决变量提升现象
我们在js中定义变量时，用var声明会出现这种情况：  
```
console.log(a); //不会报错，输出为undefined
var a=1;
```

这就是js的变量提升现象，当浏览器在解析函数时，会将var 声明的变量声明到函数的最前端，导致变量在声明之前使用不会报错，此时let关键字就解决了这个问题。let的作用域只在当前的代码块起作用。 

```
console.log(a); //ReferenceError:a is not defined
let a=1;
```
#### 2、不同代码块互不影响
由于let关键字作用只在当前代码块中起作用，所以不会受外部影响。  
```
function n() {
  let a = 1;
  if (true) {
    let a = 5;
  }
  console.log(a); // 输出1
};
```



#### 3、同一代码块不能重复定义
```
{
    var a=1;
    var a=2;//无报错
}
{
	let a=1;
	let a=2;//Uncaught SyntaxError: Identifier 'a' has already been declared
}
```
## 二、const关键字  
#### 1、const声明一个只读的常量。一旦声明，常量的值就不能改变。
```
const PI = 3.1415;
PI = 3;//Uncaught TypeError: Assignment to constant variable.
```

其本质是对象所存储的内存地址不可变。    
```
const PI={}  
PI.num=3.14159;//不会报错  
PI={num=3.14159};//VM1187:1 Uncaught SyntaxError: Identifier 'PI' has already been declared
```
#### 2、const声明的常量必须声明时就赋值；
```
const PI; // SyntaxError: Missing initializer in const declaration
```
#### 3、const声明的常量跟let的作用域一样。  
```
if (true) {
  const PI = 3.14159;
}
console.log(PI); // Uncaught ReferenceError: PI is not defined
```

## 三、super 关键字
我们都知道，this关键字总是指向函数所在的当前对象，ES6又新增super关键字，指向当前对象的原型对象。他有两种使用方式：  
#### 1、当做函数使用  
```
class parent {
    constructor() {
        console.log(11)
    }
}
class child extends parent{
    constructor() {
        super();
    }
}
let c = new child();//打印11
```
当做函数使用时，super()调用会生成一个空对象，作为context来调用父类的constructor，返回this对象，作为子类constructor的context继续调用构造函数。
#### 2、当做对象使用  
```
const proto = {
  foo: 'hello'
};
const obj = {
  foo: 'world',
  find() {
    return super.foo;
  }
};
Object.setPrototypeOf(obj, proto);
obj.find() // "hello"
```
上面代码中，对象obj.find()方法之中，通过super.foo引用了原型对象proto的foo属性。  
#### 3、注意区分super与this  
说到super与this的区别，我们就要先来看一下this关键字：  
this关键字最终指向的是调用它的对象。我们可以看下面两个例子；
```
function GetThis(){
	console.log(this);
};
GetThis();//打印出window对象。
```
为什么会这样呢。其实最后的调用我们也可以写成window.GetThis();调用他的就是window对象。
如果不信的话我们可以再举个例子；
```
var getThis={ 
	user:'me',
	fn:function(){
		console.log(this);
	}
}
getThis.fn();//打印的就时getThis对象；
```
接下来我们再看一个this与super结合的例子就能理解了：  
```
const proto = {
  x: 'hello',
  foo() {
    console.log(this.x);
  },
};
const obj = {
  x: 'world',
  foo() {
    super.foo();
  }
}
Object.setPrototypeOf(obj, proto);
obj.foo()// "world"
```
上面代码中，super.foo指向原型对象proto的foo方法，但是绑定的this却还是当前对象obj，因此输出的就是world。