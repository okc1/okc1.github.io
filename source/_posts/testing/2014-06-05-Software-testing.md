---
layout: post
title: "[Testing] Software Testing"
comments: true
category: Testing

---


## First Word

There are generally four levels of tests: unit testing, integration testing, system testing, and acceptance testing. 

Software testing methods are traditionally divided into white-box and black-box testing. 

One of the testing methodologies is "V-model". 

{% img middle /assets/images/Testing-V-Model.jpg %}

## Testing Types and process

#### Regression testing

There're a lot of types, one of them is called "Regression testing".

Regression testing focuses on finding defects __after a major code change has occurred__. In other words, it encsures that changes does not introduce new faults. 

#### Testing process

Traditional: __waterfall__. Testing is done by independent group of testers after development. This practice often results in the testing phase being used as a project buffer to compensate for project delays. 

New trend: __Agile or Extreme__, which adhere to __TDD Model__. In this process, unit tests are written first. This methodology increases the testing effort done by development.

__Bottom Up Testing__: lowest level components are tested first, then integrated and used to facilitate the testing of higher level components. 

__Top Down Testing__: top integrated modules are tested and the branch of the module is tested step by step until the end.

## Testing Methods

#### Black-box

[Black-box](http://en.wikipedia.org/wiki/Black-box_testing) testing is a method of software testing that examines the functionality of an application without peering into its internal structures or workings. This can be applied to every level of software testing: unit, integration, system and acceptance. 

#### White-box

[White-box](http://en.wikipedia.org/wiki/White-box_testing) testing (also known as structural testing) is a method of testing software that tests internal structures or workings of an application, as opposed to its functionality. In white-box testing, an internal perspective of the system and programming skills are used to design test cases. The tester chooses inputs to exercise paths through the code and determine the appropriate outputs.

#### Other-box

A black-box tester is unaware of the internal structure of the application to be tested, while a white-box tester has access to the internal structure of the application. 

[Gray-box](http://en.wikipedia.org/wiki/Grey_box_testing) testing is a combination of both. Testers require both highlevel and detailed knowledge of the application. 

## Whitebox in detail

Whitebox testing is based on program code. The extent to which source code is executed (covered). 

1. statement coverage
2. path coverage
3. (multiple-) condition coverage
4. decision / branch coverage
5. loop coverage
6. definition-use coverage

Use of "flow graphs" to test the coverage. [source](http://people.cs.aau.dk/~bnielsen/TOV07/lektioner/whitebox-07.pdf)

## Blackbox in detail

1. Equivalence partitioning
2. Boundary value analysis
3. Behavioural testing (interaction with w/ an environment)
4. Random testing (random walk thru the system/mouse click)
5. Stress testing (huge data, DoS attack, power off)
6. Error guessing (Ad hoc, not really a technique)

#### Equivalence partitioning

This is related to "validate" input. First identify input equivalence classes, then make the test case by changing each valid cases into invalid. 

The [testing theory](http://en.wikipedia.org/wiki/Equivalence_partitioning) related to equivalence partitioning says that only one test case of each partition is needed. In other words it is sufficient to select one test case out of each partition to test the program. To use more cases will not find new faults. 

The values within one partition are considered to be "equivalent". Thus the number of test cases can be reduced considerably.

> Example: 
>
> There are 12 months per year 
>
> Valid partition is from january to december
>
> Invalid partition is from <=0 and >=13

A longer but better [example](http://users.csc.calpoly.edu/~jdalbey/205/Resources/grocerystore.html)

#### Boundary Value Analysis

1. Testing boundary conditions (directly on, above, and beneath the edges)
2. Choose input boundary values
3. Choose input boundary values that reaches output boundary (given the input value, choose expected output +/- 1) 

> Example: 
>
> Suppose an integer boundary is 1 to 50, Then test for 0,2 values & 49, 51 vales.
>
> Suppose input = 5, output = 100, then test input = 5, output = 99, 100, 101

Don’t start with designing white-box test cases! Start with black-box test cases, then check white-box coverage. 

[source](http://people.cs.aau.dk/~bnielsen/TOV07/lektioner/blackbox-07.pdf)

#### More examples

__Q: how to test a log-in window__?

A: Eq. class: username empty, exits, don't exist and exceed length limit. Same for password field. Boundary: input length equals, less than or larger than length limit. [source](http://www.geekinterview.com/question_details/23184)

__Q: how to test a vendor machine__?

1. Functional: put in $$ and get a coke

2. Edge condition: put in Chinese RMB?

3. Stress: keep putting $$ and popping goods

4. Security: can you break the machine? 

## Last Word

Sometime it is not feasible to test everything. Instead, prioritize your testing so that you only focus on areas that present the greatest risk or have the greatest probability of occurring. 

For example, you might choose to test the slowest client computer, the busiest server, or the least reliable network link. 

[source](http://technet.microsoft.com/en-us/library/cc782852(v=ws.10).aspx)
