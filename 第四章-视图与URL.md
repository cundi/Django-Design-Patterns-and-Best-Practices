第四章-视图和URL
***************
  
本章，我们会讨论以下话题：  
    
    * 基于类的和基于函数的视图
    * Mixins
    * 装饰器
    * 常见视图模式
    * 设计URL  

## 顶层的视图
Django中，视图是可以调用的，它接受请求，返回响应。通常它是一个函数或者一个有`as_view()`这样的特殊方法的类。  

这两种情况下，我们创建一个普通的接受`HTTPRequest`作为自己的第一个参数并返回一个`HTTPResponse`的Python函数。`URLConf`也可以对这个函数传递额外的参数。这些参数由URL部分捕捉到，或者是设置了默认值。  

这里是简单视图的例子：  

```python
    # In views.py
    from django.http import HttpResponse


    def hello_fn(request, name="World"):
        return HttpResponse("Hellp {}!".format(name))
```  

这两行视图函数非常简单和好理解。目前我们还没有用`request`参数来做任何事情。例如，通过查看`GET/POST`参数， URI路径，或者`REMOTE_ADDR`这样的HTTP头部，我们验证请求可以更好地理解所调用视图中的上下文。   

`URLConf`中所对应的行如下：  

```python
    # In urls.py
        url(r'^hello-fn/(?P<name>\w+)/$', views.hello_fn),
        url(r'^hello_fn/$', views.hello_fn),
```  

我们重复使用相同的视图以支持两个URL模式。第一个模式获得了一个name参数。第二个模式没有从URL获得任何参数，这个例子中视图会使用默认的`World`名字。  

## 让视图变得更高级
基于类的视图在Django 1.4中被引入。下面是之前的视图在用了同等功能的基于类的视图重写之后的样子：  

```python
    from django.views.generic import View


    class HelloView(View):
        def get(self, request, name="World"):
            return HttpResponse("Hello {}!".format(name))
```  

同样地，对应的`URLConf`也有两行，一如下面命令所示：  

```python
    # In urls.py
        url(r'^hello-cl/(?P<name>\w+)/$', views.HelloView.as_view()),
        url(r'^hello-cl/$', views.HelloView.as_view()),
```  

这个`view`类和我们之前的视图函数之间有多个有趣的不同点。最明显的一点就是我们需要定义一个类。接着，我们明确地定义了我们唯一要处理的`GET`请求。之前的视图对`GET`，`POST`做出了同样的响应，或者其他的HTTP词汇，下面是在Django shell中使用测试客户端：  

```python
    >>> from django.test import Client
    >>> c = Client()
    >>> c.get("http://0.0.0.0:8000/hello-fn/").content
    b'Hello World!'
    >>> c.post("http://0.0.0.0:8000/hello-fn/").content
    b'Hello World!'
    >>> c.get("http://0.0.0.0:8000/hello-cl/").content
    b'Hello World!'
    >>> c.post("http://0.0.0.0:8000/hello-cl/").content
    b''
```  

从安全和可维护性的观察角度来看，还是显式更好一些。  

当你需要定制视图的时候，使用类的好处才会清楚的体现出来。即，你需要改变问候内容。你可以写一个任意类型的普通视图类，并派生出所指定的问候类：  

```python
    class CreetView(View):
        greeting = "Hello {}!"
        default_name = "World"
        def get(self, request, **kwargs):
            name = kwargs.pop("name", self.default_name)
            return HttpResponse(self.greeting.format(name))


    class SuperVillianView(GreetView):
        greeting = "We are the future, {}. Not them."
        default_name = "my friend"
```  

现在，`URLConf`可以引用派生的类：  

```python
    # In urls.py
        url(r'^hello-su/(?<name>\w+)/$', views.SuperVillianView.as_view()),
        url(r'^hello-su/$', views.SuperVillianView.as_view()),
```  

按照类似的方式来定制视图函数不可行时，你需要添加多个有默认值的关键字参数。这样做很快会变得不可控制。这就是为什么通用视图从视图函数迁移到基于类的视图的原因。  

>##### Django Unchained
After spending 2 weeks hunting for good Django developers, Steve started to think out of the box. Noticing the tremendous success of their recent hackathon, he and Hart organized a Django Unchained contest at S.H.I.M. The rules were simple—build one web application a day. It could be a simple one but you cannot skip a day or break the chain. Whoever creates the longest chain, wins.  

