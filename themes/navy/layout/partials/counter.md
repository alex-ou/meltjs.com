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
<div id="app" class="demo">
</div>
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
