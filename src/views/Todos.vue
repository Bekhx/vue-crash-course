<template>
  <div>
    <AddToDo 
      @add-todo='addToDo'
    />
    <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <Loader v-if='loading' />
    <ToDoList
        v-else-if='filteredTodos.length'
        v-bind:todos='filteredTodos'
        @remove-todo='removeToDo'
    />
    <p v-else>No-todos!</p>
  </div>
</template>

<script>
import AddToDo from '@/components/AddToDo'
import ToDoList from '@/components/ToDoList'
import Loader from '@/components/Loader'
export default {
  name: 'app',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
            this.todos = json
            this.loading = false
        }, 50);
      })
  },
  /* watch: {
      filter(value) {
          console.log(value);
      }
  }, */
  computed: {
      filteredTodos() {
          if (this.filter === 'all') {
              return this.todos
          }

          if (this.filter === 'completed') {
              return this.todos.filter(t => t.completed)
          }

          if (this.filter === 'not-completed') {
              return this.todos.filter(t => !t.completed)
          }
      }
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
    ToDoList, AddToDo, Loader
  }
}
</script>

<style>
  hr {
    margin: 0;
    margin: 20px 0;
  }
  select {
    cursor: pointer;
  }
</style>