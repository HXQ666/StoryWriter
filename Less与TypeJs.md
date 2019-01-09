> 前言：讲起前端，我们就不能不讲CSS与Javascript，在这两种技术广泛应用的今天，他们的扩展也是层出不穷，css的扩展有Less、Sass、Stylus 等，js的超集有Typescript等。今天我们就简单来聊聊Less与Typescript以及静态模块打包器webpack。本文为简单普及性知识，旨在让大家学会怎么去用这三项技术，以及这三项技术在开发的过程中给我们带来的便利性与好处。
> 本文借鉴了以下同学的文章，特此感谢。
> - HANS许的[Less与TypeScript的简单理解与应用，并使用WebPack打包静态页面](https://www.cnblogs.com/xuhuale/p/10229627.html)
> - dkvirus的[三十分钟学会 Less](https://www.jianshu.com/p/48018e5da7dd)。
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
以上是设置boder的css，但是现在我们要将3px改成5px怎么办呢，我们就要一个个去改，如果多了我们就会很烦，还有可能漏掉一两个没改，在设置颜色中此类问题更为严重，优秀的程序员怎么可能容忍这样的情况呢，所以此时CSS的预编译技术就出现了。在Less中我们就可以把上述代码改写成如下：
```
@borderSize:3px
.border{
	boder-radius:@borderSize;
	-webkit-border-radius:@borderSize;
	-moz-border-radius:@borderSize;
}
```
上面就是Less的语法-变量的一种形式，如果我们此时要去改变border的大小我们只要改变borderSize的值即可。
#### 3、怎么去用Less
<1>、浏览器用法     
我们先来讲一下浏览器用法：  
首先我们要先写好页面所需要的less文件，然后引入less.js即可。如下：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546779305779.png)  
> Tips：注意你的less样式文件一定要在引入less.js前先引入。
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
本节旨在教会大家如何使用less以及less的基本语法，这里还有许多好用的语法没有讲到，比如内置函数、运算、神奇的import等等。less的语法与魅力请有兴趣的同学移步[Less中文网](http://lesscss.cn/)或者本人将在未来写一篇有关Less的详细文章，敬请期待。

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

接下来我们根据tsconfig.json文件与vscode来配置一个在编写ts文件时按保存可以时时编译成js文件的方法：
首先，我们先在项目的根目录建一个ts文件：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546820712430.png)
然后，我们去tsconfig.json配置要生成的js目录：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546821074744.png)
接下来点击vs上方菜单的终端，点击运行任务，选择tsc-监视：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546820802687.png)
此时终端会显示成这样，证明监视成功：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546820860038.png)
我们在ts文件中写ts代码，按ctrl+s保存时，会自动在我们设置好的目录下生成js文件：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546820992268.png)

配置项的具体含义请移步官网的[Typescript配置项说明](https://www.tslang.cn/docs/handbook/tsconfig-json.html)

#### 4、Typescript常用语法概要
我们接下来稍微介绍一下Typescript的常用语法：
<1>、数据类型
```
布尔类型:boolean
数字类型:number
字符串类型:string
数组类型:array
元组类型:tuple
枚举类型:enum(新)
任意类型:any(新)
null和undefined
void类型(新)
never类型(新)
```
Typescript为了使代码更加规范与更容易维护，新增了数据类型校验：
```
//js代码,es5的正确写法
var flag=true;
flag=1;
```
但是在Typescript这样写是错误的。写ts变量时必须指定数据类型。
```
//ts写法
var flag:boolean=true;
flag=1;//直接报错。
```
<2>、类
```
//ts语法
class person{
    name:string;
    constructor(name:string){
        this.name=name
    }
    getname():string{
        return this.name;
    };
    setname(name:string):void{
        this.name=name;
    }
}
var p= new person('张三');
alert( p.getname());
p.setname('李四');
alert(p.getname())
//编译后的js
var person = /** @class */ (function () {
    function person(name) {
        this.name = name;
    }
    person.prototype.getname = function () {
        return this.name;
    };
    ;
    person.prototype.setname = function (name) {
        this.name = name;
    };
    return person;
}());
var p = new person('张三');
alert(p.getname());
p.setname('李四');
alert(p.getname());
```
我们可以看到,其实Ts的类跟我们后端语言C#之类的非常相像。
## 三、webpack
#### 1、什么是webpack？
在当今的社会，作为 web 开发，会越来越意识到前端的重要性，随着 HTML5、 CSS3、 ES6 各种技术的发展，前端的开发越来越庞大。甚至有些应用就是单页面应用(SPA)，纯 JavaScript 开发，JavaScript 文件的管理也是一个问题。JavaScript 模块化编程，已经成为一个迫切的需求，这就出现了 JavaScript 的模块解决方案。webpack是一个前端模块化方案，更侧重模块打包，我们可以把开发中的所有资源（图片、js 文件、css 文件等）都看成模块，通过 loader（加载器）和 plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。
总的来说就是如下图：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546868168518.png)
#### 2、如何使用webpack
<1> 、安装webpack
安装webpack首先必须要有nodejs的环境，我们用npm工具去安装webpack，命令为：
```
npm install -g webpack
/*在webpack 3中，webpack本身和它的CLI以前都是在同一个包中，但在第4版中，他们已经将两者分开来更好地管理它们*/
npm install -g webpack-cli
```
安装完毕后我们查看版本如下图：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546868064591.png)

<2> 、简单上手webpack
接下来我们来做一个最简单的webpack的打包编译。
我首先在vscode新建一个文件夹webpackDemo,新建一个hellowebpack.js的文件，写几句js代码
接下来我们在这个目录下运行命令：
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546869950896.png)
从警告信息中我们就可以知道，我们没有设定mode，webpack分为开发模式和生产模式。我们看下这两种模式的编译
![
](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546870319896.png)
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546870366886.png)
从图中我们也能看出来production编译出来的明显比较小。
上面这种方法是全局去告诉webpack要编译哪个文件，那我们也可以用另外一种方法：
我们先用 npm init -y 初始化项目，新建一个package.json文件。
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546872088375.png)
这里面包含了项目的很多信息，记录项目的描述信息：项目作者、项目描述、项目依赖哪些包、插件配置信息等等。
其中scripts对象是指定了运行脚本命令的npm命令行缩写
我们将test改为build，用来简写webpack。
![enter description here](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1546872410827.png)
我们再用--save -dev安装局部本地依赖，此时package.json就会有安装依赖包的信息：
![enter description here](https://markdown.xiaoshujiang.com/img/spinner.gif "[[[1546872677399]]]" )