<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/> <!-- Embed functionality for adding todos -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" /> <!-- Embed the todos functionality, calling the deleteTodo function on event del-todo -->
  </div>
</template>

<script>

import Todos from '../components/Todos'; // Functionality for the Todos list
import AddTodo from '../components/AddTodo'; // Functionality for adding todo
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },

  data() {
    return {
      todos: []
    }
  },

  methods: {
    // deleteTodo makes a request to server, deletes it, gets response, then adds it to the UI
    deleteTodo(id) {
      axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id)) // hides the todo with corresponding id with the high-level filter function)
        .catch(err => console.log(err));
    },
    // addTodo makes a request to JSON placeholder, adds it, gives response, then gets added to UI
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', { // adds response to backend
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    }
  },

  created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(res => this.todos = res.data) // fills out todos array in line 26
        .catch(err => console.log(err));
    }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>
