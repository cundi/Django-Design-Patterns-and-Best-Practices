第二章 应用模式
----------------------
In this chapter, we will cover the following topics:
本章，我们将学习以下内容：  

* Gathering requirements
* 获取请求
* Creating a concept document
* 创建一个概念文档  
* HTML mockups
* HTML原型
* How to divide a project into Apps
* 如何将一个项目分为多个app  
* Whether to write a new app or reuse an existing one
* 是重新写一个新的app还是使用已有的  
* Best practices before starting a project
* 开始一个项目之前的最佳实践  
* Why Python 3?
* 为什是Python3?  
* Starting the SuperBook project
* 启动SuperBook项目  

Many novice developers approach a new project by beginning to write code right away. More often than not it leads to incorrect assumptions, unused features and lost time. Spending some time with your client in understanding core requirements even in a project short on time can yield incredible results. Managing requirements is a key skill worth learning.
很多的开发新手接触到一个新的项目后立即开始码代码目。通常情况下项目会被引入错误的设想，无用的功能并且浪费掉很多时间。花些时间在你的客户身上，来理解一个项目中的核心请求事件，即使很短的时间也能产生惊人的效果。管理需求是一个值得学习的很重要的技巧。  

## 如何获取请求
`创新不关乎肯定一切，而是关乎对所有重要的特性说不
---Steve Jobs`  

I saved several doomed projects by spending a few days with the client to carefully listen to their needs and set the right expectations. Armed with nothing but a pencil and paper (or their digital equivalents), the process is incredibly simple but effective. Here are some of the key points to remember while gathering requirements:
我通过与客户耗去数天来仔细地的倾听他们的需求，设定合理的期望值，拯救了好几个注定失败的项目。除了纸（或者他们的数字设备）和一支笔之外什么也没用，处理过程极其简单但是却很有效。这里是一些获取请求的关键地方：  

1. Talk directly to the application owners even if they are not technical savvy.
1. 直接和应用的所有者沟通即使他们没有技术背景

2. Make sure you listen to their needs fully and note them.
2. 确保你完整的倾听他们的需求并提醒他们。

3. Don't use technical jargon such as "models". Keep it simple and use end-user friendly terms such as a "user profile".
3. 不要使用“模型”这一类的技术术语。保证用语简单，使用终端用户能理解的术语比如“用户账户”。  

4. Set the right expectations. If something is not technically feasible or difficult, make sure you tell them right away.
4. 合理的期望值。如果某件事情在技术行不可行，或者很难实现，要保证你以正确的方法告知他们。  

5. Sketch as much as possible. Humans are visual in nature. Websites more so. Use rough lines and stick figures. No need to be perfect.
5. 描述的尽可能具象。在大自然中人类是依靠视觉。网站更是如此。使用粗线条和图形表。不需要多么的完美。  
6. Break down process flows such as user signup. Any multistep functionality needs to be drawn as boxes connected by arrows.
6. 分解处理流程，比如用户注册。任何多步骤的功能都需要以用箭头连接的方框画出。

7. Finally, work through the features list in the form of user stories or in any easy way to understand the form.
7. 最后，解决用户叙述表格中的特性或者以任何简单的方式去理解它。

8. Play an active role in prioritizing the features into high, medium, or low buckets.
8. 扮演一个活动的角色

9. Be very, very conservative in accepting new features.
9. 在融合新特性上要非常，非常地保守。

10. Post-meeting, share your notes with everyone to avoid misinterpretations.
10. 开会，和大家分享你的笔记以避免误解。  

The first meeting will be long (perhaps a day-long workshop or couple of hour-long meetings). Later, when these meetings become frequent, you can trim them down to 30 minutes or one hour.
第一个会议会比较长（可能是一整个工作日，或者好几个小时）。之后，当这些会议的沟通变的顺畅时，你可以将它们削减到30分钟或者一个小时。  

The output of all this would be a one page write-up and a couple of poorly drawn sketches.
所有的这一切的结果会是写了满满的一整页，以及好几张的乱糟糟的草图。  

In this book, we have taken upon ourselves the noble project of building a social network called SuperBook for superheroes. A simple sketch based off our discussions with a bunch of randomly selected superheroes is shown as follows:
在本书，我们已经着手建构我们自己的一个为超级英雄而构建的称做SuperBook的社会网络。A simple sketch based off our discussions with a bunch of randomly selected superheroes is shown as follows:

