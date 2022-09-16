# Resumen

### Diferencias entre JS y TS

**JavaScript** es un lenguaje interpretado (no necesita compilación). Tipado dinámico (variables pueden cambiar de tipo, y puedes añadir propiedades a objetos).&#x20;

{% hint style="info" %}
JS es un lenguaje orientado a objetos basado en prototipos, en el cual, los objetos no son creados mediante la instanciación de clases, sino mediante la clonación de objetos o mediante la escritura de código por parte del programador. Estos prototipos también se pueden extender.
{% endhint %}

{% hint style="info" %}
ECMAScript es un estándar de JS con la función de asegurar la interoperabilidad de las páginas web entre los diferentes navegadores.
{% endhint %}

**Typescript** es un superset de JS, de tipado estático opcional para evitar errores en el runtime.

Typescript sigue las últimas especificaciones de ECMAScript y añade interfaces, decorators, class member variables (fields), generics, enums, keywords (readonly, public, private, protected)

{% hint style="info" %}
Si reasignas el tipo de una variable en TS obtienes un compile-time error.
{% endhint %}

### Type Annotations

#### Primitive Data Types

| `string`  | `any`     |   |   |
| --------- | --------- | - | - |
| `boolean` | `unknoun` |   |   |
| `number`  | `never`   |   |   |
| `symbol`  | `void`    |   |   |
| `bigint`  |           |   |   |

`bigint` . From ES2020 onwards. Mix numbers and bigint in arithmetic operations is an error because the tow are separate domains.

```typescript
let foo: bigint = BigInt(100); // the BigInt function
let bar: bigint = 100n; // a BigInt literal

foo = bar; // error: Type 'bigint' is not assignable to type 'number'.
bar = foo; // error: Type 'number' is not assignable to type 'bigint'.

console.log(3145 * 10n); // error
console.log(BigInt(3145) * 10n); // okay!
```

`symbol` is a data type that is always unique and immutable. It is used to create unique keys for object properties. Started with ECMAScript 2015.

```typescript
let sym1 = Symbol();
let sym2 = Symbol("key"); // optional description
let sym3 = Symbol("key");

sym2 === sym3; // false, symbols are unique

let obj = {
  [sym1]: "value",
};
console.log(obj[sym1]); // "value"
```

`undefined` for variables that has not been assigned a value. A function that doesn't return a value have a value of undefined.

`null` for intentional absence of value

`never` When a function never ends or return an error.

#### Literal Type

```typescript
let leftAlignment: 'left' = 'left';
```

It's used for variables that will only allow one value. But by _combining_ literals into unions, you can express a much more useful concept - for example, functions that only accept a certain set of known values:

```typescript
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");     // OK
printText("Hello, world", "centre");   // Type-checker Error
```

You can also convert an entire object to be type literals:

```typescript
const req = { url: "https://example.com", method: "GET" } as const;
```

#### Union Type

```typescript
let padding: string | number;
```

### Custom Types

You can create custom types:

* with `type` keyword (custom type and type alias)
* declaring a `class` or an `interface`
* declaring an `enum`

{% hint style="info" %}
**Types** (_Custom Types and Aliases types_) **are not transpiled to JS**.
{% endhint %}

#### Object Literal Notation

```typescript
type Patient = {
name: string;
heigth?: number; // Optional property
}
```

#### Type Guards

`typeof` and `instanceof` are operator to get information about the type of values we have at **RUNTIME**.

{% code title="typeof example" %}
```typescript
let padding: number | string = 2;

console.log(typeof padding) // number
```
{% endcode %}

`instanceof` need a constructor in order to work.

{% code title="instanceof example" %}
```typescript
class Person{
constructor(public name: string) { }
}

let person1: Person;
let person2 = new Person("John");

console.log(person1 instanceof Person) // false. Error.
console.log(person2 instanceof Person) // true
```
{% endcode %}

#### Alias Types

```typescript
type Foot = number; 

let f:Foot = 2;
console.log(typeof f); // number, because it's his runtime value.
```

You can use a type alias to make a shorthand for a type:

```typescript
type GreetingLike = string | (() => string) | MyGreeter;

function greet(g: GreetingLike): void;
```

### `readonly` keyword

We wil use `const` for immutable variables and `readonly` for immutable class properties.

```typescript
class Foo {
readonly double:number; // Explicit declaration of a class property.

constructor(single:number) { // Implicit declaration
    this.double = single*2;
}
```

### Interfaces

An abstract type that tells the compiler which property names a given object can have.

{% hint style="info" %}
**Interfaces are a subset of types.**

Like the types, interfaces are not transpiled to JS.

Unlike the types, interfaces can't be used in union or intersections.
{% endhint %}

### Structural vs Nominal type systems

Nominal = Equal type if names are the same or descendants.

Structural = Equal types if the structure are the same, including access level modifiers ( public, private or protected ) and methods.

