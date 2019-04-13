> 在js调试中，大部分的前端人员都是采用console.log()方法来打印出调试的数据，但是很多人都不知道console这个对象有很多很实在的方法，本文就来介绍一下这些方法的使用。
## 一、console.log()
console.log()这个方法是前端人员最熟悉的了，几乎我们每天都会使用，除了简单的打印对象功能，那么以下两种使用方法你知道吗？
1、多参数记录
![](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555141882360.png)
当我们要去比对两个对象时，想让这两个对象整齐的在两边，这时console.log()就能帮上我们的忙。
2、格式化输出
console.log(msg, values)；这种跟C#的string.Format()有点像，console.log()能支持字符串、整数、浮点数、object对象以及css样式的格式化输出。占位符及其描述如下表。
| 占位符 | 描述       |
| ------ | ---------- |
| %s     | 字符串     |
| %d/%i  | 整数       |
| %f     | 浮点数     |
| %o/%O  | object对象 |
| %c     | css样式    |
接下来我们来做一下举例：
①、字符串格式化为在占位符的地方原样输出我们的值：
![console.log()字符串格式化输出](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555143209250.png)
②、整数与浮点数一致我们这里就不过多举例了：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555143915587.png)
③、对于object对象的格式化输出就有比较大区别了，当为%o时输出和不使用格式化输出打印出来的结果一样，当为%O时，可以看到对象的各个属性，比如我们打印一个DOM节点，%o打印的是此节点及其子节点，%O打印的是是该dom节点各个对象属性。
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555144127890.png)
④、css样式输出，样式会在%c后面都加上这个样式
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555144782291.png)
## 二、console.dir()
这个方法在大部分时候都跟console.log()一致，但是还是略有不同。
![console.dir()](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555145034566.png)
在查询DOM结构时，更能体现出两者的不同。console.log(element)打印的dom结构，而console.dir(element)打印的则是整个dom对象。
![console.dir()](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555145222570.png)
## 三、console.table()
令人意外的是，很多人都不知道有这个方法，其作用是当我们想对一个复杂的对象进行输出时，使用console.log()往往是输出一些不能一目了然的数据，此时console.table()就能帮我们把这个对象整理成一个列表，以便于我们很清晰的看到数据。
![console.table()](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1555145465913.png)


