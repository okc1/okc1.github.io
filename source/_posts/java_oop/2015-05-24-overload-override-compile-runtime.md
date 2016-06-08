---
layout: post
title: "[Java OOP] Overload, Override, Compile, Runtime (Static/Dynamic Polymph) "
comments: true
category: Java OOP

---

# The master statement

Overloading is Compile Time and Overriding is Runtime. 

# Examples

## Overloading 

    public static class test
    {
        static void Main(string[] args)
        {
            Foo();
            Foo("test");
        }

        public static void Foo()
        {
            Console.WriteLine("No message supplied");
        }

        public static void Foo(string message)
        {
            Console.WriteLine(message);
        }
    }

This is called __static (compile-time) polymorphism__ because the compiler is aware of exactly which method you are calling. 

## Overriding

When the PrintMessage() function is call, it determines which version of GetMessage() to use at runtime, __based on the type of IMessage__ that is passed in.

    public static class MessagePrinter
    {
        public static void PrintMessage(IMessage message)
        {
            Console.WriteLine(message.GetMessage());
        }
    }

    public interface IMessage
    {
        public string GetMessage();
    }

    public class XMLMessage : IMessage
    {
        public string GetMessage()
        {
            return "This is an XML Message";
        }
    }

    public class SOAPMessage : IMessage
    {
        public string GetMessage()
        {
            return "This is a SOAP Message";
        }
    }

This is __dynamic (runtime) polymorphism__. This is due to the fact that the compiler doesn't necessarily know what type of object is being passed in at compile-time.  

# Conclusion

## Overloading

Compile time Polymorphism = Static Polymorphism = Early binding

## Overriding

Runtime Polymorphism = Dynamic Polymorphism = Late binding = 

Reference: [How Overloading is Compile Time and Overriding is Runtime from stackoverflow.com](http://stackoverflow.com/questions/10915828/how-overloading-is-compile-time-and-overriding-is-runtime)
