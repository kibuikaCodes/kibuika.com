---
title: Primitives vs Objects (Value vs Reference)
description: A light look into values and references.
date: 2022-06-26T11:00:00.000Z
---

I'll kick this off with some examples that will act as the base of this article.

```js
const a = 1
const b = 2

a === b // false

const c = 1
const d = 1

c === d // true

const e = [1]
const f = [1]
const g = f

e === f // false
e === [1] // false
g === f // true
```

The comparison of a and b makes sense, right? But for the comparison of e and f, e and [1], g and f, that is where things get interesting. Someone who doesn't know what is actually happening will just say Javascript is weird, but it really isn't.

Javascript provides us with two types of datatypes: Primitives and Objects. Each of this datatype is passed differently to a variable. Primitives are passed by value while Objects are passed by reference.

## Primitives
Primitives are numbers, booleans, strings, symbols and special values like undefined and null

```js
const number = 2;
const boolean = true;
const string = 'Hello World!';
const missingItem = null;
const nothing = undefined;
```

Like I said, primitive values are passed by value. This means that every time you assign a primitive value to a variable, a copy of that value is created. 

```js
let a = 10; 
let b = a;

// mutate b
b = b + 10;

console.log(b) // 20
console.log(a) // 10
```

The very first statement declares a variable ```a``` and initializes it with the number ```1```. The second statement ```let b = a```, declares another variable ```b``` and initializes it with the value of the variable ```a```. Since we are dealing with primitives here, a copy of the number ```1``` is assigned to ```b```.

When we change the the value of ```b```, ```b = b + 10```, we are basically increasing the value of ```b``` by ```10```. Notice the value of ```b``` increases to ```20``` while the value of ```a``` remains the same.

## Objects
Objects are the other category od fata types that Javascript provides us. Objects include: the plain object, arrays, functions, dates, regex, etc. Anything that is not a primitive is an object in js.

```js
const person = {
    name: "Steve"
}

const array = [2, 3, 4, 5]

const functionObj = (a1, a2) => {
    return a1 + a2;
}
```

Unlike primitive values where the value assigned to a variable is the actual copy of that value, objects are assigned by reference. This means that when you declare a variable ```person``` and assign it an object, that object is created in memory and the address of that memory location is assigned to the variable ```person```.

Let's break this down.
```js 
const person = {
    name: "Steve"
}
```
The object ```{name: "Steve"}``` is created in memory and the location of that memory is, let's say ```1234567```, this is the address that points to that location in memory. Ideally this ```address``` is what is "assigned" to the variable ```person```.
So instead of ```person``` holding an actual copy of the onject, it just points to a location in memory where the object has been created.

```person =============> 1234567```
```js
 // address 1234567
 {
    name: "Steve"
 }
 ```

 What happens when we assign a new variable the value of an existing object?

 ```js
 let person = {
    name: "Steve"
 }

 let newPerson = person;

 newPerson.age = 24;

 console.log(person) // {name: "Steve", age: 24}
 console.log(newPerson) // {name: "Steve", age: 24}

 ```

 What tha heck!!. Yes. Remember when we said that ```Objects```(the data type) points to memory locations? This is what is happening. Our object ```{name: "Steve"}``` is created in memory and its address is "assigned" to the variable person. When we declare a new variable ```newPerson``` and assign it the value of ```person```, what we are doing is assigning a reference to the memory location. Basically, both ```person``` and ```newPerson``` are pointing to the same memory location.

 ```person ============> 1234567```
 ```newPerson ===========> 1234567```

 That is why when we add a new property ```age``` with a value of ```24``` to ```newPerson```, this also applies to ```person``` because it is pointing to the same memory location.

 And this is what ```pass by reference``` is all about. We are passing references and not actual values.


 ### Highlights
 - Javascript is not weird
 - Pass by value means an actual copy of that value is assigned to the variable. This happens with ```Primitives``` data types (numbers, strings, boolean, null, undefined)
 - Pass by reference means that the value is created in memory and an address to that memory location is what the variable will "hold". This happens with ```Objects``` data types (object, array, function, date, regex)
