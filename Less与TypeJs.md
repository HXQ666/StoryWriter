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
如果我们此时要去改变border的大小我们只要改变borderSize的值即可。
#### 3、怎么去用Less
<1>、浏览器用法
首先我们要先写好页面所需要的less文件，然后引入less.js即可。如下：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546779305779.png)  
> 注意你的less样式文件一定要在引入less.js前先引入。
备注：请在服务器环境下使用！本地直接打开可能会报错！

当浏览器加载后less.js后文件，会去解析rel为stylesheet/less文件，并将转译后的内容生成style元素内嵌在HTML的head节点中，如下图：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546779602154.png)

此种方式缺点：耗性能，优点：简单开发时候无需一直预编译；
<2>、服务端用法
我们可以用nodejs将less文件编译成css，再引用css文件。
上节课我们已经讲过了npm与nodejs的用法，接下来我们就演示一遍全局安装less：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546779910071.png)
这样我们就安装了less，我们也可以看less的编译器lessc的版本，那我们如何将一个less文件编译成一个css文件呢？
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546780584316.png)
利用less编译器即可将指定的less编译成css到指定的目录底下。
#### 4、Less语法
本节旨在教会大家如何使用less，less的语法与魅力请有兴趣的同学移步[Less中文网](http://lesscss.cn/)或者本人将在未来写一篇有关Less的详细文章，敬请期待。

## 二、TypeScript
#### 1、什么是Typescript？
TypeScript是一种由微软开发的自由和开源的编程语言。它是JavaScript的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。截止目前，Typescript已经发布了最新的3.1版本。[Typescript中文网](https://www.tslang.cn);
#### 2、为什么要去用Typescript？

ypeScript的设计目的应该是解决JavaScript的“痛点”：弱类型和没有命名空间，导致很难模块化，不适合开发大型程序。另外它还提供了一些语法糖来帮助大家更方便地实践面向对象的编程。