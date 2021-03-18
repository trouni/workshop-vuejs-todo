<template>
  <div>
    <button class="btn" @click="toggleForm()">
      {{ formVisible ? "Cancel" : "Add Task" }}
    </button>

    <div v-if="formVisible" class="task-card new-task">
      <div>
        <input
          @keypress.enter="$nextTick(() => $refs.descriptionInput.focus())"
          type="text"
          placeholder="What is your task?"
          v-model="title"
          ref="titleInput"
        />
        <textarea
          @keypress.enter="createTask(title, description)"
          v-model="description"
          placeholder="Add some details about your task..."
          ref="descriptionInput"
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
      formVisible: false,
    };
  },

  methods: {
    toggleForm() {
      this.formVisible = !this.formVisible;
      if (this.formVisible) this.$nextTick(() => this.$refs.titleInput.focus());
      this.resetForm();
    },
    createTask(title, description) {
      this.$emit("create-task", title, description);
      this.formVisible = false;
      this.resetForm();
    },
    resetForm() {
      this.title = "";
      this.description = "";
    },
  },
};
</script>

<style lang="scss">
@keyframes expand-vertical {
  from {
    min-height: 0;
    height: 0;
  }
  to {
    min-height: 6rem;
  }
}

.new-task {
  animation: "expand-vertical" 0.2s;
  overflow: hidden;
  background-color: white;
  transform: scale(1.02);
  border-left: solid 5px #35495e;
  &,
  &:hover {
    box-shadow: 2px 3px 10px rgba(black, 0.2);
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
