<template>
  <div>
    <NewTask @create-task="createTask" />
    <div v-if="tasks.length" class="tasks-list">
      <TaskCard
        v-for="(task, index) in tasks"
        :key="index"
        :title="task.title"
        :description="task.description"
        :done="task.done"
        :task-index="index"
        @toggle-task="toggleTask"
      />
    </div>
    <p v-else>You don't have any tasks yet...</p>
  </div>
</template>

<script>
import TaskCard from "./TaskCard";
import NewTask from "./NewTask";

export default {
  name: "TasksList",
  components: {
    TaskCard,
    NewTask,
  },

  data() {
    return {
      tasks: (JSON.parse(localStorage.getItem("tasks")) || []).sort((task) =>
        task.done ? 1 : -1
      ),
    };
  },

  watch: {
    tasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },

  methods: {
    createTask(title, description, done = false) {
      this.tasks.unshift({ title, description, done });
    },
    toggleTask(taskIndex) {
      const taskToUpdate = this.tasks[taskIndex];
      taskToUpdate.done = !taskToUpdate.done;
      this.$set(this.tasks, taskIndex, taskToUpdate);
    },
  },
};
</script>
