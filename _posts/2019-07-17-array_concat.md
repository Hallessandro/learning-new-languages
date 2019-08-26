---
layout: post
title: "#17 - Quick Tip - Array.prototype.concat()"
author: "Hallessandro D´villa"
categories: programming, javascript
tags: [programming, javascript, arrays]
image: coverPosts/array_concat.png
header-img: "array_concat.png"
---

Hello everyone, I'm back, this time with a quick tip about how to use the **concat()** method to merge arrays in JavaScript, so no time to waste, let's get started.

The **concat()** method is used to merge one array with another array or element passed as parameter. As others JavaScript methods,**concat()** don't change the original array, but instead returns a new array with all the changes.  Let's see a example: 

```javascript
const firstList = [1,2,3];
const secondList = [4,5,6];

const result = firstList.concat(secondList);
//The result will be equal to [1,2,3,4,5,6]
```
If you pass two or more diferents arrays as parameter to **concat()**, this will works to and the elements will be add in the new array, following the order of the parameters. 

```javascript
const firstArray = [1];
const secondArray = [2,3,4];
const thirdArray = [5,6];

const result = firstArray.concat(secondArray, thirdArray);
//The result will be equal to [1,2,3,4,5,6]
```
We can pass too, single values or more complex elements like objects and these elements don't need to be of the same type, we can concat a array of numbers with strings, there's no problem.
```javascript
const firstArray = [1];
const secondArray = [2,3,4];

const stringNumber = "5";

const objectTest = {"name": "Batman", "super_power": "Money"};

const result = firstArray.concat(secondArray, stringNumber, objectTest);
//The result will be equal to [1,2,3,4,"5",{"name": "Batman", "super_power": "Money"}]
```
And for last, we can merge nested arrays, like this: 

```javascript
const firstArray = [[1]]
const secondArray = [2, 3]
const thirdArray = [4, [5,6,7]]

const result = firstArray.concat(secondArray, thirdArray);
//The result will be equal to [[1], 2, 3, 4, [5,6,7]]
```
We can add a new value to one of the nested arrays, like this: 
```javascript
result[0].push("0"); 
//The result will be equal to [[1, "0"], 2, 3, 4, [5,6,7]]
```
So, this is all for now folks, thanks for reading and see you soon! 