￼￼￼￼￼￼
![2015-05-28 14 27 35](https://cloud.githubusercontent.com/assets/10941075/7853834/d6eb7c44-0545-11e5-9ae0-8024411bfaed.png)  

*A sketch of the SuperBook website in responsive design. Desktop (left) and smartphone (right) layouts are shown.
*按照响应式设计的SuperBook网站草图。桌面（左边）和手机（右边）的效果如上.*

## 你是一个会讲故事的人吗？
So what is this one page write-up? It is a simple document that explains how it feels to use the site. In almost all the projects I have worked with, when someone new joins the team, they don't normally go through every bit of paperwork. He or she would be thrilled if they find a single-page document that quickly tells them what the site is meant to be.
那么这一章写的是什么呢？这是一个解释使用这个网站是做何感觉的简易文档。在我做过的几乎所有的项目中，
每当有新人参与进来，我发先他们通常都不会去做一点书面上的工作。但是当他或她发现仅有一页的文档告诉他们
这个网站是什么样子的时候他们会异常的激动。

You can call this document whatever you like—concept document, market requirements document, customer experience documentation, or even an Epic Fragile StoryLog™ (patent pending). It really doesn't matter.
你可以把这个文档称作任何你喜欢的名字——概念文档，市场需求文档，客户体验文档或者甚至叫做Epic Fragile StoryLog(正在申请专利☺)。这都无所谓。

The document should focus on the user experience rather than technical or implementation details. Make it short and interesting to read. In fact, Joel Spolsky's rule number one on documenting requirements is "Be Funny".
这篇文档的关注点在用户体验而不是技术或者实施细节。它尽可能的简短并且有趣。事实上，Joel Spolsky写文档的
第一个原则就是“有趣”。

If possible, write about a typical user (persona in marketing speak), the problem they are facing, and how the web application solves it. Imagine how they would explain the experience to a friend. Try to capture this.
如果可能，写一个典型的用户(通过市场营销人员的发言)，讲述他们遇到的问题，然后他们是如何通过web应用解决的。
想象一下他们是如何向朋友解释他们的体验的。尽可能的抓住它。

Here is a concept document for the SuperBook project:
这是一篇解释SuperBook项目相关概念的文档：

>### 注释

>**SuperBook**的概念
The following interview was conducted after our website SuperBook was launched in the future. A 30 minute user test was conducted just prior to the interview.
>下面的是采访是在未来我们的网站SuperBook网站运行起来之后的记录。一个半小时的用户测试在采访之前就做过了。  

>**请你作下自我介绍**
My name is Aksel. I am a gray squirrel living in downtown New York. However, everyone calls me Acorn. My dad, T. Berry, a famous hip-hop star, used to call me that. I guess I was never good enough at singing to take up the family business.
我叫阿克苏。我是一个生活在纽市中心的灰松鼠。不过呢，大家都叫我阿康。我爹叫缇巴厘是一个嘻哈音乐明星，他过去也这样叫俺。我猜啊，我从来在唱歌方面就差好多，因此没能够子承父业。  

Actually, in my early days, I was a bit of a kleptomaniac. I am allergic to nuts, you know. Other bros have it easy. They can just live off any park. I had to improvise—cafes, movie halls, amusement parks, and so on. I read labels very carefully too.
实际哩，在我很小的时候，我就有点儿喜欢偷东西。医生说我对坚果过敏，这也是大家伙都知道嘀。我们家其他的几个哥哥吃坚果都没啥事儿。我的几个兄弟都可以在任何地方活下去。我也曾酒馆，电影院，游乐园，还有好多地方把歌唱。我看唱片的时候，忒别认真。  

>**好吧，阿康。你知道为什么被挑选为测试用户吗？**  

Probably, because I was featured in a NY Star special on lesser-known superheroes. I guess people find it amusing that a squirrel can use a MacBook (Interviewer: this interview was conducted over chat). Plus, I have the attention span of a squirrel.
可能吧，因为我是纽约大明星里最少知道超级英雄的人。我猜啊，这人类啊都笑话俺这只可以用苹果电脑的松鼠。补充一句，我可是一只非常有耐心的松鼠噢。  

>**就你所见到的，你来说一说你所认识的SuperBook是个什么样子**

I think it is a fantastic idea. I mean, people see superheroes all the time. However, nobody cares about them. Most are lonely and antisocial. SuperBook could change that.
我认为这是个很特别的想法。我的意思是人们一直都在看超级英雄。然而没有人关心他们。
他们大部分都是孤独和不爱交际的。SuperBook可以改变这个情况。

>*What do you think is different about Superbook?* 
>**你认为SuperBook有什么不同？**
It is built from the ground up for people like us. I mean, there is no "Work and Education" nonsense when you want to use your secret identity. Though I don't have one, I can understand why one would.

>*Could you tell us briefly some of the features you noticed?* 
>**你能简单地说一下你注意到的几个特点吗？**
Sure, I think this is a pretty decent social network, where you can:
当然，我认为这是一个非常合理的社会网络，你可以：
```
－ Sign up with any user name (no more, "enter your real name", silliness)
－ 注册任何用户名称(不要输入真实的名字，这是愚蠢的)
－ Fans can follow people without having to add them as "friends"
－ 粉丝可以关注他人而不用加他们为好友
－ Make posts, comment on them, and re-share them
－ 发帖子，评论他们并且可以转发
－ Send a private post to another user
－ 给另一个人发送私信
```
>Everything is easy. It doesn't take a superhuman effort to figure it out. Thanks for your time, Acorn.
这些都很简单，不需要话费很大的力气去发现它。

>*Thanks for your time, Acorn.

## HTML版面的设计
In the early days of building web applications, tools such as Photoshop and Flash were used extensively to get pixel-perfect mockups. They are hardly recommended or used anymore.
在构建web应用的前几天，像Photoshop和Flash这样的工具做到像素级别的模型效果使用是非常广泛的。
这些工具被推荐的都不再推荐了。

Giving a native and consistent experience across smartphones, tablets, laptops, and other platforms is now considered more important than getting that pixel-perfect look. In fact, most web designers directly create layouts on HTML.
现在对智能手机、平板、笔记本电脑和其他的平台保持原生和体验一致比像素层面的效果更为重要了。实际上，大多数的web设计者都基于HTML构建布局。

Creating an HTML mockup is a lot faster and easier than before. If your web designer is unavailable, developers can use a CSS framework such as Bootstrap or ZURB Foundation framework to create pretty decent mockups. 
构建一个HTML版本相比以前快了很多。如果你暂时还没找到Web设计，那么开发者可以利用Bootstrap或者ZRUB这样的基本的CSS框架来构建非常漂亮的版面。

The goal of creating a mockup is to create a realistic preview of the website. It should not merely focus on details and polish to look closer to the final product compared to a sketch, but add interactivity as well. Make your static HTML come to life with working links and some simple JavaScript-driven interactivity.
构建版面的目的就是为了创建一个实际上可用网站的预览。相对于草图，它不仅仅关注于细节和润色更加接近与最终产品，
更要有内部交互。使用活动链接和一些简单的Javascript驱动的交互让你的静态HTML页面动起来。

A good mockup can give 80 percent of customer experience with less than 20 percent of the overall development effort.
一个好的版面可以小于20%的开发总成本，达到80%的客户体验。

## 设计应用
When you have a fairly good idea of what you need to build, you can start to think about the implementation in Django. Once again, it is tempting to start coding away. However, when you spend a few minutes thinking about the design, you can find plenty of different ways to solve a design problem.
当你对于自己所要构建的东西有相当好的构思时，你可以开始思考如何使用Django来实现它。再者，这可以诱导人开始编程。然而，当你花了几分钟时间来思考设计时，你可以发现非常多的不同方法来解决一个设计问题。

You can also start designing tests first, as advocated in Test-driven Design (TDD) methodology. We will see more of the TDD approach in the testing chapter.
一如测试驱动的开发方法论中提倡的那样，你也可以首先从测试开始。我们会在测试章节见到更多的TDD方法。我们会在测试那章见到更多的TDD方法。

Whichever approach you take, it is best to stop and think—"Which are the different ways in which I can implement this? What are the trade-offs? Which factors are more important in our context? Finally, which approach is the best?"
不论你选择的方式是哪一种，最好是停下来想一想——“我要使用哪一种方法来实现它？折衷考虑如何？在我们的应用场景中哪一个因素才是最重要的？最后要考虑的是，哪种方法才是最好的选择？”

Experienced Django developers look at the overall project in different ways. Sticking to the DRY principle (or sometimes because they get lazy), they think—"Have I seen this functionality before? For instance, can this social login feature be implemented using a third-party package such as django-all-auth?"
有经验的Django开发者多角度的看待整个项目。敲定DRY原则，或者有时候只是因为他们很懒，他们在想我之前是不是见到过这个功能？比如，这个社交登录功能是否可以使用诸如django-all-auth这样的第三方包来实现呢？

If they have to write the app themselves, they start thinking of various design patterns in the hope of an elegant design. However, they first need to break down a project at the top level into apps。
如果他们必须自己编写，那么他们会开始考虑多种设计模式以确定一种最优雅的设计。不过，他们首先需要在顶层将一个项目分割到应用中去。


### 将一个项目分离为多个应用、
Django applications are called projects. A project is made up of several applications or apps. An app is a Python package that provides a set of features.
Django的应用称做**project**。一个项目由多个应用或者**apps**组成。应用是一组拥有特定功能的Python包。

Ideally, each app must be reusable. You can create as many apps as you need. Never be afraid to add more apps or refactor the existing ones into multiple apps. A typical Django project contains 15-20 apps.
理论上说，每个app都必须是可以重复使用的。你可以按照自己的需要创建尽可能多的app。绝对不要害怕添加更多的app，或者重构一个已经存在的应用到多个app。一个典型的Djanog项目包含15到20个app。

An important decision to make at this stage is whether to use a third-party Django app or build one from scratch. Third-party apps are ready-to-use apps, which are not built by you. Most packages are quick to install and set up. You can start using them in a few minutes.
到了这一步，一个重要的决定就是是否使用Django的第三方应用，还是从零编写一个。第三方应用是无需你自己开发，便可以开箱即用的。大多数的包都可以很快安装并完成配置，几分钟之后就能够使用它们。

On the other hand, writing your own app often means designing and implementing the models, views, test cases, and so on yourself. Django will make no distinction between apps of either kind.
换句话来说，编写自己的应用意味着要常常自己设计并实现模型，视图，测试。Django和其他类型的应用并没有区别。

### 用自己写的，还是使用别人的
One of Django's biggest strengths is the huge ecosystem of third-party apps. At the time of writing, djangopackages.com lists more than 2,600 packages. You might find that your company or personal library has even more. Once your project is broken into apps and you know which kind of apps you need, you will need to take a call for each app—whether to write or reuse an existing one.
Django的一个强大之处在于它的大量的第三方应用生态。在我写这篇文档的时候，djangopackages.com列出了2600
多个第三方包。你也许会在公司或者个人库中发现更多。一旦你将你的项目分解成多个应用，你就回知道你需要哪种类型的
应用，你需要每一个应用是自己动手造一个还是使用已经存在的。

It might sound easier to install and use a readily available app. However, it not as simple as it sounds. Let's take a look at some third-party authentication apps for our project, and list the reasons why we didn't use them for SuperBook at the time of writing:
安装和使用现成的应用听起来似乎很简单。然而它并没有听起来那么简单。让我们看一下适合我们项目的经过认证的
第三方应用并列出我们为什么不把它们使用在SuperBook上的原因：

- Over-engineered for our needs: We felt that python-social-auth with support for any social login was unnecessary
- 对于需求过度设计：我们认为python-socil-auth支持任何社交登陆是不必要的
- Too specific: Using django-facebook would mean tying our authentication to that provided by a specific website
- 太过具体：使用django-facebook意味着把我们的认证体系绑定到了提供服务的具体网站
- Python dependencies: One of the requirements of django-allauth is python-openid, which is not actively maintained or unapproved
- Python依赖关系：django-allauth的一个依赖包是python-openid，这个包已经不被积极维护了或者说不被认可。
- Non-Python dependencies: Some packages might have non-Python dependencies, such as Redis or Node.js, which have deployment overheads
- 非Python依赖：一些包也许没有Python依赖，例如Redis或者Node.js，这回带来开发花销。
- Not reusable: Many of our own apps were not used because they were not very easy to reuse or were not written to be reusable
- 不可复用：许多我们的应用是不可复用的因为它们不容易被复用或者根本就不是为复用而写的。
  
None of these packages are bad. They just don't meet our needs for now. They might be useful for a different project. In our case, the built-in Django auth app was good enough.
On the other hand, you might prefer to use a third-party app for some of the following reasons:
不是说这些包非常烂。只是现在它们不符合我们的需求。也许它们对其他不同的项目非常有用。对于我们的情况，
Django内建的认证应用已经足够好。从另一方面说，你喜欢使用第三方包也许出于以下一些原因：

- Too hard to get right: Do your model's instances need to form a tree? Use django-mptt for a database-efficient implementation

- Best or recommended app for the job: This changes over time but packages such as django-redis are the most recommended for their use case
- 最好的或者推荐使用的：这个总是会变但是比如django-redis对于它们的使用情况总是最好的推荐
- Missing batteries: Many feel that packages such as django-model-utils and django-extensions should have been part of the framework

- Minimal dependencies: This is always good in my book
- 最少的依赖：这在我的书中总是最好的

So, should you reuse apps and save time or write a new custom app? I would recommend that you try a third-party app in a sandbox. If you are an intermediate Django developer, then the next section will tell you how to try packages in a sandbox.
那么，我应该重复使用应用来节省时间还是重写一个新的应用？我建议你在沙箱中尝试下第三方应用。如果你是一个中级水平的Django开发者，那么下面的章节会教会你如何在沙箱中使用应用。

#### 我的应用沙箱
From time to time, you will come across several blog posts listing the "must-have Django packages". However, the best way to decide whether a package is appropriate for your project is Prototyping.
有时候你会遇到多个列有“Django必备包”的博文。不过呢，要确定一个包是否适合你的项目的方式是原型。

Even if you have created a Python virtual environment for development, trying all these packages and later discarding them can litter your environment. So, I usually end up creating a separate virtual environment named "sandbox" purely for trying such apps. Then, I build a small project to understand how easy it is to use.
即便你因为开发而创建了多个Python虚拟环境，尝试了所有的包然后丢弃它们，但这会搞乱你的虚拟环境。所以，通常的结果是我新建一个独立的称作“沙箱“的虚拟环境，完全只为了尝试这类应用。然后，我构建一个的小型的应用来理解如何使用它。

Later, if I am happy with my test drive of the app, I create a branch in my project using a version control tool such as Git to integrate the app. Then, I continue with coding and running tests in the branch until the necessary features are added. Finally, this branch will be reviewed and merged back to the mainline (sometimes called master) branch.
之后，要是我乐意的话，我会测试应用，使用诸如Git这样的版本控制工具在项目中创建一个集成到应用到分支。然后，我继续

### 它是由哪个包组成的？
To illustrate the process, our SuperBook project can be roughly broken down into the following apps (not the complete list):
为了阐明过程，我们的SuperBook项目可以粗略地分解为下列app（没有全部列出）：
 　>**Authentication** (built-in django.auth): This app handles user signups, login, and logout
  **Authentication**（内建django.auth): 这个app处理用户注册，登录，和登出。

  **Accounts** (custom): This app provides additional user profile information
  **Accounts**（定制）： 这个app提供额外的用户账户信息。

  **Posts** (custom): This app provides posts and comments functionality
  **Posts**（定制）： 这个app提供发表和回复功能

  **Pows** (custom): This app tracks how many "pows" (upvotes or likes) any item gets
  **Pows**（定制）： 这个app跟踪有多少“碰”（支持或者喜欢）

  **Bootstrap forms** (干净的表单): This app handles the form layout and styling
  **Boostrap forms**（crispy-forms）： 这个app处理表单布局和风格

