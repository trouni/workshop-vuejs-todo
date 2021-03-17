<template lang="html">
  <div :class="['task-card', { done: done }]">
    <div>
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <Checkbox @click.native="$emit('toggle-task', taskIndex)" :checked="done" />
  </div>
</template>

<script>
import Checkbox from "./Checkbox";

export default {
  components: {
    Checkbox,
  },

  props: {
    title: String,
    description: String,
    done: Boolean,
    taskIndex: Number,
  },
};
</script>

<style lang="scss">
.task-card {
  display: flex;
  text-align: left;
  background-color: rgba(#35495e, 0.03);
  transition: all 0.3s;
  min-height: 6rem;
  border-bottom: solid 1px rgba(#35495e, 0.1);
  border-left: solid 5px #41b883;
  &:hover {
    background-color: white;
    transform: scale(1.02);
    box-shadow: 2px 3px 10px rgba(black, 0.1);
  }
  & > div {
    min-width: 2rem;
    margin: 0 1rem;
  }
  & > div:first-child {
    padding: 1rem 0;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  &.done {
    border-left: solid 5px rgba(#35495e, 0.3);
    h3,
    p {
      text-decoration: line-through;
      opacity: 0.3;
    }
    &:hover {
      transform: unset;
      box-shadow: unset;
    }
  }
}
</style>
