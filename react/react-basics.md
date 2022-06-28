# React Basics

React is a front-end library (server-side stuff is not needed) that make easier to compose large apps by making reusable Components which encapsule HTML and logic into classes or functions.

That Components are written using a JS syntax extension called JSX, which is transpiled to Vanilla JS by Babel.

You can add React to a website by doing [this](https://reactjs.org/docs/add-react-to-a-website.html).&#x20;

{% embed url="https://reactjs.org/" %}
ReactJS Documentation
{% endembed %}

### Create React App

CRA is an utility script that:

* Creates a skeleton React project.
* Set it up to run JS files through Babel automatically.
* Lets us use super-modern JS features.
* Make testing & depolyment easier.

CRA is built on top of Webpack, a JS utility that :&#x20;

* Enable module importing/exporting.
* Package up all CSS/images/JS into a single file to reduce HTTP requests for performance.
* Allow hot reload when you change a source file (only reload relevant files).

#### CRA Installation

```bash
# 1. Download and install nodejs (https://nodejs.org)

# 2. Check installation was successful
> node -v
> npm -v
> npx -v

# 3. Create a brand new React App
> npx create-react-app my_app
> cd my_app
> npm start
```

{% hint style="info" %}
If you've previously installed `create-react-app` globally via `npm install -g create-react-app`, we recommend you uninstall the package using `npm uninstall -g create-react-app` or `yarn global remove create-react-app` to ensure that `npx` always uses the latest version.
{% endhint %}

{% embed url="https://create-react-app.dev/" %}
Create React App Documentation
{% endembed %}

### React Conventions

#### Top-Level Component should be named App

* App acts as an entry point, and as a container for all other components.

#### Use index.js to render \<App />

{% code title="index.js" %}
```jsx
import React from 'react'; 
import ReactDOM from 'react-dom/client'; 
import './index.css'; 
import App from './App'; 

const root = ReactDOM.createRoot(document.getElementById('root')); 
root.render( 
    <React.StrictMode> 
        <App />
    </React.StrictMode> 
    );
```
{% endcode %}

#### Component Conventions

* One component per file
* Component name as filename : Eg. (Car.js for Car Component)
* Component style as Component name: Eg. (Car.css for Car Component)
* Components extends Component (imported from React)
* Export the Component as default object

{% code title="Example.js" %}
```jsx
// Import React for give context to an unknown code reader.
import React, {Component} from 'react';

// CRA will automatically combine all Components CSS in a single file
import './Example.css'; 

class Example extends Component { 

    render() {
        return (
            <div className="Example"> 
                <p className="Example-title"></p>
                <p className="Example-subtitle"></p>            
            </div>
        }
    }

export default Example;
```
{% endcode %}

### React Core Concepts

```jsx
// Some code
```

#### Component

* A component is a React building block.&#x20;
* It combines logic (JS) and presentation (JSX).

#### Props

* Props make components reusable and customizable.
* Props are only passed from parent components to child components.&#x20;
* Props are immutable (read-only) data. A component is not allowed to change its own props values.
* Default values for props can be setted.

It



#### State

