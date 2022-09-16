# Ambient Declaration

The declare keyword in TypeScript is used for the Ambient declaration of variables or for methods. Ambient Declarations is like an import keyword. Which tells the compiler that the source exists in another file. We use Ambient declarations in TypeScript for using the third party libraries of JavaScript, jQuery, Node, etc. declare keyword directly integrate these libraries in our code and decrease the chance of error in our TypeScript code.

We use declare keyword only in Ambient file to use the libraries method and variables.

{% code title="Third Party Code" %}
```javascript
var pi_1 = 3.1415926535 ;
var pi_2 = 3.14159265358979323846 ;
var pi_3 = 3.141592653589793238462643383279 ;
```
{% endcode %}

{% code title="Ambient TS file" %}
```typescript
declare var pi_1 : number ;

console.log("Value of pi is :", pi_1)
```
{% endcode %}
