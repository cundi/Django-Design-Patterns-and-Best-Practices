
第一章 Django和模式
------------------   

在这一章，我们讨论以下话题： 

	 我们为什么选择Django？
	 Django是工作原理
	 什么是模式？
	 常见的模式合集
	 Django中的模式
	

我们为什么选择Django？  

每个web应用都不尽相同，就像一件手工制作的家具一样。你几乎会很少发现大批量的生成能够完美地达到你的需求。即使你从一个基本需求开始，比如一个博客或者一个社交网络，你都需要缓慢地开发，

这就是类似Django或者Rails的web框架非常流行的原因。框架加速了开发，而且它带有很多练好的经过实践的内容。

Python可能比其他流行的编程语言具有更多的web框架。

开箱即用的admin接口，它是Django才有的独一无二的特点，早些时候，特别是在数据记录和测试方面它大有裨益。而Django的开发文档作为一个出色的开源项目早已是备受赞誉。

最后，Django在多个高流量的网站中历经实战的考验。它对于常见的攻击比如跨站脚本和跨站请求攻击有着异常敏锐观察。

尽管，在理论上，可能对于所有类型的网站Django不是最佳选择，你可以是使用Django构建任何类型的网站。例如，要构建一个基于web聊天的实时接口，或许你要使用Tornado，但是web引用剩下的部分你可以仍旧使用Django来完成。对于开发你要学会选择正确的工具。

某些内建的特性，比如admin接口，如果你使用过其他的web框架或许让你听上去感觉有点怪怪的。为了Django的设计，就让我们找出它是如何问世的。

##Django的历史
When you look at the Pyramids of Egypt, you would think that such a simple and minimal design must have been quite obvious. In truth, they are products of 4,000 years of architectural evolution. Step Pyramids, the initial (and clunky) design, had six rectangular blocks of decreasing size. It took several iterations of architectural and engineering improvements until the modern, glazing, and long-lasting limestone structures were invented.  

Looking at Django you might get a similar feeling. So, elegantly built, it must have been 􏰁awlessly conceived. 􏰚n the contrary, it was the result of rewrites and rapid iterations in one of the most high-pressure environments imaginable—a newsroom!  

In the fall of 2003, two programmers, Adrian Holovaty and Simon Willison, working at the Lawrence Journal-World newspaper, were working on creating several local news websites in Kansas. These sites, including LJWorld.com, Lawrence.com, and KUsports.com—like most news sites were not just content-driven portals chock-
full of text, photos, and videos, but they also constantly tried to serve the needs of the local Lawrence community with applications, such as a local business directory, events calendar, classifieds, and so on.  


###一个框架的诞生
This, of course, meant lots of work for Simon, Adrian, and later Jacob Kaplan Moss who had joined their team; with very short deadlines, sometimes with only a few hours' notice. Since it was the early days of web development in Python, they had to write web applications mostly from scratch. So, to save precious time, they gradually refactored out the common modules and tools into something called "The CMS."  

Eventually, the content management parts were spun off into a separate project called the Ellington CMS, which went on to become a successful commercial CMS product. The rest of "The CMS" was a neat underlying framework that was general enough to be used to build web applications of any kind.  

By July 2005, this web development framework was released as Django (pronounced Jang-Oh) under an open source Berkeley Software Distribution (BSD) license.
It was named after the legendary jazz guitarist Django Reinhardt. And the rest,
as they say, is history.  

###移除魔法
Due to its humble origins as an internal tool, Django had a lot of Lawrence 􏰈ournal􏰃World􏰃specific oddities. To 􏰀ake Django truly general purpose, an effort dubbed "Removing the Lawrence" was already underway.  

However, the 􏰀ost significant refactoring effort that Django developers had to undertake was called "Removing the Magic." This ambitious project involved cleaning up all the warts Django had accumulated over the years, including a lot of magic (an informal term for implicit features) and replacing them with a more natural and explicit Pythonic code. For example, the model classes used to be imported from a magic module called django.models.*, rather than directly importing them from the models.py 􏰀odule they were defined in.  