>The winner—Brad Zanni was a real surprise. Being a traditional designer with hardly any programming background, he had once attended week-long Django training just for kicks. He managed to create an unbroken chain of 21 Django sites, mostly from scratch.  

>The very next day, Steve scheduled a 10 o' clock meeting with him at his office. Though Brad didn't know it, it was going to be his recruitment interview. At the scheduled time, there was a soft knock and a lean bearded guy in his late twenties stepped in.  

>As they talked, Brad made no pretense of the fact that he was not
a programmer. In fact, there was no pretense to him at all. Peering through his thick-rimmed glasses with calm blue eyes, he explained that his secret was quite simple—get inspired and then focus.
He used to start each day with a simple wireframe. He would then create an empty Django project with a Twitter bootstrap template. He found Django's generic class-based views a great way to create views with hardly any code. Sometimes, he would use a mixin or two from Django-braces. He also loved the admin interface for adding data on the go.  

>His favorite project was Labyrinth—a Honeypot disguised as a baseball forum. He even managed to trap a few surveillance bots hunting for vulnerable sites. When Steve explained about the SuperBook project, he was more than happy to accept the offer. The idea of creating an interstellar social network truly fascinated him.  

>With a little more digging around, Steve was able to find half a dozen more interesting profiles like Brad within S.H.I.M. He learnt that rather that looking outside he should have searched within the organization in the first place.  
  
## 基于类的通用视图
通常，基于类的通用视图为了能更好地重复使用代码，便利用以面向对象的方法（模板方法模式）实现的视图。我讨厌术语`generic views`。我更乐意把它们叫做`stock view`。就像所储备的照片，你可以按照自己的常见需要对它们做出轻微的调整。  

通用视图的产生是因为Django开发者发现他们在每一个项目中都在重复构建同类型的视图。几乎每个项目都需要有一个页面来显示一个对象的列表（`List View`），或者一个对象的具体内容（`Detail View`），有或者是一个用来创建对象的表单。依照DRY精神，这些可重复使用的视图被Django打包在一起。  

这里给出Django 1.7 中通用视图速查表格：  

|类型 |类名称    |描述                                                         |
|:---|:--------|:------------------------------------------------------------|
基本|*View*|这是所有视图的父类。它执行派遣和清醒检测。
基本|*TemplateView*|传递模板。暴露*URLConf*的关键字到上下文。
基本|*RedirectView*|对任意*GET*请求做出重定向。
列表|*ListView*|传递任意可迭代的项，比如*queryset*。
详细|*DetailView*|传递基于来自*URLConf*的*pk*或者*slug*。
编辑|*FormView*|传递并处理表单
编辑|*CreateView*|传递并处理生成新对象的表单。
编辑|*UpdateView*|传递并处理更新对象的表单。
编辑|*DeleteView*|传递并处理删除对象的表单。
日期|*ArchiveIndexView*|传递含有日期字段的对象列表，并把最新的日期放在最前面。
日期|*YearArchiveView*|传递基于*URLConf*中所给定的*year*的对象列表
日期|*MonthArchiveView*|传递基于*year*和*month*的对象列表。
日期|*WeekArchiveView*|传递基于*year*和*week*数的对象列表。
日期|*DayArchiveView*|传递基于*year*，*month*和*day*的对象列表。
日期|*TodayArchiveView*|传递基于当日日期的对象列表。
日期|*DateDetailView*|传递一个基于*year*，*month*，和*day*，通过自身的*pk*或者*slug*来区分的对象。

  
我们已经提过类似`BaseDetailView`这样的基类，或是`SingleObjectMixin`这样的mixins。它们设计成父类。多数情况下，你不会直接地运用它们。  

大多数人对基于类的视图和基于类的通用视图感到迷惑。因为它们的名称相似，但是它们并非是同一个东西。这导致一些令人担心的误会：  

    *通用视图仅仅是Django的一组集合*：谢天谢地，这是错的。在基于类的通用视图中是没有什么特殊魔法的。  
    它们省去了你创建自己的一组基于类的通用视图的麻烦。你也可以使用类似`django-vanilla-views`这样的第三方库，它对于标准的通用视图有一个更为简单的实现方法。记住使用自定义的的通用视图或许会让其他人对你的代码感到陌生。  

    *基于类的视图必须总是从一个通用视图中派生*：同样地，通用视图类也没有什么魔法。尽管，有百分之九十的时间，你都发现类似`View`的通用类当作基类来使用是最令人满意的，你免去了自己去实现相似的特性的麻烦。  

