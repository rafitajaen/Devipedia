# React Core Concepts

### Components

* A component is a React's building block.&#x20;
* It combines logic (JS) and presentation (JSX).

### Props

* Props make components reusable and customizable.
* Props are **immutable** (read-only) data. A component is not allowed to change its own props values.
* Props are only passed from parent components to child components. (_Downward data flow pattern_).
* Default props values for missing props can be setted.

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

### State

* It is the internal data of a Component
* That data changes over time.
* It is stored as a Plain Old Javascript Object (POJO) aka (key/value object)

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

#### setState Method

* <mark style="color:red;">`this.setState()`</mark>  is used to update the state of a component.
* It is **asynchronous**. React controls when the state will actually change for performance reasons because the component needs to be re-rendered when it is updated. It's risky to assume previuos call has finished when you call it.

```jsx
/**
* UPDATING PRIMITIVE STATES
**/

// Update state when it's independent from previous state
this.setState( { status: "Connected", isLoading: false } );

// Update state when it's dependant of previous state
this.setState( previous => { counter: previous.counter + 1 } );

/**
* UPDATING MUTABLE DATA STRUCTURES
**/

this.state = {
    todos: [
        { task: "Learn JS", done: false, id: 1 },
        { task: "Code", done: false, id: 2 },
    ]
};

complete(id) {
    const updatedTodos = this.state.todos.map( item => {
                            (item.id === id)
                                ? return {...item, done: true}
                                : return item
                        });
    this.setState( { todos: updatedTodos} );
}


```

#### Types of state should be tracked

* **UI logic**: Changes in the state of interface. (Eg. : isModalOpen, isLoading, etc)
* **Businness logic**: Changes in the state of data. (Eg. : notifications, counters, etc)

{% hint style="danger" %}
Don't call this.setState() inside constructor() because Component is not mounted yet.
{% endhint %}

**State Design**

Minimize to put as little data in your state. If a value doesn't change, it should be a prop instead.

### Events

* Firing events results in changes of state.
* Every "Browser Event" is represented by a JSX built-in attribute. (Eg. : onClick)
* React Events take Callback Functions as event listeners.
* React events are named using camelCase, rather than lowercase

```jsx
<button onClick={ e => { console.log(e, 'Clicked') } } > Click Me! </button>
```

{% embed url="https://reactjs.org/docs/events.html" %}
Full list of React Events
{% endembed %}

#### Events Prevent Default

You cannot return `false` to prevent default behavior in React. You must call `preventDefault` explicitly. For example, with plain HTML, to prevent the default form behavior of submitting, you can write:

```html
<form onsubmit="console.log('You clicked submit.'); return false">
  <button type="submit">Submit</button>
</form>
```

In React, this could instead be:

```jsx
function Form() {
  function handleSubmit(e) {
    e.preventDefault();    
    console.log('You clicked submit.');
  }

  return (
    <form onSubmit={ handleSubmit } >
      <button type="submit" > Submit </button>
    </form>
  );
}
```

Here, `e` is a synthetic event. React defines these synthetic events according to the [W3C spec](https://www.w3.org/TR/DOM-Level-3-Events/), so you don’t need to worry about cross-browser compatibility. React events do not work exactly the same as native events. See the [`SyntheticEvent`](https://reactjs.org/docs/events.html) reference guide to learn more.

### Event Handlers

When using React, you generally don’t need to call `addEventListener` to add listeners to a DOM element after it is created. Instead, just provide a listener when the element is initially rendered.

{% hint style="danger" %}
**About the meaning of `this` in JSX callbacks**

In JavaScript, class methods are not [bound](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global\_objects/Function/bind) by default. If you forget to bind `this.handleClick` and pass it to `onClick`, `this` will be `undefined` when the function is actually called.

This is not React-specific behavior; it is a part of [how functions work in JavaScript](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/). Generally, if you refer to a method without `()` after it, such as `onClick={this.handleClick}`, you should bind that method.
{% endhint %}

{% embed url="https://reactjs.org/docs/handling-events.html" %}
Handling Events in ReactJS
{% endembed %}

#### Binding Eventhandlers Methods

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

#### Binding by Public class fields syntax

If calling `bind` annoys you, you can use [public class fields syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Public\_class\_fields#public\_instance\_fields) to correctly bind callbacks:

```jsx
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  handleClick = () => {
    console.log('this is:', this);
  };
  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

#### Binding by Arrow function

Second way to bind callbacks correctly without using `bind`.

{% hint style="danger" %}
The problem with this syntax is that a different callback is created each time the `LoggingButton` renders. In most cases, this is fine. However, if this callback is passed as a prop to lower components, those components might do an extra re-rendering. We generally recommend binding in the constructor or using the class fields syntax, to avoid this sort of performance problem.
{% endhint %}

```jsx
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={() => this.handleClick()}>
        Click me
      </button>
    );
  }
}
```

### Passing Arguments to Event Handlers <a href="#passing-arguments-to-event-handlers" id="passing-arguments-to-event-handlers"></a>

Inside a loop, it is common to want to pass an extra parameter to an event handler. For example, if `id` is the row ID, either of the following would work:

```jsx
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

The above two lines are equivalent, and use [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow\_functions) and [`Function.prototype.bind`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_objects/Function/bind) respectively.

In both cases, the `e` argument representing the React event will be passed as a second argument after the ID. With an arrow function, we have to pass it explicitly, but with `bind` any further arguments are automatically forwarded.