At that time, Django had about a hundred thousand lines of code, and it was a significant rewrite of the 􏰅PI. 􏰚n May 􏰛, 􏰜􏰤􏰤􏰦, these changes, al􏰀ost the si􏰄e of a small book, were integrated into Django's development version trunk and released as Django release 􏰤.􏰧􏰨. This was a significant step toward the Django 􏰛.􏰤 ���  ���ilestone.

###Django坚持做得更好
Every year, conferences called DjangoCons are held across the world for Django developers to meet and interact with each other. They have an adorable tradition
of giving a semi-humorous keynote on "why Django sucks." This could be a member of the Django community, or someone who works on competing web frameworks or just any notable personality.  

Over the years, it is amazing how Django developers took these criticisms positively and mitigated them in subsequent releases. Here is a short summary of the improvements corresponding to what once used to be a shortcoming in Django and the release they were resolved in:  

```
• New form-handling library (Django 0.96)
• Decoupling admin from models (Django 1.0)
• Multiple database support (Django 1.2)
• Managing static files better 􏰋Django 􏰛.􏰥􏰌
• Better time zone support (Django 1.4)
• Customizable user model (Django 1.5)
• Better transaction handling (Django 1.6)
• Built-in database migrations (Django 1.7)
```
  

###Django是如何工作的？
要真正的欣赏Django，你需要撇开表象来看本质。它启发你同时让你不知所措。如果你已经熟悉它，或许就想要跳过这一节。

