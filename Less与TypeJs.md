> 前言：讲起前端，我们就不能不讲CSS与Javascript，在这两种技术广泛应用在web应用的今天，他们的扩展也是层出不穷，css的扩展有Less、Sass、Stylus 等，js的超集有Typescript等。今天我们就简单来聊聊Less与Typescript以及webpage技术。本文为简单普及性知识。
## 一、Less
#### 1、什么是Less？
Less是基于CSS的一种扩展技术，包含变量、混合、函数、运算，可以简化CSS代码，降低维护成本。必须通过解析器将less文件转换为css文件供页面使用。Less让 CSS 更易维护、方便制作主题、扩充。Less 可以运行在 Node 或浏览器端。[Less中文网](http://lesscss.cn/)。
#### 2、为什么去用Less
我们在平常web开发过程中写css是否碰到如下的情形：  
```
.border{
	boder-radius:3px;
	-webkit-border-radius:3px;
	-moz-border-radius:3px;
}
```
以上是设置boder的css，但是现在我们要将3px改成5px怎么办呢，我们就要一个个去改，如果多了我们就会很烦，还有可能漏掉一两个没改，在设置颜色中此类问题更为严重，此时CSS的预编译技术就出现了。在Less中我们就可以把上述代码改写成如下：
```
@borderSize:3px
.border{
	boder-radius:@borderSize;
	-webkit-border-radius:@borderSize;
	-moz-border-radius:@borderSize;
}
```
#### 3、怎么去用Less
