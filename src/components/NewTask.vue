<template>
  <div>
    <button class="btn" @click="formHidden = !formHidden">
      {{ formHidden ? "Add Task" : "Cancel" }}
    </button>
    <div
      v-show="!formHidden"
      class="task-card new-task"
      @keyup.enter="createTask(title, description)"
    >
      <div>
        <input
          type="text"
          placeholder="What is your task?"
          v-model="title"
          ref="titleInput"
        />
        <textarea
          rows="1"
          v-model="description"
          placeholder="Add some details about your task..."
        ></textarea>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
      formHidden: true,
    };
  },

  methods: {
    createTask(title, description) {
      this.$emit("create-task", title, description);
      this.formHidden = true;
      this.title = "";
      this.description = "";
    },
  },
};
</script>

<style lang="scss">
@keyframes new-task-form {
  from {
    min-height: 0;
    height: 0;
  }
  to {
    min-height: 6rem;
  }
}

.new-task {
  animation: "new-task-form" 0.2s forwards;
  overflow: hidden;
  background-color: white;
  transform: scale(1.02);
  box-shadow: 2px 3px 8px rgba(black, 0.08);
  border: solid 1px #35495e;
  border-left: solid 5px #35495e;
  z-index: 1000;
  &:hover {
    box-shadow: 2px 3px 8px rgba(black, 0.08);
  }
  input {
    font-size: 1.17rem;
    font-weight: bold;
    width: 100%;
  }
  textarea {
    width: 100%;
    font-size: 0.9rem;
    resize: none;
  }
}
</style>
