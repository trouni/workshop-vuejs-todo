<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" height="100" />
    <h1>Task Manager</h1>
    <TasksList />
  </div>
</template>

<script>
import TasksList from "./components/TasksList.vue";

export default {
  name: "App",

  components: {
    TasksList,
  },
};
</script>

<style lang="scss">
@import "./assets/style.scss";

#app {
  font-family: Poppins, Helvetica, Arial, sans-serif;
  font-weight: 100;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: auto;
  margin-top: 60px;
  max-width: 600px;
}
</style>
