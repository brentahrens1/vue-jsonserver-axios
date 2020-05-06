<template>
  <div id="app">
    <h1>Todos</h1>
    <input type="text" v-model="todosName" @keyup.enter="addToDo">
    <ul>
      <li v-for="todo of todos" :key="todo.id">
        {{ todo.name }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

const baseURL = 'http://localhost:3000/todos'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      todosName: ''
    }
  },
  async created() {
    try {
      const res = await axios.get(baseURL)

      this.todos = res.data
    } catch(e) {
      console.log(e)
    }
  },
  methods: {
    async addToDo() {
      const res = await axios.post(baseURL, { name: this.todosName })

      this.todos = [...this.todos, res.data]

      this.todosName = ''
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
}
li {
  list-style: none;
  text-align: center;
}
input {
  padding: .5rem;
  width: 12rem;
  border-radius: 5px;
  border: 1px solid #000;
  outline: none;
  font-size: 1.5rem;
}
ul {
  margin: 0;
  margin-top: 1rem;
  padding: 0;
}
</style>
