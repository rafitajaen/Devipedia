# Variables: var, const, let

In JavaScript, there are three keywords available to declare a variable, and each has its differences. Those are `var`, `let` and `const`.

**Short explanation**

Variables declared with `const` keyword can't be reassigned, while `let` and `var` can.

I recommend always declaring your variables with `const` by default, but with `let` if it is a variable that you need to _mutate_ or reassign later.

|       | Scope    | Reassignable | Mutable                                                                        | [Temporal Dead Zone](https://github.com/mbeaudru/modern-js-cheatsheet#tdz\_sample) |
| ----- | -------- | ------------ | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| const | Block    | No           | [Yes](https://github.com/mbeaudru/modern-js-cheatsheet#const\_mutable\_sample) | Yes                                                                                |
| let   | Block    | Yes          | Yes                                                                            | Yes                                                                                |
| var   | Function | Yes          | Yes                                                                            | No                                                                                 |

**Sample code**

```
const person = "Nick";
person = "John" // Will raise an error, person can't be reassigned
```

```
let person = "Nick";
person = "John";
console.log(person) // "John", reassignment is allowed with let
```

**Detailed explanation**

The [_scope_](https://github.com/mbeaudru/modern-js-cheatsheet#scope\_def) of a variable roughly means "where is this variable available in the code".

**var**

`var` declared variables are _function scoped_, meaning that when a variable is created in a function, everything in that function can access that variable. Besides, a _function scoped_ variable created in a function can't be accessed outside this function.

I recommend you to picture it as if an _X scoped_ variable meant that this variable was a property of X.

```
function myFunction() {
  var myVar = "Nick";
  console.log(myVar); // "Nick" - myVar is accessible inside the function
}
console.log(myVar); // Throws a ReferenceError, myVar is not accessible outside the function.
```

Still focusing on the variable scope, here is a more subtle example:

```
function myFunction() {
  var myVar = "Nick";
  if (true) {
    var myVar = "John";
    console.log(myVar); // "John"
    // actually, myVar being function scoped, we just erased the previous myVar value "Nick" for "John"
  }
  console.log(myVar); // "John" - see how the instructions in the if block affected this value
}
console.log(myVar); // Throws a ReferenceError, myVar is not accessible outside the function.
```

Besides, _var_ declared variables are moved to the top of the scope at execution. This is what we call [var hoisting](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var\_hoisting).

This portion of code:

```
console.log(myVar) // undefined -- no error raised
var myVar = 2;
```

is understood at execution like:

```
var myVar;
console.log(myVar) // undefined -- no error raised
myVar = 2;
```

**let**

`var` and `let` are about the same, but `let` declared variables

* are _block scoped_
* are **not** accessible before they are assigned
* can't be re-declared in the same scope

Let's see the impact of block-scoping taking our previous example:

```
function myFunction() {
  let myVar = "Nick";
  if (true) {
    let myVar = "John";
    console.log(myVar); // "John"
    // actually, myVar being block scoped, we just created a new variable myVar.
    // this variable is not accessible outside this block and totally independent
    // from the first myVar created !
  }
  console.log(myVar); // "Nick", see how the instructions in the if block DID NOT affect this value
}
console.log(myVar); // Throws a ReferenceError, myVar is not accessible outside the function.
```

Now, what it means for _let_ (and _const_) variables for not being accessible before being assigned:

```
console.log(myVar) // raises a ReferenceError !
let myVar = 2;
```

By contrast with _var_ variables, if you try to read or write on a _let_ or _const_ variable before they are assigned an error will be raised. This phenomenon is often called [_Temporal dead zone_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal\_Dead\_Zone\_and\_errors\_with\_let) or _TDZ_.

> **Note:** Technically, _let_ and _const_ variables declarations are being hoisted too, but not their assignation. Since they're made so that they can't be used before assignation, it intuitively feels like there is no hoisting, but there is. Find out more on this [very detailed explanation here](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified) if you want to know more.

In addition, you can't re-declare a _let_ variable:

```
let myVar = 2;
let myVar = 3; // Raises a SyntaxError
```

**const**

`const` declared variables behave like _let_ variables, but also they can't be reassigned.

To sum it up, _const_ variables:

* are _block scoped_
* are not accessible before being assigned
* can't be re-declared in the same scope
* can't be reassigned

```
const myVar = "Nick";
myVar = "John" // raises an error, reassignment is not allowed
```

```
const myVar = "Nick";
const myVar = "John" // raises an error, re-declaration is not allowed
```

But there is a subtlety : `const` variables are not [**immutable**](https://github.com/mbeaudru/modern-js-cheatsheet#mutation\_def) ! Concretely, it means that _object_ and _array_ `const` declared variables **can** be mutated.

For objects:

```
const person = {
  name: 'Nick'
};
person.name = 'John' // this will work ! person variable is not completely reassigned, but mutated
console.log(person.name) // "John"
person = "Sandra" // raises an error, because reassignment is not allowed with const declared variables
```

For arrays:

```
const person = [];
person.push('John'); // this will work ! person variable is not completely reassigned, but mutated
console.log(person[0]) // "John"
person = ["Nick"] // raises an error, because reassignment is not allowed with const declared variables
```
