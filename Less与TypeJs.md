> 前言：讲起前端，我们就不能不讲CSS与Javascript，在这两种技术广泛应用在web应用的今天，他们的扩展也是层出不穷，css的扩展有Less、Sass、Stylus 等，js的超集有Typescript等。今天我们就简单来聊聊Less与Typescript以及webpage技术。本文为简单普及性知识，旨在让大家学会怎么去用这三项技术，以及这三项技术在开发的过程中给我们带来的便利性与好处。
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
缺点：使用麻烦 优点：提高站点性能；
#### 4、Less语法
我们在这里简单的说几点less的语法使用。
<1>、变量
```
//less写法
@color:#fff;
@classname: header;
.@classname{
	background-color:@color
}
//编译后的css
.header{
	background-color:#fff
}
```
从例子中我们就可以看到，变量不仅仅可以作为样式属性值：background-color: @color;，还可以作为类名：.@classname 表示的就是 .header，less编译时使用 @ 符号获取变量，仅仅将 @变量名 看成是一个字符串。这样我们就有很多应用场景了，可以让我们的代码减少了很多的重复性，也利于后期的修改与维护。
<2>、混合
```
//css语法
#menu a {
    color: #111;
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}
#menu span {
    height: 16px;
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}
//less语法
.bordered {
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}

#menu a {
    color: #111;
    .bordered;
}

#menu span {
    height: 16px;
    .bordered;
}
```
- 混合也是减少代码书写量的一个方法；
- 混合的类名在定义的时候加上小括弧 ()，那么在转译成 css 文件时就不会出现；
- 混合的类名在被调用的时候加上小括弧 ()和不加上小括弧 ()是一样的效果，看个人习惯

<3>、函数
```
// less语法
.border-radius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
//编译成css
#header {
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
}
.button {
  -webkit-border-radius: 6px;
  -moz-border-radius: 6px;
  border-radius: 6px;
}
```
可以看到，这里就用到了函数的概念，在 #header 和 .button 中分别传入不同的参数，结果也就生成不同的代码。
本节旨在教会大家如何使用less，less的语法与魅力请有兴趣的同学移步[Less中文网](http://lesscss.cn/)或者本人将在未来写一篇有关Less的详细文章，敬请期待。

## 二、TypeScript
#### 1、什么是Typescript？
TypeScript是一种由微软开发的自由和开源的编程语言。它是JavaScript的一个超集，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程。截止目前，Typescript已经发布了最新的3.1版本。[Typescript中文网](https://www.tslang.cn);下图为Typescript与ES6、ES5的关系。Typescript包含了ES6与ES5,简而言之，我们可以在Typescript写ES6与ES5的语法。
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546783020963.png)
#### 2、为什么要去用Typescript？
ypeScript的设计目的应该是解决JavaScript的“痛点”：弱类型和没有命名空间，导致很难模块化，不适合开发大型程序。另外它还提供了一些语法糖来帮助大家更方便地实践面向对象的编程。
#### 3、如何使用Typescript
<1>、安装Typescript
Visual Studio 2017和Visual Studio 2015 Update 3默认包含了TypeScript。 如果你的Visual Studio还没有安装TypeScript，你可以下载它。
既然我们讲到了npm，我们也可以用npm去安装Typescript。
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546782080526.png)
如图，我们也可以去看Typescript的编译器的版本。
<2> 、配置配置文件
我们如果要将一个Typescript文件（.ts文件）编译成一个js文件，那么每次都要去运行tsc命令是不是很烦呢，那如果要编译整个项目呢？有没有那种我们边写ts边生成js的方法呢？答案肯定是有的。接下来我们去配置配置文件。   
我们去运行tsc --init命令，在项目的根目录生成tsconfig.json的配置文件，
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546783856530.png)
如果一个目录下存在一个tsconfig.json文件，那么它意味着这个目录是TypeScript项目的根目录。 tsconfig.json文件中指定了用来编译这个项目的根文件和编译选项。 一个项目可以通过以下方式之一来编译：  
- 不带任何输入文件的情况下调用tsc，编译器会从当前目录开始去查找tsconfig.json文件，逐级向上搜索父目录。  
- 不带任何输入文件的情况下调用tsc，且使用命令行参数--project（或-p）指定一个包含tsconfig.json文件的目录。  
- 当命令行上指定了输入文件时，tsconfig.json文件会被忽略。    

配置项的具体含义请移步官网的[Typescript配置项说明](https://www.tslang.cn/docs/handbook/tsconfig-json.html)

#### 4、Typescript常用语法概要
我们接下来稍微介绍一下Typescript的常用语法：
①、类