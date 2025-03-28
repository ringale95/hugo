+++
date = '2025-02-21T16:51:24-05:00'
draft = true
title = 'OOPS revision'
+++

## OOPS

Create JAVA file with name as public class name. If there are two classes in one file remember this!

- In Java, the filename must match the public class name.
- If a file contains multiple classes, only one class can be public.
- If you keep public class Main, the filename must be Main.java.



JVM: runs java application at run time and calls the main method in java code.

.java ->(compile) .class  -> JVM memory(method, heap, stack, PC registers)

Class loader generates binary files from class file and save it in method area(class structure(constructors, methods, fields), static variables, interfaces, constant pools).

JVM memory is divided into :
- Method area (Stores class metadata, static variables, constant pool)
- Stack (Stores local variables, method calls, reference variables)
- Heap (Stores objects, instance variables)


Objects is an entity that has states and behavior. Using objects we can pass messages to each other.
State tells us how object looks and behavior tells us what it does.

Instantiating a class means creating an object.


`Class is a template from which objects are created.`
Classes define states as instance variables and behaviors as instance methods.


## Constructors in java are :
- Default
- Parameterized
- Copy
    (Pass object in constructor)


    A constructor can be a private to restrict creating objects

- Constructor chaining within same class:
```
public class Person {
    private String name;
    private int age;

    // Constructor with all parameters
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Constructor with default age
    public Person(String name) {
        this(name, 30); // Calling the constructor with two parameters
    }

    // Default constructor
    public Person() {
        this("Unknown"); // Calling the constructor with one parameter
    }

    @Override
    public String toString() {
        return "Name: " + name + ", Age: " + age;
    }

    public static void main(String[] args) {
        Person person1 = new Person("Alice", 25);
        Person person2 = new Person("Bob");
        Person person3 = new Person();

        System.out.println(person1);
        System.out.println(person2);
        System.out.println(person3);
    }
}
```

## Encapsulation:
Wrapping up of variable and methods into single unit(class). Use private variables and provide getter and setter methods for controlled access.

## Inheritance
Inheritance is a mechanism where a child class inherits the properties and behavior of a parent class. Establish parent child relationships.
Single Inheritance: One child class inherits from one parent class.

Multilevel Inheritance: A class inherits from another class, which itself is a child of another class.

Hierarchical Inheritance: Multiple classes inherit from the same parent class.

Multiple Inheritance (via Interfaces): Java does not support multiple inheritance with classes, but interfaces can achieve it.

## Polymorphism

Means "many forms" and allow same method to behave differently based on objects that calls it.
Two types:
- Method overloading (compile time polymorphism) :Same method name with different parameter lists.
- Method overriding (runtime polymorphism) :A method in a subclass provides a specific implementation of a method defined in the parent class. Uses `@Override` annotation.

## Abstraction:
Process of `hiding implementation details` and `show necessary functionalities`. Reduce code complexity and increase reusability

What is abstract class?
- A class that cannot be instantiated and have abstract methods.(Method without a body)
- Can have concrete method with implmenetation as well.
- We use `@override` to overrride the abstract method

## Interface:
- Contact that classess must follow.
- All methods are abstract
- support multiple inheritance

We use `abstract` keyword to make a class or method abstract
```
abstract class Shape {
    abstract double calculateArea(); 
}
```

## What is difference between interfaces and abstract class?
- Methods:
  - I : only abstract method. Uses `implements`
  - A : Both abstract and concrete methods. USES `extends`

- Variables:
  - I : Only public, static, final variables
  - A : Have instance variables

- Constructors:
  - I : Cannot have constructors
  - A : Can have constructors.

- Access Modifiers:
  - I :Always public
  - A: Methods are private, protected, public

- Multiple Inheritance:
  - I : Supported
  - A : Not supported

- When to use?
  - I : When differenct classes need to have or must follow a common contract
  - A : When there is a common behavior to share

- Objects:
  - I : No object creation
  - A : No object creation