Here, an app has been marked to be built from scratch (tagged "custom") or the third-party Django app that we would be using. As the project progresses, these choices might change. However, this is good enough for a start.
这里，一个app已经被标记为从零构建（标记为“定制”），或者我们要使用的第三方Django应用。随着，项目的发展，这些选项或许改变。不过，这对一个新手足够了。

## 在开始项目之前
While preparing a development environment, make sure that you have the following in place:
在准备开发环境之前，确保你本机有如下的条件：
```
• A fresh Python virtual environment: Python 3 includes the venv module or you can install virtualenv. Both of them prevent polluting your global Python library.
• 一个干净的Python虚拟机：Python3本省包含虚拟模块或者你可以安装一个virutalenv。这两者都是确保
不会污染你的全局Python库。

• Version control: Always use a version control tool such as Git or Mercurial. They are life savers. You can also make changes much more confidently and fearlessly.
• 版本控制：总是要使用一个版本控制工具例如Git或者Mercurial。他们是“救生员”。你可以放心和大胆地
更改你的代码。

• Choose a project template: Django's default project template is not the only option. Based on your needs try others such as twoscoops (https://github.com/twoscoops/django-twoscoops-project) or edge (https://github.com/arocks/edge).
• 选择一个项目模板：Django的默认项目模板不是唯一的选择。根据你的需要选择其他的模板，例如：
twoscoops (https://github.com/twoscoops/django-twoscoops-project) 或者
edge(https://github.com/arocks/edge)。

• Deployment pipeline: I usually worry about this a bit later, but having an easy deployment process helps to show early progress. I prefer Fabric or Ansible.
• 开发路线图：不久之后我总是对这个有点担心，但是拥有一个轻松的开发过程能帮助你战士早起的进度。
我更倾向于使用Fabric或者Ansible。
```
  

