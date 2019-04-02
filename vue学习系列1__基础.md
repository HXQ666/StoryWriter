## 一、vue简介
vue是目前最火的一个前端框架，React是最流行的一个前端框架(React可开发万展与手机App，vue借助Weex也可开发手机App)。  
vue与Angularjs、Reactjs并称前端三大主流框架。  
vue是一套构建用户界面的框架，只关注视图层，容易上手，且便于与第三方库既有项目整合。  
## 二、MVVM
要理解MVVM这个思想，我们首先得理解后端的MVC思想，MVC指的是Model/View/Controller(实体模型/视图页面/控制器),这是一种软件设计典范，其优点是：
+ .耦合性低，将视图层与业务层分离，允许更改视图层代码而不用重新编译模型和控制器代码；
+  重用性高，MVC模式允许使用各种不同样式的视图来访问同一个服务器端的代码，因为多个视图能共享一个模型；
+  可维护性高，分离视图层和业务逻辑层也使得WEB应用更易于维护和修改。
![MVC](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1554212706354.png)
MVVM是前端视图层的分层开发思想，分成了M、V和VM，其中VM是M和V之间的调度者。MVVM的思想，主要是为了让我们开发更加方便，因为MVVM提供了数据的双向绑定（数据双向绑定由VM提供）。
![MVVM](https://www.github.com/HXQ666/StoryWriterImg/raw/master/小书匠/1554212936072.png)
