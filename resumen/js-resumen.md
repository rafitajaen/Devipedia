---
description: Resumen conciso de JavaScript
---

# JS Resumen

### Variable declaration



|         |   Scope  | Reassignable |     Mutable    |                      |   |
| ------- | :------: | :----------: | :------------: | -------------------- | - |
| `const` |   block  |     Error    | Objects, Array | TDZ (ReferenceError) |   |
| `let`   |   block  |      Yes     |       Yes      | TDZ (ReferenceError) |   |
| `var`   | function |      Yes     |       Yes      | Hoisting (undefined) |   |

#### **Hoisting**

* `var` declarations are preprocessed before any code executed. It appears that the variable declaration is moved to the top of their scope.
* `var` declaration is hoisted, not its initialization.

{% hint style="warning" %}
TODO: `'use strinct'`
{% endhint %}

### Arrow functions

#### Rest parameters are supported

```javascript
(a, b, ...r) => expression
```

#### Default parameters are supported

```javascript
(a=400, b=20, c) => expression
```

#### Destructuring within params supported

```javascript
([a, b] = [10, 20]) => a + b;  // result is 30
({ a, b } = { a: 10, b: 20 }) => a + b; // result is 30
```

{% hint style="warning" %}
TODO: `this` reference
{% endhint %}

### Function default parameter value

The default parameter is applied in two and only two situations:

* No parameter provided
* `undefined` parameter provided

In other words, if you pass in `null` the default parameter **won't be applied**.

```javascript
const myFunc = (x = 10) => x ;

console.log(myFunc(undefined)) // 10 -- undefined value is provided so default value is assigned to x
console.log(myFunc(null)) // null -- a value (null) is provided, see below for more detailsjav
```

### Destructuring Objects and Arrays

```javascript
const person = {  
    firstName: "Nick",  
    lastName: "Anderson",  
    age: 35,  
    sex: "M"
}

const { firstName: first, age, city = "Paris" } = person; 

console.log(age) // 35 -- A new variable age is created and is equal to person.age
console.log(first) // "Nick" -- A new variable first is created and is equal to person.firstName
console.log(firstName) // ReferenceError -- person.firstName exists BUT the new variable created is named first
console.log(city) // "Paris" -- A new variable city is created and since person.city is undefined, city is equal to the default value provided "Paris".
```

```javascript
const myArray = ["a", "b", "c"];

const [x, y] = myArray; 

console.log(x) // "a"
console.log(y) // "b"
```

### Array methods - map / filter / reduce / find

**Functional programming** (often abbreviated FP) is the process of building software by composing **pure functions**, avoiding **shared state,** **mutable data,** and **side-effects**.

Functional programming is a declarative paradigm, meaning that the program logic is expressed without explicitly describing the flow control.

A **pure function** is a function which:

* Given the same inputs, always returns the same output, and
* Has no side-effects

```javascript
const students = [  
    { name: "Nick", grade: 10 },  
    { name: "John", grade: 15 },  
    { name: "Julia", grade: 19 },  
    { name: "Nathalie", grade: 9 },
];

const aboveTenSum = students  
    .map(student => student.grade) // we map the students array to an array of their grades  
    .filter(grade => grade >= 10) // we filter the grades array to keep those 10 or above  
    .reduce((prev, next) => prev + next, 0); // we sum all the grades 10 or above one by one
    
    console.log(aboveTenSum) // 44 -- 10 (Nick) + 15 (John) + 19 (Julia), Nathalie below 10 is ignored
```

####
