---
layout: post
title: "#12 - A Brief Introduction of Strings in Python"
author: "Hallessandro D´villa"
categories: programming
tags: [python, strings]
image: coverPosts/str_python.png
header-img: "coverPosts/str_python.png"
---
Hey guys, today I will talk about how to use strings In Python, and some useful methods available. Strings in python are exactly equal a strings in other languages like Java or Javascript, a sequence of one or more characters. 

Strings can be created within either single quotes ' or double quotes " in Python, so to create a string, enclose a sequence of characters in one or the other, like this: 

```python
​"This is a string in double quotes." 
'This is a string in single quotes.'
```

For print the value of a string, just use the print() function, like this: 

```python
print("This is a string") Output: This is a string
```

### STRING CONCATENATION

Concatenation means joining strings together end-to-end to create a new string. In Python to concatenate strings, we use the + operator. The + operator is used for sum the values of two or more numbers, but when used with strings, this guy concatenate the value of the strings, like this: 

```python
string1 = "Hello" 
string2 = "world" 
print(string1 + string2) 
Output: Hello world
```

Note; The + operator not be used with two different data types, we can’t concatenate strings and integers for example, if you try something like this: 

```python
print(“Jose” + 51)
```

The following error will be receive: 

```python
TypeError: Can't convert 'int' object to str implicitly.
```

If you want to create the string “Jose51”, you could this by putting the number 51 in quotes, or using the function str(), like this: 

```python
my_str = "Jose"  
age = 51 
print(my_str + str(age)) 
Output: Jose51
```

You can concatenate how many strings you want, but your code will not be very readable with too many concatenations, so use sparingly.

### STRING REPLICATION

If you need print a same string several times, you can easily do this with the * operator. Like the + operator, the * operator has a different use when used with numbers. Let’s print “Go Packers “ 5 times, without typing this 9 times or using CTRL C + CTRL V. 

```python
print("Go Packers " * 5) 
Output: Go Packers Go Packers Go Packers Go Packers Go Packers
```

### USING STRING FORMATTERS

In the string class, Python has a very useful method called str.format(), this guy allows you to do variable substitutions and value formatting. This let’s you concatenate elements together within a string through positional formatting. 

Formatters work by putting a pair of curly braces {} into a string and calling the str.format() method, like this:

```python
print("Jose has {} books.".format(5)) 
Output: Jose has 5 books.
```

Formatters also can be used for multiple placeholders, like this: 

```python
my_str = "Jose has {} oranges and {} apples."  
print(my_str.format(5,3)) 
Output: Jose has 5 oranges and 3 apples.
```

When we leave the curly braces empty without any parameters, Python will replace the values passed through the str.format() in order. The values passed to the str.format() method are essentially a tuple, and each individual value contained in the tuple can be called by your index number. 

```python
my_str = "Jose has {0} oranges and {1} apples."  
print(my_str.format(5,3)) 
Output: Jose has 5 oranges and 3 apples.
```

Knowing the index number, we can change the order the parameters, like this: 

```python
my_str = "Jose has {1} oranges and {0} apples."  
print(my_str.format(5,3)) 
Output: Jose has 3 oranges and 5 apples.
```

### AN OVERVIEW THROUGH ANOTHER USEFUL METHODS

- **find():** Returns the index of first occurrence of a substring passed as parameter:

```python
​my_str = "Hello world" 
print(my_str.find("world")) 
Output: 6
```

- **index():** Returns the index of a substring: 

```python
my_str = "Hello world" 
print(my_str.find("world")) 
Output: 6
```

- **join():** Returns a string in which the string elements of sequence have been joined by str separator:

```python
​s = "-"
seq = ("a", "b", "c")
print s.join( seq ) 
Output: a-b-c
```

- **lower():** Returns a lowercase string: 

```python
my_str = "HELLO"  
print(my_str.lower()) 
Output: hello
```

- **upper():** Returns a uppercase string: 

```python
​my_str = "hello" 
print(my_str.lower()) 
Output: HELLO
```

- **swapcase()**: Swap uppercase strings to lowercase and vice versa: 

```python
​my_str = "hello"
print(my_str.swapcase()) 
Output: HELLO
```

- **rstrip():** This method returns a copy of the string in which all chars have been stripped from the end of the string (default whitespace characters): 

```python
​str = "     this is string example....wow!!!     "
print (str.rstrip()) 
Output: this is string example....wow!!!  
str = "88888888this is string example....wow!!!8888888"
print (str.rstrip('8')) 
Output: 88888888this is string example....wow!!!
```

- **strip():** This method returns a copy of the string in which all chars have been stripped from the beginning and the end of the string:

```python
​str = "0000000this is string example....wow!!!0000000" 
print (str.strip('0')) 
Output: this is string example....wow!!!
```

- **replace():** Returns a copy of the string with all occurrences of substring old replaced by new. If the optional argument max is given, only the first count occurrences are replaced:

```python
str = "this is string example....wow!!! this is really string" 
print (str.replace("is", "was"))
Output: thwas was string example....wow!!! thwas was really string 
print (str.replace("is", "was", 3)) 
Output: thwas was string example....wow!!! thwas is really string
```

- **startswith():** Returns true if found matching string otherwise false:

```python
str = "this is string example....wow!!!" 
print (str.startswith( 'this' )) 
Output: True 
print (str.startswith( 'is', 2, 4 )) 
Output: True 
print (str.startswith( 'this', 2, 4 ))
Output: False```
```

Besides these, there are other methods that are worth your attention, so I recommend taking a look at the [official documentation](https://docs.python.org/2/library/string.html) of the String class.

So, this is all folks, I wish a happy new year for everyone, and soon I will be back with some new post. Thanks for reading!