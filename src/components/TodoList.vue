<template>
  <div class="container">
    <h1>Todo List</h1>

    <input
      type="text"
      class="todo-input"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />

    <todo-item
      class="list-item-container"
      v-for="(todo, index) in todosFiltered"
      :key="todo.id"
      :todo="todo"
      :index="index"
      @removeTodo="removeTodo"
      @finishedEdit="finishedEdit"
    />

    <Footer :remaining="remaining" />

    <filters :filter="filter" @setFilter="setFilter" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoItem from "./TodoItem.vue";
import Footer from "./Footer.vue";
import Filters from "./Filters.vue";

interface Todo {
  id: number;
  title: string;
  completed: boolean;
  editing: boolean;
}

export default Vue.extend({
  name: "todo-list",
  components: { TodoItem, Footer, Filters },
  data: () => ({
    newTodo: "",
    beforeEditCache: "",
    idForTodo: 3,
    filter: "all",
    todos: [
      { id: 1, title: "Teste 1", completed: false, editing: false },
      { id: 2, title: "Teste 2", completed: false, editing: false }
    ]
  }),
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.completed).length;
    },

    todosFiltered() {
      if (this.filter === "active")
        return this.todos.filter(todo => !todo.completed);
      if (this.filter === "completed")
        return this.todos.filter(todo => todo.completed);
      return this.todos;
    }
  },
  methods: {
    addTodo(): void {
      if (this.newTodo.trim().length === 0) return;

      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
        editing: false
      });

      this.newTodo = "";
      this.idForTodo++;
    },

    removeTodo(index: number): void {
      this.todos.splice(index, 1);
    },

    finishedEdit({ index, todo }: { index: number; todo: Todo }) {
      this.todos.splice(index, 1, todo);
    },

    setFilter(filter: string) {
      this.filter = filter;
    }
  }
});
</script>

<style scoped lang="scss">
.container {
  max-width: 700px;
  margin: 16px auto;
}

.todo-input {
  width: 100%;
  height: 40px;
  margin-top: 24px;
  background: #fff;
  border-radius: 8px;
  padding: 16px;
  font-size: 18px;
}

.list-item-container {
  width: 100%;
  height: 40px;
  border-radius: 8px;
  margin-top: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #fff;
}
</style>
