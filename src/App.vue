<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from "axios";

import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

export default {
  name: "app",
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    async deleteTodo(id) {
      try {
        this.todos = this.todos.filter(todo => todo.id !== id);
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
      } catch (err) {
        console.error(err);
      }
    },
    async addTodo(todo) {
      const { title, completed } = todo;

      try {
        const { data: todo } = await axios.post(
          "https://jsonplaceholder.typicode.com/todos",
          {
            title,
            completed
          }
        );

        this.todos = [...this.todos, todo];
      } catch (err) {
        console.error(err);
      }
    }
  },
  created: async function() {
    const { data: todos } = await axios.get(
      "https://jsonplaceholder.typicode.com/todos?_limit=10"
    );

    this.todos = todos;
  }
};
</script>

<style lang="scss">
* {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;

  &:hover {
    background: #666;
  }
}
</style>
