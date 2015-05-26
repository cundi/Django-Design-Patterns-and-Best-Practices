第四章-视图和URL
***************
  
本章，我们会讨论以下话题：  
    
    * 基于类的和基于函数的视图
    * Mixins
    * 装饰器
    * 常见视图模式
    * 设计URL  

##顶层的视图
Django中，视图被定义成可定义的，它接受请求，返回响应。通常它是一个函数或者一个有`as_view()`这样的特殊方法的类。  

这两种情况下，我们创建一个普通的接受`HTTPRequest`作为自己的第一个参数并返回一个`HTTPResponse`的Python函数。`URLConf`也可以对这个函数传递额外的参数。这些参数由URL部分捕捉到，或者是设置了默认值。  

这里有个简单视图的例子：  

    # In views.py
    from django.http import HttpResponse


    def hello_fn(request, name="World"):
        return HttpResponse("Hellp {}!".format(name))

这两行视图函数非常简单和好理解。目前我们还没有用`request`参数来做任何事情。例如，通过查看`GET/POST`参数， URI路径，或者`REMOTE_ADDR`这样的HTTP头部，我们验证请求可以更好地理解所调用视图中的上下文。   

`URLConf`中所对应的行如下：  

    # In urls.py
        url(r'^hello-fn/(?P<name>\w+)/$', views.hello_fn),
        url(r'^hello_fn/$', views.hello_fn),

我们重复使用相同的视图以支持两个URL模式。第一个模式获得了一个name参数。第二个模式没有从URL获得任何参数，这个例子中视图会使用默认的`World`名字。  

##让视图变得更高级
基于类的视图在Django 1.4中被引入。下面是之前的视图在用了同等功能的基于类的视图重写之后的样子：  

    from django.views.generic import View


    class HelloView(View):
        def get(self, request, name="World"):
            return HttpResponse("Hello {}!".format(name))

同样地，对应的`URLConf`也有两行，一如下面命令所示：  

    # In urls.py
        url(r'^hello-cl/(?P<name>\w+)/$', views.HelloView.as_view()),
        url(r'^hello-cl/$', views.HelloView.as_view()),

这个`view`类和我们之前的视图函数之间有多个有趣的不同点。最明显的一点就是我们需要定义一个类。接着，我们明确地定义了我们唯一要处理的`GET`请求。之前的视图对`GET`，`POST`做出了同样的响应，或者其他的HTTP词汇，下面是在Django shell中使用测试客户端：  

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

从安全和可维护性的观察角度来看，还是显式更好一些。  

当你需要定制视图的时候，使用类的好处才会清楚的体现出来。即，你需要改变问候内容。你可以写一个任意类型的普通的视图类，并派生出所指定问候类：  

    class CreetView(View):
        greeting = "Hello {}!"
        default_name = "World"
        def get(self, request, **kwargs):
            name = kwargs.pop("name", self.default_name)
            return HttpResponse(self.greeting.format(name))


    class SuperVillianView(GreetView):
        greeting = "We are the future, {}. Not them."
        default_name = "my friend"

现在，`URLConf`可以引用派生的类：  

    # In urls.py
        url(r'^hello-su/(?<name>\w+)/$', views.SuperVillianView.as_view()),
        url(r'^hello-su/$', views.SuperVillianView.as_view()),

按照类似的方式来定制视图函数不可行时，你需要添加多个有默认值的关键字参数。这样做很快会变得不可控制。这就是为什么通用视图从视图函数迁移到基于类的视图的原因。  

###Django Unchained
After spending 2 weeks hunting for good Django developers, Steve started to think out of the box. Noticing the tremendous success of their recent hackathon, he and Hart organized a Django Unchained contest at S.H.I.M. The rules were simple—build one web application a day. It could be a simple one but you cannot skip a day or break the chain. Whoever creates the longest chain, wins.
The winner—Brad Zanni was a real surprise. Being a traditional designer with hardly any programming background, he had once attended week-long Django training just for kicks. He managed to create an unbroken chain of 21 Django sites, mostly from scratch.
The very next day, Steve scheduled a 10 o' clock meeting with him at his office. Though Brad didn't know it, it was going to be his recruitment interview. At the scheduled time, there was a soft knock and a lean bearded guy in his late twenties stepped in.
As they talked, Brad made no pretense of the fact that he was not
a programmer. In fact, there was no pretense to him at all. Peering through his thick-rimmed glasses with calm blue eyes, he explained that his secret was quite simple—get inspired and then focus.
He used to start each day with a simple wireframe. He would then create an empty Django project with a Twitter bootstrap template. He found Django's generic class-based views a great way to create views with hardly any code. Sometimes, he would use a mixin or two from Django-braces. He also loved the admin interface for adding data on the go.
His favorite project was Labyrinth—a Honeypot disguised as a baseball forum. He even managed to trap a few surveillance bots hunting for vulnerable sites. When Steve explained about the SuperBook project, he was more than happy to accept the offer. The idea of creating an interstellar social network truly fascinated him.
With a little more digging around, Steve was able to find half a dozen more interesting profiles like Brad within S.H.I.M. He learnt that rather that looking outside he should have searched within the organization in the first place.
  
##基于类的通用视图
通常基于类的同样视图为了能更好的重复使用代码，而按照面向对象的方法（模板方法模式）来使用视图实现。我讨厌术语`generic views`。我更乐意把它们叫做`stock view`。就像所储备的照片，你可以按照自己的常见需要对它们做出轻微的调整。  

通用视图的产生是因为Django开发者发现他们在每一个项目中都在重复构建同类型的视图。几乎每个项目都需要有一个页面来显示一个对象的列表（`List View`），或者一个对象的具体内容（`Detail View`），有或者是一个用来创建对象的表单。依照DRY精神，这些可重复使用的视图被Django打包在一起。  

这里给出Django 1.7 中通用视图速查表格：  

|类型 |类名称    |描述                                                         |
|----|:--------|:------------------------------------------------------------:|
