<script>
import TodoList from "../components/TodoList.vue";
import AddTodo from "../components/AddTodo.vue";
import axios from "axios";
export default {
  name: "Home",
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
  <main >
    <AddTodo v-on:add-todo="addTodo" />
    <TodoList v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
  </main>
</template>

<style scoped></style>
