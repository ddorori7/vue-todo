<template>
  <div id="app" class="container">
    <h1 class="text-center mb-5">TODO APP</h1>
    <input
      v-model="todoText"
      type="text"
      class="w-100 p-2"
      placeholder="해야할일!"
      @keyup.enter="addTodo"
    />
    <hr />
    <Todo
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-checkbox="toggleCheckbox"
      @click-delete="deleteTodo"
    />
  </div>
</template>

<script>
import Todo from "@/components/Todo.vue";

export default {
  name: "App",
  components: { Todo },
  data() {
    return {
      todoText: "",
      todos: [{ id: 1, text: "just do it", checked: false }],
    };
  },
  methods: {
    addTodo(e) {
      this.todos.push({
        id: Math.random() + e.target.value,
        text: e.target.value,
        checked: false,
      });
      this.todoText = "";
    },
    toggleCheckbox({ id, checked }) {
      const index = this.todos.findIndex((todo) => {
        return todo.id === id;
      });
      this.todos[index].checked = checked;
    },
    deleteTodo({ id }) {
      // const index = this.todos.findIndex((todo) => {
      //   return todo.id === id;
      // });
      // this.todos.splice(index, 1);
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
