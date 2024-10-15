<template>
  <h1 class="w-full text-center mt-10 text-slate-600 font-semibold">
    TODO APP
  </h1>
  <div class="flex flex-col gap-2 items-center mt-10">
    <Todo
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @changeStatus="changeStatus"
      @deleteTodo="deleteTodo"
      @setActiveTodo="updateActiveTodo"
    />
    <CreateTodo @addTodo="newTodo" />

    <ActiveTodo
      :class="activeTodo !== null ? 'block' : 'hidden'"
      v-bind:todo="activeTodo"
      @close="close"
    />
  </div>
</template>

<script lang="ts">
import { TrashIcon } from "@heroicons/vue/16/solid";
import ActiveTodo from "./components/activeTodo.vue";
import Todo from "./components/Todo.vue";
import CreateTodo from "./components/createTodo.vue";

type Todo = {
  id: number;
  name: string;
  status: string;
};

export default {
  data() {
    return {
      todos: [{ id: 0, name: "The newest todo in da city", status: "" }],
      activeTodo: null,
    };
  },
  methods: {
    changeStatus(status: string, id: number) {
      this.todos = this.todos.map((todo) =>
        todo.id === id ? { ...todo, status } : { ...todo }
      );
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    newTodo(name: string) {
      const id = this.todos.length
        ? this.todos[this.todos.length - 1].id + 1
        : 0;
      this.todos.push({
        id,
        name,
        status: "",
      });
    },
    updateActiveTodo(todo: Todo | null) {
      this.activeTodo = todo;
      console.log(this.activeTodo);
    },
    close() {
      this.activeTodo = null;
    },
  },
  components: {
    TrashIcon,
    Todo,
    CreateTodo,
    ActiveTodo,
  },
};
</script>

<style scoped></style>
