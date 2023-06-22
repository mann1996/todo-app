<template>
  <div class="flex flex-col gap-2">
    <div v-for="todo in todos" class="flex items-center gap-2 py-2 px-4 shadow-sm hover:shadow-md">
      <input type="checkbox" :id="`complete-todo-${todo.id}`" :checked="todo.completed" v-on:change="toggleTodo($event, todo)" />
      <div :class="{ 'line-through': todo.completed }">{{ todo.title }}</div>
      <button class="ml-auto text-gray-50 bg-red-500 rounded-full p-1 hover:bg-red-600" v-on:click="deleteTodo($event, todo.id)"><CrossIcon /></button>
    </div>
  </div>
</template>
<script>
import CrossIcon from "./icons/CrossIcon.vue";
export default {
  components: { CrossIcon },
  props: ["todos"],
  methods: {
    /**
     *
     * @param {Event} event
     * @param {any} todo
     */
    toggleTodo(event, todo) {
      const value = event.currentTarget.checked;

      todo.completed = value;
    },

    deleteTodo(e, id) {
      this.$emit("delete-todo", id);
    },
  },
};
</script>
