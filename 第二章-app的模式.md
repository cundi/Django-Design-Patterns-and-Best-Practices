第二章 应用模式
----------------------
  
本章，我们将学习以下内容：  

* 获取请求  
* 创建一个概念文档  
* 如何将一个项目分为多个app  
* 是重新写一个新的app还是使用已有的  
* 开始一个项目之前的最佳实践  
* 为什是Python3?  
* 启动SuperBook项目  

很多的开发新手从依照正确方法来写代码开始，完成一个新的项目。而更多的人经常被引到错误的假想，未被使用的功能，并且浪费掉很多时间。花些时间在你的客户身上，来理解一个项目中的核心请求事件，即使很短的时间也能产生惊人的效果。管理请求是一个值得学习的关键知识点。  

## 如何获取请求
`创新不关乎肯定一切，而是关乎对所有重要的特性说不
---Steve Jobs`  

我通过与客户耗去数天来仔细地的倾听他们的需求，以及合理的期望值，拯救了好几个注定失败的项目。除了纸（或者他们的数字设备）和一支笔之外什么也没用，处理过程极其简单但是却很有效。这里是一些获取请求的关键地方：  

    1. 直接和应用的所有者沟通即使他们没有技术背景。  
    2. 确保你完整的倾听他们的需求并提醒他们。  
    3. 不要使用“模型”这一类的技术术语。保证用语简单，使用终端用户能理解的术语比如“用户账户”。  
    4.合理的期望值。如果某件事情在技术行不可行，或者很难实现，要保证你以正确的方法告知他们。  
    5.描述的尽可能具象。在大自然中人类是依靠视觉。网站更是如此。使用粗线条和图形表。不需要多么的完美。  
    6.分解处理流程，比如用户注册。任何多步骤的功能都需要以用箭头连接的方框画出。
    7.最后，解决用户叙述表格中的特性，
    8.扮演一个活动的角色
    9.在融合新特性上要非常，非常地保守。
    10.开会，和大家分享你的笔记以避免误解。  

第一个会议会比较长（可能是一整个工作日，或者好几个小时）。之后，当这些会议的沟通变的顺畅时，你可以将它们削减到30分钟或者一个小时。  

所有的这一切的结果会是写了满满的一整页，以及好几张的乱糟糟的草图。  

在本书，我们已经着手建构我们自己的一个为超级英雄而构建的称做SuperBook的社会网络。A simple sketch based off our discussions with a bunch of randomly selected superheroes is shown as follows:

