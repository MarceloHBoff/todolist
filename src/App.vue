<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <TodoList />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import TodoList from "./components/TodoList.vue";

@Component({
  components: {
    TodoList,
  },
})
export default class App extends Vue {}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  outline: 0;
  box-sizing: border-box;
}

body {
  background-color: #312e38;
  color: #fff;
  -webkit-font-smoothing: antialiased;
}

button,
input {
  border: 0;
  background: transparent;
}

button {
  cursor: pointer;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
