---
layout: post
title: Basics about Java
date: 2023-01-03
categories: [Java]
tags: [Java]
---
# Compilation
Why make a class file at all?
* class file has been type checked. Distributed code is safer.
* class files are ‘simpler’ for machine to execute. Distributed code is faster. 
* Minor benefit: Protects your intellectual property. No need to give out source.

<figure align="center">
    <img src = "/assets/images/computer%20science/java_compilation.png">
    <figcaption>figure from <a href="https://docs.google.com/presentation/d/1gEHCa3PLFE3FikAwwO1WhZAXKjWEQ9F1HM9qECoZCUo/edit#slide=id.g5897096ee_059">CS61B</a> 
    </figcaption>
</figure>

<figure align="center">
    <img src = "/assets/images/computer%20science/java_compilation_2.png">
    <figcaption>figure from <a href="https://stackoverflow.com/questions/1326071/is-java-a-compiled-or-an-interpreted-programming-language">Stackoverflow</a> 
    </figcaption>
</figure>

```shell
$ ls
Main.java  Triangle.java
$ javac Triangle.java
$ ls
Main.java  Triangle.class  Triangle.java
$ java Triangle.java
*
**
***
****
*****
```

# Defining and instantiating classes
<figure align="center">
    <img src = "/assets/images/computer%20science/java_class_1.png">
    <figcaption>figure from <a href="https://docs.google.com/presentation/d/1gEHCa3PLFE3FikAwwO1WhZAXKjWEQ9F1HM9qECoZCUo/edit#slide=id.g5849d008c_081">CS61B</a> 
    </figcaption>
</figure>

The constructor `public Dog(int startingWeight)` in Java does the same thing as `def __inti__(self)` in Python.

Roughly speaking: **If the method needs to use “my instance variables”, the method must be non-static. In other words, static methods can’t access “my” instance variables, because there is no “me”**. Unless you get the variables through some instances, like:
```java
public static Dog maxDog(Dog d1, Dog d2) {
	if (d1.weightInPounds > d2.weightInPounds) {
   		return d1;
	}
	return d2;
}
```

You can access class attributes through instances, but it's confusing and not recommended! Always access class attributes through class names and access instance attributes through instances.

In the non-statics methods, you can use keyword `this` which is the same as `self` in Python.
```java
public Dog maxDog(Dog d2){
    if (this.weightInPounds > d2.weightInPounds) {
        return this;
    }else {
        return d2;
    }
}
```
# References
## Class instantiations
When we instantiate an object:
* Java first allocates a box of bits for each instance variables of the class and fills them with a default value
* The constructor then usually fills every such box with some other value
## Reference types
There are 8 primitive types in Java: byte, short, int, long, float, double, boolean, char.

Everything else, including arrays, is a **reference type**.
## Reference type variable declarations
When we declare a variable of any reference type:
* Java allocates exactly a box of size 64 bits, no matter what type of object.
* These bits can be either set to:
  * Null(all zeros)
  * The 64 bit "address" of a specific instance of that class(returned by `new`)

As for arrays:
* Creates a 64 bit box for storing an int array address. (declaration)
* Creates a new Object, in this case an int array. (instantiation)
* Puts the address of this new Object into the 64 bit box named `a`. (assignment)

## The golden rule of equals(GRoE)
Given variables y and x, `y = x` copies all the bits from x into y, no matter primitive types or reference types. If it's reference type, in terms of our visual metaphor, we “copy” the arrow by making the arrow in the `y` box point at the same instance as `x`.

**Passing parameters obeys the same rule**: Simply copy the bits to the new scope.

In the example, below, after `switcheroo`, foobar.x:10 foobar.y: 20 baz.x: 30 baz.y: 40.
```java
public class Foo {
  public int x, y;
  
  public Foo (int x, int y) {
    this.x = x;
    this.y = y;
  }
  public static void switcheroo (Foo a, Foo b) {
    Foo temp = a;
    a = b;
    b = temp;
  }

  public static void main (String[] args) {
    Foo foobar = new Foo(10, 20);
    Foo baz = new Foo(30, 40);
    switcheroo(foobar, baz);   
  }
 }
```
# Class object
## static variables/methods VS instance variables/methods
In the code below, `title`, `library` are instance variables and `Book`, `getTitle` are instance methods, which can not be accessed by class name or static methods. `last` is static variable and `lastBookTitle` is static method, which can be accessed by instance or class name.
```java
class Book {
  public String title;
  public Library library;
  public static Book last = null;
  public Book(String name) {
    title = name;
    last = this;
    library = null;
  }
  public static String lastBookTitle() {
    return last.title;
  }
  public String getTitle() {
    return title;
  }
}

```
## Generics
Java allows us to defer type selection until declaration. 
```java
public class SLList<BleepBlorp> {
   private IntNode sentinel;
   private int size;


   public class IntNode {
      public BleepBlorp item;
      public IntNode next;
      ...
   }

   ...
}


SLList<Integer> s1 = new SLList<>(5);
s1.insertFront(10);
 
SLList<String> s2 = new SLList<>("hi");
s2.insertFront("apple");
```
* In the .java file implementing your data structure, specify your “generic type” only once at the very top of the file.
* In .java files that use your data structure, specify desired type once:
  * Write out desired type during declaration.
  * **Use the empty diamond operator <> during instantiation**.
* When declaring or instantiating your data structure, use the **reference type**.
  * int: Integer 
  * double: Double 
  * char: Character 
  * boolean: Boolean 
  * long: Long
```java
DLList<Double> s1 = new DLList<>(5.3);

double x = 9.3 + 15.2;
s1.insertFront(x);

```
# Arrays

Three valid notations:
* x = new int[3];
* y = new int[]{1, 2, 3, 4, 5};
* int[] z = {9, 10, 11, 12, 13};

Especially, `int[0]` means empty array.
## copy
Two ways to copy arrays:
* Item by item using a loop. 
* Using `arraycopy`. `System.arraycopy(b, 0, x, 3, 2)`. Takes 5 parameters:
  * Source array 
  * Start position in source 
  * Target array 
  * Start position in target 
  * Number to copy 

`arraycopy` is (likely to be) faster, particularly for large arrays. 

## 2D arrays

```java
int[][] matrix;
matrix = new int[4][]; //Creates 1 total array.
matrix = new int[4][4]; //Creates 5 total arrays.


```





# References
1. [CS61B](https://sp21.datastructur.es/)