## 视图mixin
Mixin是在基于类的视图中按照DRY原则写代码的精髓所在。就像模型mixin一样，视图mixin得益于Python的多重继承，因此它可以很好的重复使用大部分的功能。在Python 3 中它们常常是无父类的类（或者是在Python 2 中新格式的类都派生自`object`）。  

Mixin会在定义过的地方拦截视图的处理过程。例如，大多数的通用视图使用`get_context_data`设置上下文字典。它是一个插入额外上下文的好地方，比如一个用户可以查看所有指向发布文章的`feed`变量，一如下面命令所示：  

```python
    class FeedMixin(object):
        def get_context_data(self, **kwargs):
            context = super().get_context_data(**kwargs)
            context["feed"] = models.Post.objects.viewable_posts(self.request.user)
            return context
```  

首先`get_context_data`方法在基类中调用所有与自己同名的方法来生成上下文。接下来，他用`feed`变量更新上下文字典。  

现在，在基类的列表中，这个mixin通过包含它就可以很容易地来添加用户的订阅。这就是说，如果SuperBook需要有一个发布新文章便可被订阅的表单的典型社交网络主页，你可以像下面这样使用这个mixin：  

```python
    class MyFeed(FeedMixin, generic.CreateView):
        model = models.Post
        template_name = "myfeed.html"
        success_url = reverse_lazy("my_feed")
```  

一个写的很好的mixin比需要非常高的要求。它应该在多数情况下都可以被灵活运用。在前面的例子中，`FeedMixin`会重写派生类中的`feed`上下文变量。如果父类要把`feed`用作上下文变量，它可以通过包含这个mixin发挥作用。因此，在使用mixin之前，你需要检查mixin的源代码以及其他的类，以确保没有方法或者上下文变量的冲突。  


## mixins的顺序
你或许见过有多个mixins的代码：  

```python
    class ComplexView(MyMixin, YourMixin, AccesMixin, DetailView):
```  

It can get quite tricky to figure out the order to list the base classes. Like m􏰀ost things in Django, the normal rules of Python apply. Python's **Method Resolution Order** (MRO) determines how they should be arranged.  

要找到列出基类的顺序是非常棘手的一件事。就像Django中的大多数情形一样，要用到就是Python的基本规则。Python的**方法解析顺序**决定了它们该如何被排列出来。  

In a nutshell, m􏰀ixins co􏰀me first and base classes com􏰀e last. The m􏰀ore speciali􏰓ed the parent class is, the more it moves to the left. In practice, this is the only rule you will need to remember.   

简单来说就是，把mixin放在最前面，而基类放在最后面。如果有更多的父类，这些父类都会被放到左边。

To understand why this works, consider the following simple example:  

```python
class A:
       def do(self):
           print("A")

class B:
    def do(self):
           print("B")

class BA(B, A):
       pass

class AB(A, B):
       pass

BA().do() # Prints B
AB().do() # Prints A
```
  
As you would expect, if B is mentioned before A in the list of base classes, then B's method gets called and vice versa.  

Now imagine A is a base class such as CreateView and B is a mixin such as FeedMixin. The mixin is an enhancement over the basic functionality of the base class. Hence, the 􏰀ixin code should act first and in turn, call the base method if needed. So, the correct order is BA 􏰐􏰀ixins first, base last􏰑.  

The order in which base classes are called can be determined by checking the `__mro__` attribute of the class:  

```python
>>> AB.__mro__
 (__main__.AB, __main__.A, __main__.B, object)
```
  
So, if AB calls `super()`, first A gets called; then, A's `super()` will call B, and so on.  

>```Python's MRO usually follows a depth􏰉first, left􏰉to􏰉right order to select a method in the class hierarchy. More details can be found at http://www.python.org/download/releases/2.3/mro/.
```  

## 装饰器  
Before class-based views, decorators were the only way to change the behavior of function-based views. Being wrappers around a function, they cannot change the inner working of the view, and thus effectively treat them as black boxes.  

