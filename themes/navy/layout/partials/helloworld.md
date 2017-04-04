``` html
<div id="app">
</div>
```

``` js
Melt.app({
  elem: '#app', //the root DOM element
  model: {
    message: 'Hello World'
  },
  template: '<span>{model.message}</span>'
})
```
<div id="helloworld" class="demo">
</div>
<script>
Melt.app({
  elem: '#helloworld', //the root DOM element
  model: {
    message: 'Hello World'
  },
  template: '<span>{model.message}</span>'
})
</script>
