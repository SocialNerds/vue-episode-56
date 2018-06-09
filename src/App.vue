<template>
<div>
  <div>{{name}}</div>
  <div v-if="todos.length === 0">Add some todos!</div>
  <div v-else><button v-on:click="removeCompleted">Clear</button></div>
  <ul>
    <li v-for="(data, index) in todos" :key="index">
      <input type="checkbox" v-on:click="toggleTodo(index)" :checked="data.completed">{{data.title}}
      <button v-on:click="removeTodo(index)">X</button>
    </li>
  </ul>
  <form @submit.prevent="addTodo">
    <input type="text" placeholder="Todo name..." v-model="title">
    <input type="submit" value="Add todo"/>
  </form>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      name: 'Hello darkness my old friend!',
      title: '',
      todos: [
        {title: 'Fix some bugs', completed: false}
      ]
    }
  },
  methods: {
    addTodo() {
      if (this.title !== '') {
        this.todos.push({title: this.title, completed: false});        
        this.title = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    removeCompleted(index) {
      this.todos = this.todos.filter(todo => !todo.completed);
    },
    toggleTodo(index) {
      this.todos[index].completed = !this.todos[index].completed;
    }
  }
}
</script>

<style>
</style>
