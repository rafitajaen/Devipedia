# JS Concepts for React

### Imports/Exports

{% code title="helpers.js" %}
```javascript
function help() {}
function sing() {}
function sort() {}

// Use 'export default' to export most important function/object in a file.
export default help;
export {sing, hello};
```
{% endcode %}

```javascript
// Import from your codebase ( You need to use: './filename' )
import help, {sing, sort} from './helpers';  

// Import from node_modules ( Directly 'module_name' )
import React, {Components} from 'react';
```

### Conditionals in JSX

```jsx
// Ternary operator for Conditionals
{
    num === 7
        ? <img src="..." />
        : null
}

// Sugar syntax
{ num === 7 && <img src="..." /> }
```