A decorator is function that takes a function and returns the decorated function. 􏰇onfused? There is so􏰀e syntactic sugar to help you. 􏰏se the annotation notation @, as shown in the following login_required decorator example:  

```python
@login_required
def simple_view(request):
       return HttpResponse()
```
  
The following code is exactly same as above:  

```python
def simple_view(request):
       return HttpResponse()
   simple_view = login_required(simple_view)
```  

Since `login_required` wraps around the view, a wrapper function gets the control first. If the user was not logged in, then it redirects to `settings.LOGIN_URL`. Otherwise, it executes `simple_view` as if it did not exist.
Decorators are less 􏰈exible than 􏰀ixins. However, they are si􏰀pler. You can
use both decorators and mixins in Django. In fact, many mixins are implemented with decorators.

## 视图模式  
Let's take a look at some common design patterns seen in designing views.  

### 模式-访问控制视图
*问题*：页面需要基于用户是否登录，是否是站点成员，或者其他的任何条件，按照条件访问。  

*解决方法*：使用mixins或者装饰器控制到视图的访问。  

### 问题细节
大多数的网站都有当你登录才能访问的页面。另外的一些页面可以被匿名访问或者普通游客访问。如果一个匿名访客视图访问一个面向已登录用户的页面，它们会被路由到登录页面。理论上，在登录后，他们应该被路由回第一次想要见到的页面。  

## 方案详情
有两个控制到一个视图的访问方法：  

    1. 通过对基于函数视图或者基于类视图使用一个装饰器实现控制：  

```python
@login_required(MyView.as_view())
```  

    2. 通过覆盖mixin的类视图的`dispatch`方法实现控制：  

```python
 class LoginRequiredMixin:
           @method_decorator(login_required)
           def dispatch(self, request, *args, **kwargs):
               return super().dispatch(request, *args, **kwargs)
```  

    这里我们真的不需要装饰器。更为明确地形式建议如下：  

```python
class LoginRequiredMixin:
           def dispatch(self, request, *args, **kwargs):
               if not request.user.is_authenticated():
                   raise PermissionDenied
               return super().dispatch(request, *args, **kwargs)
```  


当异常`PermissionDenied`抛出时，Django会在根目录中显示`403.html`模板，如果模板不存在，就会出现“403 Forbidden”页面。  

当然，  

这里使用它们控制到登录和匿名访问的视图：  

```python
from braces.views import LoginRequiredMixin, AnonymousRequiredMixin
   class UserProfileView(LoginRequiredMixin, DetailView):
       # This view will be seen only if you are logged-in
       pass
   class LoginFormView(AnonymousRequiredMixin, FormView):
       # This view will NOT be seen if you are loggedin
       authenticated_redirect_url = "/feed"
```  

Django中站点成员是使用设置在用户模型中的`is_staff`标识的用户。  
同样地，你可以使用称做`UserPassesTestMixin`的django-braces mixin：  

```python
    from braces.views import UserPassesTestMixin

    class SomeStaffView(UserPassesTestMixin, TemplateView):
        def test_func(self, user):
            return user.is_staff
```  


你也可以创建执行特定检查的mixins，比如对象是否被原作者或者其他人（使用登录用户比对）编辑：  

```python
    class CheckOwnerMixin:
        # 被用于派生自SingleObjectMixin的类
        def get_object(self, queryset=None):
            obj = super().get_object(queryset)
            if not obj.owner == self.request.user:
                raise PermissionDenied
            return obj
```  

## 模式-上下文加强器
*问题*：多个基于类的通用视图需要相同的上下文变量。  

*解决方法*：创建一个设置为共享上下文变量的mixin。  

### 问题细节

Django templates can only show variables that are present in its context dictionary. However, sites need the same information in several pages. For instance, a sidebar showing the recent posts in your feed might be needed in several views.  

However, if we use a generic class-based view, we would typically have a limited set of context variables related to a specific 􏰀odel. 􏰊etting the sa􏰀e context variable in each view is not DRY.   

### 方案详情  
Most generic class-based views are derived from ContextMixin. It provides
the get_context_data method, which most classes override, to add their own context variables. While overriding this method, as a best practice, you will need to call get_context_data of the superclass first and then add or override your context variables.  

We can abstract this in the form of a mixin, as we have seen before:  

