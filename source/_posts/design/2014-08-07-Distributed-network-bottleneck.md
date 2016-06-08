---
layout: post
title: "[Design] Distributed Network Bottleneck"
comments: true
category: Design

---

## Question

[link](http://www.mitbbs.com/article_t/JobHunting/32702821.html)

> 一个distributed的环境，有很多机器，现在你发现性能有问题，可能是网络带宽造成的，你怎么解决？ (你不能更换网络设备的前提下)

### Answer

1. Identify problem 

首先得判定是否真的是网络造成的，就算是网络问题，哪些机器之间的网络问题？ 这个得先大概了解high level component dependency relationship，

看看是不是cpu memory disk都没有问题。 可以profile几个机器看看是不是 a lot of time spent waiting for network calls.

2. Locate the faulty component

判定是网络问题之后看是哪些components之间，或是某个component里面有很多网络通讯。

3. Improvement

不能更换设备的话，能不能改network topology来让critical path machine之间的带宽有改善。

要是不能改topology就只能改程序了。还是先identify top offender,然后就只能慢慢改了

4. What's more

要还有时间的话就可以聊聊问啥不能换设备，是资金问题还是用的已经是top of the line了？

或者是在public cloud上？

Answer suggested by user __remus__. 
