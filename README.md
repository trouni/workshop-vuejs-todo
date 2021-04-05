### JavaScript Workshop
# Introduction to Vue.js

<p align="center" width="100%">
  <img src="src/assets/logo.png" alt="Vue.js Logo" height="100px" style="margin: auto;">
</p>

**REGISTER:**

<a href="https://info.lewagon.com/tokyo-vuejs" target="_blank">https://info.lewagon.com/tokyo-vuejs</a>

This workshop will teach you how to build <a href="https://trouni-vue-task-manager.netlify.app/" target="_blank">this simple Todo app</a>.

Note: the slide version of this workshop is available <a href="https://slides.trouni.com/?src=trouni/workshop-vuejs-todo" target="_blank">here</a>

---

## Setup

**TODO:**

Clone the git repository for this workshop

```zsh
git clone https://github.com/trouni/workshop-vuejs-todo.git
```

**OR** [download the ZIP file](https://github.com/trouni/workshop-vuejs-todo/archive/refs/heads/main.zip) and unzip the archive to your projects folder or desktop.


**TODO:**

Run `yarn install` to install the project's dependencies, then `yarn serve` to launch a local server.

```sh    
yarn install # Installs dependencies

yarn serve # Compiles and hot-reloads for development
```

You should now be able to view your app on http://localhost:8080.

---

## Intro to Vue Components


### Component File Structure

```vue
<!-- Component.vue -->

<template>
  <div>
    <!-- HTML structure -->
  </div>
</template>

<script>
// Data & logic
</script>

<style lang="scss">
/* Styling */
</style>
```

⚠️ The `<template>` should only have a **single** root element.


### Creating your first components

Create a new `/components/TasksList.vue` file with the following code:

```vue
<!-- TasksList.vue -->

<template>
  <div id="tasks">
    <p>This is my first Vue.js component</p>
  </div>
</template>
```


Then import the component in your `App.vue` file.

```vue
<!-- App.vue -->

<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" height="100">
    <h1>Task Manager</h1>
    <TasksList />
  </div>
</template>

<script>
import TasksList from './components/TasksList.vue'

export default {
  name: 'App',
  components: {
    TasksList
  }
}
</script>
```


Let's replace the text with a static card:

```html
<template>
  <div id="tasks">
    <div class="task-card">
      <div>
        <h3>Create a card component</h3>
        <p>Create a new TaskCard.vue file in the components folder, then import it in TasksList.vue</p>
      </div>
    </div>
  </div>
</template>
```


### Styling components

You can add styling rules for each component in the `<style>` section. Try it out!



## Making dynamic components


First of all, we should move the task card into its own component. Move the previous code into a `TaskCard.vue` and add this styling:

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


### Defining the State of a Component with `data`

Let's define some `data` and use the mustaches `{{ }}` to interpolate the values in our HTML template.

**💡Tip**: Install the awesome [Vue.js Chrome DevTools extension](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd) to inspect data (and more) in your Vue app.

```vue
<!-- TaskCard.vue -->

<template>
  <div class="task-card">
    <div>
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <div>{{ done ? "✅" : "⭕️" }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Make the card component dynamic",
      description:
        "Learn about using the data option and passing data to child components using props",
      done: false
    };
  },
};
</script>
```


**We want our component to be reusable:**

Let's assign the `title` and `description` dynamically.


### Passing Data to Child Components with `props`

> Props are custom attributes you can register on a component. When a value is passed to a prop attribute, it becomes a property on that component instance. 

Props are basically special data attributes **that come from the parent component**.


Let's replace the `data` option with `props`:

```vue
<!-- TaskCard.vue -->

<script>
export default {
  props: {
    title: String,
    description: String,
    done: { type: Boolean, default: false }
  },
};
</script>
```


We can now pass the `title` and `description` from the parent component:

```vue
<!-- TasksList.vue -->

<TaskCard
  title="Make the card component dynamic"
  description="Learn about using the data option and passing data to child components using props"
  done="true"
/>
```



## Vue Directives


Add some static tasks to help us implement our app:

```vue
<!-- TasksList.vue -->

data() {
  return {
    tasks: [
      {
        title: "Create a card component",
        description:
          "Create a new TaskCard.vue file in the components folder, then import it in TasksList",
        done: true,
      },
      {
        title: "Make the card component dynamic",
        description:
          "Learn about using the data option and passing data to child components using props",
        done: true,
      },
      {
        title: "Bind the attributes to the data",
        description:
          "Use the v-bind directive to bind the title and description to our data",
        done: false,
      },
    ],
  };
},
```


### Binding Attributes to Props and Data with `v-bind`

We want to use the values from our `tasks` in the `title` and `description` attributes of our `TaskCard` component, but mustaches cannot be used inside HTML attributes.

Instead, use a `v-bind` directive (shorthand `:`).

```vue
<!-- TasksList.vue -->

<TaskCard
  v-bind:title="tasks[0].title"
  v-bind:description="tasks[0].description"
  v-bind:done="tasks[0].done"
/>
```


### Binding HTML Classes

We can bind the class attribute to add a `done` class to the card when the task is completed.

```vue
<!-- TaskCard.vue -->

<template>
  <div :class="['task-card', { done: done }]">
  <!-- ... -->
</template>
```


### Iterate with `v-for`

Let's now display all of our tasks by iterating over the `tasks` array using the `v-for` directive.

```vue
<!-- TasksList.vue -->

<TaskCard
  v-for="(task, index) in tasks"
  :key="index"
  :title="task.title"
  :description="task.description"
  :done="task.done"
/>
```


### Conditional Rendering with `v-if` / `v-else`

Let's display a small message when we have no tasks in our app.

```vue
<!-- TasksList.vue -->

<div v-if="tasks.length > 0" class="tasks-list">
  <TaskCard
    <!-- ... -->
  />
</div>
<p v-else>You don't have any tasks yet...</p>
```


### Adding Behavior with `methods`

Implement an `addTask()` method to push a new task inside of the `tasks` array.

```vue
<!-- TasksList.vue -->

<script>
  // ...
  methods: {
    addTask(title, description, done = false) {
      this.tasks.unshift({ title, description, done });
    },
  },
  // ...
</script>
```


### Listen for events with `v-on`

Let's add a button to test that our method works and make it listen to `click` events using `v-on` (shorthand `@`).

```vue
<!-- TasksList.vue -->

<button
  class="btn round-icon"
  v-on:click="addTask('My new task', 'My new description')"
>＋</button>
```


### Capturing user input with `v-model`

We still need to be able to enter the `title` and `description` ourselves. Let's add some inputs to our `TasksList`.

```html
<!-- TasksList.vue -->

<div class="task-card new-task">
  <div>
    <input
      type="text"
      placeholder="What would you like to do?"
    />
    <textarea
      placeholder="Add some details about your task..."
    ></textarea>
  </div>
</div>
```


Add the following styles to your `TasksList` component:

```vue
<!-- TasksList.vue -->

<style lang="scss">
@keyframes expand-vertical { from { min-height: 0; height: 0; } to { min-height: 6rem; } }
.task-card.new-task {
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


We can bind the input fields with data attributes in our component.

```vue
<!-- TasksList.vue -->

<template>
  <!-- ... -->
    <input
      type="text"
      placeholder="What would you like to do?"
      v-model="newTitle"
    />
    <textarea
      placeholder="Add some details about your task..."
      v-model="newDescription"
    ></textarea>
  <!-- ... -->
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTitle: "",
      newDescription: "",
    };
  },
};
</script>
```


### Update the `v-on` directive

```vue
<!-- TasksList.vue -->

