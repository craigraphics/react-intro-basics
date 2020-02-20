# react-intro-basics

## What is React?
React is a JavaScript library created for building UI components.

### How does React Work?
React creates a VIRTUAL DOM in memory.
Instead of manipulating the browser's DOM directly, React creates a virtual DOM in memory, where it does all the necessary manipulating, before making the changes in the browser DOM.
React finds out what changes have been made, and changes only what needs to be changed.

### The Render Function
The `ReactDOM.render()` function takes two arguments, HTML code and an HTML element.
The purpose of the function is to display the specified HTML code inside the specified HTML element.

```JavaScript
ReactDOM.render(<p>Hello</p>, document.getElementById('root'));
```
### The Root Node
The root node is the HTML element where you want to display the result.
It is like a container for content managed by React.

### What is JSX?
JSX stands for JavaScript XML, it allows us to write HTML in React and makes it easier to write and add HTML in React.
JSX allows us to write HTML elements in JavaScript and place them in the DOM without any createElement()  and/or appendChild() methods.
JSX converts HTML tags into react elements.

### React Components
Components are independent and reusable bits of code. They serve the same purpose as JavaScript functions, but work in isolation and returns HTML via a render function.
Components come in two types, Class components and Function components.

### Class Component
When creating a React component, the component's name must start with an upper case letter.
The component has to include the `extends React.Component` statement, this statement creates an inheritance to React.Component, and gives your component access to React.Component's functions.

The component also requires a `render()` method, this method returns HTML.

```JavaScript
class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}
ReactDOM.render(<Car />, document.getElementById('root'));
```

### Function Component
A Function component also returns HTML, and behaves pretty much the same way as a Class component, but Class components have some additions.

```JavaScript
function Car() {
  return <h2>Hi, I am also a Car!</h2>;
}
ReactDOM.render(<Car />, document.getElementById('root'));
```

#### Component Constructor
If there is a `constructor()` function in your component, this function will be called when the component gets initiated.
The constructor function is where you initiate the component's properties. In React, component properties should be kept in an object called `state`.
The constructor function is also where you honor the inheritance of the parent component by including the `super()` statement, which executes the parent component's constructor function, and your component has access to all the functions of the parent component (React.Component).

```JavaScript
class Car extends React.Component {
  constructor() {
    super();
    this.state = {color: "red"};
  }
  render() {
    return <h2>I am a {this.state.color} Car!</h2>;
  }
}
```
### React Props
Props are arguments passed into React components via HTML attributes.
To send props into a component, use the same syntax as HTML attributes:

```JavaScript
const myelement = <Car brand="Ford" />;

class Car extends React.Component {
  render() {
    return <h2>I am a {this.props.brand}!</h1>;
  }
}
```

#### Pass Data
Props are also how you pass data from one component to another, as parameters.

```JavaScript
class Car extends React.Component {
  render() {
    return <h2>I am a {this.props.brand}!</h2>;
  }
}

class Garage extends React.Component {
  render() {
    return (
      <div>
      <h1>Who lives in my garage?</h1>
      <Car brand="Ford" />
      </div>
    );
  }
}

ReactDOM.render(<Garage />, document.getElementById('root'));
```

#### Props in the Constructor
If your component has a constructor function, the props should always be passed to the constructor and also to the React.Component via the `super()` method.


```JavaScript
class Car extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <h2>I am a Car!</h2>;
  }
}

ReactDOM.render(<Car model="Mustang"/>, document.getElementById('root'));
```

### React State
React components has a built-in state object which is where you store property values that belongs to that component itself.
When the state object changes, the component re-renders.

#### Creating the state Object
The state object is initialized in the constructor, it can contain as many properties as needed:

```JavaScript
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = {brand: "Ford"};
  }
  render() {
    return (
      <div>
        <h1>My Car</h1>
      </div>
    );
  }
}
```

#### Using the state Object
Refer to the state object anywhere in the component by using the `this.state.propertyname` syntax:

```JavaScript
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      brand: "Ford",
      model: "Mustang",
      color: "red",
      year: 1964
    };
  }
  render() {
    return (
      <div>
        <h1>My {this.state.brand}</h1>
        <p>
          It is a {this.state.color}
          {this.state.model}
          from {this.state.year}.
        </p>
      </div>
    );
  }
}
```

#### Changing the state Object
To change a value in the state object, use the `this.setState()` method.

When a value in the state object changes, the component will re-render, meaning that the output will change according to the new value(s).

```JavaScript
changeColor = () => {
  this.setState({color: "blue"});
}
```

