<template>
  <div id="app">
    <app-header></app-header>
    <app-todo-board></app-todo-board>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import TodoBoard from "./components/TodoBoard.vue";

export default {
  components: {
    appHeader: Header,
    appTodoBoard: TodoBoard
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
