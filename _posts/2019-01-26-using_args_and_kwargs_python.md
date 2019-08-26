---
layout: post
title: "#14 - How to use *args and **kwargs"
author: "Hallessandro D´villa"
categories: programming
tags: [python, functions, list, programming]
image: coverPosts/python.png
header-img: "coverPosts/python.png"
---
Hi guys, my name is Hallessandro, I am a software developer that currently works and live in Brazil, and today in this post let's talk again about Python, this time how to use *args and **kwargs in our Python functions.

Firstly let's create a simple function to sum two numbers: 

```python
def soma(a,b):
    return a + b
.
print(soma(1,3))
```

Our function is simple but works like as expected, when the numbers 1 and 3 are passed as parameters, the result will be 4. But what happens when three numbers are passed as parameters? This happens: 

```python
TypeError: soma() takes exactly 2 arguments (3 given)
```
<img src="../assets/img/memes/pikachu.jpg" alt="drawing" style="width:200px;"/>

We can't pass three numbers for our function, because they just be defined for receive two numbers. So is it, I need create another function to receive and sum three numbers? And for sum four numbers, will be another function? Man, this seens like a lot of dumb code. 

### Using *args

> The asterisk (*) before the word args, it's really important, don't forget it. 

***args** can be used as a parameter to send a non-keyworded variable-length argument list to functions, so if you suspect that you may need more arguments later on, you need use *args instead pass normal arguments, something like this: 

```python
def soma(*args):
    result = 0
    for num in args:
        result += num
    return result

print(soma(1)) #Output: 1
print(soma(1,2)) #Output: 3
print(soma(1,2,3)) #Output: 6
print(soma(1,2,3,4)) #Output: 10
```
***args** it's nothing more than a list, so you can iterate over it and get all the elements values and sum. This way the function can receive 1, 2, 10, 20 or how many arguments do you need, there's no problem, our function now can deal with this. 

### Using **kwargs

**kwargs works like *args, but instead pass a list as argument to a function, a dictionary is used. With **kwargs is possible pass how many arguments you would like. 

Let's see a example of how kwargs work. 

```python
def names_of_chars(**kwargs):
    print(kwargs)

names_of_chars(name1="Sagat", name2="Luigi", name3="Batman")
```

The result of the code above is: 
```python
{'name2': 'Luigi', 'name3': 'Batman', 'name1': 'Sagat'}
```
Because the dictionary data type is unordered, we received the keyvalue pairs in a random order, but it is important to note that a dictionary called **kwargs is created and we can work with it just like we can  work with other dictionaries.

Let's create another program to show one time more how kwargs works. 

```python
def names_of_games(**kwargs):
    for key, value in kwargs.items():
        print("The name of the {} is {}".format(key, value))

names_of_games(game1="Plants vs Zombies", game2="Titanfall 2", game3="Halo 5", game4="God of War", game5="Celeste")

#Output
#The name of the game5 is Celeste
#The name of the game4 is God of War
#The name of the game3 is Halo 5
#The name of the game2 is Titanfall 2
#The name of the game1 is Plants vs Zombies
```
How you can see the kwargs lost the order of elements, but we can pass how many we would like. 

### Using *args and **kwargs in Function Calls

We can also use *args and **kwargs to pass arguments into functions. First, let’s look at an example with *args.

```python
def sum_elements(n1, n2, n3):
    print("The result is {} ".format(n1+n2+n3))

args = (1, 5, 7)
sum_elements(*args)

#Output 
#The result is 13
```
How you can see in the code above, instead pass three arguments to the function sum_elements, we pass just one using the args syntax. It's possible combine the args syntax with named parameters like this: 

```python
def print_elements(value1, value2, value3, value4):
    print("The value is {}.".format(value1))
    print("The value is {}.".format(value2))
    print("The value is {}.".format(value3))
    print("The value is {}.".format(value4))

args = [5, 9]
print_elements(3, 10, *args)  

#Output
#The value is 3.
#The value is 10.
#The value is 5.
#The value is 9.
```
Similarly, kwargs can be used to call a function, let's see a example of how do this: 

```python
def print_kwargs(k1, k2, k3):
    print("Kwarg 1: {}".format(k1))
    print("Kwarg 2: {}".format(k2))
    print("Kwarg 3: {}".format(k3))

kwargs = {"k1":"Sagat", "k2":"Ryu", "k3":"Cammy"}
print_kwargs(**kwargs)

#Output
# Kwarg 1: Sagat
# Kwarg 2: Ryu
# Kwarg 3: Cammy
```
So how you can see when calling a function, we can use *args and **kwargs to pass arguments.

For now this is all folks, thanks for reading and feel free to contact me. 