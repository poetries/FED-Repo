#后台与服务篇

尽管在最初我也想去写一篇文章来说说后台的发展史，后来想了想还是让我们把它划分成不同的几部分。以便于我们可以更好的说说这些内容，不过相信这是一个好的开始。

##RESTful与服务化

###设计RESTful API

> REST从资源的角度来观察整个网络，分布在各处的资源由URI确定，而客户端的应用通过URI来获取资源的表征。获得这些表征致使这些应用程序转变了其状态。随着不断获取资源的表征，客户端应用不断地在转变着其状态，所谓表征状态转移。

因为我们需要的是一个Machine到Machine沟通的平台，需要设计一个API。而设计一个API来说，RESTful是很不错的一种选择，也是主流的选择。而设计一个RESTful服务，的首要步骤便是设计资源模型。

###资源

互联网上的一切信息都可以看作是一种资源。

HTTP Method | Operation Performed 
------------|---------------------
GET         | Get a resource (Read a resource)
POST        | Create a resource
PUT         | Update a resource
DELETE      | Delete Resource


设计RESTful API是一个有意思的话题。下面是一些常用的RESTful设计原则:

- 组件间交互的可伸缩性
- 接口的通用性
- 组件的独立部署
- 通过中间组件来减少延迟、实施安全策略和封装已有系统

判断是否是 RESTful的约束条件

 - 客户端-服务器分离
 - 无状态
 - 可缓存
 - 多层系统
 - 统一接口
 - 随需代码（可选）
 

##微服务

###微内核

这只是由微服务与传统架构之间对比而引发的一个思考，让我引一些资料来当参考吧.

> 单内核：也称为宏内核。将内核从整体上作为一个大过程实现，并同时运行在一个单独的地址空间。所有的内核服务都在一个地址空间运行，相互之间直接调用函数，简单高效。微内核：功能被划分成独立的过程，过程间通过IPC进行通信。模块化程度高，一个服务失效不会影响另外一个服务。Linux是一个单内核结构，同时又吸收了微内核的优点：模块化设计，支持动态装载内核模块。Linux还避免了微内核设计上的缺陷，让一切都运行在内核态，直接调用函数，无需消息传递。

对就的微内核便是:

>微内核――在微内核中，大部分内核都作为单独的进程在特权状态下运行，他们通过消息传递进行通讯。在典型情况下，每个概念模块都有一个进程。因此，假如在设计中有一个系统调用模块，那么就必然有一个相应的进程来接收系统调用，并和能够执行系统调用的其他进程（或模块）通讯以完成所需任务。

如果读过《操作系统原理》及其相关书籍的人应该很了解这些，对就的我们就可以一目了然地解决我们当前是的微服务的问题。

