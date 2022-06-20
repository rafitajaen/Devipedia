# Desestructurar objetos y arrays

_Destructuring_ is a convenient way of creating new variables by extracting some values from data stored in objects or arrays.

To name a few use cases, _destructuring_ can be used to destructure function parameters or _this.props_ in React projects for instance.

**Explanation with sample code**

* Object

Let's consider the following object for all the samples:

```
const person = {
  firstName: "Nick",
  lastName: "Anderson",
  age: 35,
  sex: "M"
}
```

Without destructuring

```
const first = person.firstName;
const age = person.age;
const city = person.city || "Paris";
```

With destructuring, all in one line:

```
const { firstName: first, age, city = "Paris" } = person; // That's it !

console.log(age) // 35 -- A new variable age is created and is equal to person.age
console.log(first) // "Nick" -- A new variable first is created and is equal to person.firstName
console.log(firstName) // ReferenceError -- person.firstName exists BUT the new variable created is named first
console.log(city) // "Paris" -- A new variable city is created and since person.city is undefined, city is equal to the default value provided "Paris".
```

**Note :** In `const { age } = person;`, the brackets after _const_ keyword are not used to declare an object nor a block but is the _destructuring_ syntax.

* Function parameters

_Destructuring_ is often used to destructure objects parameters in functions.

Without destructuring

```
function joinFirstLastName(person) {
  const firstName = person.firstName;
  const lastName = person.lastName;
  return firstName + '-' + lastName;
}

joinFirstLastName(person); // "Nick-Anderson"
```

In destructuring the object parameter _person_, we get a more concise function:

```
function joinFirstLastName({ firstName, lastName }) { // we create firstName and lastName variables by destructuring person parameter
  return firstName + '-' + lastName;
}

joinFirstLastName(person); // "Nick-Anderson"
```

Destructuring is even more pleasant to use with [arrow functions](https://github.com/mbeaudru/modern-js-cheatsheet#arrow\_func\_concept):

```
const joinFirstLastName = ({ firstName, lastName }) => firstName + '-' + lastName;

joinFirstLastName(person); // "Nick-Anderson"
```

* Array

Let's consider the following array:

```
const myArray = ["a", "b", "c"];
```

Without destructuring

```
const x = myArray[0];
const y = myArray[1];
```

With destructuring

```
const [x, y] = myArray; // That's it !

console.log(x) // "a"
console.log(y) // "b"
```