## SuperBook-少年来吧，接受你的任务
This book believes in a practical and pragmatic approach of demonstrating Django design patterns and the best practices through examples. For consistency, all our examples will be about building a social network project called SuperBook.
这本书坚信通过例子来展示Django的设计模式和最佳实践是最实际和实用的方法。为了一致性，所有的例子都是围绕
构建一个叫做SuperBook的社交网络项目。

SuperBook focusses exclusively on the niche and often neglected market segment of people with exceptional super powers. You are one of the developers in a team comprised of other developers, web designers, a marketing manager, and a project manager.


The project will be built in the latest version of Python (Version 3.4) and Django (Version 1.7) at the time of writing. Since the choice of Python 3 can be a contentious topic, it deserves a fuller explanation.
这个项目由最新版本的Python(版本3.4)和Django(版本1.7)构建——在本书写的时候。因为选择Python3可能会引起一些争议，我们会给出一个充分的解释。

### 为什么选Python 3？
While the development of Python 3 started in 2006, its first release, Python 3.0, was released on December 3, 2008. The main reasons for a backward incompatible version were—switching to Unicode for all strings, increased use of iterators, cleanup of deprecated features such as old-style classes, and some new syntactic additions such as the nonlocal statement.
Python3的开发始于2006年，它的首次发布，Python3.0，于2008年12月3号释放。它不向后兼容的一个主要原因是把所有strings都转换为了Unicode字符串，增强了迭代器的使用，去除了一些弃用的特性例如旧式类，增加了一些新的语法糖
例如非本地声明。

