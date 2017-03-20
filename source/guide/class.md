---
title: HTML Class Binding
type: guide
order: 6
---

The appearance of HTML elements are typically controlled by adding or removing classes dynamically. In MeltJS, you can bind to the `class` to add or remove a set of CSS classes simultaneously.
## Single Class Binding

You can toggle a class by binding to a Javascript expression. In the following example the `completed` class will be added to the `span` element if `isCompleted` variable evaluates to true, removed if false.
```html
<span class.completed="{isCompleted}"> Todo </span>
```

## Multiple Class Binding
MeltJS support a `class.*={expression}` binding which allows you to easily add or remove multiple classes. The expression evaluation result can be either object or array.
### Object Syntax
When the binding expression is evaluated as object, keys of the result get added to the class list when the expression given in the value evaluates to a truthy value, otherwise they are removed.

In the following example, `foo` and `bar` will be added to the span's class list since their values evaluate to truthy values.
```html
<div id="app1">
  <span class.*="{model.myClasses}">
  I have two classes - 'foo' and 'bar'
  </span>
</div>
```
```javascript
Melt.app({
  elem: '#app1',
  model: {
    myClasses: {
     foo: true,
     bar: false,
     baz: 1 > 0
    }
  }
})
```
{% raw %}
<div id="app1" class="demo">
   <span class.*="{model.myClasses}">I have two classes - 'foo' and 'bar' </span>
</div>
<script>
Melt.app({
  elem: '#app1',
  model: {
    myClasses: {
     foo: true,
     bar: false,
     baz: 1 > 0
    }
  }
})
</script>
{% endraw %}

### Array Syntax
When the binding expression is evaluated as an array, the items of the array will be added as classes.
```html
<span class.*="['foo', 'bar', 'baz']">
  I have three classes - 'foo', 'bar' and 'baz'
</span>
```

In fact, array syntax is just a shorthand version of object syntax. The following code will the the same thing:

```html
<span class.*="{{'foo': true, 'bar':true, 'baz':true}}">
  I have three classes - 'foo', 'bar' and 'baz'
</span>
```

<p class="tip">
The binding syntax above may look strange at fist sight, but it's the right syntax. The outer curly bracket is the binding syntax which means whatever inside is a Javascript expression and can be evaluated to a value. The inner curly bracket is just the object notation.
</p>

The array's element can be object, in this case, MeltJS will apply the object rules to the items to modify the element's classes.