下图：在一个典型的Django应用中web请求是如何被处理的。  
![django request](http://ww1.sinaimg.cn/mw1024/6184c0e3gw1ertof4w7ckj20m50d8dhi.jpg)

前面的图片展示了从一个访客的浏览器到Django应用并返回的一个web请求的简单历程。如下是数字标识的路径：

	1. 浏览器发送请求（基本上是字节类型的字符串）到web服务器。
	
	2. web服务器（比如，Nginx）把这个请求转交到一个WSGI（比如，uWSGI），或者直接地文件系统能够取出
	一个文件（比如，一个CSS文件）。
	
	3. 不像web服务器那样，WSGI服务器可以直接运行Python应用。请求生成一个被称为environ的Ptyhon字典，
	而且，可以选择传递过去几个中间件的层，最终，达到Django应用。
	
	4. URLconf中含有属于应用的urls.py选择一个视图处理基于请求的URL的那个请求，这个请求就已经变成了
	HttpRequest——一个Python字典对象。
	
	5. 被选择的那个视图通常要做下面所列出的一件或者更多件事情： 
	
	   通过模型与数据库对话。
	   使用模板渲染HTML或者任何格式化过的响应。
	   返回一个纯文本响应（不被显示的）。
	   抛出一个异常。
	   
	6. HttpResponse对象离开Django后，被渲染为一个字符串。
	
	7. 在浏览器见到一个美化的，渲染后的web页面。
	

虽然某些细节被省略掉，这个解释应该有助于欣赏Django的高级架构。它也展示了关键的组件所扮演的角色，比如模型，视图，和模板。Django的很多组件都基于这几个广为人知设计模式。  

##什么是模式？
What is co􏰀􏰀on between the words 􏰇Blueprint,􏰇 􏰇􏰆caffolding,􏰇 and 􏰇Maintenance􏰇? These software development terms have been borrowed from the world of building construction and architecture. However, one of the 􏰀ost in􏰁uential ter􏰀s co􏰀es from a treatise on architecture and urban planning written in 1977 by the leading Austrian architect Christopher Alexander and his team consisting of Murray Silverstein, Sara Ishikawa, and several others.  

The term "Pattern" came in vogue after their seminal work, A Pattern Language: Towns, Buildings, Construction 􏰋volu􏰀e 􏰜 in a five􏰃book series􏰌 based on the astonishing insight that users know about their buildings more than any architect ever could. A pattern refers to an everyday problem and its proposed but time-tested solution.  

In the book, Christopher Alexander states that "Each pattern describes a problem, which occurs over and over again in our environment, and then describes the core of the solution to that problem in such a way that you can use this solution
a million times over, without ever doing it the same way twice."  

For example, the Wings Of Light pattern describes how people prefer buildings with more natural lighting and suggests arranging the building so that it is composed of wings. These wings should be long and narrow, never more than 25 feet wide. Next time you enjoy a stroll through the long well-lit corridors of an old university, be grateful to this pattern.  

Their book contained 253 such practical patterns, from the design of a room to the design of entire cities. Most importantly, each of these patterns gave a name to an abstract problem and together formed a pattern language.  

Re􏰀e􏰀ber when you first ca􏰀e across the word déjà vu? You probably thought "Wow, I never knew that there was a word for that experience." Similarly, architects were not only able to identify patterns in their environ􏰀ent but could also, finally, name them in a way that their peers could understand.  

In the world of software, the term design pattern refers to a general repeatable solution to a commonly occurring problem in software design. It is a formalization of best practices that a developer can use. Like in the world of architecture, the pattern language has proven to be extremely helpful to communicate a certain way of solving a design problem to other programmers.  

There are several collections of design patterns but some have been considerably 􏰀ore in􏰁uential than the others.  
  
###四人组模式
One of the earliest efforts to study and document design patterns was a book
titled Design Patterns: Elements of Reusable Object-Oriented Software by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides, who later became known as the Gang of Four (GoF). This book is so in􏰁uential that 􏰀any consider the 􏰜􏰥 design patterns in the book as fundamental to software engineering itself.  

In reality, the patterns were written primarily for object-oriented programming languages, and it had code examples in C++ and Smalltalk. As we will see shortly, many of these patterns might not be even required in other programming languages with better higher-order abstractions such as Python.  

The 􏰜􏰥 patterns have been broadly classified by their type as follows􏰂：  

```
• Creational Patterns: These include Abstract Factory, Builder Pattern, Factory Method, Prototype Pattern, and Singleton Pattern
• Structural Patterns: These include Adapter Pattern, Bridge Pattern, Composite Pattern, Decorator Pattern, Facade Pattern, Flyweight Pattern, and Proxy Pattern
• Behavioral Patterns: These include Chain of Responsibility, Command Pattern, Interpreter Pattern, Iterator Pattern, Mediator Pattern, Memento Pattern, Observer Pattern, State Pattern, Strategy Pattern, Template Pattern, and Visitor Pattern
```
  
While a detailed explanation of each pattern would be beyond the scope of this book, it would be interesting to identify some of these patterns in Django itself:  

Django中的模式与此对比： 

|四人组模式		|Django组件		|		解释					|
| ------------- |:-------------:|----------------------:|
|命令模式        |HttpRequest    |把一个request封装进一个对象
|观察者模式		|Signals		|一个对象改变状态时，它的所有侦听器都被通知并自动更新
|模板模式		|基于类的视图		| 一个算法的步骤可以不用改变算法结构来重新定义子类

而这些模式是对于学习Django内部的人来说构造最有趣的，Django下面的模式可以再次分类——这也是个常见的问题。

###Django是MVC吗？
Model-View-Controller (MVC) is an architectural pattern invented by Xerox PARC in the 70s. Being the framework used to build user interfaces in Smalltalk, it gets an early mention in the GoF book.  

Today, MVC is a very popular pattern in web application frameworks. Beginners often ask the question􏰩is Django an M􏰊􏰖 fra􏰀ework?  

The answer is both yes and no. The MVC pattern advocates the decoupling of
the presentation layer from the application logic. For instance, while designing
an online game website API, you might present a game's high scores table as an HTML, 􏰪ML, or co􏰀􏰀a􏰃separated 􏰋􏰖􏰆􏰊􏰌 file. However, its underlying 􏰀odel class would be designed independent of how the data would be finally presented.
MVC is very rigid about what models, views, and controllers do. However, Django takes a much more practical view to web applications. Due to the nature of the HTTP protocol, each request for a web page is independent of any other request. Django's framework is designed like a pipeline to process each request and prepare a response.  

Django calls this the Model-Template-View (MTV) architecture. There is separation of concerns between the database interfacing classes (Model), request-processing classes 􏰋􏰊iew􏰌, and a te􏰀plating language for the final presentation 􏰋Te􏰀plate􏰌.
  
If you compare this with the classic MVC—"Model" is comparable to Django's Models, "View" is usually Django's Templates, and "Controller" is the framework itself that processes an incoming HTTP request and routes it to the correct view function.  

If this has not confused you enough, Django prefers to name the callback function to handle each URL a "view" function. This is, unfortunately, not related to the MVC pattern's idea of a View.  

MVC对于模型，视图，和控制该做什么设定的非常严格。然而，到web应用Django采取的是更实用的视图。要处理原生的HTTP协议，每个到web页面的请求独立于其他的请求。Django的框架设计的像一个管道处理每个请求，准备好响应。  

Django称之为模型-模板-视图（MTV）架构。数据库接口类（模型）和 请求处理类（视图），以及最终表现的模板语言之间有着独立关系。  

如果你将它于经典的MVC比较，“模型”可以通Django的模型比较，“视图”  

要是这些都还不足以让你感到迷惑，Django倾向于选择命名回调函数处理每个URL的“视图”函数。即，一个没有MVC视图概念的视图。

###福勒模式
In 2002, Martin Fowler wrote Patterns of Enterprise Application Architecture, which described 40 or so patterns he often encountered while building enterprise applications.  

Unlike the GoF book, which described design patterns, Fowler's book was about architectural patterns. Hence, they describe patterns at a much higher level of abstraction and are largely programming language agnostic.
Fowler's patterns are organized as follows:  

```
• Domain Logic Patterns: These include Domain Model, Transaction Script, Service Layer , and Table Module
• Data Source Architectural Patterns: These include Row Data Gateway, Table Data Gateway, Data Mapper, and Active Record
• Object-Relational Behavioral Patterns: These include Identity Map, Unit of Work, and Lazy Load
• Object-Relational Structural Patterns: These include Foreign Key Mapping, Mapping, Dependent Mapping, Association Table Mapping, Identity
Field, Serialized LOB, Embedded Value, Inheritance Mappers, Single Table Inheritance, Concrete Table Inheritance, and Class Table Inheritance
• Object-Relational Metadata Mapping Patterns: These include Query Object, Metadata Mapping, and Repository
• Web Presentation Patterns: These include Page Controller, Front Controller, Model View Controller, Transform View, Template View, Application Controller, and Two-Step View
• Distribution Patterns: These include Data Transfer Object and Remote Facade
• Offline Concurrency Patterns: These include Coarse Grained Lock, Implicit Lock, Optimistic 􏰚f􏰁ine Lock, and Pessi􏰀istic 􏰚f􏰁ine Lock
• Session State Patterns: These include Database Session State, Client Session State, and Server Session State
• Base Patterns: These include Mapper, Gateway, Layer Supertype, Registry, Value Object, Separated Interface, Money, Plugin, Special Case, Service Stub, and Record Set
```
  
Almost all of these patterns would be useful to know while architecting a Django application. In fact, Fowler's website at http://martinfowler.com/eaaCatalog/ has an excellent catalog of these patterns. I highly recommend that you check them out.
Django also implements a number of these patterns. The following table lists a few of them:  

Django中的模式与此对比：  

|四人组模式	  	|Django组件	  	|解释					|
|-------------	|:-------------:|--------------------:	|
|活动记录		|Django模型		|封装数据库访问，对数据添加域名逻辑
|类表继承		|模型继承		|继承中的每个实体都映射到一个独立的表
|标识自动		|Id字段			|在一个对象中保存一个数据库ID字段以维护标识
|模板视图		|Django模板 		|使用HTML的内嵌生成器渲染到HTML


###还有更多的模式？
Yes, of course. Patterns are discovered all the ti􏰀e. Like living beings, so􏰀e mutate and form new patterns: take, for instance, MVC variants such as Model–view–presenter (MVP), Hierarchical model–view–controller (HMVC), or Model View ViewModel (MVVM).  

Patterns also evolve with ti􏰀e as better solutions to known proble􏰀s are identified. For example, Singleton pattern was once considered to be a design pattern but now is considered to be an Anti-pattern due to the shared state it introduces, similar to using global variables. An Anti-pattern can be defined as co􏰀􏰀only reinvented but a bad solution to a problem.  
  
Some of the other well-known books which catalog patterns are Pattern-Oriented Software Architecture (known as POSA) by Buschmann, Meunier, Rohnert, Sommerlad, and Sta; Enterprise Integration Patterns by Hohpe and Woolf; and
The Design of Sites: Patterns, Principles, and Processes for Crafting a Customer-Centered Web Experience by Duyne, Landay, and Hong.  


##本书中模式
This book will cover Django􏰃specific design and architecture patterns, which would be useful to a Django developer. The upcoming sections will describe how each pattern will be presented.  

*Pattern name*
The heading is the pattern name. If it is a well-known pattern, the commonly used name is used; otherwise, a terse, self-descriptive name has been chosen. Names are important, as they help in building the pattern vocabulary. All patterns will have the following parts:  
*Problem*:􏰂 This brie􏰁y 􏰀entions the proble􏰀.
  
*Solution*: This summarizes the proposed solution(s).
  

*Problem Details*: This elaborates the context of the problem and possibly gives an example.
*Solution Details*: This explains the solution(s) in general terms and provides a sample Django implementation.

本书覆盖针对对于Django开发者会很有用的Django的设计和架构模式。接下来的章节会描述每个模式是如何实现的。

**模式名称**
标题是模式名称。如果它是知名的模式，常用的名字被使用；否则，简洁的，自描述的名称被选择。名称非常重要，它们有助于构建模式词汇。所有的模式都有以下部分：  

###鉴审模式
Despite their near universal usage, Patterns have their share of criticism too. The most common arguments against them are as follows:  

```
• Patterns compensate for the missing language features: Peter Norvig found that 16 of the 23 patterns in Design Patterns were 'invisible or simpler' in Lisp. Considering Python's introspective facilities and first􏰃class functions, this 􏰀ight as well be the case for Python too.
• Patterns repeat best practices: Many patterns are essentially formalizations of best practices such as separation of concerns and could seem redundant.
• Patterns can lead to over-engineering: Implementing the pattern might be less efficient and excessive co􏰀pared to a si􏰀pler solution.

```
尽管它们近乎于通用，模式共享也有它们的审鉴共享。它们的最常见参数如下：  
略

###如何使用模式  
While some of the previous criticisms are quite valid, they are based on how patterns are misused. Here is some advice that can help you understand how best to use design patterns:
  
```
• Don't implement a pattern if your language supports a direct solution
• Don't try to retro􏰃fit everything in ter􏰀s of patterns
• Use a pattern only if it is the most elegant solution in your context
• Don't be afraid to create new patterns
```

>####最佳实践  
In addition to design patterns, there might be a recommended approach to solving a problem. In Django, as with Python, there might be several ways to solve a problem but one idiomatic approach among those.  


###Python之禅和Django的设计哲学  
Generally, the Python community uses the term 'Pythonic' to describe a piece of idiomatic code. It typically refers to the principles laid out in 'The Zen of Python'. Written like a poem, it is extremely useful to describe such a vague concept.
  
>Try entering import this in a Python prompt to view 'The Zen of Python'.  

Furthermore, Django developers have crisply documented their design philosophies while designing the framework at https://docs.djangoproject.com/en/dev/ misc/design-philosophies/.  

While the document describes the thought process behind how Django was designed, it is also useful for developers using Django to build applications. Certain principles such as Don't Repeat Yourself (DRY), loose coupling, and tight cohesion can help you write more maintainable and idiomatic Django applications.  

Django or Python best practices suggested by this book would be formatted in the following manner:
  
>#####Best Practice:
Use BASE_DIR in settings.py and avoid hard-coding directory names.  

>####最佳实践：  
在settings.py中使用BASE_DIR，避免硬编码目录名称。  

##总结  
In this chapter, we looked at why people choose Django over other web frameworks, its interesting history, and how it works. We also examined design patterns, popular pattern collections, and best practices.  

In the next chapter, we will take a look at the first few steps in the beginning of a Django project such as gathering requirements, creating mockups, and setting up the project.  



