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