￼￼￼￼￼￼
![2015-05-28 14 27 35](https://cloud.githubusercontent.com/assets/10941075/7853834/d6eb7c44-0545-11e5-9ae0-8024411bfaed.png)  

*按照响应式设计的SuperBook网站草图。桌面（左边）和手机（右边）的效果如上.*

## 你是一个会讲故事的人吗？
那么这一章写的是什么呢？这是一个解释使用这个网站是做何感觉的简易文档。


>### 注释
>**SuperBook**的概念
下面的访问记录是在未来我们的网站SuperBook运营之后所做的整理。  

>#### 注释
>**SuperBook的理念**
>下面的是采访是在未来我们的网站SuperBook网站运行起来之后的记录。一个半小时的用户测试在采访之前就做过了。  

>**请你作下自我介绍**
俺叫阿克苏。俺是一个生活在纽市中心的灰松鼠。不过呢，大家都叫俺阿康。俺爹叫缇巴厘是一个嘻哈音乐明星，他过去也这样叫俺。俺猜啊，俺从来在唱歌方面就差好多，因此没能够子承父业。  

>实际哩，在俺很小的时候，俺就有点儿喜欢偷东西。医生说俺对坚果过敏，这也是大家伙都知道嘀。俺家其他的几个哥哥吃坚果都没啥事儿。俺几个兄弟都可以在任何地方活下去。俺也曾酒馆，电影院，游乐园，还有好多地方把歌唱。俺看唱片的时候，忒别认真。  

>**好吧，阿康。你为什么被挑选为测试用户，你知道为什么吗？**  

>可能吧，因为俺是纽约大明星里最少知道超级英雄的人。俺猜啊，这人类啊都笑话俺这只可以用苹果电脑的松鼠。补充一句，俺可是一只非常有耐心的松鼠。  

>**就你所见到的，你来说一说你所认识的SuperBook是个什么样子**

>Actually, in my early days, I was a bit of a kleptomaniac. I am allergic to nuts, you know. Other bros have it easy. They can just live off any park. I had to improvise—cafes, movie halls, amusement parks, and so on. I read labels very carefully too.  

>*Ok, Acorn. Why do you think you were chosen for the user testing?  *

>Probably, because I was featured in a 􏰍Y 􏰊tar special on lesser􏰉known superheroes. I guess people find it a􏰀using that a squirrel can use
a MacBook (Interviewer: this interview was conducted over chat). Plus, I have the attention span of a squirrel.  

>*Based on what you saw, what is your opinion about SuperBook? * 

>I think it is a fantastic idea. I mean, people see superheroes all the time. However, nobody cares about them. Most are lonely and antisocial. SuperBook could change that.  

>*What do you think is different about Superbook?*  

>It is built from the ground up for people like us. I mean, there is no "Work and Education" nonsense when you want to use your secret identity. Though I don't have one, I can understand why one would.  

>*Could you tell us briefly some of the features you noticed?*  

>Sure, I think this is a pretty decent social network, where you can:  
```
• Sign up with any user name (no more, "enter your real name", silliness)
• Fans can follow people without having to add them as "friends"
• Make posts, comment on them, and re-share them
• Send a private post to another user
```
>E􏰋verything is easy. It doesn't take a superhu􏰀an effort to figure it out. Thanks for your time, Acorn.  

## HTML建模
在构建web应用的前几天，像Photoshop和Flash这样的工具做到像素级别的模型效果使用是非常广泛的。 They are hardly recommended or used anymore.  

Giving a native and consistent experience across smartphones, tablets, laptops, and other platforms is now considered more important than getting that pixel-perfect look. In fact, most web designers directly create layouts on HTML.  

Creating an HTML mockup is a lot faster and easier than before. If your web designer is unavailable, developers can use a CSS framework such as Bootstrap or ZURB Foundation framework to create pretty decent mockups.  

The goal of creating a mockup is to create a realistic preview of the website. It should not 􏰀erely focus on details and polish to look closer to the final product compared to a sketch, but add interactivity as well. Make your static HTML come to life with working links and some simple JavaScript-driven interactivity.  

A good mockup can give 80 percent of customer experience with less than 20 percent of the overall development effort.  

## 设计应用
当你对于自己所要构建的东西有相当好的构思时，你可以开始思考如何使用Django来实现它。再者，这可以诱导人开始编程。然而，当你花了几分钟时间来思考设计时，你可以发现非常多的不同方法来解决一个设计问题。  

一如测试驱动的开发方法论中提倡的那样，你也可以首先从测试开始。我们会在测试章节见到更多的TDD方法。我们会在测试那章见到更多的TDD方法。

Whichever approach you take, it is best to stop and think—"Which are the different ways in which I can i􏰀ple􏰀ent this? What are the trade􏰉offs? Which factors are 􏰀ore i􏰀portant in our context? Finally, which approach is the best?􏰎  

Experienced Django developers look at the overall project in different ways. 􏰊ticking to the DRY principle 􏰐or so􏰀eti􏰀es because they get la􏰓y􏰑, they think 􏰌􏰎Have I seen this functionality before? For instance, can this social login feature be implemented using a third-party package such as django-all-auth?􏰎
If they have to write the app themselves, they start thinking of various design patterns in the hope of an elegant design. However, they first need to break down a project at the top level into apps。  


### 将一个项目分离为多个app
Django的应用称做*project*。一个项目由多个应用或者*apps*组成。应用是具有一组特性的Python包。  

理论上说，每个app都必须是可以重复使用的。你可以按照自己的需要创建尽可能多的app。绝对不要害怕添加跟多的app，或者重构一个已经存在的应用到多个app。一个典型的Djanog项目包含15到20个app。  

An important decision to make at this stage is whether to use a third-party Django app or build one from scratch. Third-party apps are ready-to-use apps, which are not built by you. Most packages are quick to install and set up. You can start using them in a few minutes.  

On the other hand, writing your own app often means designing and implementing the models, views, test cases, and so on yourself. Django will make no distinction between apps of either kind.  

### 用自己写的，还是使用别人的
One of Django's biggest strengths is the huge ecosystem of third-party apps. At the time of writing, djangopackages.com lists 􏰀ore than 􏰁,􏰅􏰂􏰂 packages. You 􏰀ight find that your co􏰀pany or personal library has even 􏰀ore. 􏰔nce your project is broken into apps and you know which kind of apps you need, you will need to take a call for each app—whether to write or reuse an existing one.  

It might sound easier to install and use a readily available app. However, it not as simple as it sounds. Let's take a look at some third-party authentication apps for our project, and list the reasons why we didn't use them for SuperBook at the time of writing:  
```
• Over-engineered for our needs: We felt that python-social-auth with support for any social login was unnecessary
• Too specific: Using django-facebook would mean tying our authentication to that provided by a specific website
• Python dependencies: One of the requirements of django-allauth is python-openid, which is not actively maintained or unapproved
• Non-Python dependencies: Some packages might have non-Python dependencies, such as Redis or Node.js, which have deployment overheads
• Not reusable: Many of our own apps were not used because they were not very easy to reuse or were not written to be reusable
```
  
None of these packages are bad. They just don't meet our needs for now. They might be useful for a different project. In our case, the built-in Django auth app was good enough.
On the other hand, you might prefer to use a third-party app for some of the following reasons:
  
```
• Too hard to get right􏰕 Do your 􏰀odel's instances need to for􏰀 a tree? Use django-mptt for a database􏰉efficient i􏰀ple􏰀entation
• Best or recommended app for the job: This changes over time but packages such as django-redis are the most recommended for their use case
• Missing batteries: Many feel that packages such as django-model-utils and django-extensions should have been part of the framework
• Minimal dependencies: This is always good in my book
```
  
S􏰊o, should you reuse apps and save ti􏰀e or write a new custo􏰀 app? I would recommend that you try a third-party app in a sandbox. If you are an intermediate Django developer, then the next section will tell you how to try packages in a sandbox.  
￼

#### 我的app沙箱
From time to time, you will come across several blog posts listing the "must-have Django packages". However, the best way to decide whether a package is appropriate for your project is Prototyping.  

Even if you have created a Python virtual environment for development, trying all these packages and later discarding them can litter your environment. So, I usually end up creating a separate virtual environment named "sandbox" purely for trying such apps. Then, I build a small project to understand how easy it is to use.  

Later, if I am happy with my test drive of the app, I create a branch in my project using a version control tool such as Git to integrate the app. Then, I continue with coding and running tests in the branch until the necessary features are added. Finally, this branch will be reviewed and merged back to the mainline (sometimes called master) branch.  

### 它是由哪个包组成的？
为了阐明过程，我们的SuperBook项目可以粗略地分解为下列app（没有全部列出）：
  
  **Authentication**（内建django.auth): 这个app处理用户注册，登录，和登出。  
  **Accounts**（定制）： 这个app提偶那个额外的用户账户信息。
  **Posts**（定制）： 这个app提供发表和回复功能
  **Pows**（定制）： 这个app跟踪有多少“碰”（支持或者喜欢）
  **Boostrap forms**（crispy-forms）： 这个app处理表单布局和风格  

  这里，一个app已经被标记为从零（标记为“定制”）构建，或者我们要使用的第三方Django应用。随着，项目的发展，这些选项或许改变。不过，这对一个新手足够了。  

