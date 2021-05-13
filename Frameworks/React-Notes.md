# React (JS)

## Why React?
- Fast (Because of virtual DOM)
- Reusable Components
- Currently highly in demand

## ReactDOM and JSX
`ReactDOM` is used to insert HTML into a HTML file,
this is done by passing the `conent` and the `target element` 
to the `render` function. Take the following files as example:

```HTML
<!-- index.html -->

<html>
    <head>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <!-- The div we will be targeting in the index.js -->
        <div id="root"></div>
        <script src="index.pack.js"></script>
    </body>
</html>
```

```JS
//index.js

import React from "react"
import ReactDOM from "react-dom"

ReactDOM.render(<h1>Hello World</h1>, document.getElementbyId("root"))
```

Since the first argument (content) would be marked as incorrect since JS or TS by
default don't know how HTML looks like.
Luckily React includes something called `JSX` which is something like a pseudo
language which is a `JS version of HTML`.

The content has to be `one JSX element`, multiple elements are not allowed.
But it is possible to have one element with other elements nested inside it. 

```JS
//index.js

import React from "react"
import ReactDOM from "react-dom"

//This is NOT allowed
ReactDOM.render(
    <h1>Hello World</h1>
    <p>I'm Marcel</p>, 
    document.getElementbyId("root")
)

//Instead do it like this
ReactDOM.render(
    <div>
        <h1>Hello World</h1>
        <p>I'm Marcel</p>
    </div>,
    document.getElementbyId("root")
)
```

This works because we just have one JSX element we are injecting (the div).

## Functional Components
Like the name suggests `functional components` are created by writing a function.
Like mentioned in the [Why React?](#why-react) section one benefit of react is
the possibility to create reusable components, this is what this is about.

```JS
function MyIntroduction(){
    return (
    <div>
        <h1>Hello World</h1>
        <p>I'm Marcel</p>
    </div>
    )
}

ReactDOM.render(
    <MyIntroduction />,
    document.getElementbyId("root")
)
```

The component function itself just needs to return the JSX element,
by convention the function is written in `CamelCase starting with a uppercase
character`.
The component then can be referenced in the render function with a JSX tag.

To clean up the structure we should move our component to a separate file

```JS
//MyIntroduction.js

function MyIntroduction(){
    return (
    <div>
        <h1>Hello World</h1>
        <p>I'm Marcel</p>
    </div>
    )
}

export default MyIntroduction
```

```JS
//index.js

import MyIntroduction from "./components/MyIntroduction"

ReactDOM.render(
    <MyIntroduction />,
    document.getElementbyId("root")
)
```

It is also possible to use JS inside JSX elements as the following example shows
```JS
import React from "react"
import ReactDOM from "react-dom"

function App() {
  const date = new Date()
  const hours = date.getHours()
  let timeOfDay
  
  if (hours < 12) {
    timeOfDay = "morning"
  } else if (hours >= 12 && hours < 17) {
    timeOfDay = "afternoon"
  } else {
    timeOfDay = "night"
  }
  
  return (
    <h1>Good {timeOfDay}!</h1>
  )
}

ReactDOM.render(<App />, document.getElementById("root"))
```

## Styling Components
Let's start styling our MyIntroduction component with css classes,
since we are not dealing with HTML but with JSX this is a bit different to 
what you would expect.
Instead of `class` we have to use `className`. I also have to mention that
we `cannot apply` this to our components (e.g. `<MyIntroduction />`),
since those don't refer to HTML elements

```JS
//MyIntroduction.js

function MyIntroduction(){
    return (
    <div className="intro">
        <h1 className="border-heading">Hello World</h1>
        <p className="intro-text">I'm Marcel</p>
    </div>
    )
}

export default MyIntroduction
```

We can also use inline styling, this is especially useful if we want to manipulate the style in JS. But since we have to use JS for the styling properties like `background-color` will not work, to get around this we can `use camelCase` (e.g. `backgroundColor="#fff"`). Another issue we could face is that values like 100px or 100% will not work, in this case its enough to wrap the value in `"` (e.g. `width="20%"`) 

```JS
//MyIntroduction.js

const styles = {
    fontSize: 30
}

//Manipulate css
styles.color = "#83ff7d"

function MyIntroduction(){
    return (
    <div style={styles}>
        <h1>Hello World</h1>
        <p>I'm Marcel</p>
    </div>
    )
}

export default MyIntroduction
```

## Props
React props are comparable with the `src` inside a `img` tag (`<img src=""/>`) and are used to alter information in a component. For example we could have a title prop that will inserted as a heading in the component.

```JS
function Contact(props){
    return (
        <div>
            <h3>{props.name}</h3>
            <p>Phone: {props.phone}</p>
            <p>Email: {props.email}</p>
        </div>
    )
}

ReactDOM.render(
    <div>
        <Contact 
            name="Markus Mueller"  
            phone="1234 123456"
            email="m.mueller@muellers.at"
        />
        
        <Contact 
            name="Eva Eggenberg" 
            phone="1235 123456"
            email="eva.egg@eggenberg.org"
        />
        
        <Contact 
            name="Marcel Walk" 
            phone="1236 123456"
            email="m.walk@nyasaki.cloud"
        />
        
        <Contact 
            name="John Doe"
            phone="1237 123456"
            email="jdoe@mail.cli"
        />
    </div>,
    document.getElementById("root")
)
```

the function parmeter `props` is a `object` that contains all properties
we define when using the component (in the render method in this case)

## Class Components
We can use class components to further clean up our code, they work 
similar to function based components. It requires a `render method`, this 
method will act like our function so we can copy paste the return 
statement from out functions directly into our render method.

```JS
class App extends React.Component{
    render(){
        return (
            <h1>Im in a class component</h1>
        )
    }
}

export default MyIntroduction
```

If we have `props` we have to add the `this` keyword before the object 
name, it is not required to add parameters to the render method

```JS
class App extends React.Component{
    render(){
        return (
            <h1>Hello, {this.props.username}</h1>
        )
    }
}

export default MyIntroduction
```

## React States
State is the data the component maintains, in contrast to the `props`, the 
data can be changed by the component. States only can be used in 
`class based components`

In order to maintain its data using state we need a constructor method, and initialize the state object.

```JS
class App extends React.Component{

    constructor(){
        super()

        //Initialize our state object
        this.state = {}
    }

    render(){
        return (
            <h1>Hello, {this.props.username}</h1>
        )
    }
}

export default MyIntroduction
```

Changing the state can be achieved by using the `setState` method.
If we want use `setState` we need to bind the function to the class.

```JS
[...]
    constructor() {
        super()
        this.state = {
            count: 0
        }
        this.handleClick = this.handleClick.bind(this)
    }
    
    handleClick() {
        this.setState({ count: 1 })
    }
[...]
```

We can replace the value completely if we don't care what its been before
```JS
handleClick() {
        this.setState({ count: 1 })
}
```

Or we can pass a function to `setState` if we need the previous state
```JS
handleClick() {
    this.setState(prevState => {
        return {
            count: prevState.count + 1
        }
    })
}
```

## Handling Events
Handling events is similar to JS, but we need to use `camelCase` starting with a lowercase character

```JS
function App() {
    return (
        <div>
            <img src="https://www.fillmurray.com/200/100"/>
            <br />
            <br />
            <button onClick={handleClick}>Click me</button>
        </div>
    )
}
```