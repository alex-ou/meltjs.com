---
title: Conditional Rendering
type: guide
order: 4
---

You can use the structural directive `if` to conditionally render an element. `if` works in the form of `if={expression}`, if the expression evaluates to a truthy value, the host element will be rendered, otherwise removed from the DOM.

In the following example, the span whose context is 'Completed' will be rendered.
```html
<div id="app1">
  <span>
    <span if="{model.isCompleted}">Completed</span>
    <span if="{!model.isCompleted}">Not completed</span>
  </span>
</div>

```
```javascript
Melt.app({
  elem: '#app1',
  model: {
    isCompleted: true
  }
})
```
{% raw %}
<div id="app1" class="demo">
  <span>
    <span if="{model.isCompleted}">Completed</span>
    <span if="{!model.isCompleted}">Not completed</span>
  </span>
</div>
<script>
Melt.app({
  elem: '#app1',
  model: {
    isCompleted: true
  }
})
</script>
{% endraw %}
