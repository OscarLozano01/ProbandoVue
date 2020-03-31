<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <div class="post" v-for="post in posts" v-bind:key="post.id">
     <h3>{{ post.title}}</h3>
     <p>{{ post.body}}</p>
    </div>
     <h2>Lista de Usuarios</h2>
    <div>
      <table>
        <tbody>
          <tr v-for="todo in todos" :key="todo.id">
            <td class="prueba">{{ todo.id}}</td>
            <td class="prueba">{{ todo.title}}</td>
            <td class="prueba">{{ todo.completed}}</td>
            <td class="prueba">{{ todo.userId}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'app',
  data () {
    return {
      msg: 'Consumiento Datos - JSONPlaceholder',
      posts: [],
      todos: null
    }
  },
  mounted(){
    this.getTodos();
    let vue = this;
    axios.get('https://jsonplaceholder.typicode.com/posts')
    .then(function ( response ){
      vue.posts = response.data;
    })

  },
  methods: {
    getTodos(){
      axios
      .get('https://jsonplaceholder.typicode.com/todos')
      .then( response => {
        this.todos = response.data

      })
      .catch( e=> console.log(e))

    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.post {
  border: 1px solid #d9d9d9;
  padding: 20px;
  margin-bottom: 10px;
}

.prueba {
  border: 1px solid #920505;
  padding: 20px;
  margin-bottom: 10px;
}
</style>
