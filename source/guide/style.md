---
title: Inline Style Binding
type: guide
order: 5
---

The appearance of HTML elements can also be controlled by adding or removing inline styles. In MeltJS, you can bind to the `style` to add or remove inline styles simultaneously.
## Single Style Binding

You can toggle a style by binding to a Javascript expression. In the following example the font weight of the span element will be bold if `isCompleted` evaluates to a truthy value, normal otherwise.
```html
<span style.font-weight="{isCompleted ? 'bold' : 'normal'}"> Todo </span>
```

## Multiple Styles Binding
MeltJS support a `style.*={expression}` binding which allows you to easily add or removed multiple styles at the same time.

The expression needs to be evaluated as an object. Keys are the names of the styles, and the values of the keys will be assigned to the inline style properties.

In the following example, the span's text color is changed to red and the font weight bold.
```html
<div id="app1">
  <span style.*="{model.myStyles}">
  My text is red and bold
  </span>
</div>
```
```javascript
Melt.app({
  elem: '#app1',
  model: {
    myStyles: {
     'font-weight': 'bold',
     'color': 'red'
    }
  }
})
```
{% raw %}
<div id="app1" class="demo">
  <span style.*="{model.myStyles}">
  My text is red and bold
  </span>
</div>
<script>
Melt.app({
  elem: '#app1',
  model: {
    myStyles: {
     'font-weight': 'bold',
     'color': 'red'
    }
  }
})
</script>
{% endraw %}
