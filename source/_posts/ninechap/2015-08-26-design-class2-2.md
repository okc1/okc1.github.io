---
layout: post
title: "[NineChap System Design] Class 2.2: Database "
comments: true
category: NineChap

---

# Question 5

Continue from last post, now let's __support VIP services__. 

User could buy VIP services using his acccount balance. 

    class ProService {
        int userId;
        double money;
        long endTime;

        public addMoney(){}
        public buyPro(){}
    }

## Q5.1: System crash when purchasing VIP

Solution: __transaction with log__

    WriteLOG
    Transaction_1123: BEGIN
    money=20; endTime=16_07_2016

If system crash happens here, system will read the log, recover and roll back all original data. Try not to complete the transaction - just fail it. 

    WriteLOG
    Transaction_1123: BEGIN
    money=20; endTime=16_07_2016
    WriteLOG
    Transaction_1123: END
    money=10; endTime=16_08_2016

> What happens if system crash during writing the log? or during the rollback?

## Q5.2: dataset contains bad data

1. one user id have 2 corresponding pro-services information.
1. Shallow user: a pro-services info does not have corresponding user. 

Solution: have a checker class.

## Q5.3: simutaneous purchase by 2 users

Solution: lock. 

1. first process lock money & endTime.
1. Read money = 20
1. another process try to lock, but end up waiting (sleeping).
1. first process do the job, and release the lock. 
1. another process wakes up. 

> lock have time-out settings. It can be applied in distributed system as well. 

Question: does lock make your execution slow?

1. If another process is sleeping, CPU will be fully consumed by other process. So it won't impact. 

1. You can do some async processing, too. 

1. When you lock, try to lock only a small piece of code, not the entire method. In DB, lock only a row, not a table. 

1. Java [CAS](https://en.wikipedia.org/wiki/Compare-and-swap) (Compare and swap ) 

## Q5.4: Server crash

Solution: duplication. 

1. How many copies?

    Google did 3. Normally 2 in same data center, and 1 in another location. 
    
    Backup data normally is on another machine. But there's also [RAID](https://en.wikipedia.org/wiki/RAID) (redundant array of independent disks) which:
    
    > combines multiple physical disk drive components into a single logical unit for the purposes of __data redundancy, performance improvement__, or both. 

1. When does the copy happen? 

    Option 1 is __doing everyday nightly__. This is called a 'check point'.
    
    Option 2 is use another server to support __Shadow Redundancy__. All data from Machine 0 will be copied to Machine 1 WHILE it happens. The result is, Machine 1 is identical to Machine 0. If Machine 0 crashes, Machine 1 may be behind less than 1 second. 
    
    The way to duplicate is either re-play all the actions, or to read Machine 0's log and apply the new data. 

1. How to copy?

    User send data to 1 server, and from that server, pipeline. This ensures good usage of server bandwith, and serial transfer of data ensures low latency (several ms). 
    
    It's also possible to do tree-like transfer, but the above method is preferred cuz all machine consume same bandwidth.

1. What is log?

    It is actually 'checkpoint' + log. It allows you to rollback.

Data redundancy - Summary:

{% img middle /assets/images/design-class2-data-redundancy-1.png %}

## Final note: Data inconsistency

Main sources of inconsistency comes from:

1. network fault
1. disk error

The disk eror is solved by __checksum__ (compare during disk writing). 

# Summary

__[ACID](https://en.wikipedia.org/wiki/ACID) (Atomicity, Consistency, Isolation, Durability)__  is a set of properties that guarantee that database transactions are processed reliably. 

1. __Atomicity: all or nothing__

    Q5.1: System crash when purchasing VIP
    
1. __Consistency__: validate according to defined rules

    Q5.2: dataset contains bad data
    
1. __Isolation__: independency between transactions __(lock)__

    Q5.3: simutaneous purchase by 2 users
    
1. __Durability__: stored permanently

    Q5.4: Server crash

{% img middle /assets/images/design-class2-summary.png %}

Additional Questions:

1. design a user system (Netflix 2015)

Hint: table design, register, login/out, password check, find password. 

1. Design payment system (Yelp, BigCommerce 2015)

Hint: the question does not ask about table/ds design itself, but rather the problems associated with payment. Read about ACID principle. 
