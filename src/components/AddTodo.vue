<template>
  <div>
    <form @submit="addTodo" class="flex gap-2 items-center px-4 mb-4">
      <input type="text" v-model="title" placeholder="add todo...." class="bg-slate-300 py-2 px-4 flex-1 rounded-sm focus:outline-blue-500" />
      <button type="submit" class="bg-blue-500 py-2 px-4 text-gray-50 rounded-sm hover:bg-blue-600">Add</button>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo(event) {
      event.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false,
      };

      this.$emit("add-todo", newTodo);
    },
  },
};
</script>
