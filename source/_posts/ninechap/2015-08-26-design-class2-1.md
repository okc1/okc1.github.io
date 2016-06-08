---
layout: post
title: "[NineChap System Design] Class 2.1: Database "
comments: true
category: NineChap

---

# Overview

This class covers database design: 

1. design data with class and inheritance
1. design a user system (Netflix 2015)
1. design a payment system (Yelp, BigCommerce 2015)

# Question 1

__design account (login/out) system__ for our radio app. 

## Step one, scenario

1. register, update, remove account
1. login/out
1. user balance, VIP services

## Step Two, necessary

1. Ask
	
	1. total user: 100 million
	1. daily user: 1 million
	
1. predict

	1. daily active user in 3 month: 10 million
	1. register percentage: 1%
	1. daily new register: 100 thousand

1. more predict

	1. login percentage: 15%
	1. average login frequency: 1.2 (ppl may input wrong password 20% of time)
	1. daily login attempts: 10 million * 15% * 1.2 = 1.8 million
	1. average login frequency: 1.8 million / 24hr = 21 login/sec
	1. normal login frequency: 21 * 2 = 42 login/sec
	1. peak login frequency: 42 * 3 = 126 login/sec

## Step Three, Application

{% img middle /assets/images/design-class2-app-design.png %}

## Step Four, Kilobit

Data - User table should contain name and password. What else? 

    class User {
        int userId; (primary key)
        String name;
        String password;
    }

Data - User Table

    class UserTable {
        list<User> table;

        public insert(){}
        public delete(User){}
        public update(User){}
        public User select(){}
    }

> __[CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)__, (Sometimes called SCRUD with an "S" for Search) are the four basic functions of persistent storage.

# Question 2

__verification and forbidden accounts__

We have to know the concept of __Account State Lifecycle Graph__:

{% img middle /assets/images/design-class2-account-life-cycle.png %}

1. ban: fake user, advertising users... bannned by the management

1. inactive: user choose to suspend his own account, voluntarily.

1. delete account: normally we won't remove all related data (just make userId as "deleted"). Otherwise a lot of data can be violated. All your chatting history __actually remains__. 

## redesign User Table

Old User table:

    class User {
        int userId; (primary key)
        String name;
        String password;
    }

Modified User table:

    class User {
        int userId;
        char name[10];
        char hiddenPassword[10];
        int state;
    }

1. We added state, to support Account life cycle. 

1. We changed username to fixed size, for better performance on searching and storing. Can prevent certain attacks, too. 

1. save encrypted password. 

# Question 3

__design login/out process__

1. User account auto logged out after a certain period of time.
1. multiple account logged in at same time.

{% img middle /assets/images/design-class2-session-life-cycle.png %}

## Session

__Session is a conversation__ between user and server. 

1. User can have >1 session, if he log in from different devices.
1. Session must be verified, thus we have to keep __sessionId__.

Session status: "iPad online", "PC online"...

Modify User table: 

    class User {
        int userId;
        char name[10];
        char hiddenPassword[10];
        int state;
        List<session> sessionList;
    }

Important in Session table:

1. device ID
1. time-out period

    class Session {
        private sessionId;
        int userId;
        
        int deviceCode;
        long timeOut;
    }

User table would include a __session list__. 

## further improvement: session

1. we update sessionList very frequently.
1. size of sessionList is dynamic.

Solution: seperate the table. 

{% img middle /assets/images/design-class2-user-session-table.png %}

Question: When to clean up the session data (considering huge amount of data and frequent calculation)?

> Answer: every end of day. Or store sessions in-memory, so it lose all the data when machine restarts (it is used in Gaming platforms). Or we can clean up one user's session list whenever the user did a new log-in. 
>
> We do not remove session whenever it expires. It's too much calculation. 

## further improvement: inheritance

Apply inheritance to UserTable and SessionTable: 

    class Table {
        list<Row*> table;

        public insert(){}
        public delete(){}
        public update(){}
        public User select(){}
    }

    class UserTable extends Table {
    }
    
    class SessionTable extends Table {
    }

As for the Row class:

    class Row {
        List<Attributes> row;
    }
    
    class User extends Row {
    }
    
    class Session extends Row {
    }

# Question 4

__design search algorithm__

1. find my userId
1. find my userId range

Solution 1: add __HashMap__ in the table. Can do search in O(1), but can't find range. 

Solution 2: __BST data structure__. Can do search range and search in O(log2 n) time. 

## Best solution: B+ tree

__[B+ tree](https://en.wikipedia.org/wiki/B%2B_tree)__ - everything in O(logb n) which is __close to constant time__. 

Plus, B+ tree is hard disk friendly. Read more on a future post. 
