---
layout: post
title: "[Question] Junit Hand-on Notes"
comments: true
category: Question

---

## First Word

Junit is open source testing framework developed for unit testing java code. It is now the default framework for testing Java development.

#### Is it popular? 

[A very interesting survey](http://www.takipiblog.com/2013/11/20/we-analyzed-30000-github-projects-here-are-the-top-100-libraries-in-java-js-and-ruby/) shows that JUnit is THE MOST POPULAR LIBRARY FOR JAVA used by 30.7% of projects (it tied with slf4j-api). 

BTW, [Apache Commons](http://en.wikipedia.org/wiki/Apache_Commons) and [Google Guava](http://en.wikipedia.org/wiki/Google_Guava) are the most important common libraries for Java. 

## Unit Test

A unit test is a piece of code that executes a specific functionality in the code. Tests should be written for critical and complex parts of your application (not every single statement). The percentage of code which is tested by unit tests is typically called test coverage.

Unit test is really a coding process, not a testing process. 

In contrast, there is "Manual testing". 

#### Why should we use it? 

1. Test early and often automated testing.

2. Junit tests can be integrated with the build so regression testing can be done at unit level.

3. Test code reusage. 

#### Other kinds of tests?

Integration Test (also called Functional Test) test the behavior of a component or the integration between a set of components. 

Performance tests are used to benchmark software components in a repeatable way 

## TDD

TDD (Test-Driven Development) write unit test before writing the code. It is commonly believed that tests should be written before the code during development cycle. 

[Some believes](http://stackoverflow.com/questions/247086/should-unit-tests-be-written-before-the-code-is-written) that TDD results in less time in the debugger, and more time thinking about outside-in design. [Some also believes](http://sqa.fyicenter.com/FAQ/JUnit/When_Should_Unit_Tests_Should_Be_Written_In_Deve.html) that TDD is more fun than writing tests after the code seems to be working. 

## Junit

In Java, 'assert' is a keyword. So, JUnit 3.7 deprecated assert() and replaced it with assertTrue(). JUnit 4 is compatible with the assert keyword. 

#### Test Class/Suite

Test methods are contained in a class called Test class. JUnit assumes that all test methods can be executed in an arbitrary order (thus no dependency). 

Several test classes can be combined into a test suite. Running a test suite will execute all test classes in the specified order. 

#### Test fixtures 

Fixtures is a fixed state of a set of objects used as a baseline for running tests. It includes:

1. setUp() method which runs before every test invocation.

2. tearDown() method which runs after every test method.

#### "extends TestCase" or @annotation?

JUnit 3-style: create a class that "extends TestCase", and start test methods with the word test. In Eclipse, all methods named "testSomething" are automatically run.

JUnit 4-style: create a 'normal' class and prepend a @Test annotation to the method (name do not have to be "testSomething"). This is [recommended way](http://stackoverflow.com/questions/2635839/junit-confusion-use-extend-testcase-or-test). 

#### Other than normal test

There are: 

1. Expected Exception Test: @Test(expected = ArithmeticException.class)

2. Ignore Test: @Ignore("Not Ready to Run")  

3. Time Test: @Test(timeout = 1000)  

4. Suite Test: @Suite.SuiteClasses({ JunitTest1.class, JunitTest2.class })

5. Parameterized Test: read below

Junit 4 has introduced a new feature Parameterized tests. Parameterized tests allow developer to run the same test many times using different values (passed in as a collecetion). One [good example](http://www.mkyong.com/unittest/junit-4-tutorial-6-parameterized-test/). 

## Miscellaneous

Q: What happens if a JUnit Test Method is Declared as "private"?

A: If a JUnit test method is declared as "private", it compiles successfully. But the execution will fail. This is because JUnit requires that all test methods must be declared as "public".

Q: How do you test a "protected" method?

<table border="1" summary="This table defines levels of access conferred by a modifier">
<caption style="font-weight: bold" id="accesscontrol-levels">Access Levels</caption>
<tbody><tr>
<th id="h1" class="bg-color bg-img font-color">Modifier</th>
<th id="h2" class="bg-color bg-img font-color">Class</th>
<th id="h3" class="bg-color bg-img font-color">Package</th>
<th id="h4" class="bg-color bg-img font-color">Subclass</th>
<th id="h5" class="bg-color bg-img font-color">World</th>
</tr>
<tr>
<td headers="h1" class="bg-color bg-img font-color"><code>public</code></td>
<td headers="h2" class="bg-color bg-img font-color">Y</td>
<td headers="h3" class="bg-color bg-img font-color">Y</td>
<td headers="h4" class="bg-color bg-img font-color">Y</td>
<td headers="h5" class="bg-color bg-img font-color">Y</td>
</tr>
<tr>
<td headers="h1" class="bg-color bg-img font-color"><code>protected</code></td>
<td headers="h2" class="bg-color bg-img font-color">Y</td>
<td headers="h3" class="bg-color bg-img font-color">Y</td>
<td headers="h4" class="bg-color bg-img font-color">Y</td>
<td headers="h5" class="bg-color bg-img font-color">N</td>
</tr>
<tr>
<td headers="h1" style="font-style: italic" class="bg-color bg-img font-color">no modifier</td>
<td headers="h2" class="bg-color bg-img font-color">Y</td>
<td headers="h3" class="bg-color bg-img font-color">Y</td>
<td headers="h4" class="bg-color bg-img font-color">N</td>
<td headers="h5" class="bg-color bg-img font-color">N</td>
</tr>
<tr>
<td headers="h1" class="bg-color bg-img font-color"><code>private</code></td>
<td headers="h2" class="bg-color bg-img font-color">Y</td>
<td headers="h3" class="bg-color bg-img font-color">N</td>
<td headers="h4" class="bg-color bg-img font-color">N</td>
<td headers="h5" class="bg-color bg-img font-color">N</td>
</tr>
</tbody></table>

A: When a method is declared as "protected", it can only be accessed within the same package where the class is defined. Hence to test a "protected" method, define test class in the same package.

## Things that I don't understand

Q: [How do I test things that must be run in a J2EE container](http://www.tutorialspoint.com/junit/junit_interview_questions.htm) (e.g. servlets, EJBs)?

A: Refactoring J2EE components to delegate functionality to other objects that don't have to be run in a J2EE container will improve the design and testability of the software. Cactus is an open source JUnit extension that can be used for unit testing server-side java code.

Q: What are Parameterized tests in JUnit?

A: Parameterized tests allow developer to run the same test over and over again using different values.