The reaction to Python 3 in the Django community was rather mixed. Even though the language changes between Version 2 and 3 were small (and over time, reduced), porting the entire Django codebase was a significant migration effort.
Django社区中关于Python3的反应是非常复杂的。尽管2和3的差距很小(随着时间的推移会减少)，移植整个Django代码库
会是个非常有意义的工作。

On February 13, Django 1.5 became the first version to support Python 3. Developers have clarified that, in future, Django will be written for Python 3 with an aim to be backward compatible to Python 2.
在2月13号，Django1.5成为第一个支持Python3的版本。开发者对此进行了澄清，将来，Django将会用Python3来写，以向后兼容Python2为目标。

For this book, Python 3 was ideal for the following reasons:
就本书来说，Python 3 由于以下几个原因看来它是最理想的：


• Better syntax: This fixes a lot of ugly syntaxes, such as izip, xrange, and __unicode__, with the cleaner and more straightforward zip, range, and __str__.
• 更好用的语法：它修复了大量难看的语法，比如izip,xrange和__unicode__，转而用更简洁和明了的zip,
range,和__str__

• Sufficient third-party support: Of the top 200 third-party libraries, more than 80 percent have Python 3 support. 
• 足够充分的第三方支持：在前200名的第三方包中，超过80%支持Python3。