```python
class FeedMixin(object):
       def get_context_data(self, **kwargs):
           context = super().get_context_data(**kwargs)
           context["feed"] = models.Post.objects.viewable_posts(self.
   request.user)
           return context
```  
We can add this mixin to our views and use the added context variables in our te􏰀plates. 􏰍otice that we are using the 􏰀odel 􏰀anager defined in Chapter 3, Models, to filter the posts.  

A more general solution is to use StaticContextMixin from django-braces for static-context variables. For example, we can add an additional context variable latest_profile that contains the latest user to join the site:  

```python
class CtxView(StaticContextMixin, generic.TemplateView):
       template_name = "ctx.html"
       static_context = {"latest_profile": Profile.objects.latest('pk')}
```  
Here, static context means anything that is unchanged from a request to request. In that sense, you can mention QuerySets as well. However, our feed context variable needs self.request.user to retrieve the user's viewable posts. Hence, it cannot be included as a static context here.  


## 模式-服务
*问题*：Information from your website is often scraped and processed by other applications.  

*解决方法*：创建返回机器友好的格式的轻量的服务，比如JSON或者XML。

### 问题细节  
We often forget that websites are not just used by hu􏰀ans. 􏰆 significant percentage of web traffic co􏰀es fro􏰀 other progra􏰀s like crawlers, bots, or scrapers. Sometimes, you will need to write such programs yourself to extract information from another website.  

Generally, pages designed for human consumption are cumbersome for mechanical extraction. HTML pages have information surrounded by markup, requiring extensive cleanup. Sometimes, information will be scattered, needing extensive data collation and transformation.  

􏰆 􏰀achine interface would be ideal in such situations. You can not only reduce the hassle of extracting information but also enable the creation of mashups. The longevity of an application would be greatly increased if its functionality is exposed in a machine-friendly manner.  

### 方案详情  
**Service-oriented architecture (SOA)** has popularized the concept of a service. A service is a distinct piece of functionality exposed to other applications as a service. For example, Twitter provides a service that returns the most recent public statuses.  

A service has to follow certain basic principles:  

```
• Statelessness: This avoids the internal state by externalizing state information
• Loosely coupled: This has fewer dependencies and a minimum of assumptions
• Composable: This should be easy to reuse and combine with other services
```  

In Django, you can create a basic service without any third-party packages. Instead of returning HTML, you can return the serialized data in the JSON format. This form of a service is usually called a web Application Programming Interface (API).  

For exa􏰀ple, we can create a si􏰀ple service that returns five recent public posts from SuperBook as follows:  

```python
class PublicPostJSONView(generic.View):
       def get(self, request, *args, **kwargs):
           msgs = models.Post.objects.public_posts().values(
               "posted_by_id", "message")[:5]
           return HttpResponse(list(msgs), content_type="application/json")
```  

For a more reusable implementation, you can use the `JSONResponseMixin` class
from `django-braces` to return JSON using its `render_json_response` method:  

```python
from braces.views import JSONResponseMixin
   class PublicPostJSONView(JSONResponseMixin, generic.View):
       def get(self, request, *args, **kwargs):
           msgs = models.Post.objects.public_posts().values("posted_by_id", "message")[:5]
           return self.render_json_response(list(msgs))
```  

If we try to retrieve this view, we will get a JSON string rather than an HTML response:  

```python
>>> from django.test import Client
>>> Client().get("http://0.0.0.0:8000/public/").content
b'[{"posted_by_id": 23, "message": "Hello!"},
   {"posted_by_id": 13, "message": "Feeling happy"},
   ...
```  

Note that we cannot pass the QuerySet method directly to render the JSON response. It has to be a list, dictionary, or any other basic Python built-in data type recognized by the JSON serializer.  

Of course, you will need to use a package such as Django REST framework if you need to build anything more complex than this simple API. Django REST framework takes care of serializing (and deserializing) QuerySets, authentication, generating
a web-browsable API, and many other features essential to create a robust and full􏰉􏰈edged 􏰆PI.  


##设计URL  
Django has one of the 􏰀ost 􏰈exible 􏰏RL sche􏰀es a􏰀ong web fra􏰀eworks. Basically, there is no i􏰀plied 􏰏RL sche􏰀e. You can explicitly define any 􏰏RL scheme you like using appropriate regular expressions.  

