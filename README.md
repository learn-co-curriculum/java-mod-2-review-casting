# Review Type Casting

## Learning Goals

- Review Typecasting with Inheritance

## Introduction

We have already seen in the last module how type casting works on between
primitive variables and introduced their corresponding wrapper classes. Now
let us focus on type casting objects!

## Type Casting in Java

Consider the animal hierarchy from the last lesson:

![Animal Hierarchy](https://curriculum-content.s3.amazonaws.com/java-mod-2/review-casting/Animal-Inheritance.png)

As we saw in the last lesson, we have the `Animal` class acting as the parent
class with two classes extending it: the `Cat` class and the `Parrot` class.
We will use this hierarchy an example to show how downcasting and upcasting
work with these objects.

### Upcasting or Widening

As we recall, widening or upcasting is like taking the contents from a smaller
box and placing them in a larger box - we know all the contents will definitely
fit because they originally fit in a smaller box.

When we declare a variable of type `Animal`:

```java
Animal myAnimal;
```

We can assign it an `Animal` value:

```java
myAnimal = new Animal();
```

Or we can assign it a `Cat` or a `Parrot` value because both cats and parrots
are considered animals. We can be confident that anything an `Animal` object
would need will be part of the definition of `Cat` or a `Parrot` object:

```java
myAnimal = new Cat();
```

Note, however, that in this case the `myAnimal` variable is still considered to
be of type `Animal`, so the variables and methods that are part of the `Cat`
type are not accessible using the `myAnimal` variable.

This is a prime example of upcasting and is a valid promotion. Java considers
this type of casting a "safe operation", i.e. it can never fail, because the
`Animal` holds fewer properties and methods than the `Cat` class since the
`Cat` extends the `Animal` class.

### Downcasting or Narrowing

The reverse, or downcasting (also known as narrowing) is not always a "safe
operation." We can think about it like this: every cat is an animal, but not
every animal is a cat. The latter is what we are dealing with when we attempt to
downcast an object.

We have to make sure that the object we are downcasting is compatible with the
variable we are trying to assign it to. One quick check we could perform is by
using the `instanceof` operator. The `instanceof` operator checks to see whether
an object is an instance of a particular class or not and will return a boolean
value. If it evaluates to true, then the object is an instance of the class.

```java
Animal myAnimal = new Cat();

if (myAnimal instanceof Cat) {
    System.out.println("I'm a cat!");
} else if (myAnimal instanceof Animal) {
    System.out.println("I'm an animal!");
} else {
    System.out.println("I'm something else!");
}
```

This produces the following output:

```plaintext
I'm a cat!
```

As we can see, `myAnimal` object is an object of type `Cat`, not of type
`Animal` That's because there is a difference between the type at compile-time
and the type at runtime. At compile time, meaning when the code was written, the
type of the `myAnimal` variable was defined as `Animal`. However, when the
program runs, a `Cat` data type is assigned to `myAnimal` variable instead. So
the runtime type of `myAnimal` is `Cat` and this is valid through upcasting, as
we saw above.

In order to downcast, we will need to explicitly cast the object
like this:

```java
Animal myAnimal = new Cat();
Cat myCat = (Cat)myAnimal;
```

Note that the example above will compile and run because the runtime type of
`myAnimal` is `Cat`, which is compatible with the `myCat` variable. In other
words, in this case, the animal really was a cat!

But if we were to do something like this:

```java
Animal myAnimal = new Animal();
Cat myCat = (Cat)myAnimal;    // This will throw an exception
```

We would get a `ClassCastException` thrown at the code above. As we already
saw, the `myAnimal` variable evaluates to a `Cat` object at runtime. So to
cast an `Animal` as a `Cat` would make no sense to Java because the `myAnimal`
object does not have enough information in it to give to the `myCat` instance.
