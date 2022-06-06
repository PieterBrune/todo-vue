<template>
  <div>
    <input type="text" class="todo-input" placeholder="What needs to be done" v-model="newTodo" @keyup.enter="addTodo">
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
      <input type="checkbox" v-model="todo.completed">
        <div v-if="!todo.editing" @dblclick="editTodo(todo)" class="todo-item-label" :class="{ completed : todo.completed }">{{ todo.title }}</div>
        <input v-else class="todo-item-edit" type="text" v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
      </div>
      <div>
        <button @click="removeTodo(index)" class="remove-item">&times;</button>
      </div>
    </div>
  </div>
</template>

<script>

let id = 0

export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      beforeEditCache: '',
      todos: [
        {
          id: id++,
          title: 'Finish learning Vue',
          completed: false,
          editing: false
        },
        {
          id: id++,
          title: 'Finish learning Go',
          completed: false,
          editing: false
        }
      ]
    }
  },
  directives: {
    focus: {
      // directive definition
      inserted: function (el) {
        el.focus()
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return
      }

      this.todos.push({ id: id++, title: this.newTodo, completed: false, editing: false })

      this.newTodo = ''
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title
      todo.editing = true
    },
    doneEdit(todo) {
      if (todo.title.trim().length === 0) {
        todo.title = this.beforeEditCache
      }
      todo.editing = false
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;
  }

  .todo-input:focus {
    outline: 0;
  }

  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .remove-item {
    cursor: pointer;
  }

  .remove-item:hover {
    color: red;
  }

  .todo-item-left {
    display: flex;
    align-items: center;
  }

  .todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }

  .todo-item-edit {
    font-size: 20px;
    color: #2c3e58;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
  }

  .todo-item-edit:focus {
    outline: none;
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }
</style>
