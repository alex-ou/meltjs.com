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
* **Update:** The place where you define the functions that respond to user's actions and update the model. Similar to Redux, the update functions are pure functions, they should return a new model instead of mutating the existing one.

When developing with MeltJS, the typical approach is  to go from the model part, then to the template part (the view), and then to the update part.

Let's say we want to create a simple counter application which allows the users to increase and decrease the count.

<p class="tip"> The complete code of this example can be found at this [JSFiddle](https://jsfiddle.net/alex_ou/xLf7mjtw), but it would be better to open the [Hello World JSFiddle](https://jsfiddle.net/alex_ou/df3uabk1/) in a separate tab, and follow along as we go through the example.</p>

First we need to decide the data structure and the default values for the application and put it into the model.

The model is very simple in this case, it includes a count field, which should be set to 0 by default. So the initial code should be:
```html
<div id="app1">
</div>
```
``` javascript
Melt.app({
  elem: '#app1',
  model: {
    count: 0
  }
})
```

Then, we should think about how to visualize the model - render the model into html. We only want to show the count as plain text, so the code should be like this:
```html
<div id="app1">
  <span>{model.count}</span>
</div>
```
``` javascript
Melt.app({
  elem: '#app1',
  model: {
    count: 0
  }
})
```


The next step is to handle the user actions. We want to support two actions `increase`, increasing the count by 1 and `decrease`, decreasing the count by 1. In orde to do that, We need to create two update functions which take an `context` object as the argument and return a new model.

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

Then we can pass them to the update object making them available in the template, and then call it from the template. During runtime, when the buttons are clicked, MeltJS will wrap the current `model` into the `context` argument and pass it to the corresponding update functions.
```html
<div id="app1">
  <button on-click="{decrease}">-</button>
  <span>{model.count}</span>
  <button on-click="{increase}">+</button>
</div>
```
``` javascript
Melt.app({
  elem: '#app1',
  model: {
    count: 0
  },
  update: {
    increase: increase,
    decrease: decrease
  }
})
```
## Template Syntax
### Text Interpolation
MeltJS supports React-like single curly bracket notation to bind the expressions to DOM elements.
```html
<div id="app2">
</div>
```
```js
Melt.app({
  elem: '#app2',
  template:'<span>1 + 1 = {1 + 1}</span>'
})
```
{% raw %}
<div id="app2" class="demo">
</div>
<script>
Melt.app({
  elem: '#app2',
  template:
    '<div>' +
      '<span>1 + 1 = {1 + 1}</span>' +
    '</div>'
})
</script>
{% endraw %}

### Class Binding
You can use built-in `class` directive to toggle a specific class in the DOM element. In the following example the `completed` class will be added to the span element if variable `isCompleted` is `true`, and removed if it's 'false'.
```html
<span class.completed="{isCompleted}"> Todo </span>
```
You can also toggle multiple classes at the same time, here is one example to apply classes `foo` and `bar` to the span element using an array:
```html
<span class.*="{['foo', 'bar']}"> Todo </span>
```
### Structural Binding
You can not only bind the data into text and properties of the DOM, but the structure of the DOM.

The built-in directive `if` can be used to conditionally render an element based on an expression.
```html
<div id="app3">
  <div>
    <span if="{model.count > 1}">I am greater than 1</span>
    <span if="{model.count < 1}">I am less than 1</span>
  </div>
</div>
```
```js
Melt.app({
  elem: '#app3',
  model: {count: 2}
})
```
{% raw %}
<div id="app3" class="demo">
    <div>
        <span if="{model.count > 1}">I am greater than 1</span>
        <span if="{model.count < 1}">I am less than 1</span>
    </div>
</div>
<script>
Melt.app({
  elem: '#app4',
  model: {count: 2}
})
</script>
{% endraw %}

Structural directive `each` comes into play when you want to render a list of items into DOM elements.
```html
<div id="app4">
  <ul>
    <li each="{todo in model.todos}">{todo}</li>
  </div>
</div>
```
```js
Melt.app({
  elem: '#app4',
  model: {
    todos: [
      'Pay bills',
      'Exercise',
      'Buy snacks'
    ]
  }
})
```
{% raw %}
<div id="app4" class="demo">
  <ul>
    <li each="{todo in model.todos}">{todo}</li>
  </div>
</div>
<script>
Melt.app({
  elem: '#app4',
  model: {
    todos: [
      'Pay bills',
      'Exercise',
      'Buy snacks'
    ]
  }
})
</script>
{% endraw %}
## Component