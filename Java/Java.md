# Java

***

#### Inheritance

***

Inheritance in java is when one class takes on the properties of another, which allows for hierarchical structuring of code, especially in [OOP](https://en.wikipedia.org/wiki/Object-oriented_programming). When referring to the relationships between classes, there are some important definitions to know.
* A class that inherits another class is a *subclass*
* A class that is inherited from is the *super class*

**Note:**  A *subclass* cannot inherit more than one *super class*, but a *super class* can have unlimited *subclasses*.

![A dog is an animal](https://media.discordapp.net/attachments/940852738546352142/1272809068561563765/image.png?ex=66bc5351&is=66bb01d1&hm=1cb502883221cdbe24d6ed5ece2979a43f1a646368d507892ce1a866eb0fbcc9&=&format=webp&quality=lossless)

In the example above, `Animal` is the *super class* and `Dog` is the *subclass*. All dogs are animals, but not all animals are dogs. Therefore, `Dog` should inherit the properties of the `Animal` class. Let's see how this looks in code.

```java
public class Animal { // This is the super class
    ...
}

public class Dog extends Animal{ // This is the sub class
    ...
}
```

The `extends` keyword is used to represent inheritance in java. So in the example above, we see the class `Dog` "extending", or rather, inheriting the properties of the `Animal` class. When a class inherits another class, it can use the *super class's* `public` methods.

![A dog can do all of what an animal can do.](https://media.discordapp.net/attachments/940852738546352142/1272816238145310810/image.png?ex=66bc59fe&is=66bb087e&hm=e81149ccd92451e50217443f1ae57ef10cfc69775cd481cab832f017506b8259&=&format=webp&quality=lossless)

**Note:** Anything with the `private` keyword cannot be inherited (cannot be accessed from a *subclass*).

If you wish to access `private` fields within the *super class*, you can do so indirectly with *getter* and *setter* methods.

To create a class that cannot be inherited from, we can use the `final` keyword, as demonstrated below:

```java
final class goDawgs { // This class cannot be inherited
    ...
}
```

Attempting to inherit a class with the `final` keyword will produce an error.

##### Overrides

Overriding allows you to rewrite public methods already defined and belonging to a *superclass*.

**Note:** Overriding only works for public, non-static methods. To have a similar effect, you can "hide" the static method.

When overriding a method, it is good practice to include the `@Override` annotation, as demonstrated below.

```java
@Override //Override annotation
public void doStuff () {
    ...
}
```

##### Super
The super keyword is important when referring to inheritance. It can be used to call a method from a *super class* (that has been overridden in the *subclass*). In addition, it can be used to call a constructor from the *super class*.

Looking at this example, the first call of `graduate()` will refer to an overridden method located else where within the class. The `super.graduate()` will call the method located within the *super class* and **NOT** the overridden method.
```java
gradute();
super.graduate(); // Calls the method located within the Super Class.
```

It is the same concept with constructors. Now, if we wanted to call the constructor of a *super class,* we can by using `super()`. This will in turn run the base constructor of the *super class*. To run other constructors, make sure to include the correct argument(s) and the appropriate construct will execute.

**Note:** Constructors are never inherited. To use the constructor of a *super class*, you need to use the aforementioned `super()`.

Additionally, if you do not write a constructor for a *subclass*, java will automatically create a no-parameter constructor which contains `super()`.

##### Polymorphism

When we have multiple different classes related together with inheritance, we can use polymorphism to allow them to interact. This is extremely useful when we want to add functionality to a program without altering the codebase. Furthermore, it allows flexibility with objects of multiple different types. We can define an object with the variable type of a *super class* but the object type of a *subclass*. 

```java
Car mustang = new Ford();
```

When we create variables like this, the only methods available to them are the ones defined in the *super class*. However, any overwritten methods in the *subclass* still have precedence when called. Let's say we have these two classes below.

```java
public class Car { // Super class
    public void startEngine() {
        ...
    }
    
    public void eBreak() {
        ...
    }
}

public class Ford extends Car { // Sub class
    @Override
    public void startEngine() {
        ...
    }
    
    public void selfDrive() {
        ...
    }
}
```

Now, if we run the code below this, we can understand how the scoping of *polymorphism* works.

```java
Car mustang = new Ford(); // Creates a Car object named mustang
mustang.startEngine(); // Calls the overriden method located with the Ford class
mustang.eBreak(); // Calls the method located within the super class
```

Despite mustang being the type `Car` it is assigned the methods of `Ford` that's shared with `Car`. If we try and run the code below, it will cause an error. This is due to the fact that the `selfDrive()` method is never defined in the *super class* `Car`. Therefore, the `Car` variable cannot call that method (despite its definition within `Ford`).

```java
mustang.selfDrive(); // This produces an error
```

We can look at this more abstractly with a chart.

![A dog is an animal](https://cdn.discordapp.com/attachments/940852738546352142/1286787015290912931/image.png?ex=66ef2d4b&is=66eddbcb&hm=50cbf61957736c29ea4253155d66c40995bc06a68058c4b4dfdd6dbaf43034b0&)

If we were to create a variable as such,
```java
Animal toto = new Dog();
```

then `toto` would be able to use the `sleep()` method and the overridden `eat()` method. Our `toto` would not be able to use the `fetchBall()` method.

**Additional information on Inheritance, Polymorphism, and more can be found at the end of this manual.**

#### Inner Classes

***

In *Java*, you can create a class within a class. This allows you to better maintain and structure code with foundational similarities. An additional benefit of inner classes is the ability to access attributes and methods of the outer class.

Creating an inner class is just as simple as creating a regular class and is demonstrated in the code below.

```java
public class Company {
    class CocaCola {
        ...
    }
}
```

**Note:** You can make inner classes private with `private` or static with `static`. Private classes cannot be accessed by outside objects. Static classes can be accessed without having to create an object of the outer class.

An example of a `private` or `protected` class is shown below.

```java
public class Company {
    private class CocaCola {
        ...
    }
}
```

And an example of a `static` class is shown below.

```java
public class Company {
    static class CocaCola {
        ...
    }
}
```

**Additional information on inner classes and more can be found at the end of this manual.**

#### Recursion

***

Recursion is when a method refers to itself within the respective definition.
For Example:

```java
public void toRecurse() {
    toRecurse();
}
```

Within the method declaration `toRecurse` above, it refers to the method `toRecurse` (which is itself).  The purpose of recursion is to break down problems into smaller, more manageable problems.

##### Base Case

Now, you might notice in the last example that there is nothing stopping the recursion from continuing infinitely (or until a `StackOverflowError` is called). To prevent this, we must incorporate a base case. Base cases provide a recursive function the opportunity to stop further recursions.
For Example:

```Java
public int factorial(int n) {
    if (n < = 1) // this is the base case
        return 1;
    else    
        return n*fact(n-1);  
}
```

As `n` gets closer and closer to 1, it is continuing to recurse until it is, or less than, 1. This activates the *base case*, returning one, and going back up the chain of recursive calls. In addition, the `n*fact(n-1)` decreases the value of `n` for the next recursion up until `n <= 1` within the *base case*. This referenced statement is the *recursive call*, and some form modification, of the arguments being passed, that reaches the *base case* is needed.

**Additional information on Recursion, StackOverflowError, and more can be found at the end of this manual.**

### Additional Resources

***
##### Inheritance
* Inheritance: [Java Inheritance](https://www.w3schools.com/java/java_inheritance.asp)
* Inheritance: [Inheritance as a whole](https://www.youtube.com/watch?v=9QIY0fwmKwg)
* Polymorphism: [Polymorphism](https://www.w3schools.com/java/java_polymorphism.asp)
* Polymorphism: [Polymorphism more in Depth](https://www.geeksforgeeks.org/polymorphism-in-java/)

##### Inner Classes
* Inner Classes: [Inner Classes](https://www.w3schools.com/java/java_inner_classes.asp)

##### Recursion
* Recursion: [Recursion in Java](https://www.geeksforgeeks.org/recursion-in-java/)
* StackOverflowError: [The StackOverflowError in Java](https://www.baeldung.com/java-stack-overflow-error)