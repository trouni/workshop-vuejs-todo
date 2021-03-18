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
</style>