<template>
  <!-- ... -->
    <button
      class="btn round-icon"
      v-on:click="addTask(newTitle, newDescription), resetForm()"
    >＋</button>
  <!-- ... -->
</template>

<script>
  // ...
  methods: {
    addTask(title, description, done = false) {
      this.tasks.unshift({ title, description, done });
    },
    resetForm() {
      this.newTitle = ""
      this.newDescription = ""
    }
  },
  // ...
</script>
```


### Manipulate the DOM by combining `v-on` and `v-if`/`v-show`

Let's only show the inputs after we click on the `+` button.

```vue
<template>
  <div id="tasks">
    <button class="btn round-icon" @click="newFormVisible = !newFormVisible">
      {{ newFormVisible ? "✕" : "＋" }}
    </button>

    <div
      v-show="newFormVisible"
      class="task-card new-task"
      @keyup.enter="addTask(newTitle, newDescription), resetForm()"
    >
    <!-- ... -->
    <p v-else-if="!newFormVisible">You don't have any tasks yet...</p>
  </div>
</template>

<script>
  // ...
  data() {
    return {
      // ...
      newFormVisible: false,
    };
  },

  methods: {
    addTask(title, description, done = false) {
      // ...
      this.newFormVisible = false;
    },
  // ...
```



## Bonus



### Persist Data with `localStorage`

We can easily store the `tasks` array directly in the user's browser:

```vue
<!-- TasksList.vue -->

<script>
  // ...
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem("tasks")) || []
    };
  },

  watch: {
    tasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
  // ...
</script>
```



### Mark Tasks as Done

Implement this  `toggleTask` method in the `TasksList` component:

```js
// TasksList.vue
// <script> --> methods

toggleTask(taskIndex) {
  const taskToUpdate = this.tasks[taskIndex];
  taskToUpdate.done = !taskToUpdate.done;
  this.$set(this.tasks, taskIndex, taskToUpdate);
},
```

Note that Vue2 requires us to use `this.$set` rather than `this.tasks[taskIndex] = taskToUpdate` to make sure [Vue reacts to the changes in the array](https://vuejs.org/v2/guide/reactivity.html#For-Arrays).


Create this new UI component `Checkbox`:

```vue
<!-- Checkbox.vue -->

<template>
  <div :class="['checkbox', { checked: checked }]"></div>
</template>

<script>
export default {
  props: {
    checked: Boolean,
  },
};
</script>

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


Modify your `TaskCard` component to use the `Checkbox` and emit a custom event on `click`.

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



### Send Data to Parent Components using Custom Events

To pass data _upstream_ from a child to a parent component: 
1. the child component emits a custom event using `$emit('custom-event')`
2. the parent component listens for that event using `v-on:custom-event`


Let's move the input fields and style from `TasksList` to a new component `NewTask`.

```vue
<!-- NewTask.vue -->

<template>
  <div class="task-card new-task"
      @keyup.enter="submitTask(newTitle, newDescription), resetForm()">
    <div>
      <input
        type="text"
        placeholder="What would you like to do?"
        v-model="newTitle"
      />
      <textarea
        placeholder="Add some details about your task..."
        v-model="newDescription"
      ></textarea>
    </div>
  </div>
</template>

<script>
  data() {
    return {
      newTitle: "",
      newDescription: "",
    };
  },

  methods: {
    submitTask(title, description) {
      // Problem is that the `tasks` array is in the parent component, `TasksList`.
      // We need to submit the title and description "upstream".
    },
    resetForm() {
      this.newTitle = "";
      this.newDescription = "";
    },
  },
</script>

<style lang="scss">
@keyframes expand-vertical { from { min-height: 0; height: 0; } to { min-height: 6rem; } }
.task-card.new-task {
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


We can send a custom event upstream using `$emit`:

```vue
<!-- NewTask.vue -->

<script>
  // ...
  methods: {
    submitTask(title, description) {
      this.$emit("add-task", title, description);
    },
  },
  // ...
</script>
```


The parent component `TasksList` listens for the custom `add-task` event, and calls the `addTask` method when the event is triggered.

```vue
<template>
  <!-- ... -->
  <NewTask @add-task="addTask" />
  <!-- ... -->
</template>
```



## What to look at next?

- [Computed Properties](https://v3.vuejs.org/api/options-data.html#computed)
- [Vue Lifecycle Hooks](https://v3.vuejs.org/api/options-lifecycle-hooks.html)
- [Component Slots](https://v3.vuejs.org/api/options-data.html#computed)
- [Vue Router](https://router.vuejs.org/)

---

Workshop/tutorial by **Trouni Tiet**\
[LinkedIn](https://linkedin.com/trouni) | [GitHub](https://github.com/trouni)