However, as superheroes love to say—"With great power comes great responsibility.􏰎 You cannot get away with a sloppy 􏰏RL design any 􏰀more.   

URLs used to be ugly because they were considered to be ignored by users. Back in the 90s when portals used to be popular, the common assumption was that your users will come through the front door, that is, the home page. They will navigate to the other pages of the site by clicking on links.  

Search engines have changed all that. According to a 2013 research report, nearly half (47 percent) of all visits originate from a search engine. This means that any page in your website, depending on the search relevance and popularity can be the first page your user sees. 􏰆ny 􏰏RL can be the front door.  

More importantly, Browsing 101 taught us security. Don't click on a blue link in the wild, we warn beginners. Read the 􏰏RL first. Is it really your bank's 􏰏RL or a site trying to phish your login details?  

Today, URLs have become part of the user interface. They are seen, copied, shared, and even edited. Make them look good and understandable from a glance. No more eye sores such as:  

```
http://example.com/gallery/default.asp?sid=9DF4BC0280DF12D3ACB6009027
1E26A8&command=commntform
```  

Short and meaningful URLs are not only appreciated by users but also by search engines. URLs that are long and have less relevance to the content adversely affect your site's search engine rankings.  

Finally, as implied by the maxim "Cool URIs don't change," you should try to maintain your URL structure over time. Even if your website is completely redesigned, your old links should still work. Django makes it easy to ensure that this is so.  

Before we delve into the details of designing URLs, we need to understand the structure of a URL.  

##URL解剖  
Technically, URLs belong to a 􏰀ore general fa􏰀ily of identifiers called **Uniform Resource Identifiers (URIs)**. Hence, a URL has the same structure as a URI.  

A URI is composed of several parts:  

