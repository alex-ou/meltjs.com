---
title: Lists and Keys
type: guide
order: 5
---

To render an array or an object to the view, you can utilise another structural directive of MeltJS - 'each'.

Directive 'each' works well with both arrays and objects.
## Rendering Arrays
Typically, when rendering arrays, `each` works in the form of `each={item in array}`. And when you need to access the index of each item in the array, you can use it in this form: `each={(item, index) in array}`.

In the following example, the data along with its index in the `list` will be rendered into multiple `li` elements.
```html
<div id="app1">
  <ul>
    <li each="{(item, index) in model.list}">{index}: {item}</li>
  </ul>
</div>

```
```javascript
Melt.app({
  elem: '#app1',
  model: {
    list: ['foo', 'bar', 'baz']
  }
})
```
{% raw %}
<div id="app1" class="demo">
    <ul>
      <li each="{(item,index) in model.list}">{index}: {item}</li>
    </ul>
</div>
<script>
Melt.app({
  elem: '#app1',
  model: {
      list: ['foo', 'bar', 'baz']
   }
})
</script>
{% endraw %}

## Rendering Objects
When rendering objects, `each` works in the form of `each={value in object}`. When you need to access the corresponding key of each value in the object, you can use it in this form: `each={(value, key) in object}`.

In the following example, the value along with its key in the `model` will be rendered into multiple `li` elements.
```html
<div id="app1">
  <ul>
    <li each="{(value, key) in model}">{key}: {value}</li>
  </ul>
</div>

```
```javascript
Melt.app({
  elem: '#app1',
  model: {
    foo: '1',
    bar: '2',
    baz: '3',
  }
})
```
{% raw %}
<div id="app2" class="demo">
    <ul>
        <li each="{(value, key) in model}">{key}: {value}</li>
     </ul>
</div>
<script>
Melt.app({
  elem: '#app2',
  model: {
      foo: '1',
      bar: '2',
      baz: '3',
    }
})
</script>
{% endraw %}

## Working with Ranges
Generating lists with a specific number of integers is a very common thing to do, especially when you want to write simple loop iteration, so MeltJS provides a `range` function that can deliver a sequence of values to the `each` directive.

The signature of the range function is:

 ```javascript
range([start=0], end, [step=1])
 ```

It creates an array of numbers (positive and/or negative) progressing from start up to, but not including, end. A step of -1 is used if a negative start is specified without an end or step. If end is not specified, it's set to start with start then set to 0.

Here are some examples:
```javascript
range(4);
// => [0, 1, 2, 3]

range(-4);
// => [0, -1, -2, -3]

range(1, 5);
// => [1, 2, 3, 4]

range(0, 20, 5);
// => [0, 5, 10, 15]

```

Here is an example showing how `range` function works with the `each` directive. Integers from 0 to 3 inclusive are rendered into li elements.
```html
<div id="app3">
  <ul>
    <li each="{i in range(4)}">{i}</li>
  </ul>
</div>
```

```javascript
Melt.app({
  elem: '#app3'
})
```
{% raw %}
<div id="app3" class="demo">
    <ul>
    <li each="{i in range(4)}">{i}</li>
    </ul>
</div>
<script>
Melt.app({
  elem: '#app3'
})
</script>
{% endraw %}