## 在开始项目之前
While preparing a development environment, make sure that you have the following in place:  
```
• A fresh Python virtual environment: Python 3 includes the venv module or you can install virtualenv. Both of them prevent polluting your global Python library.
• Version control: Always use a version control tool such as Git or Mercurial. They are life savers. You can also 􏰀ake changes 􏰀uch 􏰀ore confidently and fearlessly.
• Choose a project template: Django's default project template is not the only option. Based on your needs try others such as twoscoops (https://github.com/twoscoops/django-twoscoops-project) or edge (https://github.com/arocks/edge).
• Deployment pipeline: I usually worry about this a bit later, but having an easy deployment process helps to show early progress. I prefer Fabric or Ansible.
```
  

## SuperBook-你的任务，你应该选择去接受
This book believes in a practical and pragmatic approach of demonstrating Django design patterns and the best practices through examples. For consistency, all our examples will be about building a social network project called SuperBook.  

SuperBook focusses exclusively on the niche and often neglected market segment of people with exceptional super powers. You are one of the developers in a tea􏰀 comprised of other developers, web designers, a marketing manager, and a project manager.  

The project will be built in the latest version of Python (Version 3.4) and Django (Version 1.7) at the time of writing. Since the choice of Python 3 can be a contentious topic, it deserves a fuller explanation.  

