---
---

``` html
<div id="app">

</div>
```
``` js
Melt.app({
  el: '#app', //the root DOM element
  model: {
    count: 0
  },
  update: {
    // The pure function that updates the model
    // Notice that the model is passed in as the argument
    increase: ({model}) => {
      return {count: model.count + 1}
    }
  },
  template:
  `<div>{model.count}
    <button on-click='{increase()}'>+</button>
  </div>`
})
```

{% raw %}
<div id="app" class="demo">
</div>
<script>
<script>
    Melt.app({
      el: '#app', //the root DOM element
      model: {
        count: 0
      },
      update: {
        increase: function (context) {
          return {count: context.model.count + 1}
        }
      },
      template: '<div>{model.count}<button on-click="{increase()}">+</button></div>'
    })
</script>
{% endraw %}