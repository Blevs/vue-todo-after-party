<template>
  <div id="app">
    <h1>Todos</h1>
    <div>
      <div class="todo" v-bind:class="{ done: todo.completed }" v-for="todo in todos" v-on:click="toggle(todo.id)" :key="todo.id">
        {{ todo.task }}
      </div>
      <form v-on:submit="addTodo">
        <input v-model="newTask" placeholder="add todo"/>
        <button type="sumbit">add todo</button>
      </form>
    </div>
  </div>
</template>

<script>
 export default {
     name: 'app',
     data() {
         return {
             newTask: "",
             todos: [
                 {
                     id: 1,
                     task: "Learn vue",
                     completed: false
                 },
                 {
                     id: 2,
                     task: "Eat food",
                     completed: true
                 }
             ]
         }
     },
     methods: {
         toggle: function(id) {
             this.todos = this.todos.map(todo => {
                 if (todo.id === id) {
                     return {...todo, completed: !todo.completed}
                 }
                 return todo;
             });
         },
         addTodo: function(event) {
             event.preventDefault();
             this.todos.push({
                 id: Date.now(),
                 task: this.newTask,
                 completed: false
             })
         }
     }
 }
</script>

<style>
 #app {
     font-family: 'Avenir', Helvetica, Arial, sans-serif;
     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     text-align: center;
     color: #2c3e50;
     margin-top: 60px;
 }
 .todo {
     padding: 10px;
     margin: 10px auto;
     background-color: #fafafa;
     /* rgb rrggbb
        00-99
        909999
        000000
        990000
        0 1 2 3 4 5 6 7 8 9
        0 1 2 3 4 5 6 7 8 9 a b c d e f
      */
     border: 1px solid #1a1a1a;
     border-radius: 5px;
     max-width: 500px;
     text-align: left;
     transition: background-color 0.3s;
     cursor: pointer;
 }

 .todo:hover {
     background-color: #dadada;
 }

 .todo.done {
 }

 .todo.done::before {
     content: "✓";
     background-color: #74AC7A;
     border-radius: 100%;
     padding: 3px;
     color: white;
     text-weight: bold;
 }
</style>
