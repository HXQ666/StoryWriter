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
<2>