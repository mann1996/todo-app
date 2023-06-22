<script>
import TodoList from "./components/TodoList.vue";
import AddTodo from "./components/AddTodo.vue";
import axios from "axios";
export default {
  components: {
    AddTodo,
    TodoList,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(todo) {
      axios
        .post("https://jsonplaceholder.typicode.com/todos", todo)
        .then((resp) => (this.todos = [...this.todos, resp.data]))
        .catch((err) => console.log(err));
    },

    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`).then((_) => (this.todos = this.todos.filter((t) => t.id !== id)));
    },
  },

  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then((resp) => (this.todos = resp.data))
      .catch((err) => console.log(err));
  },
};
</script>

<template>
  <div id="app">
    <header class="flex flex-row items-center bg-slate-800 text-gray-50 p-4">
      <router-link to="/" class="font-bold text-gray-50">Todo App</router-link>
      <router-link to="/about" class="text-gray-50 ml-6">About</router-link>
    </header>
    <div class="mt-4 max-w-[900px] mx-auto">
      <router-view></router-view>
    </div>
  </div>
</template>

<style scoped></style>
