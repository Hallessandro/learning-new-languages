---
layout: post
title: "#16 - Meaningful Names - What I Learned With Clean Code"
author: "Hallessandro D´villa"
categories: programming, clean code
tags: [programming, software, agile]
image: coverPosts/meaningful _names.png
header-img: "meaningful _names.png"
---

Hi everyone, I'm back for a new post, this time with something a little different. In this post  we will talk about the chapter "Meaningful Names" of the book [Clean Code](<https://www.amazon.com.br/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882>), write by Robert Cecil Martin also know as Uncle Bob. 

#### Insignificant Names

Names are in everywhere on our development environment, variables, functions, classes and etc. So if names are in everywhere, this means that they are a important thing on our code, and this is right. 

A bad name can make you lose hours, sometime days to solve problems, bad names can lie to you, revealing things that there are no more truths (If it were one day). So the focus of this post is talk about names and what you can do to improve ours names. 

Before we start, for explain how this post is structured,  it is split in topics, with the same name of the book and for every topic I put a sentence by the book and a explanation of the topic. 

#### Using Intention-Revealing Names

> Names  should reveal intent. Choosing god names takes time but saves more than it takes.

> We need to take care with ours names and change them without afraid, when find better ones. 

A good name needs to answer three questions. Why it exists, what it does and how it is used. If a name needs a comment to explain something, then the name does not reveal it's intent, and maybe it's time to change it. 

A string called **n** used to store the name of a city, don't reveal anything. But maybe you can think, that you can put a comment to explain what **n** is it, but instead to put a comment, just change the name for something more meaningful. 

```java
//cityName is a simple but good name
String cityName = "Toronto";
String n = "Vancouver"; //Store the name of a city
```

Check the piece of code above, instead to use a comment to say what the variable store, we can just put this information in the name of the variable. 

About comments I recommend that you read the chapter 4 of Clean Code. Maybe we can talk about this chapter in another post, but read it, it's a great and controversial chapter.

Avoid single letter names, they can only be used as local variable inside very short methods. The rule to use or not single letter names is very simple. The name should correspond to the size of its scope, so if you have a method with two lines, it's ok use a single letter name, but if you have a piece of code with more then ten lines, please avoid this. 

#### Avoid Disinformation

Be careful with your names, avoid leave false clues that will obscure the meaning of something. Abbreviations can be good to write, but is terrible to read the code, so don't be lazy, write good names with useful information.

 A simple example is that you don't should refer a group of books as bookList, unless that the group it's actually a list, if not, the name may lead a developer to false conclusions.

Comments are not the solution here, you don't need a comment, just create names meaningful.  

#### Use Pronounceable Names

> If you can’t pronounce it, you can’t discuss it without sounding like an idiot.

I think that the sentence above explain everything, names are serious thing, so don't write things unpronounceable, don't be cute and most important, if you have a good joke, keep it to the lunch time, don't put it in the code, there's no fun in disinformation. 

#### Use Searchable Names

Serious if you have a method used to save the value of a book, don't call the method as save, unless that your method be the only used to save something in the code. 

If your code works and is used for something, is very likely that in sometime in the future, you or someone else needs to found a specific variable or method inside the code, but if are ten different methods called save, how we will identify which are we looking for? 

If you have a method that save the books name and other that saves the price, called this methods as saveNameOfBook() and savePriceOfBook(), instead of called both as save, when you need to find one or other the names will help a lot. 

#### One Word per Concept

If you have three classes that implements a method called insert used to insert values in a list, when you create a new class and a method that concatenate two values inside a new variable, this method should not be called insert, because in the scope of your project, insert is used to insert values in a list, so insert should be used for concatenate values, choose another name. 

Every name in the code should have a unique meaningful, don't use the same word to do things very different. 

#### Class and Method Names

> **Classes** and objects should have noun or noun phrase names like Customer, WikiPage,
> Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name
> of a class. A class name should not be a verb.

> **Methods** should have verb or verb phrase names like postPayment, deletePage, or save.
> Accessors, mutators, and predicates should be named for their value and prefixed with get,
> set, and is according to the javabean standard.

#### Use Names from Solution and Problem Domain

Don"t use names that are out of context and are not from that specific domain. It's more natural for someone that works in automotive industry to use "engine" instead "power source", so you should not use random names, or names that you like, is very important that a name is related with the domain.

#### Conclusion

Clean Code is a great book, talk by myself, this book changes the way that I works. My intention with this post is to expose some of the good things that I learn when I read Clean Code, but this post is a simplified edition of the chapter, so I recommend that you read the entire chapter (and book, you will not regret). 

If you read and want to talk about something, feel free to send me a message. :-D Bye folks, until next time. 

