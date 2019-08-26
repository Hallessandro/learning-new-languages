---
layout: post
title: "#8 - JavaScript - Spread and Rest Operators"
author: "Hallessandro D´villa"
categories: programming
tags: [javascript, eS6, ecmascript, spread]
image: coverPosts/spread.png
header-img: "coverPosts/spread.png"
---
Hi guys, today I have a quick tip where I will show you another cool functionality of modern JavaScript, the operators spread and rest. This little guys has been implanted in ES6 and bellow is a description of each one. 

**Rest operator:** Used to merge a list of function arguments into an array:

```javascript
function sortArgs(...args){
  	//args is an array so we can use array methods like sort or map  
    return args.sort();
}
```

If you have a function call sum() and do you want this function sum all of arguments passed as parameter, independent if one or ten arguments are passed, for example you just need make something like this: 

```javascript
function sum(...args){
    let sum = 0;
    for (let arg of args) sum += arg;
    return sum;
}
print(sum(1,3,4)); //8
print(sum(2,2,2,1)); //7
print(sum(1,2,3,4,5,6,7,8,9)); //45
```

> Rest parameter must be at the end, something like **function(a, ..b, c)** don't make sense. 

**Spread operator:** Used to split up array elements or objects properties: 

```javascript
const oldArray = [1,2,3];
const newArray = [...oldArray, 4, 5];
console.log(newArray); //[1,2,3,4,5]

const oldObject = {name: 'Batman', age: '25'};
const newObject = {...oldObject, city:'Gothan'};
console.log(newObject); //{name: 'Batman', age: '25', city:'Gothan'};
```

The spread operator can be used anywhere in the array literal and it can be used multiple times, like this: 

```javascript
let nfcnorth = ['Packers', 'Bears', 'Lions', 'Vikings'];
let nfcsouth = ['Buccaneers', 'Falcons', 'Panthers', 'Saints'];

let nfc = ['49ers', ...nfcnorth, 'Rams', 'Cowboys', ...nfcsouth, 'Eagles', 'Giants'];
console.log(nfc);

```

#### Great uses of the Spread Operator

1. Combine arrays

   ```javascript
   const array = [1,2,3];
   let newArray = [4, 5];
   newArray.push(...array);
   print(newArray); //[4,5,1,2,3];
   ```

   > If you make something like newArray.push(array) the result would be [4,5, [1,2,3]];

2. Copying arrays

   ```javascript
   const array = [1,2,3];
   const newArray = [...array];
   console.log(newArray); //[1,2,3]
   ```

3. Using **Math** Functions

   ```javascript
   let numbers = [8, 20, 15, 2];
   Math.min(...numbers); //1
   ```

4. Combining with Destructuring

   ```javascript
   let { x, y, ...z } = { x: 1, y: 2, w: 3, z: 4 };
   console.log(x); // 1
   console.log(y); // 2
   console.log(z); // { w: 3, z: 4 }
   ```

As I said this would be a quick tip, so this is all folks, until next time! :-D