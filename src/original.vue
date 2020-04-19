<template>
  <div id="app">
    <Header />
    <AddTodo  v-on:add-todo="addTodo"/>
    <!-- v-bind is used to bind -->
    <Todos v-bind:todos = 'todos' v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';
export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: [] 
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res =>   console.log(res), this.todos = this.todos.filter(todo => todo.id !== id))
      
      .catch(err => console.log(err));


    },
    addTodo(newTodo) {
      // using destructor to pull out title from todo object
      const { title, completed } = newTodo
      // we're making a post request here using axios
      axios.post('https://jsonplaceholder.typicode.com/todos' , {
        title,
        completed
      })

      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err));
    }
  },
  // created() is a special method used to make initial request for json files
  // and routers and jason todos are taken from https://jsonplaceholder.typicode.com
  // we can use fetch api if needed but here we've used axios which works the same as fetch. To use that first install using 'npm i axios'
  // axios is a http library using which we can make request and so on
  // axios will return a promise and we get that using '.then()' and catch the error using '.catch(err)'
  // in the https link '?_limit=5' is used to set the limit to the json package.
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
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

  body{
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