文章的来源是James Lewis与Martin Fowler写的[Microservices](http://martinfowler.com/articles/microservices.html)。对就于上面的

 - monolithic kernel
 - microkernel

与文中的

 - monolithic services
 - microservices

我们还是将其翻译成``微服务``与``宏服务``。

引起原文中对于微服务的解释:

> 简短地说，微服务架构风格是一种使用一套小服务来开发单个应用的方式途径，每个服务运行在自己的进程中，通过轻量的通讯机制联系，经常是基于HTTP资源API，这些服务基于业务能力构建，能够通过自动化部署方式独立部署，这些服务自己有一些小型集中化管理，可以是使用不同的编程语言编写，正如不同的数据存储技术一样。

原文是:

> In short, the microservice architectural style [1] is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery. There is a bare mininum of centralized management of these services, which may be written in different programming languages and use different data storage technologies.

而关于微服务的提出是早在2011年的5月份

> The term "microservice" was discussed at a workshop of software architects near Venice in May, 2011 to describe what the participants saw as a common architectural style that many of them had been recently exploring.

简单地与微内核作一些对比。微内核，**微内核部分经常只但是是个消息转发站**，而微服务从某种意义上也是如此，他们都有着下面的优点。

 - 有助于实现模块间的隔离
 - 在不影响系统其他部分的情况下，用更高效的实现代替现有文档系统模块的工作将会更加容易。

对于微服务来说

 - 每个服务本身都是很简单的
 - 对于每个服务，我们可以选择最好和最合适的工具来开发
 - 系统本质上是松耦合的
 - 不同的团队可以工作在不同的服务中
 - 可以持续发布，而其他部分还是稳定的


从某种意义上来说微服务更适合于大型企业架构，而不是一般的应用，对于一般的应用来说他们的都在同一台主机上。无力于支付更多的系统开销，于是如**微服务不是免费的午餐**一文所说

 - 微服务带来很多的开销操作
 - 大量的DevOps技能要求
 - 隐式接口
 - 重复努力
 - 分布式系统的复杂性
 - 异步性是困难的！
 - 可测试性挑战

因而不得不再后面补充一些所知的额外的东西。

针对于同样的话题，开始了解其中的一些问题。当敏捷的思想贯穿于开发过程时，我们不得不面对持续集成与发布这样的问题。我们确实可以在不同的服务下工作，然而当我们需要修改API时，就对我们的集成带来很多的问题。我们需要同时修改两个API！我们也需要同时部署他们！

##混合微服务

在设计所谓的"Next-Generation CMS"，即Echoes CMS的时候，对于我这种懒得自己写Django App的人来说，通过我会去复制别人的代码，于是我继续在Github上漫游。接着找到了DjangoProject.com的源码，又看了看Mezzanine(ps: 我博客用的就是这个CMS)。于是从DjangoProject复制了Blog的代码，从Mezzanine复制了conf的代码，然后就有了Echoes的codebase。然后，继之前的文章(《微服务的小思考》我想了想， 这不就是我想要的模型么?

微服务与Django

Django 应用架构
Django MVC结构如下如示:

![Django MVC](http://repractise.phodal.com/img/backend/django_mvc.png)

然后，记住这张图，忘记上面的MVC，Django实际上是一个MTV

 - Model
 - Template
 - View

主要是Django中的views.py通常是在做Controller的事。

然而对于一个Django的应用来说，他的架构如下所示:

![Django apps architecture](http://repractise.phodal.com/img/backend/django-app.jpg)

Django的每个App就代表着程序的一个功能。每个App有自己的models、views、urls、templates所以对于一个app来说他的结构如下:

```bash
.
|______init__.py
|____models.py
|____tests.py
|____views.py
```

如果是新版的Django那么它的结构如下:

```bash
.
|______init__.py
|____admin.py
|____migrations
| |______init__.py
|____models.py
|____tests.py
|____views.py
```

上面少了templates，最后会有一个总的URL，即第一张图的URL Dispatcher。接着，让我们看看微服务是怎样的。

一个典型的微服务如下所示:

![microservices architecture](http://repractise.phodal.com/img/backend/microservices_a.jpg)

有不同的技术栈python、spring、scala，但是他们看上去和Django应用的图差不多，除了数据库不一样。


与其将复杂的测试、逻辑部分变得不可测，不如把这些部分放置于系统内部。

![Linux OS Hybrid](http://repractise.phodal.com/img/backend/linux_os.jpg)

当我们在我们的服务器上部署微服务的时候，也就意味着实现所以的服务都是在我们系统的内部，我们有一个Kernel以及他们的Kernel Moduels，即微服务群们。他们调用DB，或者某些第三方服务。

System Libraries相当于我们的URL Dispatcher。而我们的URL Dispatcher实际上所做的便是将各自调用的服务指向各自的app。

这样我们即可以解决部署的问题，又可以减少内部耦合。

##其他

> 我猜，微服务的流行是因为程序员可以欢乐地使用自己的语言，哪怕是Logo。


参考

[Microservices - Not A Free Lunch!](http://highscalability.com/blog/2014/4/8/microservices-not-a-free-lunch.html)

[Microservices](http://martinfowler.com/articles/microservices.html)