• No legacy code: We are creating a new project, rather than dealing with legacy code that needs to support an older version.
• 没有遗留代码：我们在创造一个新的项目，而不是在处理需要支持旧版本的遗留代码。

• Default in modern platforms: This is already the default Python interpreter in Arch Linux. Ubuntu and Fedora plan to complete the switch in a future release.
• 默认存在于最新的平台：在Arch　Linux中已经是默认的Python解释器。Ubuntu和Fedra计划在将来完全切换到Python3。

• It is easy: From a Django development point of view, there are very few changes, and they can all be learnt in a few minutes.
• 使用方便：站在Django开发的观点来看，其改变非常微小，所有变更的地方学起来也很快。  

  
The last point is important. Even if you are using Python 2, this book will serve you fine. Read Appendix A to understand the changes. You will need to make only minimal adjustments to backport the example code.
最后一点很重要。即使你现在使用的是Python 2，本书中的例子也能够很好的运行。

### 开始项目
This section has the installation instructions for the SuperBook project, which contains all the example code used in this book. Do check the project's README file for the latest installation notes. It is recommended that you create a fresh directory, superbook, first that will contain the virtual environment and the project source code.
本节是SuperBook项目的安装说明，它包含在本书中使用的所有代码实例。要为最新的安装注释检查项目的README文件。推荐你创建一个新的目录，superbook，首先包含虚拟环境，项目源码。

