``` html
<div id="todo-app">
</div>
```

``` js
Melt.component('todo-list', {
  template:
    `<ul>
      <li each="item in props.todos"
        key="{item.id}">
        {item.text}
      </li>
    </ul>`
})

Melt.component('add-todo', {
  template:
    `<form on-submit="onSubmit">
      <input ref="input">
      <button type="submit">
        Add Todo
      </button>
    </form>`,
  class: function AddTodoComponent () {
    this.onSubmit = function (e) {
      e.preventDefault()
      const input = this.refs.input
      var text = input.value
      if (!text.trim()) {
        return
      }
      input.value = ''
      this.props.onAddTodo(text)
    }
  }
})

Melt.container('app', {
  template:
    `<div>
      <add-todo on-add-todo="{addTodo}">
      </add-todo>
      <todo-list todos="{model.todos}">
      </todo-list>
    </div>`
})

Melt.app({
  elem: '#app',
  template: '<app></app>',
  model: {
    todos: []
  },
  update: {
    addTodo: function (context, text) {
      var model = context.model
    	return {
          todos: model.todos.concat({
            id: Date.now(),
            text: text
          })
        }
  	}
  }
})

```

<div id="todo-app" class="demo">
</div>
<script>
    Melt.component('todo-list', {
      template:
        `<ul>
          <li each="item in props.todos"
            key="{item.id}">
            {item.text}
          </li>
        </ul>`
    })

    Melt.component('add-todo', {
      template:
        `<form on-submit="onSubmit">
          <input ref="input">
          <button type="submit">Add Todo</button>
        </form>`,
      class: function AddTodoComponent () {
        this.onSubmit = function (e) {
          e.preventDefault()
          const input = this.refs.input
          var text = input.value
          if (!text.trim()) {
            return
          }
          input.value = ''
          this.props.onAddTodo(text)
        }
      }
    })

    Melt.container('app', {
      template:
        `<div>
          <add-todo on-add-todo="{addTodo}"></add-todo>
          <todo-list todos="{model.todos}"></todo-list>
        </div>`
    })

    Melt.app({
      elem: '#todo-app',
      template: '<app></app>',
      model: {
        todos: []
      },
      update: {
        addTodo: function (context, text) {
          var model = context.model
        	return {
              todos: model.todos.concat({
                id: Date.now(),
                text: text
              })
            }
      	}
      }
    })
</script>
