EventBus
========
###EventBus中文注解。个人对EventBus源码的阅读理解。

* 说明和看法
   * 目前为止对于register, unRegister,  post中涉及到的类和重要方法都做了注释，有很深刻的认识。比如post的线程调度，注册函数是如何通过反射找到的等等流程
   * EventBus一般在用的时候我们一般直接getDefault，其实可以通过EventBusBuilder这个类进行链式操作来构造EventBus实例，具体请自己查看源码。很重要的一个变量就是**ignoreGeneratedIndex**，如果你通过new EventBusBuilder().ignoreGeneratedIndex(true);这个对象来去构造EventBus，那么EventBus不会通过反射去得到注册函数，而是通过编译时期的注解处理器去获得信息。具体代码请查看SubscriberMethodFinder类。
   * 虽然EventBus会默认通过反射获得注册函数，但是获取一次之后会缓存在一个map里面，所以不会每一次都去通过反射去获得注册函数
   * 可以很明显的看到EventBus对于扩展性，框架设计做的一些操作。并且代码简单易懂，不会像系统源码那样一个类就几千行。还是很值得阅读的入门级别的源码。
   
#### 不论是设计模式，还是ThreadLocal，Executor，反射注解的运用，EventBus都是一个很值得阅读的框架源码。

---
EventBus is a publish/subscribe event bus optimized for Android.<br/>
<img src="EventBus-Publish-Subscribe.png" width="500" height="187"/>

EventBus...

 * simplifies the communication between components
    * decouples event senders and receivers
    * performs well with Activities, Fragments, and background threads
    * avoids complex and error-prone dependencies and life cycle issues
 * makes your code simpler
 * is fast
 * is tiny (~50k jar)
 * is proven in practice by apps with 100,000,000+ installs
 * has advanced features like delivery threads, subscriber priorities, etc.

 [![Build Status](https://travis-ci.org/greenrobot/EventBus.svg?branch=master)](https://travis-ci.org/greenrobot/EventBus)

EventBus in 3 steps
-------------------
1. Define events:<br/>
<code>public class MessageEvent { /* Additional fields if needed */ }</code><br/><br/>
2. Prepare subscribers<br/>
Register your subscriber (in your onCreate or in a constructor):<br/>
<code>eventBus.register(this);</code><br/><br/>
Declare your subscribing method:<br/>
<code>@Subscribe</code><br/>
<code>public void onEvent(AnyEventType event) {/* Do something */};</code><br/><br/>
3. Post events:<br/>
<code>eventBus.post(event);</code>

This [getting started guide](http://greenrobot.org/eventbus/documentation/how-to-get-started/) shows these 3 steps in more detail.

Add EventBus to your project
----------------------------
Please ensure that you are using the latest version by [checking here](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.greenrobot%22%20AND%20a%3A%22eventbus%22)

Gradle:
```
    compile 'org.greenrobot:eventbus:3.0.0'
```

Maven:
```
<dependency>
    <groupId>org.greenrobot</groupId>
    <artifactId>eventbus</artifactId>
    <version>3.0.0</version>
</dependency>
```

[Or download EventBus from Maven Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22de.greenrobot%22%20AND%20a%3A%22eventbus%22)

Homepage, Documentation, Links
------------------------------
For more details on EventBus please check [EventBus' website](http://greenrobot.org/eventbus). Here are some direct links you may find useful:

[Features](http://greenrobot.org/eventbus/features/)

[Documentation](http://greenrobot.org/eventbus/documentation/)

[Changelog](http://greenrobot.org/eventbus/changelog/)

[FAQ](http://greenrobot.org/eventbus/documentation/faq/)

How does EventBus compare to other solutions, like Otto from Square? Check this [comparison](COMPARISON.md).

License
-------
Copyright (C) 2012-2016 Markus Junginger, greenrobot (http://greenrobot.org)

EventBus binaries and source code can be used according to the [Apache License, Version 2.0](LICENSE).

More Open Source by greenrobot
==============================
[__greenrobot-common__](https://github.com/greenrobot/greenrobot-common) is a set of utility classes and hash functions for Android & Java projects.

[__greenDAO__](https://github.com/greenrobot/greenDAO) is an ORM optimized for Android: it maps database tables to Java objects and uses code generation for optimal speed.

[Follow us on Google+](https://plus.google.com/b/114381455741141514652/+GreenrobotDe/posts) or check our [homepage](http://greenrobot.org/) to stay up to date.
