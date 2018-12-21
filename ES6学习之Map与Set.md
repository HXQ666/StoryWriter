> 前言：什么是ES6？ECMAScript 6（简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。其中相比较于ES5新增了诸多的特性，并且ES6可转换为ES5的语法。->[在线ES6转换为ES5工具](http://google.github.io/traceur-compiler/demo/repl.html#%0A)。本文参考了阮一峰老师的[《ES6标准入门》](http://es6.ruanyifeng.com/)。
## 一、Set  
Set类似于数组，但是成员都是唯一的，例子如下：  
```
const s = new Set();
[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));
for (let i of s) {
  console.log(i);
}// 输出 2 3 5 4
```
Set可通过add方法添加值，但是不会重复。
Set可接受一个数组参数作为初始化：
```
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
items.size;//输出5
[...items];//输出[1,2,3,4,5];
```
size为Set的属性
由此特性，我们也多了一种去除数组数据重复的方法。此方法判断值的算法类似于精确相等'==='，且两个对象永不相等。
Set有如下方法
add(value)：添加某个值，返回 Set 结构本身。
delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
has(value)：返回一个布尔值，表示该值是否为Set的成员。
clear()：清除所有成员，没有返回值。 
```
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
const newItem=items.add(6));//返回本身{1,2,3,4,5,6}
let isDel= newItem.delete(1);//isDel为true，此时newItem为{2,3,4,5,6}
let isHas = newItem.has(7);//isHas为false
newItem.clear();//无返回值，此时newItem为空{}
```
Array.from方法可以将 Set 结构转为数组。  由此我们又有了一种可以去除数组重复的方法。
```
const items = new Set([1, 2, 3, 4, 5, 5, 5, 5, 5]);
const array = Array.from(items);
console.log(array)//输出[1,2,3,4,5]
```
Set的遍历方法：  
```
var itemd=new Set([1,2,3,4,5]);
```
①.keys(),返回键名的遍历器
```
for (let item of itemd.keys()) {
  console.log(item);
}//输出1 2 3 4 5
```
②.values()返回键值的遍历器,但是Set结构没有键值只有键名，所以与此遍历器与keys()遍历器方法作用一致。
③.entries(),返回键值对的遍历器 
```
for (let item of itemd.entries()) {
  console.log(item);
}//返回[1,1] [2,2] [3,3] [4,4] [5,5]
```
④.forEach()
```
itemd.forEach((value, key) => console.log(key + ' : ' + value))
//返回1:1 2:2 3:3 4:4 5:5 
```
## 二、WeakSet  
WeakSet 结构与 Set 类似，也是不重复的值的集合。  
但是有如下两个区别：  
①.WeakSet 中的对象都是弱引用，WeakSet 的成员只能是对象，而不能是其他类型的值。
```
const ws=new WeakSet();
ws.add(1);//Uncaught TypeError: Invalid value used in weak set
```
②.WeakSet 中的对象都是弱引用，垃圾回收机制会自动回收该对象所占用的内存，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。  
接下来学习一下其语法： 
```
const item=[[1,2],[3,4]];//成员必须为对象，如const itme=[1,2];作为参数就会报错。
const ws=new WeakSet(item);
const itemNew=[5,6];
ws.add(itemNew);//新增一个成员;返回新的实例
ws.delete(itemNew);//删除指定的成员,返回一个布尔值
ws.has(itemNew);//判断某个值是否存在，返回一个布尔值
```
因为WeakSet是弱引用，所以没有size属性，也不能遍历，WeakSet 的一个用处，是储存 DOM 节点，而不用担心这些节点从文档移除时，会引发内存泄漏。
例子如下：
```
const foos = new WeakSet()
class Foo {
  constructor() {
    foos.add(this)
  }
  method () {
    if (!foos.has(this)) {
      throw new TypeError('Foo.prototype.method 只能在Foo的实例上调用！');
    }
  }
}
```
## 三、Map
我们都知道js的对象（object）本质上是键值对的集合，但是一般来说键只能是字符串，导致了诸多的限制。
```
const data = {};
const key = {
	a:1
}
data[key] = 'keydata';
data;//{[object Object]: "keydata"}
```
上面本意是将key对象当做data对象中的一个键，但是却自动转为字符串[object Object]。所以ES6引入了Map数据结构来解决此类问题。  
Map跟Object一样也是键值对结构，但是键不局限与字符串，各种类型的值都可以当做键。
与Set数据结构一样，Map也有其属性与方法。下面我们来一一看下：  
```
const map = new Map([
  ['name', '打伞的鱼666'],
  ['title', 'ES6学习之Map与Set']
]);
map.size; // Map属性，判断成员数量，输出为2
map.has('name'); // 判断是否有这个成员，输出布尔值
map.get('name'); // 参数为键，输出为键值
map.set(1, 'aaa');//设置新成员，若是同一个键赋值多次，则后面那次会覆盖前面那次
map.get('content');//获取未知键则返回undefined
map.delete('name');//删除某个成员，返回布尔值
map.clear();//清除所有成员，没有返回值
```
特别注意的是，只有同一个对象，Map结构才视为一个键，例子如下：
```
const map = new Map();
map.set(['a'], 555);
map.get(['a']) // 内存地址不同，输出为undefined
const b=['b'];
map.set(b,'b');
map.get(b);//同一个对象，输出为'b';
```
Map与Set的遍历器一致，也有四种的遍历器。需要注意的是，Map遍历的顺序是插入的顺序。
```
const map = new Map([
  ['name', '打伞的鱼666'],
  ['title', 'ES6学习之Map与Set']
]);
for (let key of map.keys()) {
  console.log(key);//输出 name  title
}
for (let value of map.values()) {
  console.log(value);//输出 打伞的鱼666  ES6学习之Map与Set
}
for (let item of map.entries()) {
  console.log(item[0], item[1]);
//输出 name 打伞的鱼666
//    title ES6学习之Map与Set
}
// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}
//或者
for (let [key, value] of map) {
  console.log(key, value);
}
map.forEach((value, key) => console.log(key + ' : ' + value));
//输出 name : 打伞的鱼666
//	 title : ES6学习之Map与Set

```
接下来我们看下Map数据结构如何与其他数据类型进行互相转换:  
①.与数组进行转换  
```
[...map];//输出[["name", "打伞的鱼666"],["title", "ES6学习之Map与Set"]]
```
②.数组 转为 Map
将数组传入 Map 构造函数即可
```
new Map([
  ['name', '打伞的鱼666'],
  ['title', 'ES6学习之Map与Set']
]);
```
③.Map 转为对象
```
function strMapToObj(strMap) {
  let obj = Object.create(null);
  for (let [key,value] of strMap) {
    obj[key] = value;
  }
  return obj;
}
strMapToObj(map);
```
如果键为字符串则能正常转换为对象，但是键不是字符串时，会先把键转换为字符串再转换成对象。
④.对象转为 Map
function objToStrMap(obj) {
  let strMap = new Map();
  for (let k of Object.keys(obj)) {
    strMap.set(k, obj[k]);
  }
  return strMap;
}