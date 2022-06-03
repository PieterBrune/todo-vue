<template>
  <div>
    <input type="text" class="todo-input" placeholder="What needs to be done" v-model="newTodo" @keyup.enter="addTodo">
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div>
        <div>{{ todo.title }}</div>

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
      todos: [
        {
          id: id++,
          title: 'Finish learning Vue',
          completed: false
        },
        {
          id: id++,
          title: 'Finish learning Go',
          completed: false
        },
      ]
    }
  },
  methods: {
    addTodo() {

      if (this.newTodo.trim().length === 0) {
        return
      }

      this.todos.push({id: id++, title: this.newTodo, completed: false })

      this.newTodo = ''
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
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
</style>