Ideally, every Django project should be in its own separate virtual environment. This makes it easy to install, update, and delete packages without affecting other applications. In Python 3.4, using the built-in venv module is recommended since it also installs pip by default:
理论上，每一个Django项目都应该有自己的虚拟环境。使用虚拟环境可以让Django的安装，升级显得很轻松，而且删除包也不会影响到其他的应用。在Python 3.4中，建议使用内建的venv模块，因为它默认也安装了pip：

```python
$ python3 -m venv sbenv
$ source sbenv/bin/activate
$ export PATH="`pwd`/sbenv/local/bin:$PATH"
```
  
These commands should work in most Unix-based operating systems. For installation instructions on other operating systems or detailed steps please refer to the README file at the Github repository: https://github.com/DjangoPatternsBook/superbook. In the first line, we are invoking the Python 3.4 executable as python3; do confirm if this is correct for your operating system and distribution.
这些命令可以运行在大多数的基于Unix的操作系统。需要其他操作系统的安装指导或者详细的步骤说明请根据GitHub仓库
中的README文件：https://github.com/DjangoPatternsBook/superbook。
在首行，我们把Python3.4的引用改为Python3；确认一下对于你的操作系统这个操作是否正确。

The last export command might not be required in some cases. If running pip freeze lists your system packages rather than being empty, then you will need to enter this line.
代码中位于最后`export`命令在某些情况下不是必须的。如果运行`pip freeze`列出的系统包是空的，那么你需要输入这一行。

>#### 提示
Before starting your Django project, create a fresh virtual environment.
开始Django项目之前，创建一个新的虚拟环境

Next, clone the example project from GitHub and install the dependencies:
接下来，从GitHub克隆项目例子，并安装依赖：

```python
    $ git clone https://github.com/DjangoPatternsBook/superbook.git
    $ cd superbook
    $ pip install -r requirements.txt
```

If you would like to take a look at the finished SuperBook website, just run migrate and start the test server:
如果你想看一看已完成的SuperBook网站，只要运行migrate并启动测试服务器就行了：

```python
    $ cd final
    $ python manage.py migrate
    $ python manage.py createsuperuser
    $ python manage.py runserver
```

In Django 1.7, the migrate command has superseded the syncdb command. We also need to explicitly invoke the createsuperuser command to create a super user so that we can access the admin.
在Django1.7中，migrate命令已经取代了syncdb命令。我们也需要明确地调用creteasuperuser命令来创建一个超级用户，这样我们就可以访问admin了。

You can navigate to http://127.0.0.1:8000 or the URL indicated in your terminal and feel free to play around with the site.
你可以浏览`http://127.0.0.1:8000`或者在终端指明URL，随便玩玩这个网站。

## 总结  
Beginners often underestimate the importance of a good requirements-gathering process. At the same time, it is important not to get bogged down with the details, because programming is inherently an exploratory process. The most successful projects spend the right amount of time preparing and planning before development so that it yields the maximum benefits.
新手总是低估了一个优质的`请求－获取`流程的重要性。于此同时，重要的是不要被细节所束缚，因为从本质来说，编程就是一个探索的过程。很多成功的项目在开发之前都花掉了大量的时间来准备和计划，这样才能获得最佳效果。

We discussed many aspects of designing an application, such as creating interactive mockups or dividing it into reusable components called apps. We also discussed the steps to set up SuperBook, our example project.
我谈论了设计应用的很多方面，比如创建交互模型，或者是将它分割到多个称为app的可重复使用组件。同时我们也讨论了配置项目SuperBook的步骤。

In the next chapter, we will take a look at each component of Django in detail and learn the design patterns and best practices around them.
在下一章，我们会详细地浏览Django的每个组件，并学习与这些组件相关的最佳实践。

--------------------
© Creative Commons BY-NC-ND 3.0   |   [我要订阅](https://github.com/cundi/Django-Design-Patterns-and-Best-Practices/subscription)   |   [我要捐助](https://github.com/cundi/Web.Development.with.Django.Cookbook/issues/3)