### 为什么选Python 3？
While the development of Python 􏰄 started in 􏰁􏰂􏰂􏰅, its first release, Python 􏰄.􏰂, was released on December 3, 2008. The main reasons for a backward incompatible version were—switching to Unicode for all strings, increased use of iterators, cleanup of deprecated features such as old-style classes, and some new syntactic additions such as the nonlocal statement.  

The reaction to Python 3 in the Django community was rather mixed. Even though the language changes between Version 2 and 3 were small (and over time, reduced), porting the entire Django codebase was a significant 􏰀igration effort.  

􏰔n February 􏰃􏰄, Django 􏰃.􏰜 beca􏰀e the first version to support Python 􏰄. Developers have clarified that, in future, Django will be written for Python 􏰄 with an ai􏰀 to be backward compatible to Python 2.  

For this book, Python 3 was ideal for the following reasons:  

```
• Better syntax􏰕 This fixes a lot of ugly syntaxes, such as izip, xrange, and __unicode__, with the cleaner and more straightforward zip, range, and __str__.
• Sufficient third-party support: Of the top 200 third-party libraries, more than 80 percent have Python 3 support.
• No legacy code: We are creating a new project, rather than dealing with legacy code that needs to support an older version.
• Default in modern platforms: This is already the default Python interpreter in Arch Linux. Ubuntu and Fedora plan to complete the switch in a future release.
• It is easy: From a Django development point of view, there are very few changes, and they can all be learnt in a few minutes.
```
  
The last point is important. Even if you are using Python 2, this book will serve you fine. Read 􏰆ppendix 􏰆 to understand the changes. You will need to make only minimal adjustments to backport the example code.  

### 开始项目
本节是SuperBook项目的安装说明，它包含在本书中使用的所有代码实例。要为最新的安装注释检查项目的README文件。推荐你创建一个新的目录，superbook，首先包含虚拟环境，项目源码。  

Ideally, every Django project should be in its own separate virtual environment. This makes it easy to install, update, and delete packages without affecting other applications. In Python 3.4, using the built-in venv module is recommended since it also installs pip by default:  

```python
$ python3 -m venv sbenv
$ source sbenv/bin/activate
$ export PATH="`pwd`/sbenv/local/bin:$PATH"
```
  
These commands should work in most Unix-based operating systems. For installation instructions on other operating systems or detailed steps please refer to the README file at the 􏰒ithub repository􏰕 https://github.com/DjangoPatternsBook/ superbook. In the first line, we are invoking the Python 􏰄.􏰝 executable as python3;
do confir􏰀 if this is correct for your operating syste􏰀 and distribution.  

The last export command might not be required in some cases. If running pip freeze lists your system packages rather than being empty, then you will need to enter this line.  

>### 提示
*开始Django项目之前，创建一个新的虚拟环境*  
接着，从GitHub克隆项目例子，并安装依赖：  

>```python
    $ git clone https://github.com/DjangoPatternsBook/superbook.git
    $ cd superbook
    $ pip install -r requirements.txt
```  

如果你想看一看已完成的SuperBook网站，只要运行migrate并启动测试服务器就行了：  

```python    
    $ cd final
    $ python manage.py migrate
    $ python manage.py createsuperuser
    $ python manage.py runserver  
```  

在Django1.7中，migrate命令已经被syncdb命令取代。我们也需要明确地调用creteasuperuser命令来创建一个超级用户，这样我们就可以访问admin了。  

你可以浏览`http://127.0.0.1:8000`或者在终端指明URL，随便玩玩这个网站。  
  
  
##总结  
Beginners often underestimate the importance of a good requirements-gathering process. At the same time, it is important not to get bogged down with the details, because programming is inherently an exploratory process. The most successful projects spend the right amount of time preparing and planning before develop􏰀ent so that it yields the 􏰀axi􏰀u􏰀 benefits.  

We discussed many aspects of designing an application, such as creating interactive mockups or dividing it into reusable components called apps. We also discussed the steps to set up SuperBook, our example project.  

In the next chapter, we will take a look at each component of Django in detail and learn the design patterns and best practices around them.  

--------------------
© Creative Commons BY-NC-ND 3.0   |   [我要订阅](https://github.com/cundi/Django-Design-Patterns-and-Best-Practices/subscription)   |   [我要捐助](https://github.com/cundi/Web.Development.with.Django.Cookbook/issues/3)