```
URI = Scheme + Net Location + Path + Query + Fragment
```
For example, a URI (http://dev.example.com:80/gallery/ videos?id=217#comments) can be deconstructed in Python using the urlparse function:  

```python
>>> from urllib.parse import urlparse
>>> urlparse("http://dev.example.com:80/gallery/videos?id=217#comments")
ParseResult(scheme='http', netloc='dev.example.com:80', path='/gallery/
videos', params='', query='id=217', fragment='comments')
```  

The URI parts can be depicted graphically as follows:  

![2015-05-28 15 33 49](https://cloud.githubusercontent.com/assets/10941075/7854758/f8740cc4-054e-11e5-94c1-533bdb7f20bc.png)
  
Even though Django documentation prefers to use the term URLs, it might more technically correct to say that you are working with URIs most of the time. We will use the terms interchangeably in this book.  

Django URL patterns are mostly concerned about the 'Path' part of the URI. All other parts are tucked away.  


##url.py中发生了什么？  
It is often helpful to consider urls.py as the entry point of your project. It is usually the first file I open when I study a Django project. 􏰋ssentially, urls.py contains the root 􏰏RL configuration or URLConf of the entire project.  

It would be a Python list returned from patterns assigned to a global variable called urlpatterns. Each incoming URL is matched with each pattern from top to botto􏰀 in a sequence. In the first 􏰀atch, the search stops, and the request is sent to the corresponding view.  

Here, in considerably si􏰀plified for􏰀, is an excerpt of urls.py from Python.org, which was recently rewritten in Django:  

```python
 urlpatterns = patterns(
       '',
       # Homepage
       url(r'^$', views.IndexView.as_view(), name='home'),
       # About
       url(r'^about/$',
           TemplateView.as_view(template_name="python/about.html"),
           name='about'),
       # Blog URLs
       url(r'^blogs/', include('blogs.urls', namespace='blog')),
       # Job archive
       url(r'^jobs/(?P<pk>\d+)/$',
           views.JobArchive.as_view(),
           name='job_archive'),
       # Admin
       url(r'^admin/', include(admin.site.urls)),
   )
```  

Some interesting things to note here are as follows:  

```
• The first argu􏰀ent of the patterns function is the prefix. It is usually blank
for the root URLConf. The remaining arguments are all URL patterns.
• Each URL pattern is created using the url function, which takes five arguments. Most patterns have three arguments: the regular expression pattern, view callable, and name of the view.
• The about pattern defines the view by directly instantiating TemplateView. Some hate this style since it mentions the implementation, thereby violating separation of concerns.
• Blog 􏰏RLs are 􏰀entioned elsewhere, specifically in urls.py inside the blogs app. In general, separating an app's 􏰏RL pattern into its own file is good practice.
• The jobs pattern is the only example here of a named regular expression.
```
  
In future versions of Django, urlpatterns should be a plain list of URL pattern objects rather than arguments to the patterns function. This is great for sites with lots of patterns, since urlpatterns being a function can accept only a maximum of 255 arguments.  

If you are new to Python regular expressions, you 􏰀ight find the pattern syntax to be slightly cryptic. Let's try to demystify it.  

##URL模式语法  
URL regular expression patterns can sometimes look like a confusing mass of punctuation marks. However, like most things in Django, it is just regular Python.  

It can be easily understood by knowing that URL patterns serve two functions: to match URLs appearing in a certain form, and to extract the interesting bits from a URL.  

The first part is easy. If you need to 􏰀atch a path such as `/jobs/1234`, then just use the `"^jobs/\d+" `pattern (here `\d` stands for a single digit from `0` to `9`). Ignore the leading slash, as it gets eaten up.
The second part is interesting because, in our example, there are two ways of extracting the job ID (that is, `1234`), which is required by the view.  

The simplest way is to put a parenthesis around every group of values to be captured. Each of the values will be passed as a positional argument to the view. For example, the `"^jobs/(\d+)"` pattern will send the value "1234" as the second argu􏰀ent 􏰐the first being the request􏰑 to the view.  

The problem with positional arguments is that it is very easy to mix up the order. Hence, we have name-based arguments, where each captured value can be named. Our example will now look like `"^jobs/(?P<pk>\d+)/" `. This means that the view will be called with a keyword argument pk being equal to "1234".  

If you have a class-based view, you can access your positional arguments in `self. args` and name-based arguments in `self.kwargs`. Many generic views expect their arguments solely as name-based arguments, for example, self.kwargs["slug"].  

##Mnemonic – parents question pink action-figures
I admit that the syntax for name-based arguments is quite difficult to remember. Often, I use a simple mnemonic as a memory aid. The phrase "Parents Question Pink Action-figures" stands for the first letters of Parenthesis, Question mark, (the letter) P, and Angle brackets.    

Put them together and you get (`?P<` . You can enter the name of the pattern and figure out the rest yourself.    

It is a handy trick and really easy to remember. Just imagine a furious parent holding a pink-colored hulk action figure.    

Another tip is to use an online regular expression generator such as http://pythex. org/ or https://www.debuggex.com/tocraftandtestyourregularexpressions.  

##命名和命名空间  
Always name your patterns. It helps in decoupling your code from the exact URL paths. For instance, in the previous URLConf, if you want to redirect to the about page, it might be tempting to use redirect("/about"). Instead, use redirect("about"), as it uses the name rather than the path.
Here are some more examples of reverse lookups:  

```python
>>> from django.core.urlresolvers import reverse
>>> print(reverse("home"))
"/"
>>> print(reverse("job_archive", kwargs={"pk":"1234"}))
"jobs/1234/"
```  

Names must be unique. If two patterns have the same name, they will not work. So, some Django packages used to add prefixes to the pattern name. For example, an application named blog might have to call its edit view as 'blog-edit' since 'edit' is a common name and might cause conflict with another application.  

Namespaces were created to solve such problems. Pattern names used in a namespace have to be only unique within that namespace and not the entire project. It is recommended that you give every app its own namespace. For example, we can create a 'blog' namespace with only the blog's URLs by including this line in
the root URLconf:  

```python
   url(r'^blog/', include('blog.urls', namespace='blog')),
```  

Now the blog app can use pattern names, such as 'edit' or anything else as long as they are unique within that app. While referring to a name within a namespace, you will need to mention the namespace, followed by a ':' before the name. It would be` "blog:edit" `in our example.  

As Zen of Python says—"Namespaces are one honking great idea—let's do more of those." You can create nested namespaces if it makes your pattern names cleaner, such as "blog:comment:edit". I highly recommend that you use namespaces in your projects.  

##模式顺序
Order your patterns to take advantage of how Django processes them, that is, top-down. A good rule of thumb is to keep all the special cases at the top. Broader patterns can be mentioned further down. The broadest—a catch-all—if present, can go at the very end.  
For example, the path to your blog posts might be any valid set of characters, but you might want to handle the About page separately. The right sequence of patterns should be as follows:  

```python
   urlpatterns = patterns(
       '',
       url(r'^about/$', AboutView.as_view(), name='about'),
       url(r'^(?P<slug>\w+)/$', ArticleView.as_view(), name='article'),
   )  
```  

If we reverse the order, then the special case, the AboutView, will never get called.  

## URL模式风格  
Designing URLs of a site consistently can be easily overlooked. Well-designed URLs can not only logically organize your site but also make it easy for users to guess paths. Poorly designed ones can even be a security risk: say, using a database ID (which occurs in a monotonic increasing sequence of integers) in a URL pattern can increase the risk of information theft or site ripping.  

Let's examine some common styles followed in designing URLs.  

## 分布存储URL
Some sites are laid out like Departmental stores. There is a section for Food, inside which there would be an aisle for Fruits, within which a section with different varieties of Apples would be arranged together.  
In the case of URLs, this means that you will find these pages arranged hierarchically as follows:  

```
   http://site.com/ <section> / <sub-section> / <item>  
```  

The beauty of this layout is that it is so easy to climb up to the parent section. Once you remove the tail end after the slash, you are one level up.  

For example, you can create a similar structure for the articles section, as shown here:  

```python
   # project's main urls.py
   urlpatterns = patterns(
'',
       url(r'^articles/$', include(articles.urls), namespace="articles"),
   )
   # articles/urls.py
   urlpatterns = patterns(
       '',
       url(r'^$', ArticlesIndex.as_view(), name='index'),
       url(r'^(?P<slug>\w+)/$', ArticleView.as_view(), name='article'),
)  
```  

Notice the 'index' pattern that will show an article index in case a user climbs up from a particular article.  

## RESTful URLs
In 2000, Roy Fielding introduced the term Representational state transfer (REST) in his doctoral dissertation. Reading his thesis (http://www.ics.uci.edu/~fielding/ pubs/dissertation/top.htm) is highly recommended to better understand the architecture of the web itself. It can help you write better web applications that do not violate the core constraints of the architecture.  

One of the key insights is that a URI is an identifier to a resource. A resource can be anything, such as an article, a user, or a collection of resources, such as events. Generally speaking, resources are nouns.  

The web provides you with some fundamental HTTP verbs to manipulate resources: GET, POST, PUT, PATCH, and DELETE. Note that these are not part of the URL itself. Hence, if you use a verb in the URL to manipulate a resource, it is a bad practice.  

For example, the following URL is considered bad:  

```
http://site.com/articles/submit/  
```  

Instead, you should remove the verb and use the POST action to this URL:  

```
http://site.com/articles/  
```  

>### Best Practice
Keep verbs out of your URLs if HTTP verbs can be used instead.  

Note that it is not wrong to use verbs in a URL. The search URL for your site can have the verb 'search' as follows, since it is not associated with one resource as per REST:  

```
http://site.com/search/?q=needle  
```  

RESTful URLs are very useful for designing CRUD interfaces. There is almost a one-to-one mapping between the Create, Read, Update, and Delete database operations and the HTTP verbs.  

Note that the RESTful URL style is complimentary to the departmental store URL style. Most sites mix both the styles. They are separated for clarity and better understanding.  

### 下载练习代码
You can download the example code fies for all Packt books you have purchasedfrom your account at http://www.packtpub.com. If you purchased this bookelsewhere, you can visit http://www.packtpub. com/support and register tohave the fies e-mailed directly to you. Pull requests and bug reports to the SuperBook project can be sent to https://github.com/DjangoPatternsBook/superbook.  

## 总结  
Views are an extremely powerful part of the MVC architecture in Django. Over time, class-based views have proven to be more flexible and reusable compared to traditional function-based views. Mixins are the best examples of this reusability.  

Django has an extremely flexible URL dispatch system. Crafting good URLs takes into account several aspects. Well-designed URLs are appreciated by users too. 
In the next chapter, we will take a look at Django's templating language and how best to leverage it.  

--------------------
© Creative Commons BY-NC-ND 3.0   |   [我要订阅](https://github.com/cundi/Django-Design-Patterns-and-Best-Practices/subscription)   |   [我要捐助](https://github.com/cundi/Web.Development.with.Django.Cookbook/issues/3)
