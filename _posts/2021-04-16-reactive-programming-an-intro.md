---
layout: post
title: "Reactive programming : An Intro"
tags:
 -
---
# RxJS

Reactive programming is an asynchronous programming paradigm concerned with data streams and the propagation of change. event handling, asynchronous programming, and handling multiple values.

The observer pattern is a software design pattern in which an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of state changes. This pattern is similar (but not identical) to the publish/subscribe design pattern.

Observables are declarative—that is, you define a function for publishing values, but it is not executed until a consumer subscribes to it. The subscribed consumer then receives notifications until the function completes, or until they unsubscribe

An observable can deliver multiple values of any type—literals, messages, or events, depending on the context.

A handler for receiving observable notifications implements the Observer interface. It is an object that defines callback methods to handle the three types of notifications that an observable can send:

<img src="/as_blog/images/rxjs.jpeg" alt="rxjs image"><br>

<h3 class="alert-success"> Methods in RxJS</h3>
of(...items)—Returns an Observable instance that synchronously delivers the values provided as arguments.

from(iterable)—Converts its argument to an Observable instance. This method is commonly used to convert an array to an observable.

Whether the stream was keystrokes, an HTTP response, or an interval timer, the interface for listening to values and stopping listening is the same.

RxJS (Reactive Extensions for JavaScript) is a library for reactive programming. RxJS provides an implementation of the Observable type, which is needed until the type becomes part of the language and until browsers support it.

Provides utility functions for creating and working with observables.

These utility functions can be used for:

- Converting existing code for async operations into observables
- Iterating through the values in a stream
- Mapping values to different types
- Filtering streams
- Composing multiple streams
<h3 class="alert-success"> Observable creation functions</h3>

```js
import { from } from 'rxjs';
import { interval } from 'rxjs';
import { fromEvent } from 'rxjs';
import { ajax } from 'rxjs/ajax';
import { of } from 'rxjs';
const nums = of(1, 2, 3);

// Create an Observable out of a promise
const data = from(fetch('/api/endpoint'));

// Create an Observable that will publish a value on an interval
const secondsCounter = interval(1000);

// Create an Observable that will publish mouse movements
const mouseMoves = fromEvent(el, 'mousemove');

// Create an Observable that will create an AJAX request
  const apiData = ajax('/api/data');
```

<h3 class="alert-success"> Operator </h3>
Operators are functions that build on the observables foundation to enable sophisticated manipulation of collections. map(), filter(), concat(), and flatMap().

We can use pipes to link operators together

A set of operators applied to an observable is a recipe.that is, a set of instructions for producing the values you’re interested in. By itself, the recipe doesn’t do anything. You need to call subscribe() to produce a result through the recipe.

receipe = Opertator(Observable) `//we then subscribe to receipe`

Observale.pipe()

observables named with a trailing “$” sign.

<h3 class="alert-success"> Multicasting </h3>
A typical observable creates a new, independent execution for each subscribed observer. Multicasting is the practice of broadcasting to a list of multiple subscribers in a single execution

Operators are functions. There are two kinds of operators:

A `Pipeable Operator` is a function that takes an Observable as its input and returns another Observable. It is a pure operation: the previous Observable stays unmodified.

`Creation Operators` are the other kind of operator, which can be called as standalone functions to create a new Observable.

Observables of Observables, so-called higher-order Observables