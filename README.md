# Vue.js intro



## Setup

    yarn install


### Compiles and hot-reloads for development

    yarn serve


### Compiles and minifies for production

    yarn build

### Lints and fixes files

    yarn lint



## Vue File Structure



## Vue Components


### Create and import components

### Style components

### Props

### Data

---

## Vue Directives

### Bind attributes to props and data with `v-bind` (`:`)
`TaskCard`

### Loop with `v-for`
`TaskList`

### Conditional elements with `v-if`, `v-else`
`NewTask`
  
### Bind inputs to data with `v-model`
`NewTask`

### Listen for events with `v-on` (`@`)
`NewTask`

#### Custom events
`$emit('custom-event')` and `@custom-event`
`NewTask`/`App` 



## Bonus

### Select elements with `ref`
`NewTask`

### Vue Component Lifecycle
`NewTask`

### Store data in the browser with `localStorage`
`TaskList`




```vue
<!-- TaskCard.vue -->
<template>
  <div :class="['task-card', { done: done }]">
    <div>
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <Checkbox @click.native="$emit('toggle-task', taskIndex)" :checked="done" />
  </div>
</template>
```


```html
<!-- TaskCard.vue -->
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
```


```vue
<!-- TaskCard.vue -->
<style lang="scss">
.task-card {
  display: flex;
  min-height: 6rem;
  text-align: left;
  background-color: saturate(rgba(#41b883, 0.03), 30%);
  border-bottom: solid 1px rgba(#35495e, 0.1);
  border-left: solid 8px #41b883;
  transition: all 0.3s;
  p { font-size: 0.9rem; }
  &:hover {
    transform: scale(1.02);
    background-color: white;
    box-shadow: 2px 3px 10px rgba(black, 0.1);
  }
  & > div:first-child {
    margin: 0 1rem;
    padding: 1rem 0;
    display: flex;
    flex-grow: 1;
    flex-direction: column;
    justify-content: center;
  }
  &.done {
    border-left: solid 8px rgba(#35495e, 0.3);
    background-color: rgba(#35495e, 0.08);
    h3, p { text-decoration: line-through; opacity: 0.3; }
    &:hover { transform: unset; box-shadow: unset; }
  }
}
</style>
```



```vue
// Checkbox.vue
<style lang="scss">
$check-color: #41b883;
.checkbox {
  display: flex;
  align-self: center;
  border: solid 2px $check-color;
  border-radius: 50%;
  width: 2rem;
  height: 2rem;
  margin: 0 1rem;
  cursor: pointer;
  &:hover { background-color: rgba($check-color, 0.2); transform: scale(1.1); }
  &.checked { background-color: $check-color; }
  &.checked:after {
    content: "";
    display: inline-block;
    transform: rotate(45deg) translate(-35%, 40%);
    height: 1rem;
    width: 1rem;
    margin-left: 60%;
    border-bottom: 5px solid white;
    border-right: 5px solid white;
  }
}
</style>
```

```scss
// NewTask.vue
<style lang="scss">
@keyframes expand-vertical { from { min-height: 0; height: 0; } to { min-height: 6rem; } }
.new-task {
  animation: expand-vertical 0.2s;
  overflow: hidden;
  background-color: white;
  border-left: solid 5px #35495e;
  &, &:hover { transform: scale(1.1); box-shadow: 2px 3px 10px rgba(black, 0.2); }
  & + .tasks-list { pointer-events: none; }
  input { font-size: 1.17rem; font-weight: bold; width: 100%; }
  textarea { width: 100%; font-size: 0.9rem; resize: none; }
}
</style>
```



What's next?
- computed properties
- Vue lifecycle
- slots
- Vue router