### React Lifecycle
Each component in React has a lifecycle which you can monitor and manipulate during its three main phases.
The three phases are: Mounting, Updating, and Unmounting.

### Mounting
Mounting means putting elements into the DOM. React has four built-in methods that gets called, in this order, when mounting a component:

`constructor()
getDerivedStateFromProps()
render()
componentDidMount()`

The `render()` method is required and will always be called, the others are optional and will be called if you define them.

#### constructor
The `constructor()` method is called before anything else, when the component is initiated, and it is the natural place to set up the initial state and other initial values.

The `constructor()` method is called with the props, as arguments, and you should always start by calling the `super(props)` before anything else, this will initiate the parent's constructor method and allows the component to inherit methods from its parent (React.Component).

#### getDerivedStateFromProps
The `getDerivedStateFromProps()` method is called right before rendering the element(s) in the DOM.This is the natural place to set the state object based on the initial props. It takes state as an argument, and returns an object with changes to the state.

#### render
The `render()` method is required, and is the method that actual outputs HTML to the DOM.

#### componentDidMount
The `componentDidMount()` method is called after the component is rendered.
This is where you run statements that requires that the component is already placed in the DOM.


### Updating
The next phase in the lifecycle is when a component is updated. A component is updated whenever there is a change in the component's state or props. React has five built-in methods that gets called, in this order, when a component is updated:

`getDerivedStateFromProps()
shouldComponentUpdate()
render()
getSnapshotBeforeUpdate()
componentDidUpdate()`


### Unmounting
The next phase in the lifecycle is when a component is removed from the DOM, or unmounting as React likes to call it. React has only one built-in method that gets called when a component is unmounted:

`componentWillUnmount()`
The componentWillUnmount method is called when the component is about to be removed from the DOM.


### React Events
Just like HTML, React can perform actions based on user events. It has the same events as HTML: click, change, mouseover etc.

#### Adding Events
React events are written in camelCase syntax:
`onClick` instead of `onclick`.

React event handlers are written inside curly braces:
`onClick={shoot}`  instead of `onClick="shoot()"`.

```JavaScript
<button onClick={shoot}>Take the Shot!</button>
```

#### Bind this
For methods in React, the `this` keyword should represent the component that owns the method. That is why you should use arrow functions. With arrow functions, this will always represent the object that defined the arrow function.

```JavaScript
class Football extends React.Component {
  shoot = () => {
    alert(this);
    /*
    The 'this' keyword refers to the component object
    */
  }
  render() {
    return (
      <button onClick={this.shoot}>Take the shot!</button>
    );
  }
}

ReactDOM.render(<Football />, document.getElementById('root'));
```
In class components, the `this` keyword is not defined by default, so with regular functions the `this` keyword represents the object that called the method, which can be the global window object, a HTML button, etc.

Passing Arguments
If you want to send parameters into an event handler, you have two options:

1. Make an anonymous arrow function:

```JavaScript
class Football extends React.Component {
  shoot = (a) => {
    alert(a);
  }
  render() {
    return (
      <button onClick={() => this.shoot("Goal")}>Take the shot!</button>
    );
  }
}

ReactDOM.render(<Football />, document.getElementById('root'));
```

2. Bind the event handler to this.
Note that the first argument has to be this.

```JavaScript
class Football extends React.Component {
  shoot(a) {
    alert(a);
  }
  render() {
    return (
      <button onClick={this.shoot.bind(this, "Goal")}>Take the shot!</button>
    );
  }
}

ReactDOM.render(<Football />, document.getElementById('root'));
```

### Adding Forms in React
Just like in HTML, React uses forms to allow users to interact with the web page. Handling forms is about how you handle the data when it changes value or gets submitted. In React, form data is usually handled by the components. When the data is handled by the components, all the data is stored in the component state.
You can control changes by adding event handlers in the `onChange` attribute, and control the submit action by adding an event handler in the `onSubmit` attribute::

```JavaScript
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { username: '' };
  }
  mySubmitHandler = (event) => {
    event.preventDefault();
    alert("You are submitting " + this.state.username);
  }
  myChangeHandler = (event) => {
    this.setState({username: event.target.value});
  }
  render() {
    return (
      <form onSubmit={this.mySubmitHandler}>
      <h1>Hello {this.state.username}</h1>
      <p>Enter your name, and submit:</p>
      <input
        type='text'
        onChange={this.myChangeHandler}
      />
      <input
        type='submit'
      />
      </form>
    );
  }
}

ReactDOM.render(<MyForm />, document.getElementById('root'));
```
