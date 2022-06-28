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

{% hint style="warning" %}
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
// 'import React' give context to the code reader.
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
        )
    }
}

export default Example;
```
{% endcode %}

### React Core Concepts

{% code title="Match.jsx" %}
```jsx
// <Match local="Liverpool" visitant="Manchester" />

import React, {Component} from 'react';

class Match extends Component { 
    static defaultProps = {
        local : "Local",
        visitant : "Visitant",
    }
    
     constructor(props) {
        super(props);
        this.state = {
            localCounter: 0,
            visitantCounter: 0,
            isOver: false
        }
        this.localGoal = this.localGoal.bind(this);
        this.visitantGoal = this.visitantGoal.bind(this);
        this.finishMatch = this.finishMatch.bind(this);
    }
    
    localGoal() {
        !this.state.isOver &&
        this.setState(
            (previous) => ( {...previous, localCounter : previous.localCounter + 1 } )
        );
    }
    visitantGoal() {
        !this.state.isOver &&
        this.setState(
            (previous) => ( {...previous, visitantCounter : previous.visitantCounter + 1 } )
        );
    }
    finishMatch() {
        !this.state.isOver &&
        this.setState(
            (previous) => ( {...previous, isOver : true } )
        );
    }
    
    render() {
        return (
            <div className="Match">
                <h1>{this.props.local} - {this.props.visitant}</h1>
                <h2>{this.state.localCounter} - {this.state.visitantCounter}</h2>
                <p> { this.state.isOver ? 'Match Over' : 'Match In Progress' }</p>
                <br />
                <button onClick={this.localGoal} > Local Goal </button>
                <button onClick={this.visitantGoal} > Visitant Goal </button>
                <button onClick={this.finishMatch} > Finish Match </button>
            </div>
        );
    }
}

export default Match.jsx
```
{% endcode %}

```
// Some code
```

#### Component

* A component is a React's building block.&#x20;
* It combines logic (JS) and presentation (JSX).

#### Props

* Props make components reusable and customizable.
* Props are only passed from parent components to child components.&#x20;
* Props are immutable (read-only) data. A component is not allowed to change its own props values.
* Default values for props can be setted.

{% code title="Hello.jsx" %}
```jsx
// <Hello from="Me" to="You" isFriend />

class Hello extends Component { 
    static defaultProps = {
        to : "Ringo",
        from : "John",
        isFriend : false
    }
    
    render() {
        return (
            {
                this.props.isFriend
                    ? <p> Hi this.props.to ! </p>
                    : <p> Hello this.props.to from this.props.from </p> 
            }       
        );
    }
}
```
{% endcode %}

#### State

* It is the internal data of a Component
* That data changes over time.
* It is stored as a Plain Old Javascript Object (POJO) (key/value object)

```jsx
class ClickCounter extends Component {
    constructor(props) {
        super(props);
        this.state = { clicks = 0 };
    }
}
```

{% hint style="info" %}
If a component is stateless you can omit the constructor function.
{% endhint %}

* **this.setState()**
  * It is used to update the component state.
  * It is asynchronous. React controls when the state will actually change for perfonmance reasons because the component needs to be re-rendered.

{% hint style="danger" %}
Don't call this.setState() inside constructor() because Component is not mounted yet.
{% endhint %}

#### Events

* Firing events results in changes of state.
* Every "Browser Event" is represented by a JSX built-in attribute. (Eg. : onClick)
* JSX built-in attributes take Callback Functions as event listeners.
* JSX built-in attributes are written in Camel Case.

```jsx
<button onClick={ e => { console.log(e, 'Clicked') } } > Click Me! </button>
```

### Sugar Syntax for State and EventHandlers

{% hint style="danger" %}
**It is not real JS.** This sugar syntax need some extra configuration in Babel transpilation in order to enable it.&#x20;
{% endhint %}

```jsx
class MatchSugar extends Component {
    state = {
        localCounter: 0,
        visitantCounter: 0,
        isOver: false
    }
    localGoal    = () => {......}
    visitantGoal = () => {......}
    finishMatch  = () => {......}
}
```

### Reserved Keywords in React

You cannot use the following HTML attributes in React:

* class (Instead, you will use className)
* for (Instead, you will use htmlFor)

### Inline CSS in React

Pass a JS Object to style attribute using Camel Case.

{% code title="Box.jsx" %}
```jsx
// <Box favouriteColor="cyan" />

class Box extends Component {
    render() {
        const inlineCSS = {
            color: 'magenta',
            backgroundColor : this.props.favouriteColor,
            fontSize : '15px'
        }
        
        return <p style={inlineCSS}> ... </p> 
    }
}
```
{% endcode %}
