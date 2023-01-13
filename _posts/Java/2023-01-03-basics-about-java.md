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



















