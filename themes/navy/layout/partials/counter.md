``` html
<div id="counter-app">
</div>
```

``` js
Melt.app({
  elem: '#app', //the root DOM element
  model: {
    count: 0
  },
  update: {
//Pure functions that returns a new model
    decrease: function (context) {
      var model = context.model
      return {count: model.count - 1}
    },
    increase: function (context) {
      var model = context.model
      return {count: model.count + 1}
    }
  },
  template:
  `<div>
    <span>{model.count}</span>
    <button on-click='{decrease}'>
        Decrease
    </button>
    <button on-click='{increase}'>
        Increase
    </button>
  </div>`
})
```
<div id="counter-app" class="demo">
</div>
<script>
    Melt.app({
      elem: '#counter-app', //the root DOM element
      model: {
        count: 0
      },
      update: {
        // The pure function that updates the model
        // Notice that the model is passed in as the argument
        decrease: function (context) {
        	var model = context.model
          return {count: model.count - 1}
        },
        increase: function (context) {
        	var model = context.model
          return {count: model.count + 1}
        }
      },
      template:
      `<div>
      	<span>{model.count}</span>
      	<button on-click='{decrease}'>Decrease</button>
        <button on-click='{increase}'>Increase</button>
      </div>`
    })
</script>
