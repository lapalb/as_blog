---
layout: post
title: "React : Decoding the most used Frontend Framework"
tags:
 -
---
# React

I have been a religious fanboy on Angular Cinematic universe for long. This weekend I decided to go through the react and to understand why so much fuss is created around around React. This blogs will be an introduction to React Framework.

React was developed by Facebook as a frontend library. Unlike Angular, it is not a framework. Frameworks offers a very opinionated way of coding.

To use react, all we need is to import react and react DOM library.

```html
<!--React Import-->
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>

<!--JSX Import-->
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

To Run our code, all we need to use in `React.render(JSX_ELEMENT,selector).`  This will grab the selector and put our element there.

To Generate Boilerplate code we have `create-react-app`  It uses `webpack` to bundle content

<img src="/as_blog/images/createReact.jpeg" alt="rxjs image"><br>

```bash
npx create-react-app my-app
cd my-app
npm start

#This will Create a bundled App.js, App.css, App.test.js and the source file is contained in idex.css and index.js
```

## JSX

JSX allows use to use an HTML element, right in the JavaScript code. Also, it allows us to use expression

When the JSX expressions are compiled, they are converted into JavaScript **objects**, representing React elements. React then uses these elements to build the corresponding HTML DOM and display it in the browser. React only update the element which requires updation. The way it is done is that react creates what is called virtual dom and manipulating virtual DOM is easy. It then goes ahead to calculate the diff of Virtual DOM and then rerenders only the part of DOM which has changed.

## Component

Components are reusable part of DOM. There are two ways to create component. `Functional Component` and `Class Component`

```jsx
//Functional Component return JSX Element. It can take props(Constant Value)
function Hello(props) {
  return <h1>Hello {props.name}.</h1>;
}
const el = <Hello name="Akanksha"/>; 
const selector = document.getElementById('root')
ReactDOM.render(el, selector);
```

```jsx
//Class component must extends React.Component and implement render method
class Hello extends React.Component {
  render() {
    return <h1>Hello {this.props.name}.</h1>;
  }
}
```

If component needs constant values, props is the best choice. Otherwise state needs to be implemented. 

```jsx
//State should not be modified directly. Instead, React provides a setState() method, that can be used to modify the state.
class Hello extends React.Component {
	
	state = {
    name: "Akanksha",
		age: 20
  }
	doSomthing = function(){
		this.setState({ 
			name: "Akanksha Updated",
		  age: 25
		});
	}

  render() {
    return <h1>Hello {this.state.name}.</h1>;
  }
}
```

If functional component needs state, then we need to use `useState` hooks

```jsx
import React, { useState } from 'react';

function Hello() {
  const [name, setName] = useState("Akanksha");

  return <h1>Hello {name}.</h1>;
}
```

## LifeCycle Method

These methods are called when component is mounted and when it is updated and when it is unmounted

Class Component

---

componentDidMount

componentWillUnmount

componentDidUpdate

Functional Component

---

React provides a special Hook called `useEffect` to make lifecycle methods available in functional components