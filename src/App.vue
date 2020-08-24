<template>
  <div id="app">
    <div class="header">
      <h1>
      ToDoList
    </h1>
    <router-link class='link' to="/">Home</router-link>
    <span class="span"> | </span>
    <router-link class='link' to="/todos">Todos</router-link>
    </div>

    <router-view />
  </div>
</template>

<script>
import AddToDo from '@/components/AddToDo'
import ToDoList from '@/components/ToDoList'
export default {
  name: 'app',
  data() {
    return {
      todos: []
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos = json
      })
  },
  methods: {
    removeToDo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addToDo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    ToDoList, AddToDo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:  #2c3e50;
}
h1, .span, .link {
  color: #fff;
}
h1 {
  margin: 0;
  margin-bottom: 15px;
}
body {
  margin: 0;
}
.header {
  background-color: #2c3e50;
  padding: 30px 0 20px;
}
</style>
