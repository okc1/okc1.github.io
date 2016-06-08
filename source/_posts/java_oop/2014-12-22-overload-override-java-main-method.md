---
layout: post
title: "[Java OOP] Override/overload Java main method "
comments: true
category: Java OOP

---

### Can we overload main method in Java?

Can. But only __public static void main(String[] args)__ will be used when [your class is launched by the JVM](http://stackoverflow.com/questions/3759315/can-we-overload-the-main-method-in-java). 

You can call other __main() method__ yourself from code. 

Eg.

    class Simple{  
      public static void main(int a){  
      System.out.println(a);  
      }  

      public static void main(String args[]){  
      System.out.println("main() method invoked");  
      main(10);  
      }  
    }

output: 

    main() method invoked
    10

### Can we override main method in Java?

No.

[MAIN is a class method](http://stackoverflow.com/questions/9083876/override-main-method). Hence, it does not makes sense to "override" it (or any static method). The concept of "overriding" is only for instance methods.
