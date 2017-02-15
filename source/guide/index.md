---
title: Introduction
type: guide
order: 2
---


## Overview
Inspired by Elm, MeltJS is a light framework for building reactive web user interfaces. It has a strong emphasis on simplicity.

MeltJS has three essential parts:
* **Model:** The state of the whole application
* **Template:** The way to render the model as HTML, MeltJS uses single curly bracket notation to bind the expressions to DOM elements
* **Update:** The place where you define the functions that respond to user's actions and update the models. Similar to Redux, the update functions are pure functions, they should return a new model instead of mutating the mode

When developing with MeltJS, the typical approach is  to go from the model part, then to the template part (the view), and then to the update part.

Let's say we want to create a simple counter application which allows the users to increase and decrease the count.

<p class="tip"> The complete code of this example can be found at this [JSFiddle](https://jsfiddle.net/alex_ou/xLf7mjtw), but it would be better to open the [Hello World JSFiddle](https://jsfiddle.net/alex_ou/df3uabk1/) in a separate tab, and follow along as we go through the example.</p>

First we need to decide the data structure and the default values for the application and put it into the model.

The model is very simple in this case, it includes a count field, which should be set to 0 by default. So the initial code should be:

``` javascript
Melt.app({
  elem: '#app1',
  model: {
    count: 0
  }
})
```

Then, we should think about how to visualize the model - render the model into html. We only want to show it as plain text, so the code should be like this:

``` javascript
Melt.app({
  elem: '#app1',
  model: {
    count: 0
  },
  template:
  '<div>' +
    '<span>{model.count}</span>' +
  '</div>'
})
```


The next step is to handle the user actions. We want to support two actions `increase` and `decrease`. We just need to create two update functions which take an `context` object as the argument and return a new model.

``` javascript
function increase (context) {
    //the model is inside the context object
    var model = context.model
    return {count: model.count + 1}
}

function decrease (context) {
    var model = context.model
    return {count: model.count - 1}
}
```

Then we can pass them to the update section, and call it from the template. During runtime, when the buttons are clicked, MeltJS will wrap the current `model` into the `context` argument and pass it to the corresponding update functions.

``` javascript
Melt.app({
  elem: '#app1',
  model: {
    count: 0
  },
  template:
    '<div>' +
      '<button on-click="{decrease}">-</button>' +
      '<span>{model.count}</span>' +
      '<button on-click="{increase}">+</button>' +
    '</div>',
  update: {
    increase: increase,
    decrease: decrease
  }
})
```
## Template Syntax
MeltJS supports React-like single curly bracket notation to bind the expressions to DOM elements.
Text interpolation is easy:
```html
<span>1 + 1 = {1 + 1}</span>
```
You can also use built-in `class` directive to toggle a specific class in the DOM element:
```html
<span class.completed="{isCompleted}"> Todo </span>
```
or toggle multiple classes at the same time, here is one example to apply multiple classes using an array:
```html
<span class.*="{['foo', 'bar']}"> Todo </span>
```

## Component